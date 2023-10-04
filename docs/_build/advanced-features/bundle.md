---
title: Reference user-entered details with data bundles
order: 3
layout: post-toc
redirect_from: 
---

# Reference user-entered details with data bundles

Zapier stores data from users' authentication and input forms for API calls in the `bundle` object. You can reference that data in your integration using {% raw %}`{{bundle.bundleName.field}}`{% endraw %} text in API requests and connection labels, replacing `bundleName` with the bundle name and `field` with the input field key or API response field key you need. You can also reference bundles in custom code if you switch to Code Mode for a request, using the same name but without the curly brackets, for example `return bundle.bundleName.field;` to have JavaScript code return a specific field.

If an API response includes a nested field, you can reference it as `field.nestedfield`, for example {% raw %}`{{bundle.inputData.data.name}}`{% endraw %} to reference a `name` nested field inside the `data` field.

Zapier integrations include the following bundles:

- authData
- inputData
- meta
- rawRequest and cleanedRequest
- outputData
- targetURL
- subscribeData
- process.env

## authData

Reference with: {% raw %}`{{bundle.authData.field}}`{% endraw %}

Includes data users enter into the authentication input form, including the `username` field for [basic authentication](https://platform.zapier.com/build/basicauth) and any other field added to the authentication input form with other authentication methods. Additionally, with OAuth v2, session authentication, and digest authentication, `authData` includes all data returned by the Token Exchange Endpoint url, referenced with the following, replacing `field` with the field name from your API response:
{% raw %}`{{bundle.authData.field}}`{% endraw %}

For example, the Access Token value will often be accessed via {% raw %}`{{bundle.authData.access_token}}`{% endraw %} or {% raw %}`{{bundle.authData.accessToken}}`{% endraw %}.

However, the `authData` bundle does not support nested objects: all values returned from authentication functions need to be at the top level. This bundle also does not include values provided by intermediate steps in OAuth v2 or session authentication flows, like `redirect_uri`.

Commonly used authData fields include:
- Username: {% raw %}`{{bundle.authData.username}}`{% endraw %}
- Password: {% raw %}`{{bundle.authData.password}}`{% endraw %}
- Access Token: {% raw %}`{{bundle.authData.access_token}}`{% endraw %} or {% raw %}`{{bundle.authData.accessToken}}`{% endraw %}

## inputData

Reference with: {% raw %}`{{bundle.inputData.field}}`{% endraw %}

In authentication configuration, including connection labels, `inputData` contains the fields returned from the test API call, as well as some values provided by intermediate steps in more complex auth flows, such as the OAuth v2 `redirect_uri`. Values returned by the test API call are typically used to add a [connection label](./auth#label) to new integration connections.

In triggers and actions, `inputData` contains the data that users enter into the input forms for this particular run of the trigger or action. The {% raw %}`{{curlies}}`{% endraw %} (mapped fields from previous Zap steps) are rendered with their raw data from previous steps. 

If you want the input field data with the original {% raw %}`{{curlies}}`{% endraw %} and not the data from previous steps, use {% raw %}`{{bundle.inputDataRaw.field}}`{% endraw %} instead. This is less common. 

Commonly used inputData fields include:
- Zapier Redirect URI: {% raw %}`{{bundle.inputData.redirect_uri}}`{% endraw %}
- Authorization Code: {% raw %}`{{bundle.inputData.code}}`{% endraw %}
- ID of selected triggering event: {% raw %}`{{bundle.inputData.id}}`{% endraw %}

## meta

Reference with: {% raw %}`{{bundle.meta.field}}`{% endraw %}

`bundle.meta` contains information on what the user is doing. It has the following options for `field`:

| key | default | description |
| --- | --- | --- |
| `isLoadingSample` | `false` | If true, this run was initiated manually via the Zap Editor |
| `isFillingDynamicDropdown` | `false` | If true, this poll is being used to populate a dynamic dropdown. You only need to return the fields you specified (such as `id` and `name`), though returning everything is fine too |
| `isPopulatingDedupe` | `false` | If true, the results of this poll will be used to initialize the deduplication list rather than trigger a zap. You should grab as many items as possible. See also: [deduplication](#dedup) |
| `limit` | `-1` | The number of items you should fetch. `-1` indicates there's no limit. Build this into your calls insofar as you are able |
| `page` | `0` | Used in [paging](#paging) to uniquely identify which page of results should be returned |
| `isTestingAuth` | `false` | (legacy property) If true, the poll was triggered by a user testing their account (via [clicking "test"](https://cdn.zapier.com/storage/photos/5c94c304ce11b02c073a973466a7b846.png) or during setup). We use this data to populate the auth label, but it's mostly used to verify we made a successful authenticated request |

## rawRequest and cleanedRequest
> Note: `bundle.rawRequest` and `bundle.cleanedRequest` are only available in the `perform` for webhooks, `getAccessToken` for OAuth v2 and `performResume` in callback actions.

Reference with: {% raw %}`{{bundle.rawRequest}}`{% endraw %} or {% raw %}`{{bundle.cleanedRequest.field}}`{% endraw %}

It includes the raw or cleaned information, respectively, from the HTTP request that triggered the `perform` method, or from the user's browser request that triggers the `getAccessToken` call from OAuth v2 authentication. You can reference individual fields with `cleanedRequest`.

Use `bundle.rawRequest` if you need access to header data. In `bundle.rawRequest`, headers other than `Content-Length` and `Content-Type` will be prefixed with `Http-`, and all headers will be named in Camel-Case.

## outputData

Reference with: {% raw %}`{{bundle.outputData}}`{% endraw %}

> Note: `bundle.outputData` is only available in the `performResume` in a callback action - read about that advanced functionality [here](https://github.com/zapier/zapier-platform/blob/main/packages/cli/README.md#zgeneratecallbackurl). 

Using `bundle.outputData` will return a whatever data you originally returned in the `perform`, allowing you to mix that with `bundle.rawRequest` or `bundle.cleanedRequest`.

## targetUrl
Referenced with: {% raw %}`{{bundle.targetUrl}}`{% endraw %}

In triggers using REST hooks, this returns the URL your app should send data to when the triggering event occurs, such as `https://hooks.zapier.com/1234/abcd`.

## subscribeData
Referenced with: {% raw %}`{{bundle.subscribeData}}`{% endraw %}

In triggers using REST hooks, this includes the data returned by your API from the `performSubscribe` function. This should include all information needed to send a `DELETE` request to your server to stop sending webhook data to Zapier when the user turns off a Zap.

## process.env

Reference with: {% raw %}`{{process.env.field}}`{% endraw %}

Commonly used process.env fields include:
- Client Secret: {% raw %}`{{process.env.CLIENT_SECRET}}`{% endraw %}
- Client ID: {% raw %}`{{process.env.CLIENT_ID}}`{% endraw %} 


