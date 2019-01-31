---
title: Advanced Features
order: 9
layout: post-toc
redirect_from: /docs/
---

<a id="environment"></a>
## Environment Variables

Some APIs require additional data to authenticate or connect to your app. You may need a custom API key to pass to the API, along with users’ authentication credentials. Or you might want to set a sub-domain, role, user permissions, or other API configurations differently for your beta integration and live, active versions of your integration.

Zapier’s environment variables let you set these on a per-version basis for your app. Much like in local development environments such as the one in [Zapier’s CLI developer platform](https://zapier.github.io/zapier-platform-cli/#environment), environment variables store key and value pairs outside of your app’s API calls. Instead of hardcoding critical, secret values into your API authentication, trigger, and action calls, it’s best to add them as environment variables in your app’s _Advanced_ settings, then reference the environment variable in your API calls.

> **Tip**: Zapier’s built-in OAuth v2 Authentication automatically includes client ID and client secret fields, for two of the most commonly used environment variables. Only use the custom environment variables for other variables.

### How to Add Environment Variables

![Zapier Environment Variables](https://cdn.zapier.com/storage/photos/031d216898813b0d07c5d3936f075e51.png)
_Add any environment variables you need in key and value pairs_

To add environment variables, open your integration in Zapier visual editor and select the _Advanced_ tab in the left sidebar. There you can add your environment variables including a key and a value for each. Click _Add_ to include additional environment variables, or click the `x` icon to remove variables if needed.

### How to Reference Environment Variables

![Use Zapier Environment Variable](https://cdn.zapier.com/storage/photos/0b8ad13d723229c67df03ad1c114dd91.png)
_Use environment variables in Zapier’s API call forms or in custom code_

The easiest way to use environment variables in any Zapier integration API call is through the _Request Body_ form. Add your API URL, then click the _Show Options_ link and select _Request Body_ to see the data Zapier will send to your API. Add a new row, then enter your environment variable key as your API expects, then reference the environment variable in Zapier with the following text, replacing `YOUR_KEY` with your actual key:

{% raw %}`{{process.env.YOUR_KEY}}`{% endraw %}

Zapier will then replace that variable with the value for that key from your _Advanced_ settings—and will use the correct value every time if you change it in the future.

You can reference environment variables directly in your API calls the same way—though it’s best practice to include them in Zapier’s default request body instead. You can also reference them in custom code if you switch your API call to code mode.

### How to Change Environment Variables

![Edit Zapier Environment Variables](https://cdn.zapier.com/storage/photos/b3273bf07dc46636595fd11edee1da1f.png)
_You can change environment variable values, but not the original keys_

Need to change your environment variables for a new version of your integration, or before releasing your beta integration to the public? Open the _Advanced_ page in Zapier visual editor, and this time edit the text in the _Values_ column with the new variable values. You cannot edit the keys.

If you need to change a key and its value, first delete the old key, then add a new one instead.

<a id="computed"></a>
## Computed Fields

![Zapier Computed Fields](https://cdn.zapier.com/storage/photos/b82edea722597f88f5c0d21a46d6c847.png)

When adding an input field in your integration's authentication, Zapier includes a _Field Type_ option with two field options: _Field_ and _Computed Field_. The former is a standard input field much like those in the trigger and action [input designer](https://zapier.github.io/visual-builder/docs/input-designer), where users enter info needed for authentication such as usernames, passwords, and API keys.

Computed Fields, on the other hand, store values obtained from an integration's API test call, so they can be referenced in your integration's subsequent API calls.

Say your app includes a username that can be fetched with an API call using the API key—and your other API calls require the username be used. You would add a computed field that references that value from your server's response, much like the way you reference fields in connected accounts.

Zapier stores all fields returned by authentication API test call. Computed fields, however, are marked as _required_, so if the test API call does not return the field referenced in your computed field, Zapier will show an error.

If your app API calls in triggers or actions require account details or other info that users shouldn't have to enter manually, include a computed field in your app's authentication input fields. For the _Key_, use the exact same field name as the one your API returns. Zapier then will match the API test call's output to the field you included, so you can reference it from the input bundle with the following text, replacing `field` with your field key:

{% raw %}`{{bundle.authData.field}}`{% endraw %}