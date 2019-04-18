---
title: Zapier Deduplication
order: 4
layout: post-toc
redirect_from: /legacy/
---

# Zapier Deduplication

> We do the deduplication automatically for you, but you must be mindful of how it works. The important bits are outlined below!

Deduplication tl;dr:

*   Provide a unique `id` key.
*   Sort reverse-chronologically by time created.

An unfortunate artifact of [polling]({{base_url}}polling/) for new data is that we must deduplicate the results we get back from your API. After all, we don't want to trigger an action multiple times when a newly created item in your API exists in multiple distinct polls.

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

Every time a new Zap is created or turned on, we make a call to your API to populate our deduplication mechanism. We will cache and store each `id` field in our database.

After this, we will poll at an interval (based on customer's plan) looking for changes against this cached list of `id`s.

Now let's say we created a new to-do:

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

Only the first to-do with `id` equal to `8` will be seen as a new item. That particular JSON object will then be passed through to the action in the user's Zap. The others will be ignored since we already have seen their ids.

Your API must be able to return results in reverse-chronological order to make sure new/updated items can be found on the first page of results, as we don't fetch additional pages. [Wufoo is a great example](https://wufoo.github.io/docs/#form-entries) of an API that supports sorting on any field and direction.

One other requirement is the `id` field should always be supplied and unique among all items in the result.

## Custom or multiple ID fields

What if the items your API returns do not have an `id` field? Or how would you go about adding a *Updated to-do* trigger to our to-do app? In both cases you'll use [scripting]({{base_url}}scripting/#trigger-methods) to modify the API response.

Let's assume your to-do API has an endpoint to return to-dos sorted by `updatedAt` in descending direction. This is how you would use the scripting post poll trigger method:

{% highlight javascript %}
{% raw %}
var Zap = {
  TRIGGER_KEY_post_poll: function(bundle) {
    var items = z.JSON.parse(bundle.response.content);
    items.forEach(function(item) {
      item.originalId = item.id;
      item.id = item.id + '-' + item.updatedAt;
    });
    return items;
  }
}
{% endraw %}
{% endhighlight %}

Notice how we preserve the original value before setting `id` to a new combined value that is unique for every update of a to-do.

## Re-order items

What if your API cannot order its results in reverse-chronological order? How would you fetch the last page if you don't know how many pages there might be? Again scripting can help you deal with this.

Depending on your API it is most likely you will need to use the scripting poll trigger method. This will let you handle the [request(s) to your API]({{base_url}}scripting/#making-outbound-requests-zrequest).

One possible scenario could be:

1. Fetch the first page, containing the oldest items, but also the total number of pages.
2. Fetch the last page and reverse the order of the items before returning it.
