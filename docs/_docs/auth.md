---
title: Authentication
order: 3
layout: post-toc
redirect_from: /docs/
---

# Authentication

Every Zap step starts with App authentication. Users select an app they wish to use, then authenticate their account with that app so Zapier can access their data.

Authentication allows Zapier access to an individual account in an app. Users connect one specific app account to Zapier, then Zapier can watch it for new or updated data, search for existing data, and create or update new data in that individual account on the app. Zapier may access the account until the authorization expires, is revoked, or credentials are changed, and may automatically refresh OAuth 2-powered authentications if enabled in the integration.

Once users authenticate their account on an app through Zapier, they can use any of that app's Zap steps without authenticating again. Users may also authenticate an app again if they wish to use additional accounts from an app with Zapier, typically to manage multiple projects or to use both work and personal accounts in workflows.

When building a Zapier integration, you define how the Zapier platform connects to your app to authenticates users, and add an API call where Zapier can test the account authentication. You can then test that API call yourself and connect an account to Zapier, which you can then use to test any subsequent Zap Triggers and Actions you add to the integration.

<a id="schemes"></a>
## Zapier Supported Authentication Schemes

![Zapier Authentication](https://cdn.zappy.app/1ecb446a74b35c93aa6d213219df3878.png)

All Zapier integrations that can access or add private data for users require authentication. The only apps don't require authentication include data feeds (such as news or weather updates) or utilities (such as file format conversion tools or public search engines). If you're building an integration for any app that stores private data and requires an account to use , your integration will require authentication.

Add authentication to your integration before adding triggers or actions. To do so, click the _Authentication_ tab in the left sidebar of Zapier's visual builder, then select the authentication scheme your app uses. Zapier supports the following five authentication schemes, each with their own settings:

### [Basic Auth](https://platform.zapier.com/docs/basic)
_As documented by [RFC 7616](https://developer.mozilla.org/en-US/docs/Web/HTTP/Authentication)_

Basic authentication lets users connect their accounts to Zapier with a username and password through a pre-built form that Zapier then passes with each API call to authenticate the user. You only have to add a test API call to confirm the username and password are valid.

Only use Basic Auth if it's the only way to authenticate your API calls, as it requires Zapier to store users' credentials.

_→ [Add Basic Auth to your Zapier Integration](https://platform.zapier.com/docs/basic)_

### [Session Auth](https://platform.zapier.com/docs/session)

Session authentication lets users enter their username and password or other app credentials, with optional custom fields if needed for authentication. Zapier then makes an API call to a token exchange URL where Zapier exchanges the credentials for an authentication token, which Zapier will use to authenticate every subsequent API call.

_→ [Add Session Auth to your Zapier Integration](https://platform.zapier.com/docs/session)_

### [API Key](https://platform.zapier.com/docs/apikey)

API key authentication lets users enter a custom API key from your app, and can optionally request additional info such as a domain. Users will need to locate an API key from your app, then enter it in the Zapier authentication form. Zapier will then pass the API key, along with any additional authentication details needed, to authenticate each API call.

_→ [Add API Key Auth to your Zapier Integration](https://platform.zapier.com/docs/apikey)_

### [OAuth v2](https://platform.zapier.com/docs/oauth)
_Same authentication flow as [Twitter](https://developer.twitter.com/en/docs/basics/authentication/overview) and [Trello](https://developers.trello.com/page/authorization)'s OAuth v2 implementation_

OAuth v2 authentication lets users sign into app accounts and allow Zapier access via a popup window from that app. The app sends a request token before the user authenticates, which Zapier then exchanges for an access token after they authenticate.

Use OAuth v2 whenever possible, as it matches users expectations for modern app authentication.

_→ [Add OAuth v2 Auth to your Zapier Integration](https://platform.zapier.com/docs/oauth)_

### [Digest Auth](https://platform.zapier.com/docs/digest)
_As documented by [RFC 7616](https://tools.ietf.org/html/rfc7616)_

Digest authentication lets users enter their username, password, and other required details for authentication in a Zapier-powered form. Then with every API call, Zapier first runs an API call to request the nonce key, before running the trigger or action's API call that passes the encrypted authentication details and any other API call data to your app. Zapier handles the nonce and quality of protection details automatically.

_→ [Add Digest Auth to your Zapier Integration](https://platform.zapier.com/docs/digest)_

> Limitation: Currently, only the MD5 algorithm is supported; MD5-sess and SHA are not implemented. In addition, server nonces are not reused, so for every `z.request` call, Zapier will sends an additional request first to get the server nonce.

<a id="label"></a>
## How to Add a Connection Label to Authenticated Accounts

![Zapier connection labels](https://cdn.zapier.com/storage/photos/ed16e77428f17e869e25d4f2111df1c9.png)
_A Zapier integration with a custom connection label (above) and without one (below)_

Zapier lets users authenticate multiple accounts for any app. By default, every new app account added to Zapier is identified by the app's name followed by a number for secondary accounts.

The connection label settings in your app's authentication options let you customize this account connection for your integration to include a username, email address, name, or other identifiable information in the connection label. That helps users distinguish between their authenticated accounts.

![Zapier Authentication Connection Label](https://cdn.zapier.com/storage/photos/f2c3d557023ce2a65b41122da34c1fdd.png)

Customize your app's connection label from the _Connection Label_ field in your Zapier integration. Zapier always includes the app's name in each account label. You can additionally include:

- Plain text that will be included after your app's full name
- Input fields with data users entered in the authentication form, referenced with {% raw %}`{{bundle.authData.field}}`{% endraw %} variables, replacing `field` for your input field name. With Basic auth, use `username` as the field.
- Output fields from your app's authentication test API call, referenced with {% raw %}`{{bundle.inputData.field}}`{% endraw %} variables, replacing `field` for your API output field name.

To add a connection label using an input field, enter the following in your _Connection Label_ field, optionally replacing `username` with the key for another input field your authentication form includes:

{% raw %}`{{bundle.authData.username}}`{% endraw %}

Alternately, you can use an output field from your test API call in the Connection Label if you know the name of the field you wish to use that your API sends to Zapier. Otherwise, skip adding the connection label first, and instead click _Connect an Account_ under step 2. Then click _Test Connected Account_ and check the _Response_ tab for a field that includes the data your app should use in the connection label. Finally, enter that field key in the following text instead of `field`, and add it to your _Connection Label_ field:

{% raw %}`{{bundle.inputData.username}}`{% endraw %}

If you need to use a nested field from your API call results, reference it as `field.nestedfield`. For example, if your test API response includes a `name` field nested under `details`, you would reference it as:

{% raw %}`{{bundle.inputData.details.name}}`{% endraw %}

You can include any field your authentication test API call returns in the connection label, though the best fields to use are usernames, domain names (if your app is self-hosted), account numbers, email addresses, or other identifiable but not fully private data. Never use passwords, API keys, or other critical, private info in connection labels.

<a id="connection-code"></a>
### How to Customize Connection Label with Code

![Zapier connection label with code](https://cdn.zapier.com/storage/photos/e9bf3fdaabe078e43b38a402106c1456.png)

You can customize your connection label further with JavaScript code, if needed. As before, Zapier will always include your app's name and integration version number first, followed by any text returned by your connection label code.

Custom code for connection labels are best used for:

- Using code to manipulate data from an auth or test call before using it in a connection label, such as to format a number or date
- Logging additional data to the authentication log
- Making a new API call to access data to use in the connection label

Click the _Edit Code_ button to switch to code mode. If the code mode is visible, Zapier will only use the code to create your connection label, and will ignore any existing text in the connection label field. If you wish to switch back to the regular field, click the _Delete Code_ button to delete your custom connection label code and revert to using the text entered in the connection label field.

Use JavaScript to customize your connection label, and include data from authData or inputData bundles as normal. Additionally, you can add custom data to Zapier's console log with the `z.console.log` function to assist testing and monitoring your app authentication.

<a id="test"></a>
## How to Test Authentication

![Test Zapier authentication](https://cdn.zapier.com/storage/photos/37a59dae4fe33ffc4894b1df23e7be83.png)

Once you've added the core details of how Zapier can authenticate users and test the connection, you need to try it out to set the final options. Click the _Connect an Account_ button to add your account with this app to Zapier.

Zapier will open a popup window like one your users will see when authenticating your app with Zapier. Enter your account info or API key, or authenticate through your app's site, using real account details for a personal or testing account.

> **Tip**: The account you add here will be the one you use to test any triggers and actions you add to Zapier in visual builder. It can also be used in live Zaps in Zapier, if you wish. These account details are not tied to your app definition, though, and if you add a collaborator to your Zapier integration, they will need to connect their own account for testing.

Once you've added your account, you'll see it with a connection label under the setup box. Then click _Test Connected Account_ to have Zapier run your testing API call and ensure your app connection works.

![Example Zapier authentication test response](https://cdn.zapier.com/storage/photos/d5cf1a5cbc5a8389ad3272d01ef71c06.png)

If everything works as expected, Zapier will receive response data from the API call and display it in the _Response_ tab. You can look through the JSON-formatted fields from the response and use any of the field names in your account [connection label](#label). You can also look at the _Bundle_ tab to see the data Zapier used in the API request, and the _HTTP_ tab to see the full request and response details.

![Example Zapier authentication error](https://cdn.zapier.com/storage/photos/3337e520ebab7b09de282e598ea70cfd.png)

If something didn't work, Zapier will show the error message in the _Response_ tab, with the full response content in the _HTTP_ tab if you need more detail. Update your authentication settings accordingly, click the _Save & Continue_ button, then try testing your connected account again—and repeat until your authentication works and tests correctly.

With that, your app authentication should be finished, and your integration ready to add triggers and actions.

<a id="change"></a>
## How to Remove or Change Zapier Integration Authentication Scheme

![Zapier Remove Authentication Scheme](https://cdn.zapier.com/storage/photos/a84d330dce6ccc18cbdeb12ca555b12d.png)

You cannot change an integration’s authentication scheme. Instead, remove an existing integration’s authentication then add a new authentication scheme.

To remove a Zapier integration's authentication scheme, open the _Authentication_ tab in the integration’s Zapier visual builder. Click the gear icon beside the existing authentication scheme, click _Delete_, then confirm to remove the authentication.

Then add your app’s new authentication scheme to the Zapier integration instead.

> **Note:** Never remove authentication from an existing, live integration. If an integration’s authentication scheme needs changed, clone a new major version and add the new authentication. Then migrate users to the new version, and deprecate the original version with breaking changes. [Learn more](https://platform.zapier.com/docs/versions){:target="_blank"}

<a id="error"></a>
## Common Authentication Error Messages

![404 error in Zapier basic auth](https://cdn.zapier.com/storage/photos/88b058e13a0321efdbdab3e0a046dfa5.png)

If Zapier cannot successfully make the test API call to verify users' credentials, you may see an error message in the Test section of your Zapier integration. Zapier shows a simplified error message in the _Response_ tab by default, along with a red x and a _Request Failed_ message in the top right.

![Zapier Error Response Content](https://cdn.zapier.com/storage/photos/2511421236621c8c5ea7c160f2a2ca7e.png)

You can find the original API response with the full error message in the _HTTP_ tab under _Response Content_.

The most common errors include:

### 404

![404 error in Zapier basic auth](https://cdn.zapier.com/storage/photos/88b058e13a0321efdbdab3e0a046dfa5.png)

The standard HTTP 404 `Not Found` error is commonly returned when:

- Test API endpoint URL is incorrect
- Test API call method is incorrect

If you encounter this error, double-check both the API endpoint URL and the call method (typically `GET`). Ensure both are set to what your API expects, then click the _Save & Continue_ button, and click the _Test Connected Account_ button again.

### 401 or 403

![401 error in Zapier basic auth](https://cdn.zapier.com/storage/photos/d13a9b1ff308b520ae4b29461cc754d6.png)

The standard HTTP 401 `Unauthorized` or HTTP 403 `Forbidden` error is commonly returned when:

- User account credentials are incorrect, expired, or revoked

Try authenticating your app user account with Zapier again. Click _Connect an Account_, add credentials for an active account on the app, then try the test again.

### 400

![400 error Zapier authentication](https://cdn.zapier.com/storage/photos/91579ed613b77fb803ff52fb900b093b.png)

The standard HTTP 400 `Bad Request` error is often returned when:

- OAuth v2 Client ID and/or Secret are incorrect or expired
- Some other part of your request, including the token request, are malformed

Check the full error message from the error or Zapier's testing logs to see if it lists why the call failed, then correct that part of your authentication flow. Then double-check that each part of your authentication flow is entered correctly, including the request headers and body on each part of your authentication flow.

### Error Parsing Response

![Error Parsing Response in Zapier Basic Auth](https://cdn.zapier.com/storage/photos/deebd9e07497a209479a66e7f1d465b0.png)

The _Error Parsing Response_ error is commonly returned when:

- API returns non-standard and especially non-JSON output
- Test API endpoint URL is incorrect

Double-check the test API URL is entered correctly. If a standard, non-API endpoint URL is entered in the test field, the site will return its raw HTML page to Zapier and will result in this error. If you do change the URL, click _Save & Continue_ then test your connection again.

If your API call is correct and returning data in a format Zapier does not expect, you will need to switch to code mode and add custom parsing for your API response. Under the _Test_ API call in the top of your app's Authentication settings, click _Switch to Code Mode_, then add custom JavaScript code to parse your API response.

### Authentication Failed Task Timed Out

![Zapier Authentication Timed Out](https://cdn.zapier.com/storage/photos/2bc7541d4859785d23a64dc5caceec22.png)

The _Authentication Failed_ error, often including _Task Timed Out_, is commonly returned when:

- API request doesn't return a response to Zapier
- API request response does not return within 30 seconds
- API request is formatted incorrectly and the server does not respond with an error code

This error often shows up when authenticating a test account, as in the above screenshot. Check your Zapier test logs to see if it shows which URL timed out, then check to ensure you've entered the correct URL in all of your app authentication settings. Finally, check the API provider to see if their site or API are temporarily down.

If the request seems to be successful but the task still times out, your API call may be taking too long to respond, or could be returning more data than Zapier can parse within the time limit. Try to use a testing API call in authentication that returns as little data as possible, such as a `/me` call that returns user account data. Or, if your API supports pagination and/or filtering, enable that and have the API return only the most recent result. Then test again to ensure the call works successfully.

### 500

![500 error when adding account in Zapier](https://cdn.zapier.com/storage/photos/22eb6cbc2c965dc196a3646511deeb7d.png)

The HTTP 500 error is the default, unformatted error that may be returned without specifying what went wrong or why. If you encounter this error, check the API endpoint URL that gave the error, and make sure your API call is configured correctly with the expected URL params, HTTP headers, and Request Body.
