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

> **Which OAuth 2 Flow Type Does Zapier Support?:** Zapier implements the "Authorization Code" [grant type](https://tools.ietf.org/html/rfc6749#section-1.3.1) when you choose OAuth 2. If your OAuth 2 implementation supports refresh tokens you may optionally configure a "Refresh Token" [request](tools.ietf.org/html/rfc6749#section-1.5). If you require a different OAuth 2 grant type, have a look at one one of the other Zapier authentication types.
> **Does Zapier Support OAuth v1?** Not with visual builder. If your integration requires OAuth v1 authentication, use [Zapier CLI](https://zapier.com/developer/documentation/v2/getting-started-cli/) to build your integration instead.

<a id="add"></a>
## How to Add OAuth v2 to a Zapier Integration

![Add OAuth to Zapier Integration](https://cdn.zapier.com/storage/photos/6284f5603abd6259759b8698f5fea85e.png)

To add OAuth authentication to a Zapier integration, open your app's _Authentication_ page in Zapier's visual builder, then select _OAuth v2_ from the authentication scheme drop-down.

You will then need the following to add OAuth authentication:

- (optionally) An Input Form to gather data from users, such as account team name or site URL for self-hosted apps
- An OAuth application configured in your own app's settings, where you'll add Zapier's OAuth Redirect URL
- A Client ID (may be called Customer or API Key) and Client Secret (may be called Customer or API secret) from your app
- An Authorization URL on your app's site where users will login with their account credentials
- (optionally) A list of API scope(s) to restrict what Zapier can access
- An Access Token Request URL where Zapier exchanges the request token for an access token
- (optionally) A Refresh Token Request URL where Zapier can refresh the access token if it expires, along with an option to have Zapier automatically refresh credentials
- A Test API endpoint where Zapier can make an API call to ensure your user credentials work
- A Connection Label to uniquely identify users' accounts

<a id="form"></a>
## Add an OAuth Input Form (optional)

> **Note**: Most apps with OAuth v2 authentication do not need an input form, so unless your API requires data from the user before contacting the authorization URL, or requires URL details to create the authorization URL, you should likely not include an input form.

![Zapier OAuth input form](https://cdn.zapier.com/storage/photos/739190c32c449a03e415ccaa83960a6f.png)

If your API's OAuth authentication needs additional details from users before it can display the authorization URL, or if it needs to have Zapier store fields received from your server to use in subsequent API calls, you can add an input form as the first step in your authentication. This will show a form to users with the fields you've added before redirecting them to your authorization URL.

To add input fields, click the _Add Fields_ button, then select the type of field you need.

Zapier includes two types of fields: standard fields, which work much like other form fields with Zapier's [input form](https://platform.zapier.com/docs/input-designer) in Triggers and actions, and computed fields silently store data received from your app's authentication API calls. If you need to store data received from your server—such as team account names, domains, or subdomains—that are available in the API authentication calls and then needed for subsequent calls, select _Computed Field_. Then add the field key, using the same field name as your API's response—and leave the remaining fields blank. Zapier will automatically store this field's data when its received from the API call. Learn more in our [Computed Fields docs](https://platform.zapier.com/docs/advanced#computed).

For input fields, select the default _Field_ type, then add:

- **Key**: The field key, ideally using the same key as your API expects for this field
- **Label**: A human friendly name for this field
- **Required**: Check if this field is required for successful API authentication
- **Type**: Choose the field type, either _string_ (default) for plain text or _password_ for obscured text
- **Help Text**: Enter a description to help users know what data to enter in this field, especially if the info is hard to find such as team names or subdomain info. Use [Markdown](https://zapier.com/blog/beginner-ultimate-guide-markdown/) to format the text, and include a link to your app's settings or documentation if needed to help users locate the data.
- **Default Value**: For optional fields, enter text that can be used by default if users don't enter a value. For required fields, enter text that can be used for authentication, but that won't be used in subsequent Zap steps.

![Edit or delete input fields](https://cdn.zapier.com/storage/photos/a5660976799c62274adfd7fe620fe96c.png)

Add the fields in the order users would expect to see them. You cannot reorder fields, though you can delete fields and add them again if needed.

Once completed, click _Continue_ to save your form and setup OAuth authentication.

<a id="redirect"></a>
## Add Zapier Redirect URL to Your App

![Zapier Redirect URI](https://cdn.zapier.com/storage/photos/0e981d8a8f61a0da112bfe83a526cec8.png)

If you haven't already, in a different tab or window open your app's application, integration, or API settings, and add a new application for your OAuth integration with Zapier. From Zapier's visual builder, copy the OAuth Redirect URL, similar to the one shown above, and add it to your application's integration settings.

If you ever need to reference Zapier's redirect URL inside your Zapier integration, use the following code:

{% raw %}`{{bundle.inputData.redirect_uri}}`{% endraw %}

<a id="credentials"></a>
## Add Application Credentials to Zapier

![Add application credentials to Zapier](https://cdn.zapier.com/storage/photos/528a6aa1c1be8204876f30f1e6276f82.png)

In your application's settings, you'll receive credentials that Zapier will use to verify itself to your app—typically called a _Client ID_ and _Client Secret_, though they may have a slightly different name. Copy that data from your app, then in Step 3 of your Zapier OAuth configuration, paste those items in their respective fields. Zapier will use that data along with the authorization URL to receive the request token.

Click _Save & Continue_ to save your progress so far.

Zapier will automatically include the Client ID and Secret in authentication API calls, but if you need to reference them in your Zapier API calls or custom code, use the following codes:

- Client Secret: {% raw %}`{{process.env.CLIENT_SECRET}}`{% endraw %}
- Client ID: {% raw %}`{{process.env.CLIENT_ID}}`{% endraw %}

<a id="authorization"></a>
## Add OAuth Endpoint Configuration

![Add Authorization URL to Zapier](https://cdn.zapier.com/storage/photos/6c41fec63315bd3770c5875799201b43.png)

Now it's time to configure how Zapier sends users to your API to allow access to their account in your app, and how Zapier gets the credentials it needs for future API calls.

First, add your application's Authorization URL, where Zapier will redirect users to authenticate with your app. You can typically copy this URL from your application or integration settings where you copied the client ID and secret previously, or from your app's API page. Typically, enter the URL in the field and leave the default settings.

Optionally, if you wish to limit Zapier's scope to let it only access specific data from your app, you can additionally add OAuth scope in the following field with a comma or space separated list.

<a id="access"></a>
## Add Access Token Request and Refresh Token Request URLs

![Access Token Zapier](https://cdn.zapier.com/storage/photos/386f1392718dea32025edf72ca21fae0.png)

Next, add your app's Access Token Request URL, typically with a `POST` call and the default settings Zapier uses if your app uses a standard OAuth configuration. You can find this URL in your application's API documentation.

By default, Zapier will pass the client ID, client secret, authorization code, redirect URI, and a standard `authorization_code` grant type in the API request body. If you need to change that, click the _Show Options_ button and add any additional call details needed.

If your API supports automated token refresh, add your API's Refresh Token Request in the following field, and check the _Automatically Refresh Token_ box. This will help Zapier stay connected to your users' accounts and enable Zaps to run in the background without interrupting users as long as possible.

Zapier will automatically include the access token in subsequent API requests, but if you need to manually add it, the access token is stored in the authData bundle and can be referenced with {% raw %}`{{bundle.authData.access_token}}`{% endraw %} or {% raw %}`{{bundle.authData.accessToken}}`{% endraw %}, depending on how your API's response references the access token.

<a id="test"></a>
## Add a Test API Call

![Test API Call Zapier OAuth](https://cdn.zapier.com/storage/photos/f31d8d06adfbf15a9da2e98ad7690021.png)

Your core authentication is set, so now add a way for Zapier to test the authorization token your app passed to Zapier, and make sure it can successfully access your users' accounts.

For that, add a URL endpoint to the _Test_ field that does not require configuration and that returns details about the user who authenticated, ideally a `/user` or `/me` call. Zapier will pass the access token with the API call by default, as it will with all subsequent API calls, but if your API requires any additional configuration, click the _Show Options_ button and add any options needed for a successful API call.

![Zapier Code Mode OAuth](https://cdn.zapier.com/storage/photos/09bda4bee7f6e064c10048c03f640359.png)

Or, if you need a specialized API call or response parsing on this or other API call steps, click the _Switch to Code Mode_ toggle. The first time you click this, Zapier will convert the data in the form to JavaScript code that you can customize or replace. You can switch back to form mode, though note that Zapier will not convert your code back to the form mode, nor will it update any subsequent changes in the form mode to your code.

<a id="label"></a>
## Add a Connection Label

Finally add a connection label to help users identify each account that they add from your app to Zapier. Zapier includes your app's name in the connection label by default, followed by the version number, then any text you include in the connection label. You can include:

- Plain text that will be included in every account connection
- Any input field from your authentication form—enter {% raw %}`{{bundle.authData.field}}`{% endraw %}, replacing `field` with your input form field key
- Output fields from your app's authentication test API call, referenced with {% raw %}`{{bundle.inputData.field}}`{% endraw %} variables, replacing `field` for your API output field name

Learn more in our [Connection Label documentation](https://platform.zapier.com/docs/auth#label).

Click _Save & Continue_ when finished to save your authentication settings.

Then, test your authentication, adding a real account to ensure Zapier can successfully connect to your app and use your test API call. Check our [Authentication Testing docs](https://platform.zapier.com/docs/auth#test) for more details, common errors you may encounter, and how to resolve those.