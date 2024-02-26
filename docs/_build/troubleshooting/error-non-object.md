---
title: Error -  Got a non-object result, expected an object from create
order: 11
layout: post-toc
redirect_from: 
---

# Error: Got a non-object result, expected an object from create

## Error shown

When you add a create action to your integration, the Zapier platform [expects a single object to be returned](https://platform.zapier.com/build/response-types), containing an `id` and details about the new item created. If an API returns a non-object result, the following error will show.

{% raw %}
`CheckError: Invalid API Response: - Got a non-object result, expected an object from create`
  {% endraw %}

## Solution

Instead, make sure your API returns an object to Zapier. To do that switch to [Code Mode](https://platform.zapier.com/build/code-mode) in your request. That will allow you to provide a JavaScript function to handle the request, and make needed changes to the structure or content of the result before returning data to the Zapier platform.

If an array is returned, you would parse the response to return the object, without being enclosed in an array.

This could be by enclosing the `results` in a `{ }`, or reaching into the array and pull out the object that represents what you want to return to the user.

> Remember: [Code Mode]((https://platform.zapier.com/build/code-mode)) is a toggle; if you switch back to Form Mode your code will be ignored!

Once you retest the create request, it should run successfully.