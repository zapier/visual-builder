---
title: Trigger data deduplication
order: 10
layout: post-toc
redirect_from: /docs/depupe
---

# Trigger data deduplication

> Zapier automatically deduplicates incoming trigger data for you, so that Zaps do not run multiple times on the same data, but you must be mindful of how it works. The important bits are outlined below!

Deduplication tl;dr:

*   Provide a unique `id` key.
*   Sort reverse-chronologically by time created.

An unfortunate artifact of [polling](https://platform.zapier.com/build/triggers#polling) for new data is that polling usually returns many results, most of which Zapier has seen before. Since we don't want to trigger an action multiple times when an item in your API exists in multiple distinct polls, we must deduplicate the data.

For example, say your endpoint returns a list of to-dos:

{% highlight javascript %}
{% raw %}
[
  {
    "id": 7,
    "created": "Mon, 25 Jun 2012 16:41:54 -0400",
    "list_id": 1,
    "description": "integrate our api with zapier",
    "complete": false
  },
  {
    "id": 6,
    "created": "Mon, 25 Jun 2012 16:41:45 -0400",
    "list_id": 1,
    "description": "get published in zapier library",
    "complete": false
  }
]
{% endraw %}
{% endhighlight %}

When a Zap is turned on, we make an initial call to your API to retrieve existing data, and cache and store each `id` field in our database.

After this, we will [poll at an interval](https://zapier.com/help/create/basics/learn-key-concepts-in-zapier#step-6) (based on a customer's plan) looking for changes against this cached list of `id`s.

Now let's say the user created a new to-do:

{% highlight javascript %}
{% raw %}
[
  {
    "id": 8,
    "created": "Mon, 25 Jun 2012 16:42:09 -0400",
    "list_id": 1,
    "description": "re-do our api to support webhooks",
    "complete": false
  },
  {
    "id": 7,
    "created": "Mon, 25 Jun 2012 16:41:54 -0400",
    "list_id": 1,
    "description": "integrate our api with zapier",
    "complete": false
  },
  {
    "id": 6,
    "created": "Mon, 25 Jun 2012 16:41:45 -0400",
    "list_id": 1,
    "description": "get published in zapier library",
    "complete": false
  }
]
{% endraw %}
{% endhighlight %}

On the next poll after the new to-do is created, the API returns all to-dos, but only the first to-do with `id` equal to `8` will be seen as a new item. That particular JSON object will then be passed through to the action in the user's Zap. The others will be ignored, since we already have seen their ids. That's the essence of deduplication.

In order for this mechanism to work, the `id` field should always be supplied and unique among all items in the result. 

Your API must also be able to return results in reverse-chronological order to make sure new/updated items can be found on the first page of results, as Zapier polling triggers don't automatically fetch additional pages. [Wufoo is a great example](https://wufoo.github.io/docs/#form-entries) of an API that supports sorting on any field and direction.

## Custom or multiple ID fields

What if the items your API returns do not have an `id` field? Or how would you go about adding a *Updated to-do* trigger to our to-do app? In both cases you would use [Code Mode](https://platform.zapier.com/build/code-mode) to modify the API response.

Let's assume your to-do API has an endpoint that can return to-dos sorted by `updatedAt` in descending direction. Here's an example of how you could add code to your trigger to incorporate the `updatedAt` value in the ID, so that Zapier recognizes a new update as a new item. Assuming that you have configured `options` with the appropriate API request URL and parameters:

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

Notice how the code preserves the original `id` value before setting `id` to a new combined value that is unique for every update of a to-do. This is useful to ensure that the original ID can still be used for other purposes, such as performing a search or associating records together.

## Re-order items

What if your API cannot order its results in reverse-chronological order? How would you fetch the last page if you don't know how many pages there might be? You can also use [Code Mode](https://platform.zapier.com/build/code-mode) to make additional requests, if necessary.

One possible scenario could be:

1. Fetch the first page, containing the oldest items, but also the total number of pages.
2. Fetch the last page and reverse the order of the items before returning it.

You should be cautious when adding additional requests to your custom code. All your requests and processing code for a trigger must [finish within 30 seconds](https://platform.zapier.com/build/operating-constraints#timeouts-triggers-1). It's not recommended to attempt to fetch all pages of results.
