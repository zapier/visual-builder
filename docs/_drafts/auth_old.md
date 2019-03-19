---
title: Authentication
order: 3
layout: post-toc
redirect_from: /docs/
---

## Authentication

![Add Zapier integration](https://cdn.zapier.com/storage/photos/5f1a0e1fc0eb5635bdf1a2983f31a9ba.png)

Most apps require authentication to access data via API calls, whether to let users access their personal data or enable access to restricted APIs. When building a Zapier integration, you define how the Zapier platform connects to your app and authenticates users.

Zapier supports five authentication schemes: Basic Auth, Session Auth, API Keys, OAuth v2, and Digest Auth. The default settings for each cover most applications’ authentication, or you can customize the authentication if your API has specific needs.

Zapier uses the authentication settings you add to your integration to request the user account, API key, or other details needed—or with session and OAuth authentication, Zapier will redirect users to your application where they can allow access to their accounts and your app can send credentials to Zapier.

![Zapier account authentication popup windows](https://cdn.zapier.com/storage/photos/b92a498ec3cadea178a24694127a2bf6.png)
_An example popup login window for OAuth v2 on the left, and for Basic Auth on the right_

When people select your integration in a Zap, they first select your app and the trigger or action step they wish to use. Zapier then asks them to authenticate with your app, where they'll see a window like one of those above, depending on your authentication scheme. With OAuth, Zapier redirects the user to your authentication site where they login with their account and authorize Zapier to access their data. With basic and API authentication, Zapier shows a form where users enter their account credentials.

## Zapier Supported Authentication Schemes

### Basic Auth
_As documented by [RFC 7616](https://developer.mozilla.org/en-US/docs/Web/HTTP/Authentication)_

The simplest authentication method, Basic Authentication requires nearly zero setup when building a Zapier integration. By default Zapier includes a login form that requests users' username and password for your app, then passes that to your app along with each API call to authenticate the user. This authentication method is only recommended if it's the only one available to your app.

### Session Auth

Session authentication works somewhat like a hybrid between Basic Auth and OAuth. Here again, users enter their username and password or other app credentials, and you can customize the fields your app needs for authentication. Then, add a token exchange URL where Zapier exchanges the credentials for an authentication token, which Zapier will then use to authenticate every API call to your app.

### API Key

API key authentication works the same as Basic Auth, only here users enter a custom API key from your app instead of their account credentials. Users will need to locate an API key from your app, then enter it in the login form Zapier shows when authenticating with your app. Zapier will then pass the API key to your app to authenticate each API call.

### OAuth v2
_Same authentication flow as [Twitter](https://developer.twitter.com/en/docs/basics/authentication/overview) and [Trello](https://developers.trello.com/page/authorization)'s OAuth v2 implementation_

OAuth authentication is the authentication scheme to use when possible, as it matches users expectations from app authentication today. When users connect an app account that supports OAuth, Zapier shows a popup window from that app where users enter their user details on the app's site and authorize Zapier to access their data. Your app sends a request token before the user authenticates, then Zapier exchanges that for an access token after they authenticate.

### Digest Auth
_As documented by [RFC 7616](https://tools.ietf.org/html/rfc7616)_

Digest authentication is similar to Basic Auth, though more customizable and where Zapier handles the nonce and quality of protection details automatically. You can add custom fields to gather authentication details your app needs from users. Then with every API call, Zapier first contacts your app's server to request the nonce key before passing the authentication details and any other API call data to your app.

> Limitation: Currently, MD5-sess and SHA are not implemented. Only the MD5 algorithm is supported. In addition, server nonces are not reused. That means for every `z.request` call, Zapier will sends an additional request first to get the server nonce.

## How to Add Authentication to a Zapier Integration

![Add Zapier integration authentication](https://cdn.zapier.com/storage/photos/5f1a0e1fc0eb5635bdf1a2983f31a9ba.png)

Authentication is the first thing added in a new Zapier integration. Select the _Authentication_ tab in Zapier visual builder, and choose the authentication scheme your API users.

From there, the steps differ slightly depending on your authentication scheme, but in general, with every authentication option you need to:

- Set your app's authentication settings
- Enter a test API endpoint where Zapier can call with your users' credentials to ensure the connection was successful
- Add a Connection Label to help users uniquely identify their account(s)
- Test the authentication and connected account to ensure authentication works

### Set Authentication Settings

**Basic, API Key, and Digest Auth**

![Add fields to authentication](https://cdn.zapier.com/storage/photos/bd27312ca8b15c35191dba9d205101fd.png)

The first step in adding authentication may not need any additional details with Basic, API key, and Digest auth, depending on your app's settings. Zapier automatically adds a form to request username and password with Basic Auth, and includes no settings to edit.

With Digest and API Key authentication, Zapier again automatically adds a form where users can enter their username and password with Digest or API key with API key authentication. Here, though, you can additionally add input fields to request additional data, such as other account details or more commonly an app URL with self-hosted apps such as databases and CMSs. Check our [Input Designer](https://platform.zapier.com/docs/input-designer) docs for details on adding input form fields—only here, you can only choose from _string_ and _password_ field types.

**Session Auth**

![Zapier Token Exchange URL](https://cdn.zapier.com/storage/photos/68bf248f14cc03e25cb70e5edd8deda0.png)

Session Auth includes the same options to add input fields in addition to the default username and password. Then, enter your API's Token Exchange URL—and set any custom headers or URL params needed—where Zapier can exchange the user details for a session token.

**OAuth 2**

![Zapier OAuth setup](https://cdn.zapier.com/storage/photos/7e2a44c1464a32a43982465c97c28a53.png)

OAuth 2 Auth requires a few additional details. You can add custom fields if needed—typically here, fields are only needed if users need to enter a custom URL for your app, or if you need to store computed fields from the user's authentication data.

Then copy Zapier's OAuth Redirect URI, and add it to your application's OAuth settings, often found in developer tools or advanced setting options. That should give you a client ID and secret from your app; copy those, and add them to the appropriate fields in Zapier.

![Authorization URL OAuth 2 Zapier](https://cdn.zapier.com/storage/photos/38230bc2ae606ca2fb7be8e0d774ae79.png)

Finally add the Authorization URL where Zapier will redirect users to authenticate with your app, the scope that Zapier needs to request from your app, and the API endpoint for your app where Zapier can request the access token exchange. Finally, add the refresh token API endpoint, if available, and set if Zapier should automatically refresh tokens upon login error.

With that, your core API connection details should be set.

### Enter a Test API Endpoint

After adding the API connection details, you'll add a test API call to the _Test_ field. Or, with Basic authentication where there are no options to set, you'll see this field option first.

Here, add a URL to an API call that requires authentication but does not require any additional input data. Typically a `/me` or `/user` call is best here—something that returns details about the account holder to verify that Zapier has successfully authenticated with and can access data in the app account.

Whenever a user adds an account to Zapier with your integration, Zapier will automatically make a call to this API to verify the account and optionally fill in connection label details.

You can add custom URL params or HTTP headers if needed. Or, you can switch to code mode to write a custom JavaScript API call. Typically, though, a simple direct API call is best here.

### Add Connection Label

![Add connection label](https://cdn.zapier.com/storage/photos/8cbd1c0af4f444f59bb623a5291b4683.png)

The final detail to add is the connection label. Zapier automatically adds a label with your app's name whenever someone authenticates with your app. You can reference fields your API test call returns in the connection label—or add plain text—to customize the label for each account user.

To reference a field from your API call, enter {% raw %}`{{bundle.authData.field}}`{% endraw %} in the _Connection Label_ field substituting your field name for `field`.

Check the _[Connection Label](#label)_ section below for more details on adding a connection label.

Then, click _Save & Continue_ to save your authentication settings before testing them in the next step.

### Test Authentication

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

<a id="label"></a>
## How to Add a Connection Label to Authenticated Accounts

![Zapier connection labels](https://cdn.zapier.com/storage/photos/ed16e77428f17e869e25d4f2111df1c9.png)
_A Zapier integration with a custom connection label (above) and without one (below)_

Zapier lets users authenticate as many accounts for any app as they want, which is commonly used to connect multiple accounts in teams, or to add a secondary account for testing. By default, every new app account added to Zapier gets the app's name, followed by a number if there is already another account authenticated for that app.

The connection label settings let you customize this account connection for your integration to include the user's actual username, email address, name, or other identifiable information in the connection label. That makes it easy for users to distinguish between each account they've added to Zapier.

![Zapier Authentication Connection Label](https://cdn.zapier.com/storage/photos/f2c3d557023ce2a65b41122da34c1fdd.png)

Customize your app's connection label from the _Connection Label_ field in your Zapier integration. You can include:

- Plain text that will be included after your app's full name
- Output fields from your app's authentication test API call, referenced with {% raw %}`{{bundle.authData.field}}`{% endraw %} variables, replacing `field` for your API output field name.

To add a connection label, you can enter an output field in the Connection Label if you know the name of the field you wish to use that your API sends to Zapier. Otherwise, skip adding the connection label first, and instead click _Connect an Account_ under step 2. Then click _Test Connected Account_ and check the _Response_ tab for a field that includes the data your app should use in the connection label. Finally, use that field name to replace `field` in the following text, add it to your _Connection Label_ field, and save the changes:

{% raw %}`{{bundle.authData.field}}`{% endraw %}

You can include any field your authentication test API call returns in the connection label, though the best fields to use are usernames, account numbers, email addresses, or other identifiable but not fully private data. Never use passwords, API keys, or other critical, private info in connection labels.

## How to Remove Authentication

![Zapier Remove Authentication Scheme](https://cdn.zapier.com/storage/photos/a84d330dce6ccc18cbdeb12ca555b12d.png)

You cannot change an integration’s authentication scheme, but you can remove an existing integration’s authentication then add a new authentication scheme. To do so, open the _Authentication_ tab in the integration’s Zapier visual builder. Click the gear icon beside the existing authentication scheme, click _Delete_, then confirm to remove the authentication.

Repeat the original steps to add your app’s new authentication scheme to the Zapier integration.

> **Note:** Never remove authentication from an existing, live integration. If an integration’s authentication scheme needs changed, clone a new major version and add the new authentication. Then migrate users to the new version, and deprecate the original version with breaking changes. [Learn more](https://platform.zapier.com/docs/versions){:target="_blank"}