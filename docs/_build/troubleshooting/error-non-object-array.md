---
title: Got a non-object result in the array, expected only objects
order: 12
layout: post-toc
redirect_from: 
---

# Error: Got a non-object result in the array, expected only objects

## Error shown

When using a REST Hook trigger, the data returned by the perform must be an array.

If an API returns a non-object result within the array, or an array of arrays, the following error will show.

{% raw %}
`Got a non-object result in the array, expected only objects ( )`
  {% endraw %}

The non-object result will be wrapped in the parentheses for the error message. 

## Solution

If the data included in the webhook needs to be transformed, or includes multiple objects, you can add custom code to parse the response data in `bundle.cleanedRequest` within the Perform into an array of objects.

If your webhook already provides an array, remove the wrapping array that Zapier includes by default and simply return `bundle.cleanedRequest`.

![image](https://cdn.zappy.app/26459a11e1630fe8318c341bf598ab5a.png)


 