---
title: Error -  An array is expected
order: 10
layout: post-toc
redirect_from: 
    - /build/faq#i-got-an-an-array-is-expected-error-how-do-i-fix-that
---

# Error: An array is expected

## Error shown

When you add a polling trigger or search action to your integration, the Zapier platform [expects a bare array of new or found items returned](https://platform.zapier.com/build/response-types), sorted in reverse chronological order. An API may instead return a result _object_ that contains the array of items the trigger/search needs.

{% raw %}
For example, for a "Find Issue" search action with GitHub's API, we might start with a `https://api.github.com/repos/{{bundle.inputData.owner}}/ {{bundle.inputData.repo}}/issues/{{bundle.inputData.issue_number}}` request:
{% endraw %}

![](https://cdn.zappy.app/a5516cc30abee4f84a58ac5b7b3dfc76.png)

When tested, Zapier will show an error message `Results must be an array, got: object,`

![](https://cdn.zappy.app/2461b0e7f49ecf5aed90d429a59ad2bf.png)

Check the API response in the HTTP tab of the _[Test your API Request](https://platform.zapier.com/build/test-triggers-actions)_ section, and you'll see an _object_ that contains the array of items we need was returned, not the array itself:

![](https://cdn.zappy.app/d569e3a05f643a9a199b5d85dc4a4fc2.png)

## Solution

Instead, return that array of channels to Zapier. To do that switch to [Code Mode](https://platform.zapier.com/build/code-mode) in your request. That will allow you to provide a JavaScript function to handle the request, and make needed changes to the structure or content of the result before returning data to the Zapier platform.

For this request, wrap the response with an array instead of the default `return results`, to have Zapier return an array of issues.

![](https://cdn.zappy.app/3bec13fa502f47ff1e5f9bfded052b4d.png)

> Remember: [Code Mode]((https://platform.zapier.com/build/code-mode)) is a toggle; if you switch back to Form Mode your code will be ignored!

Now, retest the request and it should run successfully.

![](https://cdn.zappy.app/af56c7fed5183aed462d2e7efbf78f8c.png)