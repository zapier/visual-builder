---
title: — OAuth v2
order: 7
layout: post-toc
redirect_from: /docs/
---

# Authentication — OAuth v2

OAuth v2 authentication is the easiest authentication scheme for users, as it matches the login process they expect from most modern apps. In Zapier integrations with OAuth v2, the user part of authentication typically takes place in full on the app's own site, helping users easily connect accounts without sharing account credentials or looking up API keys.

![Example OAuth login experience for users](https://cdn.zapier.com/storage/photos/6f14340218bd51f4047afcdfc71fd9b6.png)

When a user adds an app account to Zapier with OAuth v2, they will first see a familar window from that app showing either a login screen or an account selector if they're already logged in (and the app will send Zapier a request token that will be exchanged for an access token once the user approves access). They can then enter their account credentials confidently since they're entering them on that app's own site—and often, users will not need to enter credentials since they're already logged in. Once they authorize Zapier access, the app will return an access token that Zapier can use to authenticate future API calls.

## Which OAuth 2 Flow Type Does Zapier Support?

Zapier implements the "Authorization Code" [grant type](https://tools.ietf.org/html/rfc6749#section-1.3.1) when you choose OAuth v2. If your OAuth 2 implementation supports refresh tokens, you can optionally configure a "Refresh Token" [request](https://tools.ietf.org/html/rfc6749#section-1.5).

The Zapier platform does not currently support other grant types. If your integration requires a different OAuth 2 grant type, you'll need to use another supported authorization type with Zapier such as [Session auth](./session) or [API Key auth](./apikey). Visit the [Zapier Community](https://community.zapier.com/search?q=session%20oauth%20grant%20type) if you need any guidance on using Session Auth to provide an OAuth flow.

### Does Zapier Support OAuth v1?

Not within the Platform UI. If your integration requires OAuth v1 authentication, use the [Zapier CLI](https://zapier.com/developer/documentation/v2/getting-started-cli/) to build your integration instead.

<a id="add"></a>
## How to Add OAuth v2 to a Zapier Integration

![Add OAuth to Zapier Integration](https://cdn.zappy.app/e89518edce251293ff42ae0f186c0efb.png)

To add OAuth authentication to a Zapier integration, open your app's _Authentication_ page in Zapier's visual builder, then select _OAuth v2_ from the authentication scheme drop-down.

You'll need the following items to add OAuth authentication:

- An input form (optional) to gather data from users, such as account team name or site URL for self-hosted apps
- An OAuth application configured in your own app's settings, where you'll add Zapier's OAuth Redirect URL
- A Client ID (may be called Customer or API Key) and Client Secret (may be called Customer or API secret) from your app
- An Authorization URL on your app's site where users will log in with their account credentials
- A list of API scope(s) (optional) to restrict what Zapier can access
- An Access Token Request URL where Zapier exchanges the request token for an access token
- A Refresh Token Request URL (optional) where Zapier can refresh the access token if it expires, along with an option to have Zapier automatically refresh credentials
- A Test API endpoint where Zapier can make an API call to ensure your user credentials work
- A Connection Label to uniquely identify users' accounts

<a id="form"></a>
## Add an OAuth Input Form (optional)

> **Note**: Most apps with OAuth v2 authentication do not need an input form, so unless your API requires data from the user before contacting the authorization URL, or requires URL details to create the authorization URL, you should likely not include an input form.

![Zapier OAuth input form](https://cdn.zappy.app/3603f9715129250a93ecfcf78d4b5f17.png)

If your API's OAuth authentication needs additional details from users before it can display the authorization URL, or Zapier needs to store fields received from your server to use in subsequent API calls, you can add an input form as the first step in your authentication. This will show a form to users with the fields you've added before redirecting them to your authorization URL.

To add input fields, click the _Add Fields_ button, then select the type of field you need.

Zapier includes two types of fields: standard fields, which work much like other form fields with Zapier's [input form](https://platform.zapier.com/docs/input-designer) in triggers and actions, and Computed Fields, which make sure specific fields are returned by your app's authentication API call response.

For input fields, select the default _Field_ type, then add:

- **Key**: The internal name for your field, used to reference this field in Zapier API calls. For convenience, use the same key as your API uses for this field. Note: `client_id` and `client_secret` are reserved and cannot be used as keys for input form fields.
- **Label**: A human-friendly name for this field that will be shown to users in the authentication form.
- **Required? (checkbox)**: Check if this field is required for successful authentication.
- **Type**: (optional) Usually String, but select "Password" to obscure text for secret values.
- **Help Text**: Add [Markdown](https://zapier.com/blog/beginner-ultimate-guide-markdown/) formatted details on what users should enter in this field, optionally with a link to your site to help users find the data.
- **Input Format**: (optional) Help users figure out exactly what piece of data you need them to enter. For example, for a subdomain, https://{{input}}.yourdomain.com/.
- **Default Value**: (optional) If appropriate, for optional fields, enter text that can be used by default if users don't enter a value. For required fields, enter text that can be used for authentication, but that won't be used in subsequent Zap steps.

![Edit or delete input fields](https://cdn.zappy.app/573a3eb19a884c44fd67b9fa421c3bf4.png)

Add the fields in the order users would expect to see them. You cannot reorder fields, though you can delete fields and add them again if needed.

### Computed Fields

If you need to use data received from the auth API response—such as team account names, domains, or subdomains—you can add a _Computed Field_ by selecting the Field Type at the top of the form. Add the field key, using the same field key as your API's response, and leave the remaining field details blank.

Zapier will then make sure this field is included in the response data, and you can reference it in subsequent API calls. Zapier will show an error if a field marked as computed is not included in the response data. Learn more in our [Computed Fields docs](https://platform.zapier.com/docs/advanced#computed).

Once completed, click _Continue_ to save your form and setup OAuth authentication.

<a id="redirect"></a>
## Add Zapier Redirect URL to Your App

![Zapier Redirect URI](https://cdn.zappy.app/b3e6b9ca7657ba02e4864ec28ab74951.png)

If you haven't already, in a different tab or window open your app's application, integration, or API settings, and add a new application for your OAuth integration with Zapier. From Zapier's visual builder, copy the OAuth Redirect URL, similar to the one shown above, and add it to your application's integration settings.

If you ever need to reference Zapier's redirect URL inside your Zapier integration, use the following code:

{% raw %}`{{bundle.inputData.redirect_uri}}`{% endraw %}

<a id="PKCE"></a>
## Add PKCE Support

![Zapier OAuth v2 with PKCE Extension])(https://cdn.zappy.app/124a3c00d8bc37dadd953f19451205a5.png)

Zapier provides built-in support for [PKCE](https://oauth.net/2/pkce/#credentials) (Proof Key for Code Exchange and pronounced "pick-see"), an extension to the authorization code flow that adds a layer of protection against security vulnerabilities. The code generation and exchange steps of the flow occur automatically by Zapier when enabled.

<a id="credentials"></a>
## Add Application Credentials to Zapier

![Add application credentials to Zapier](https://cdn.zappy.app/ba093465f009bf6b417d55b2166c4324.png)

In your application's settings, you'll receive credentials that Zapier will use to verify itself to your app—typically called a _Client ID_ and _Client Secret_, though they may have a slightly different name. Copy that data from your app, then in Step 3 of your Zapier OAuth configuration, paste those items in their respective fields. Zapier will use that data along with the authorization URL to receive the request token.

Click _Save & Continue_ to save your progress so far.

Zapier will automatically include the Client ID and Secret in authentication API calls, but if you need to reference them in your Zapier API calls or custom code, use the following codes:

- Client Secret: {% raw %}`{{process.env.CLIENT_SECRET}}`{% endraw %}
- Client ID: {% raw %}`{{process.env.CLIENT_ID}}`{% endraw %}

<a id="authorization"></a>
## Add OAuth Endpoint Configuration

![Add Authorization URL to Zapier](https://cdn.zappy.app/1920c552acfc0cc03089feb2e9ada029.png)

Now it's time to configure how Zapier sends users to your API to allow access to their account in your app, and how Zapier gets the credentials it needs for future API calls.

First, add your application's Authorization URL, where Zapier will redirect users to authenticate with your app. You can typically copy this URL from your application or integration settings where you copied the client ID and secret previously, or from your app's API page. Typically, enter the URL in the field and leave the default settings.

Optionally, if you wish to limit Zapier's scope to let it only access specific data from your app, you can add OAuth scopes in the following field with a comma- or space-separated list.

<a id="access"></a>
## Add Access Token Request and Refresh Token Request URLs

![Access Token Zapier](https://cdn.zappy.app/517f20c1a33012af96b18036332371eb.png)

Next, add your app's Access Token Request URL, typically with a `POST` call and the default settings Zapier uses if your app uses a standard OAuth configuration. You can find this URL in your application's API documentation.

By default, Zapier will pass the client ID, client secret, authorization code, redirect URI, and a standard `authorization_code` grant type in the API request body. If you need to change that, click the _Show Options_ button and add any additional call details needed.

If your API supports automated token refresh, add your API's Refresh Token Request in the following field, and check the _Automatically Refresh Token_ box. This will help Zapier stay connected to your users' accounts and enable Zaps to run in the background without interrupting users as long as possible.

If your Access Token and Refresh Token requests don't return the tokens at the top level, use [Code Mode](./faq#how-does-code-mode-work) to modify the response so that the tokens are available at the top level. It's not possible to store an object with nested keys from the response.

Zapier will automatically include the access token in subsequent API requests, but if you need to manually add it, the access token is stored in the authData bundle and can be referenced with {% raw %}`{{bundle.authData.access_token}}`{% endraw %} or {% raw %}`{{bundle.authData.accessToken}}`{% endraw %}, depending on how your API's response references the access token.

<a id="test"></a>
## Add a Test API Call

![Test API Call Zapier OAuth](https://cdn.zappy.app/48cdb444eab9a329023b3e991bfa0da9.png)

Zapier then needs a Test API call—typically to a `/user` or `/me` endpoint that returns details about the user and needs no additional configuration—to test account authentication and ensure the access token works.

Zapier will pass the access token with the API call by default, as it will with all subsequent API calls, but if your API requires any additional configuration, click the _Show Options_ button and add any options needed for a successful API call.

![Zapier Code Mode OAuth](https://cdn.zappy.app/f9d47ff9bd4af168dcb4c4811a1e184d.png)

If you need a specialized API call or response parsing on this or other API call steps, click _Switch to Code Mode_. The first time you click this, Zapier will convert the data in the form to JavaScript code that you can customize or replace. See [How does Code Mode work?](./faq#how-does-code-mode-work) for more details.

<a id="label"></a>
## Add a Connection Label

Finally add a connection label to help users identify each account that they add from your app to Zapier. Zapier includes your app's name in the connection label by default, followed by the version number, then any text you include in the connection label. You can include:

- Plain text that will be included in every account connection
- Any input field from your authentication form (if present)
- Output fields from your app's authentication test API call

Fields can be referenced using double curly braces. For example, a `username` field would look like {% raw %}`{{username}}`{% endraw %}. 

Learn more in our [Connection Label documentation](https://platform.zapier.com/docs/auth#label).

Click _Save & Continue_ when finished to save your authentication settings.

Then, test your authentication, adding a real account to ensure Zapier can successfully connect to your app and use your test API call. Check our [Authentication Testing docs](https://platform.zapier.com/docs/auth#test) for more details, common errors you may encounter, and how to resolve those.
