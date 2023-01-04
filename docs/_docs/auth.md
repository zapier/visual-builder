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

When building a Zapier integration, you define how the Zapier platform connects to your app to authenticate users, and add an API call where Zapier can test the account authentication. After configuring authentication, you can attempt to create a connection to your app on Zapier to validate the configuration. You can then use the connection to test any Triggers and Actions you add to the integration.

<a id="schemes"></a>
## Zapier Supported Authentication Schemes

![Zapier Authentication](https://cdn.zappy.app/37e7829169eb2e07278d512c174cd708.png)

All Zapier integrations that can access or add private data for users require authentication. The only apps that don't require authentication include data feeds (such as news or weather updates) or utilities (such as file format conversion tools or public search engines). If you're building an integration for any app that stores private data and requires an account to use, your integration will require authentication.

Add authentication to your integration before adding triggers or actions. To do so, click the _Authentication_ tab in the left sidebar of Zapier's visual builder, then select the authentication scheme your app uses. Zapier supports the following five authentication schemes, each with their own settings:

### [Basic Auth](https://platform.zapier.com/docs/basic)
_As documented by [RFC 7616](https://developer.mozilla.org/en-US/docs/Web/HTTP/Authentication)_

Basic authentication lets users connect their accounts to Zapier with a username and password. Zapier passes the provided credentials with each API call to authenticate the user. For Basic Auth, username and password are requested automatically.

The only other requirement is to add a test API call to confirm the credentials are valid, but you can add additional input fields if needed.

Only use Basic Auth if it's the only way to authenticate your API calls, as it requires Zapier to store users' credentials.

_→ [Add Basic Auth to your Zapier Integration](https://platform.zapier.com/docs/basic)_

### [Session Auth](https://platform.zapier.com/docs/session)

Session authentication also starts with users providing their app credentials, such as their username and password. Using the credentials, Zapier makes an API call to a token exchange URL, and exchanges the credentials for an authentication token. The token is used to authenticate every subsequent API call.

_→ [Add Session Auth to your Zapier Integration](https://platform.zapier.com/docs/session)_

### [API Key](https://platform.zapier.com/docs/apikey)

API key authentication lets users provide an API key or similar credential from your app, along with any additional information, such as a domain. Zapier then uses the API key and any additional details to authenticate each API call.

_→ [Add API Key Auth to your Zapier Integration](https://platform.zapier.com/docs/apikey)_

### [OAuth v2](https://platform.zapier.com/docs/oauth)
_Zapier's OAuth 2 implementation is based on the `authorization_code` flow, similar to [GitHub](https://developer.github.com/v3/oauth/) and [Facebook](https://developers.facebook.com/docs/authentication/server-side/)._

OAuth 2.0 authentication lets users sign into app accounts and allow Zapier access via a popup window from that app. The app sends an authorization code when the user authenticates, which Zapier exchanges for an access token that's used to authenticate subsequent calls.

Use OAuth 2.0 whenever possible, as it matches users' expectations for modern app authentication.

_→ [Add OAuth v2 Auth to your Zapier Integration](https://platform.zapier.com/docs/oauth)_

### [Digest Auth](https://platform.zapier.com/docs/digest)
_As documented by [RFC 7616](https://tools.ietf.org/html/rfc7616)_

Digest authentication lets users enter their username, password, and other required details for authentication in a Zapier-powered form. With every subsequent request, Zapier first makes an API call to request the nonce key before running the trigger or action's API call. The encrypted authentication details and any other API call data are included in the request to your app. Zapier handles the nonce and quality of protection details automatically.

_→ [Add Digest Auth to your Zapier Integration](https://platform.zapier.com/docs/digest)_

> Limitation: Currently, only the MD5 algorithm is supported; MD5-sess and SHA are not implemented. In addition, server nonces are not reused, so for every `z.request` call, Zapier will sends an additional request first to get the server nonce.

<a id="label"></a>
## How to Add a Connection Label to Authenticated Accounts

![Zapier connection labels](https://cdn.zappy.app/ba08dccacb2a91f648506438040f0cec.png)
_A Zapier integration with a custom connection label (above) and without one (below)_

Zapier lets users authenticate multiple accounts for any app. By default, every new app account added to Zapier is identified by the app's name, followed by a number (#2, #3, ...) for accounts connected after the first.

The _Connection Label_ field in your app's authentication options lets you add additional text to the name of the account connections for your integration. The text could include a username, email address, name, or other identifiable information in the users' accounts. That helps users distinguish between their authenticated accounts.

![Zapier Authentication Connection Label](https://cdn.zappy.app/b2612dc2bf60454eea4ae37335638bf5.png)

Zapier always includes the app's name in each account label. You can add:

- Plain text that will be included after your app's full name
- Data that users entered in the authentication form
- Output fields from your app's authentication test API call

To add a field value to the connection label, enter the name of the field, surrounded by double curly braces, in the _Connection Label_ field.

For example, if your auth configuration includes a `username` field, your connection label could look like:

{% raw %}`{{username}}`{% endraw %}

Alternately, you can use an output field from your test API call in the Connection Label. If you aren't sure what fields will be returned, skip this step for now and go to Step 3, _Test your Authentication_.

After connecting an account, check the _Response_ tab to see the fields returned from the test request. Then, return to Step 2, and enter that field key in the _Connection Label_ field. So if the field you want to use is called `team`, enter:

{% raw %}`{{team}}`{% endraw %}

When setting up a simple text connection label with dynamic fields, field keys from the authentication form and the test request are both pulled up to the top level, which is why simple field keys like `username` will work.
 
You can also refer to the fields with {% raw %}`{{bundle.authData.field}}`{% endraw %} for input fields from the authentication form, replacing `field` with your input field name. Use {% raw %}`{{bundle.inputData.field}}`{% endraw %} for fields returned from the test request, replacing `field` with the field name from the API response.

If you need to use a nested field from your API call results, reference it as `field.nestedfield`. For example, if your test API response includes a `name` field nested under `details`, you would reference it as:

{% raw %}`{{bundle.inputData.details.name}}`{% endraw %}

You can include any field your authentication test API call returns in the connection label, though the best fields to use are usernames, domain names (if your app is self-hosted), account numbers, email addresses, or other identifiable but not fully private data. Never use passwords, API keys, or other critical, private info in connection labels.

<a id="connection-code"></a>
### How to Customize Connection Label with Code

![Zapier connection label with code](https://cdn.zappy.app/c099e1aaa7a6bbe1674cc830aed68573.png)

You can customize your connection label further with JavaScript code if needed. Zapier will always include your app's name first, followed by any text returned by your connection label code.

Custom code for connection labels is best used for:

- Using code to manipulate data from an auth or test call before using it in a connection label, such as to format a number or date
- Logging additional data
- Making a new API call to access data to use in the connection label

Click the _Edit Code_ button to switch to [Code Mode](./faq#how-does-code-mode-work). If the Code Mode is active, Zapier will only use the code to create your connection label, and will ignore any text that was in the _Connection Label_ field in the regular string mode. 

If you want to switch back to the regular field, click the _Delete Code_ button to delete your custom connection label code and revert to using the text entered in the _Connection Label_ field.

When writing code for the connection label, fields are not pulled up to the top level of  the `bundle` object - you must use `bundle.authData` for auth input fields, or `bundle.inputData` for fields returned from the test API request. For example, your code might look like this:

```
return bundle.authData.username;
```

This is equivalent to using {% raw %}`{{username}}`{% endraw %} in the regular string mode.

You can also add custom data to Zapier's console log with the `z.console.log` function to assist with testing and monitoring your app authentication.

<a id="test"></a>
## How to Test Authentication

![Test Zapier authentication](https://cdn.zappy.app/d8aab4144694a3646732955601841a3e.png)

Once you've added the core details of how Zapier can authenticate users and test the connection, you need to try it out to set the final options. Click the _Sign in_ button to add your account with this app to Zapier.

Zapier will open a popup window (the same one your users will see) to prompt you to enter the necessary information. Enter your account info or API key, or authenticate through your app's site, using real account details for a personal or testing account.

> **Tip**: The account you add here will be the one you use to test any triggers and actions you add to Zapier. It can also be used in live Zaps in Zapier, if you wish. These account details are not tied to your app definition, though -- they're tied to your user account. If you add a collaborator to your Zapier integration, they will need to connect their own account for testing.

If the connection attempt succeeds, you'll see the new account connection, with any connection label detail you added, under the setup box. Click _Test Authentication_ to have Zapier run your testing API call and show the results.

![Example Zapier authentication test response](https://cdn.zappy.app/f6f70c7b655e99fd8812dfb9173d8d93.png)

If the test call works as expected, Zapier will receive response data from the API call and display it in the _Response_ tab. You can look through the JSON-formatted fields from the response and use any of the field names in your account [connection label](#label). You can also look at the _Bundle_ tab to see the data Zapier used in the API request, and the _HTTP_ tab to see the full request and response details.

![Example Zapier authentication error](https://cdn.zappy.app/9892012662de1492bc4032d8eaa91763.png)

If the connection attempt fails, no account connection will be created. Zapier will show the error message in the _Response_ tab, with the full response content in the _HTTP_ tab if you need more detail. Update your authentication settings accordingly, click the _Save & Continue_ button, then try testing your connection account again. Repeat until your authentication connects and tests correctly.

With that, your app authentication should be finished, and your integration ready to add triggers and actions.

<a id="change"></a>
## How to Remove or Change Zapier Integration Authentication Scheme

![Zapier Remove Authentication Scheme](https://cdn.zappy.app/a616ced2f22bdf0873b0f910fc238424.png)

You cannot change an integration’s authentication scheme. Instead, remove an existing integration’s authentication, then add a new authentication scheme.

To remove a Zapier integration's authentication scheme, open the _Authentication_ page. Click the gear icon beside the existing authentication scheme, click _Delete_, then confirm to remove the authentication.

Then add your app’s new authentication scheme to the Zapier integration instead.

> **Note:** Never remove authentication from an existing, live integration. If an integration’s authentication scheme needs to be changed, clone a new major version and add the new authentication. [Learn more](https://platform.zapier.com/docs/versions){:target="_blank"}

<a id="error"></a>
## Common Authentication Error Messages

![404 error in Zapier basic auth](https://cdn.zappy.app/f6e4616d8e457f2ccf8dd872b2a15aac.png)

If Zapier cannot successfully make the test API call to verify users' credentials, you may see an error message in the Test section of your Zapier integration. Zapier shows a simplified error message in the _Response_ tab by default.

![Zapier Error Response Content](https://cdn.zappy.app/2598ca338518d55cb41cebc2116bd1af.png)

You can find the original API response with the full error message in the _HTTP_ tab under _Response Content_.

The most common errors include:

### 404

![404 error in Zapier basic auth](https://cdn.zappy.app/4b268ddfa326ee23cb902d05acc6ac10.png)

The standard HTTP 404 `Not Found` error is commonly returned when:

- Test API endpoint URL is incorrect
- Test API call method is incorrect

If you encounter this error, double-check both the API endpoint URL and the call method (typically `GET`). Ensure both are set to what your API expects, then click the _Save & Continue_ button, and click the _Test Connected Account_ button again.

### 401 or 403

![401 error in Zapier basic auth](https://cdn.zappy.app/e8dd16ccd395d9c466d81ce669510296.png)

The standard HTTP 401 `Unauthorized` or HTTP 403 `Forbidden` error is commonly returned when:

- User account credentials are incorrect, expired, or revoked

Try authenticating your app user account with Zapier again. Click _Connect an Account_, add credentials for an active account on the app, then try the test again.

### 400

![400 error Zapier authentication](https://cdn.zapier.com/storage/photos/91579ed613b77fb803ff52fb900b093b.png)

The standard HTTP 400 `Bad Request` error is often returned when:

- OAuth v2 Client ID and/or Secret are incorrect or expired
- Some other part of your request is malformed, particularly a token exchange request

Check the full error message from the error or Zapier's testing logs to see if it lists why the call failed, then correct that part of your authentication flow. Then double-check that each part of your authentication flow is entered correctly, including the request headers, URL parameters, and request body for each part of your authentication flow.

### Error Parsing Response

![Error Parsing Response in Zapier Basic Auth](https://cdn.zappy.app/7dc661d47076c1114b2581289646de48.png)

The _Error Parsing Response_ error is commonly returned when:

- API returns non-standard and especially non-JSON output
- Test API endpoint URL is incorrect

Double-check that the test API URL is entered correctly. If a normal webpage URL is entered in the test field, the site will return its raw HTML content to Zapier and that will likely result in this error. If you do change the URL, click _Save & Continue_, then test your connection again.

If your API call is correct and returning data in a format Zapier does not expect, you will need to switch to [Code Mode](./faq#how-does-code-mode-work) and add custom parsing for your API response. Under the _Test_ API call in the top of your app's Authentication settings, click _Switch to Code Mode_, then add custom JavaScript code to parse your API response.

### Authentication Failed Task Timed Out

![Zapier Authentication Timed Out](https://cdn.zapier.com/storage/photos/2bc7541d4859785d23a64dc5caceec22.png)

The _Authentication Failed_ error, often including _Task Timed Out_, is commonly returned when:

- The API request does not return a response to Zapier within 30 seconds
- The API request is formatted incorrectly and the server does not respond with an error code

This error often shows up when authenticating a test account, as in the above screenshot. Check your Zapier test logs to see if it shows which URL timed out, then check to ensure you've entered the correct URL in all of your app authentication settings. Finally, check the API provider to see if their site or API are temporarily down.

If the request seems to be successful but the task still times out, your API call may be taking too long to respond, or could be returning more data than Zapier can parse within the time limit. Try to use a testing API call in authentication that returns as little data as possible, such as a `/me` call that returns the connected user's account data. Or, if your API supports pagination and/or filtering, enable that and have the API return only the most recent result. Then test again to ensure the call works successfully.

### 500

![500 error when adding account in Zapier](https://cdn.zapier.com/storage/photos/22eb6cbc2c965dc196a3646511deeb7d.png)

The HTTP 500 error is the default, unformatted error that may be returned without specifying what went wrong or why. If you encounter this error, check the API endpoint URL that gave the error, and make sure your API call is configured correctly with the expected URL params, HTTP headers, and Request Body.
