---
title: — Session Auth
order: 5
layout: post-toc
redirect_from: /docs/
---

# Authentication — Session Auth

Session authentication shares elements of Basic authentication—where Zapier requests a username and password, then uses them directly to authenticate each API call—and OAuth v2—where Zapier redirects users to the app's site to allow access, then exchanges credentials for a token it uses to authenticate subsequent API calls.

For Session auth, Zapier gathers username, password, and other login details to use in an API call. The API responds by sending an auth token to Zapier. It works much like cookie-based authentication in your browser, only here the "cookie" is an auth token stored by Zapier.

![Example Zapier session login form](https://cdn.zapier.com/storage/photos/7c7092a2311cf217298cb3e3f5735385.png)

When a user adds an app account to Zapier with Session auth, they first fill out an input form with any authentication credentials that app's API requires. Zapier then sends a request to the API's token exchange endpoint with those credentials, and the API responds with an authentication token. Zapier stores that authentication token for use with subsequent API calls.

> **When to use Session authentication:** Use Session authentication with your Zapier integration if your API is designed for session-, cookie-, or token-based authentication. You can also use Session auth if your API uses a variant of OAuth that the Zapier platform doesn't explicitly support.

<a id="add"></a>
# How to Add Session Auth to a Zapier Integration

![Add Session Auth to Zapier integration](https://cdn.zapier.com/storage/photos/79ae883b7a164a0747d273f708f16c57.png)

To add Session Auth to a Zapier integration, open your app's _Authentication_ page in Zapier visual builder then select _Session Auth_ in the drop-down.

You will need the following to set up Session Auth:

- An input form, built inside Zapier, with fields for each data item your API needs for authentication
- A Token Exchange Endpoint URL, where Zapier will send user credentials from the input form to your API and receive an auth token in the response
- A Test API endpoint that Zapier can call to ensure the auth token works and allows access to the user's account
- A Connection Label to uniquely identify user accounts

<a id="form"></a>
## Add a Session Auth Input Form

The first thing to add for Session auth is an _input form_. Much like [Zapier's input designer](https://platform.zapier.com/docs/input-designer) for triggers and actions, this lets you design a simple form for users to enter their username, password, API key, domain, or any other data your API requires for authentication.

In Step 1's _Configure your Fields_ section, click _Add Fields_ to add a new field to your input form. There, add the following details:

- **Key**: The internal name for your field, used to reference this field in Zapier API calls. For convenience, use the same key as your API uses for this field.
- **Label**: A human-friendly name for this field that will be shown to users in the authentication form.
- **Required? (checkbox)**: Check if this field is required for successful authentication.
- **Type**: (optional) Usually String, but select "Password" to obscure text for secret values.
- **Help Text**: Add [Markdown](https://zapier.com/blog/beginner-ultimate-guide-markdown/) formatted details on what users should enter in this field, optionally with a link to your site to help users find the data.
- **Input Format**: (optional) Help users figure out exactly what piece of data you need them to enter. For example, for a subdomain, https://{{input}}.yourdomain.com/.
- **Default Value**: If appropriate, for optional fields, enter text that can be used by default if users don't enter a value. For required fields, enter text that can be used for authentication, but that won't be used in subsequent Zap steps.

Be sure to add one field for every piece of data users need to enter to authenticate their account with your API. Session auth does not include any default input fields.

### Computed Fields

If you need to use data received from the auth API response—such as team account names, domains, or subdomains—you can add a _Computed Field_ by selecting the Field Type at the top of the form. Add the field key, using the same field key as your API's response, and leave the remaining field details blank.

Zapier will then make sure this field is included in the response data, and you can reference it in subsequent API calls. Zapier will show an error if a field marked as computed is not included in the response data. Learn more in our [Computed Fields docs](https://platform.zapier.com/docs/advanced#computed).

Save each field after adding it, then click _Continue_ when every field your API needs has been added.

<a id="access"></a>
## Add a Token Exchange Request

![Zapier Session token exchange](https://cdn.zapier.com/storage/photos/b3c2c104aceb7e83965708f26ef47da8.png)

After collecting the credentials users enter in your input form, Zapier then needs to make an API call to exchange them for a session or access token.

Add the token exchange request URL in the field, select the correct HTTP method, and Zapier will automatically include the data from the input fields in the API request body. If your API expects the data in the URL params or HTTP headers instead, or requires additional data, click _Show Options_ and add the details your API call needs.

Optionally, click _Switch to Code Mode_ to [write custom JavaScript code](./faq#how-does-code-mode-work) for the API call instead of using the form inputs. You'll also need to do this to modify the response if your token exchange request doesn't return the token or Computed Fields data at the top level. All values to be saved should be returned at the top level, and will be referenced via {% raw %}`{{bundle.authData.field}}`{% endraw %}, where `field` is the key in the response.

Click _Save & Continue_ once finished to store your API call settings.

<a id="test"></a>
## Add a Test API Call

![Session auth test API request](https://cdn.zapier.com/storage/photos/1eadc273b3bef2c1ab584f4412acd39a.png)

Zapier then needs a Test API call—typically to a `/user` or `/me` endpoint that returns details about the user and needs no additional configuration—to test account authentication and ensure the access token works.

Add the endpoint URL to the _Test_ field, setting the correct HTTP method. Click _Show Options_ to customize the API call if needed. Alternately, click _Switch to Code Mode_ to [replace the form data with custom JavaScript code](./faq#how-does-code-mode-work) for your API call and response parsing.

As Session Auth doesn't include a defined standard for how access tokens are included in subsequent API calls, Zapier doesn't include the access token by default. Add it yourself—here, and in subsequent Trigger and Action step API calls—in your API call settings. Click _Show Options_, then add the access token to your API call's URL Params or HTTP Headers as needed. The Access Token will be in the `bundle.authData`, and typically be referenced as {% raw %}`{{bundle.authData.access_token}}`{% endraw %}, {% raw %}`{{bundle.authData.sessionToken}}`{% endraw %}, or a similar field, depending on how your token exchange response includes the token.

<a id="label"></a>
## Add a Connection Label

![Example Session auth connection label](https://cdn.zapier.com/storage/photos/541510fff1e01b358f898b33f0ced5c2.png)

Finally, add a connection label to uniquely identify each account users add from your app to Zapier. Zapier includes your app's name in the connection label by default, then any text you include in the connection label. You can include:

- Plain text that will be included in every account connection
- Any input field from your authentication form, or output from your Token Exchange API call
- Output fields from your app's authentication test API call

Learn more in our [Connection Label documentation](https://platform.zapier.com/docs/auth#label).

Click _Save & Continue_ when finished to save your authentication settings.

Then, test your authentication, adding a real account to ensure Zapier can successfully connect to your app, exchange user credentials for an access or session token, and use your test API call. Check our [Authentication Testing docs](https://platform.zapier.com/docs/auth#test) for more details, common errors you may encounter, and how to resolve those.