---
title: Add authentication with OAuth v2
order: 5
layout: post-toc
redirect_from:
  - /docs/oauth
---

# Add authentication with OAuth v2

OAuth v2 authentication matches in appearance the login process users expect from most modern apps. The user interaction with authenticating Zapier typically takes place in full on the app's own site, helping users easily connect accounts without needing to share account credentials or look up API keys.

![Example OAuth login experience for users](https://cdn.zappy.app/520541acfeeb0e0a812944e599852756.png)

The user will see a familar window from your app showing either a login screen or if they're already logged in, an account selector where they don't need to enter credentials. Once they authorize Zapier access, the app will return an access token that Zapier uses in future API calls.

Zapier implements the "Authorization Code" [grant type](https://tools.ietf.org/html/rfc6749#section-1.3.1) when you choose OAuth v2 in the Platform UI. If your OAuth v2 implementation supports refresh tokens, you can optionally configure a "Refresh Token" [request](https://tools.ietf.org/html/rfc6749#section-1.5).

Platform UI does not currently support other grant types. If your integration requires a different OAuth v2 grant type, you'll need to use another supported authorization type with Zapier such as [Session](https://platform.zapier.com/build/sessionauth) or [API Key](https://platform.zapier.com/build/apikeyauth).

If your integration requires OAuth v1 authentication, use the [Platform CLI](https://platform.zapier.com/quickstart/platform-cli-tutorial) instead of Platform UI.

## 1. Configure the OAuth v2 components

- Open the _Authentication_ tab in Zapier visual builder and select _OAuth v2_.

![Add OAuth to Zapier Integration](https://cdn.zappy.app/e89518edce251293ff42ae0f186c0efb.png)

### Optional input form

- Most apps with OAuth v2 authentication do not need an input form. If your API requires data from the user before displaying the authorization URL, or requires URL details to create the authorization URL; such as account team name or site URL for self-hosted apps, or you need to store fields received from your server to use in subsequent API calls - you'll need an input form.

- Add those additional fields by selecting _Add Fields_ and fill in the details for any field requiring user input. This will show a form to users with the fields you've added before redirecting them to your authorization URL.

![Zapier OAuth input form](https://cdn.zappy.app/3603f9715129250a93ecfcf78d4b5f17.png)

- Two types of fields are available when building an OAuth v2 input form. Standard Fields, work much like other form fields with Zapier's [input form](https://platform.zapier.com/build/input-designer) in triggers and actions. [Computed Fields](https://platform.zapier.com/build/computed-fields) make sure specific fields are returned by your app's authentication API call response.

- For standard fields to be input by the user, select the default _Field_ type. Add the most commonly needed fields first, in the order users expect, as you cannot reorder fields once added. Fill in the options as appropriate:

-- **Key**: The internal name for your field, used to reference this field in Zapier API calls. For convenience, use the same key as your API uses for this field. Note: `client_id` and `client_secret` are reserved and cannot be used as keys for input form fields.

-- **Label**: A human-friendly name for this field that will be shown to users in the authentication form.

-- **Required? (checkbox)**: Check if this field is required for successful authentication.

-- **Type**: All input fields use the `string` text field by default; select `password` instead if you would like to obscure the data as users enter it.

-- **Help Text**: Include details to assist users in authenticating with your app, especially if they may be unsure where to find the data needed within your app. Format text with [Markdown](https://zapier.com/blog/beginner-ultimate-guide-markdown/), and include a hyperlink if needed.

-- **Input Format**: (optional) Help users figure out exactly what piece of data you need them to enter. For example, for [a subdomain](https://platform.zapier.com/build/subdomain-validation), https://{{input}}.yourdomain.com/.

-- **Default Value**: Include a value for this field to be used as a fallback. For optional fields, the default value is set on initial connection creation and used in the API call instead of missing or null values every time the Zap runs. For required fields, this value is used during connection creation, but not when the Zap runs (Zapier raises an error for missing/null values instead).

- Input fields marked as password and all authentication fields with sensitive, private data such as both username and password from OAuth v2 are automatically censored at runtime. These values are stored in the Auth bundle and used in API calls, but are replaced in Zapier’s logs with a censored value like this `:censored:6:82a3be9927:`. Due to this, it is not possible to view the exact tokens or keys in Zapier's logs. To verify that the same token as was returned by the authentication, is being used in subsequent API calls; you can compare censored value characters, for example `:censored:6:82a3be9927:` would have the same value ending in 9927 when used in a subsequent call.

- Each input field is listed with its label, key, type, and required status in your authentication settings. Click the field to edit it, or click the gear icon and select _Delete_ to remove a field.

![Edit or delete input fields](https://cdn.zappy.app/573a3eb19a884c44fd67b9fa421c3bf4.png)

- For computed fields, available in OAuth v2 and Session Auth only, review [computed fields documentation](https://platform.zapier.com/build/computed-fields).

### OAuth Redirect URL

- Open your app's application, integration, or API settings, and add a new application for your OAuth integration with Zapier. From the Zapier Platform UI's Authentication _Copy your OAuth Redirect URL_ section, copy the OAuth Redirect URL and add it to your application's integration settings.

![Zapier Redirect URI](https://cdn.zappy.app/b3e6b9ca7657ba02e4864ec28ab74951.png)

- To reference the redirect URL inside your Zapier integration, use the following code:

{% raw %}`{{bundle.inputData.redirect_uri}}`{% endraw %}

### Add PKCE Support

- Zapier provides built-in support for [PKCE](https://oauth.net/2/pkce/#credentials) (Proof Key for Code Exchange and pronounced "pick-see"), an extension to the authorization code flow that adds a layer of protection against security vulnerabilities. The code generation and exchange steps of the flow occur automatically by Zapier when enabled.

![Zapier OAuth v2 with PKCE Extension](https://cdn.zappy.app/124a3c00d8bc37dadd953f19451205a5.png)

### Add Application Credentials to Zapier

- In your application's settings, you'll receive credentials that Zapier will use to verify itself to your app — typically called a _Client ID_ and _Client Secret_, though they may have a slightly different name. Copy that data from your app, then in Step 3 of your Zapier OAuth configuration, paste those items in their respective fields. Zapier will use that data along with the authorization URL to receive the request token.

![Add application credentials to Zapier](https://cdn.zappy.app/ba093465f009bf6b417d55b2166c4324.png)

- Click _Save & Continue_ to save your progress so far.

- Zapier automatically includes the Client ID and Secret in authentication API calls, but if you need to reference them in your integration's API calls or custom code, use the following codes:
  -- Client Secret: {% raw %}`{{process.env.CLIENT_SECRET}}`{% endraw %}
  -- Client ID: {% raw %}`{{process.env.CLIENT_ID}}`{% endraw %}

### Add OAuth Endpoint Configuration

- Add your application's Authorization URL, where Zapier will redirect users to authenticate with your app. Copy this URL from your application or integration settings where you copied the client ID and secret previously, or from your app's API page.

![Add Authorization URL to Zapier](https://cdn.zappy.app/1920c552acfc0cc03089feb2e9ada029.png)

- By default, Zapier will pass the client ID, state, redirect URI, and a standard `code` response type as URL Params in the request to the authorization url. If you need to change that, click the *Show Options* button and add any additional call details needed.

> **Note**: The Oauth2 `state` param is a [standard security feature](https://auth0.com/docs/secure/attack-protection/state-parameters) that helps ensure that authorization requests are only coming from your servers. Most Oauth clients have support for this and will send back the `state` query param that the user brings to your app. The Zapier Platform performs this check and this required field cannot be disabled. The state parameter is automatically generated by Zapier in the background, and can be accessed at `bundle.inputData.state`.
> Since Zapier uses the `state` to verify that GET requests to your redirect URL truly come from your app, it needs to be generated by Zapier so that it can be validated later (once the user confirms that they'd like to grant Zapier permission to access their account in your app).

- To optionally limit Zapier's scope to let it only access specific data from your app, add OAuth scopes in the _Scope_ field with a comma- or space-separated list.

- Add your app's Access Token Request URL from your API documentation, typically with a `POST` call.

![Access Token Zapier](https://cdn.zappy.app/517f20c1a33012af96b18036332371eb.png)

- By default, Zapier will pass the client ID, client secret, authorization code, redirect URI, and a standard `authorization_code` grant type in the API request body with the access token request. If you need to change that, click the _Show Options_ button and add any additional call details needed.

- If your API supports automated token refresh, add your API's Refresh Token Request URL, and check the _Automatically Refresh Token_ box. This enables users' Zaps to run in the background without interruptions as long as possible by refreshing expired access tokens automatically.

- If your Access Token and Refresh Token requests don't return the tokens at the top level, use [Code Mode](https://platform.zapier.com/build/code-mode) to modify the response so that the tokens are available at the top level. It is not possible to store an object with nested keys from the response.

- Zapier will automatically include the access token in subsequent API requests, but if you need to manually add it, the access token is stored in the `authData` bundle and can be referenced with {% raw %}`{{bundle.authData.access_token}}`{% endraw %} or {% raw %}`{{bundle.authData.accessToken}}`{% endraw %}, depending on how your API's response references the access token.

## 2. Add a Test API Request

- Add an API call to your API that requires no configuration, typically a `/user` or `/me` call. Add the URL for the API call, and set the call type, typically a `GET`. This will test the user-entered credentials to ensure it enables a successful API call to your app.

![Test API Call Zapier OAuth](https://cdn.zappy.app/48cdb444eab9a329023b3e991bfa0da9.png)

- The access token is included with the API call by default, as it will with all subsequent API calls, but if your API requires any additional configuration, click the _Show Options_ button and add any options needed for a successful API call.

![Zapier Code Mode OAuth](https://cdn.zappy.app/f9d47ff9bd4af168dcb4c4811a1e184d.png)

- To customize the test API request, select _Switch to Code Mode_ and write custom JavaScript code to handle your test API call and the response parsing as needed. The first time you click the toggle, Zapier will [convert your API call to code](https://platform.zapier.com/build/code-mode). If you switch back to Form Mode though, Zapier will not convert your code changes to the Form Mode, nor will any subsequent changes in the form be added to your code.

## 3. Configure a Connection Label

Review [connection label documentation](https://platform.zapier.com/build/connection-label) to optionally differentiate the app accounts users connect.

## 4. Test your authentication

Connect a valid user account to [test authentication](https://platform.zapier.com/build/test-auth).
