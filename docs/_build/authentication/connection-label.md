---
title: Add a connection label
order: 7
layout: post-toc
redirect_from: 
    -/build/auth#how-to-add-a-connection-label-to-authenticated-accounts
---

# Add a connection label

Zapier users can authenticate multiple accounts for any app. By default, every new app account added to Zapier is identified by the app's name, followed by a number (#2, #3, ...) for accounts connected after the first.

A connection label in the integration authentication options adds optional text as the name of each account connection to help users distinguish between their authenticated accounts.

![Zapier Authentication Connection Label](https://cdn.zappy.app/b2612dc2bf60454eea4ae37335638bf5.png)

## Prerequisites:

- A configured authentication scheme in the Platform UI

## To add a connection label

1. Enter your desired value into the _Connection Label_ field in the authentication configuration, as the name of the field, surrounded by double curly braces

2. Zapier always includes the app's name in each account label, so it is redundant to add any hard coded app name into your connection label.  

3. Instead, add either:

- Data that users enter in the authentication form
- Output fields from your app's authentication test API call

For example, if your auth configuration includes a `username` field, your connection label could look like:

{% raw %}`{{username}}`{% endraw %}

Alternatively, you can use an output field from your test API call in the Connection Label. If you aren't sure what fields will be returned, you'll want to test your authentication first, and return to the connection label. 

After connecting an account, check the _Response_ tab to see the fields returned from the test request. 

4. Field keys from the authentication form and the test request are both pulled up to the top level.
 
You can also refer to the fields with {% raw %}`{{bundle.authData.field}}`{% endraw %} for input fields from the authentication form, replacing `field` with your input field key. Use {% raw %}`{{bundle.inputData.field}}`{% endraw %} for fields returned from the test request, replacing `field` with the field key from the API response.

If you need to use a nested field from your API call results, reference it as `field.nestedfield`. For example, if your test API response includes a `name` field nested under `details`, you would reference it as:

{% raw %}`{{bundle.inputData.details.name}}`{% endraw %}

Any field your authentication test API call returns can be used in the connection label. The best fields to use are usernames, domain names (if your app is self-hosted), account numbers, email addresses, or other identifiable but not fully private data. Never use passwords, API keys, or other critical, private info in connection labels.

5. Customize your connection label further with JavaScript code as needed. 

Custom code for connection labels is best used for:

- Using code to manipulate data from an auth or test call before using it in a connection label, such as to format a number or date
- Logging additional data
- Making a new API call to access data to use in the connection label

Select _Edit Code_ to switch to _[Code Mode](link to https://coda.io/d/Overhaul-platform-docs_dRIxVbcnE_L/Use-Code-Mode-to-refine-your-API-call_suwCV#_luwtY)_. When_Code Mode_ is enabled, Zapier will only use the code to create your connection label, and will ignore any text that was in the _Connection Label_ field in the regular string mode. 

To switch back to the regular string field, click the _Delete Code_ button to delete your custom connection label code and revert to using the text entered in the _Connection Label_ field.

When writing code for the connection label, fields are not pulled up to the top level of  the `bundle` object - use `bundle.authData` for auth input fields, or `bundle.inputData` for fields returned from the test API request. For example, your code might look like this:

```
return bundle.authData.username;
```

This is equivalent to using {% raw %}`{{username}}`{% endraw %} in the regular string mode.

Add custom data to Zapier's console log with the `z.console.log` function to assist with testing and monitoring your app authentication.

![Zapier connection label with code](https://cdn.zappy.app/c099e1aaa7a6bbe1674cc830aed68573.png)