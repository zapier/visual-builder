---
title: Advanced Features
order: 13
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

When adding an input field in your integration's authentication, Zapier includes a _Field Type_ option with two field options: _Field_ and _Computed Field_. The former is a standard input field much like those in the trigger and action [input designer](https://zapier.github.io/visual-builder/docs/input-designer), where users enter info needed for authentication.

> **Note:** Only use computed fields with session and OAuth v2 authentication.

Computed Fields, on the other hand, store values obtained from an integration's API test call, so they can be referenced in your integration's subsequent API calls.

Say your app includes a subdomain that can be fetched with an API call using the API key—and your other API calls require the subdomain be used in requests. You would add a computed field that references that value from your server's response, much like the way you reference fields in connected accounts.

Zapier stores all fields returned by authentication API test call and auth process. Computed fields, however, are marked as _required_ internally, so if the auth process does not return the field referenced in your computed field, Zapier will show an error. For example, if using OAuth v.2 authentication, the `getAccessToken` request must return any computed fields included in your app's authentication input form.

If your app API calls in triggers or actions require account details or other info that users shouldn't have to enter manually, include a computed field in your app's authentication input fields. For the _Key_, use the exact same field name as the one your API returns. Zapier then will match the API test call's output to the field you included, so you can reference it from the input bundle with the following text, replacing `field` with your field key:

{% raw %}`{{bundle.authData.field}}`{% endraw %}

<a id="bundle"></a>
## Zapier Data Bundles

Zapier stores data from users' authentication and input forms for API calls in the `bundle` object. You can reference that data in your integration using {% raw %}`{{bundle.bundleName.field}}`{% endraw %} text in API requests and connection labels, replacing `bundleName` with the bundle name and `field` with the input field key or API response field key you need. You can also reference bundles in custom code if you switch to code mode, using the same name but without the curly brackets, for example `return bundle.bundleName.field;` to have JavaScript code return a specific field.

If an API response includes a nested field, you can reference it as `field.nestedfield`, for example {% raw %}`{{bundle.inputData.data.name}}`{% endraw %} to reference a `name` nested field inside the `data` field.

Zapier integrations include the following bundles:

### authData

Referenced with: {% raw %}`{{bundle.authData.field}}`{% endraw %}

Includes data users enter into the authentication input form, including the `username` field for [Basic Auth](https://zapier.github.io/visual-builder/docs/basic) and any other field added to the authentication input form with other authentication methods. Additionally, with OAuth v2, Session Auth, and Digest Auth, `authData` includes all data returned by the Token Exchange Endpoint url, referenced with the following, replacing `field` with the field name from your API response:

{% raw %}`{{bundle.authData.field}}`{% endraw %}

For example, the Access Token value will often accessed via {% raw %}`{{bundle.authData.access_token}}`{% endraw %} or {% raw %}`{{bundle.authData.accessToken}}`{% endraw %}

Commonly used authData fields include:

- Username: {% raw %}`{{bundle.authData.username}}`{% endraw %}
- Password: {% raw %}`{{bundle.authData.password}}`{% endraw %}
- Access Token: {% raw %}`{{bundle.authData.access_token}}`{% endraw %} or {% raw %}`{{bundle.authData.accessToken}}`{% endraw %}

### inputData

Referenced with: {% raw %}`{{bundle.inputData.field}}`{% endraw %}

In authentication fields and connection labels, `inputData` contains the output fields returned from the test API call, typically used to add a label to new integration connections.

In Trigger and Action steps, `inputData` contains the data from input forms that users enter themselves which Zapier passes to the app with that Trigger or Action's API call, with {% raw %}`{{curlies}}`{% endraw %} mapped fields from previous Zap steps rendered with their raw data.

If you want the input field data with the original {% raw %}`{{curlies}}`{% endraw %} and not the text from previous steps, use {% raw %}`{{bundle.inputDataRaw.field}}`{% endraw %} instead.

Commonly used inputData fields include:

- Zapier Redirect URI: {% raw %}`{{bundle.inputData.redirect_uri}}`{% endraw %}
- Authentication Code: {% raw %}`{{bundle.inputData.code}}`{% endraw %}

### rawRequest and cleanedRequest

> Note: Only used with the `getAccessToken` data from OAuth v2 authentication

Referenced with: {% raw %}`{{bundle.rawRequest}}`{% endraw %} or {% raw %}`{{bundle.cleanedRequest.field}}`{% endraw %}

Includes the raw or cleaned info, respectively, from the user's browser request that triggers the `getAccessToken` call from OAuth v2 authentication. Can reference individual fields with `cleanedRequest`.

### targetURL

Referenced with: {% raw %}`{{bundle.targetURL}}`{% endraw %}

In triggers using REST hooks, this returns the URL a site should send data to, such as `https://hooks.zapier.com/1234/abcd`.

### subscribeData

Referenced with: {% raw %}`{{bundle.subscribeData}}`{% endraw %}

In triggers using REST hooks, this includes the data from the `performSubscribe` function which is used if you need to send a `DELETE` request to your server to stop sending webhook data to Zapier

### process.env

Referenced with: {% raw %}`{{process.env.field}}`{% endraw %}

Commonly used process.env fields include:

- Client Secret: {% raw %}`{{process.env.CLIENT_SECRET}}`{% endraw %}
- Client ID: {% raw %}`{{process.env.CLIENT_ID}}`{% endraw %}
