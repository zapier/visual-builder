---
title: Authentication
order: 3
layout: post-toc
redirect_from: /docs/
---

## Authentication

Every Zapier step starts with the same thing: App authentication. Users select an app they wish to use in the step. They then authenticate with that app to allow Zapier to access their data.

Zapier authentication enables Zapier access to an individual account in an app. Users connect one specific app account to Zapier, that Zapier can then watch for new or updated data, search for existing data, and create or update new data in that individual account on the app. Zapier may access the account until the authorization expires, is revoked, or credentials are changed, and may automatically refresh OAuth 2-powered authentications if enabled in the integration.

Once users authenticate their account on an app through Zapier, they can use any of that app's Zap steps without authenticating again. Users may also authenticate an app again to a new account on that app if they wish to use multiple accounts from an app with Zapier, typically to manage multiple projects or to use both work and personal accounts in workflows.

When building a Zapier integration, you define how the Zapier platform connects to your app to authenticates users, and add an API call where Zapier can test the account authentication. Then connect an account to Zapier to test the app authentication and any subsequent Zap Triggers and Actions you add to the integration.

<a id="schemes"></a>
## Zapier Supported Authentication Schemes

![Zapier Authentication](https://cdn.zapier.com/storage/photos/5f1a0e1fc0eb5635bdf1a2983f31a9ba.png)

All Zapier integrations that can access or add private data for users require authentication. The only apps that wouldn't require authentication include data feeds (such as news or weather updates) or utilities (such as file format conversion tools or public search engines). If you're building an integration for any app that stores private data and requires and account to use it, your integration will require authentication.

Add authentication to your integration first before adding triggers or actions. To add authentication, click the _Authentication_ tab in the left sidebar of Zapier's visual builder, then select the authentication scheme your app uses. Zapier supports the following five authentication schemes, each with their own settings:

### [Basic Auth](https://zapier.github.io/visual-builder/docs/basic)
_As documented by [RFC 7616](https://developer.mozilla.org/en-US/docs/Web/HTTP/Authentication)_

The simplest authentication method, Basic authentication requires nearly zero setup when building a Zapier integration. Zapier includes a pre-built login form that requests users' username and password for your app, then passes that to your app along with each API call to authenticate the user. This authentication method is only recommended if it's the only option to authenticate with your app, as it requires Zapier to store users' credentials.

_→ [Add Basic Auth to your Zapier Integration](https://zapier.github.io/visual-builder/docs/basic)_

### [Session Auth](https://zapier.github.io/visual-builder/docs/session)

Session authentication works somewhat like a hybrid between Basic Auth and OAuth. Here again, users enter their username and password or other app credentials, and you can additionally add custom fields your app needs for authentication. Then, add a token exchange URL where Zapier exchanges the credentials for an authentication token, which Zapier will then use to authenticate every API call to your app.

_→ [Add Session Auth to your Zapier Integration](https://zapier.github.io/visual-builder/docs/session)_

### [API Key](https://zapier.github.io/visual-builder/docs/api)

API key authentication works the same as Basic Auth, only here users enter a custom API key from your app instead of their account credentials. Users will need to locate an API key from your app, then enter it in the login form Zapier shows when authenticating with your app. Zapier will then pass the API key to your app to authenticate each API call.

_→ [Add API Key Auth to your Zapier Integration](https://zapier.github.io/visual-builder/docs/api)_

### [OAuth v2](https://zapier.github.io/visual-builder/docs/oauth)
_Same authentication flow as [Twitter](https://developer.twitter.com/en/docs/basics/authentication/overview) and [Trello](https://developers.trello.com/page/authorization)'s OAuth v2 implementation_

OAuth authentication is the authentication scheme to use when possible, as it matches users expectations for app authentication today. When users connect an app account that supports OAuth, Zapier shows a popup window from that app where users enter their user details on the app's site and authorize Zapier to access their data. Your app sends a request token before the user authenticates, then Zapier exchanges that for an access token after they authenticate.

_→ [Add OAuth v2 Auth to your Zapier Integration](https://zapier.github.io/visual-builder/docs/oauth)_

### [Digest Auth](https://zapier.github.io/visual-builder/docs/digest)
_As documented by [RFC 7616](https://tools.ietf.org/html/rfc7616)_

Digest authentication is similar to Basic Auth, though more customizable and where Zapier handles the nonce and quality of protection details automatically. Digest Auth lets you add custom fields to gather authentication details from users. Then with every API call, Zapier first contacts your app's server to request the nonce key before passing the authentication details and any other API call data to your app.

_→ [Add Digest Auth to your Zapier Integration](https://zapier.github.io/visual-builder/docs/digest)_

> Limitation: Currently, MD5-sess and SHA are not implemented. Only the MD5 algorithm is supported. In addition, server nonces are not reused. That means for every `z.request` call, Zapier will sends an additional request first to get the server nonce.

<a id="label"></a>
## How to Add a Connection Label to Authenticated Accounts

![Zapier connection labels](https://cdn.zapier.com/storage/photos/ed16e77428f17e869e25d4f2111df1c9.png)
_A Zapier integration with a custom connection label (above) and without one (below)_

Zapier lets users authenticate multiple accounts for any app. By default, every new app account added to Zapier is identified by the app's name followed by a number for secondary accounts.

The connection label settings in your app's authentication options let you customize this account connection for your integration to include a username, email address, name, or other identifiable information in the connection label. That helps users distinguish between their authenticated accounts.

![Zapier Authentication Connection Label](https://cdn.zapier.com/storage/photos/f2c3d557023ce2a65b41122da34c1fdd.png)

Customize your app's connection label from the _Connection Label_ field in your Zapier integration. Zapier always includes the app's name in each account label. You can additionally include:

- Plain text that will be included after your app's full name
- Output fields from your app's authentication test API call, referenced with {% raw %}`{{bundle.authData.field}}`{% endraw %} variables, replacing `field` for your API output field name.

To add a connection label, you can enter an output field in the Connection Label if you know the name of the field you wish to use that your API sends to Zapier. Otherwise, skip adding the connection label first, and instead click _Connect an Account_ under step 2. Then click _Test Connected Account_ and check the _Response_ tab for a field that includes the data your app should use in the connection label. Finally, use that field name to replace `field` in the following text, add it to your _Connection Label_ field, and save the changes:

{% raw %}`{{bundle.authData.field}}`{% endraw %}

You can include any field your authentication test API call returns in the connection label, though the best fields to use are usernames, account numbers, email addresses, or other identifiable but not fully private data. Never use passwords, API keys, or other critical, private info in connection labels.

<a id="change"></a>
## How to Remove or Change Zapier Integration Authentication Scheme

![Zapier Remove Authentication Scheme](https://cdn.zapier.com/storage/photos/a84d330dce6ccc18cbdeb12ca555b12d.png)

You cannot change an integration’s authentication scheme. Instead, remove an existing integration’s authentication then add a new authentication scheme.

To remove a Zapier integration's authentication scheme, open the _Authentication_ tab in the integration’s Zapier visual builder. Click the gear icon beside the existing authentication scheme, click _Delete_, then confirm to remove the authentication.

Then add your app’s new authentication scheme to the Zapier integration instead.

> **Note:** Never remove authentication from an existing, live integration. If an integration’s authentication scheme needs changed, clone a new major version and add the new authentication. Then migrate users to the new version, and deprecate the original version with breaking changes. [Learn more](https://zapier.github.io/visual-builder/docs/versions){:target="_blank"}