---
title: How deduplication works in Zapier
order: 5
layout: post-toc
redirect_from: 
    - /docs/dedupe
    - /build/dedupe
---

# How deduplication works in Zapier

Zapier automatically deduplicates incoming trigger data for your integration, so that Zaps do not run multiple times on the same data. Consider the following requirements for your "New Item" and "Updated Item" triggers to work as users expect. 

- Provide a unique primary key.
  - By default, the field with the key `id` is used as the primary key.
  - Alternatively, if you're using the CLI, you can choose other fields as the primary key by enabling `primary` in `outputFields`. See [more information](https://github.com/zapier/zapier-platform/blob/main/packages/cli/README.md#how-does-deduplication-work) in the CLI docs.
- Sort reverse-chronologically by time created.

The API endpoint must list new or updated items in an array sorted in reverse chronological order.

[Polling](https://platform.zapier.com/build/trigger) usually returns many results, most of which Zapier has seen before. Since a Zap should not trigger multiple times when an item in your app exists in multiple distinct polls, the data must be deduplicated. 

For example, say your endpoint for new items returns a list of tasks:

{% highlight javascript %}
{% raw %}
[
  {
    "id": 7,
    "created": "Mon, 25 Jun 2023 16:41:54 -0400",
    "list_id": 1,
    "description": "integrate our api with zapier",
    "complete": false
  },
  {
    "id": 6,
    "created": "Mon, 25 Jun 2023 16:41:45 -0400",
    "list_id": 1,
    "description": "get published in zapier library",
    "complete": false
  }
]
{% endraw %}
{% endhighlight %}

The following assumes you're using the default primary key, the `id` field. When a Zap is first turned on, Zapier makes an initial call to your API to retrieve existing data, and caches and stores each `id` field in our database. When the Zap is turned off, that list is cleared.

Active Zaps then [poll at an interval](https://help.zapier.com/hc/en-us/articles/8496181725453#01H8C8M008GXFT36C42W1157P0) (based on a [customer's plan](https://zapier.com/pricing)) and compare the `id`s to all those seen before, trigger on new items, and update the list of seen `id`s.  

Now let's say the user created a new task:

{% highlight javascript %}
{% raw %}
[
  {
    "id": 8,
    "created": "Mon, 25 Jun 2023 16:42:09 -0400",
    "list_id": 1,
    "description": "re-do our api to support webhooks",
    "complete": false
  },
  {
    "id": 7,
    "created": "Mon, 25 Jun 2023 16:41:54 -0400",
    "list_id": 1,
    "description": "integrate our api with zapier",
    "complete": false
  },
  {
    "id": 6,
    "created": "Mon, 25 Jun 2023 16:41:45 -0400",
    "list_id": 1,
    "description": "get published in zapier library",
    "complete": false
  }
]
{% endraw %}
{% endhighlight %}

On the next poll after the new task is created, your API returns all tasks, but only the first task with `id` equal to `8` will be seen as a new item. That particular JSON object will then trigger the user's Zap and complete any subsequent action steps the user has defined. The essence of deduplication is that the other `id`s in the poll, `6` and `7` will be ignored, since their `id`s have been seen in previous polls. 

In order for deduplication to work, the `id` field should always be supplied and unique amongst all items in the result. 

Your API must return results in reverse-chronological order to make sure new/updated items can be found on the first page of results, as Zapier polling triggers don't automatically fetch additional pages. If your API lists items in a different order by default, but allows for sorting, include an order or sorting field in your polling request to ensure newest records are returned on the first page of results. [Github is a great example](https://docs.github.com/en/rest/issues/issues?apiVersion=2022-11-28#list-repository-issues) of an API that supports sorting on multiple fields in the `asc` or `desc` direction.

## Re-ordering returning items 

If your API cannot order its results in reverse-chronological order, you can use [Code Mode](https://platform.zapier.com/build/code-mode) to make additional requests, if necessary.

One possible scenario could be:

1. Fetch the first page, containing the oldest items, but also the total number of pages.
2. Fetch the last page and reverse the order of the items before returning results in an array.

When adding additional requests to your custom code, all requests and processing code for a trigger must [finish within 30 seconds](https://platform.zapier.com/build/operating-constraints#timeouts-triggers). It is not recommended to attempt to fetch all pages of results.

If the items your API returns do not have an `id` field or you're adding an Updated Item trigger, you will use [Code Mode](https://platform.zapier.com/build/code-mode) to modify the API response.

## Custom primary keys

In older, [legacy Zapier Web Builder apps](https://platform.zapier.com/manage/versions-legacy), Zapier guessed if `id` wasn't present. It is now required that you define one or more fields as the primary key.

By default, Zapier uses the field with the key `id` as the primary key if no `outputFields` has `primary: true`. The `id` field would be required in this case. Otherwise, your trigger would run into an error at runtime. If your API's items have a differently-named unique field, adapt this code snippet to ensure this test passes:

{% highlight javascript %}
{% raw %}
// ...
let items = response.data.items; // or response.json.items if you're using core v9 or older
return items.map((item) => {
  item.id = item.contactId;
  return item;
});
{% endraw %}
{% endhighlight %}

Alternatively, if you're using the CLI, you can use non-id fields as the primary key. See ["How does deduplication work?"](https://github.com/zapier/zapier-platform/blob/main/packages/cli/README.md#how-does-deduplication-work) in the CLI docs for example code.

## Updated Item triggers

When triggering on updated items, you'll want to define the `id` field to be used for deduplication. Assuming your task API has an endpoint that can return tasks sorted by `updatedAt` in descending direction, here's example code to incorporate the `updatedAt` value with the `id`, so that Zapier recognizes a new update as a new item. Assuming that you have configured `options` with the appropriate API request URL and parameters:

{% highlight javascript %}
{% raw %}
return z.request(options)
  .then((response) => {
    response.throwForStatus();
    const results = response.json;
    results.forEach(function(result) {
      result.originalId = result.id;
      result.id = result.id + '-' + result.updatedAt;
    });
    return results;
  });
{% endraw %}
{% endhighlight %}

Notice how the code preserves the original `id` value before setting `id` to a new combined value that is unique for every update of a task. This is useful to ensure that the original ID can still be used for other purposes, such as performing a search or associating records together.

Alternatively, if you're using the CLI, you can set `primary: true` for the `id` and `updatedAt` fields. See ["How does deduplication work?"](https://github.com/zapier/zapier-platform/blob/main/packages/cli/README.md#how-does-deduplication-work) in the CLI docs for example code.
