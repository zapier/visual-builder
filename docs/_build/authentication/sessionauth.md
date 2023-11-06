---
title: Add authentication with Session Authentication
order: 6
layout: post-toc
redirect_from: 
    - /docs/session
---

# Add authentication with Session Authentication

Session authentication has elements of Basic authentication — where Zapier requests a username and password, and OAuth v2 — where Zapier redirects users to the app's site to allow access. User credentials are exchanged for a token used to authenticate subsequent API calls.

It is similar to cookie-based authentication in your browser, only here the "cookie" is an auth token stored by Zapier.

![Example Zapier session login form](https://cdn.zapier.com/storage/photos/7c7092a2311cf217298cb3e3f5735385.png)

Use Session authentication with your Zapier integration if your API is designed for session-, cookie-, or token-based authentication. 

## 1. Build an input form

- Open the _Authentication_ tab in Zapier visual builder and select _Session Auth_.

![Add Session Auth to Zapier integration](https://cdn.zappy.app/2453d5aa12c5aa4fe02beae9d85f6786.png)

- Session auth does not include any default input fields. Add the fields required by your API by selecting _Add Fields_ and fill in the details for each field. Add the most commonly needed fields first, in the order users expect, as you cannot reorder fields once added. 

- Two types of fields are available when building an OAuth v2 input form. Standard Fields, work much like other form fields with Zapier's [input form](https://platform.zapier.com/build/input-designer) in triggers and actions. [Computed Fields](https://platform.zapier.com/build/authentication/computed-fields) make sure specific fields are returned by your app's authentication API call response.

- For each field, add the required _Key_, the name your API uses to reference this field.

- Fill in the optional fields, as appropriate, especially the _Label_:

-- **Label**: A human-friendly name for this field that will be shown to users in the authentication form.

-- **Required? (checkbox)**: Check if this field is required for successful authentication.

-- **Type**: All input fields use the `string` text field by default; select `password` instead if you would like to obscure the data as users enter it.

-- **Help Text**: Include details to assist users in authenticating with your app, especially if they may be unsure where to find the data needed within your app. Format text with [Markdown](https://zapier.com/blog/beginner-ultimate-guide-markdown/), and include a hyperlink if needed.

-- **Input Format**: (optional) Help users figure out exactly what piece of data you need them to enter. For example, for a subdomain, https://{{input}}.yourdomain.com/.

-- **Default Value**: Include a value for this field to be used as a fallback. For optional fields, the default value is set on initial connection creation and used in the API call instead of missing or null values every time the Zap runs. For required fields, this value is used during connection creation, but not when the Zap runs (Zapier raises an error for missing/null values instead).

- Input fields marked as password and all authentication fields with sensitive, private data such as both username and password from Session Auth are automatically censored at runtime. These values are stored in the Auth bundle and used in API calls, but are replaced in Zapier’s logs with a censored value like this `:censored:6:82a3be9927:`.

- Each input field is listed with its label, key, type, and required status in your authentication settings. Click the field to edit it, or click the gear icon and select _Delete_ to remove a field.

- For computed fields, available in OAuth v2 and Session Auth only, review [computed fields documentation](https://platform.zapier.com/build/authentication/computed-fields). 

## 2. Add a Token Exchange Request

- Add the token exchange request URL and select the HTTP method.  Zapier will automatically include the data from the input fields in the API request body. If your API expects the data in the URL Params or HTTP headers instead, or requires additional data, click _Show Options_ and add the details your API call needs. It is typically not recommended to pass any sensitive information such as the password in the URL Params. Passing it through the headers or the body is preferable.

![Zapier Session token exchange](https://cdn.zappy.app/70908a4341146b3df38c9a3169f68cfb.png)

- To customize the token exchange request, select _Switch to Code Mode_ and write custom JavaScript code to handle the API call and the response parsing as needed. The first time you click the toggle, Zapier will [convert your API call to code](https://platform.zapier.com/build/code-mode). If you switch back to Form Mode though, Zapier will not convert your code changes to the Form Mode, nor will any subsequent changes in the form be added to your code.

- If your token exchange request doesn't return the token and/or any [computed fields](https://platform.zapier.com/build/authentication/computed-fields) at the top level, also use [Code Mode](https://platform.zapier.com/build/code-mode) to modify the response so those fields are available at the top level. It is not possible to store an object with nested keys from the response.

- All values will be referenced via {% raw %}`{{bundle.authData.field}}`{% endraw %}, where `field` is the key in the response.

## 3. Add a Test API Request

- Add an API call to your API that requires no configuration, typically a `/user` or `/me` call. Add the URL for the API call, and set the call type, typically a `GET`. This will test the user-entered credentials to ensure it enables a successful API call to your app. 

- Session Auth doesn't include a defined standard for how access tokens are included in subsequent API calls, so unlike other authenticaton methods, Zapier doesn't include the access token by default. You'll need to add it in the test request and in subsequent Trigger and Action step API calls. 

- Click _Show Options_, then add the access token to your API call's URL Params or HTTP Headers as needed. It is typically not recommended to pass any sensitive information such as the password in the URL Params. Passing it through the headers or the body is preferable. The Access Token will be in the `bundle.authData`, and typically be referenced as {% raw %}`{{bundle.authData.access_token}}`{% endraw %}, {% raw %}`{{bundle.authData.sessionToken}}`{% endraw %}, or a similar field, depending on how your token exchange response includes the token.

![Session auth test API request](https://cdn.zappy.app/bf9711293b10af85200fb8d7bfe21e39.png)

## 4. Configure a Connection Label

Review [connection label documentation](https://platform.zapier.com/build/connection-label) to optionally differentiate the app accounts users connect.  

## 5. Test your authentication

Connect a valid user account to [test authentication](https://platform.zapier.com/build/test-auth).