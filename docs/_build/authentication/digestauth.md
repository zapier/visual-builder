---
title: Add authentication with Digest Auth
order: 4
layout: post-toc
redirect_from: 
    - /docs/digest
---

# Add authentication with Digest Authentication

Digest Auth prompts users to enter their username and password, optionally along with any additional data your API requires for authentication. Zapier makes an unauthenticated API call to get the nonce from your server, and uses it to encrypt and pass the authentication data to your server with each API call.

![Zapier digest auth form](https://cdn.zapier.com/storage/photos/3c842632d017aa50ba6470201d02f416.png)

Use Digest Auth if your API uses the [RFC 7616](https://tools.ietf.org/html/rfc7616) authentication standard, where users enter their username and password to be passed encrypted to your API with the nonce key your app sends to Zapier on the first API call.

## 1. Build an input form

- Open the _Authentication_ tab in Zapier visual builder and select _Digest Auth_.

![Add Digest Auth to Zapier Integration](https://cdn.zappy.app/fccd6ab8ba9c837158907d39eef1f288.png)

- The pre-built input form includes username and password fields already.

- Add additional fields if your API documentation requires it by selecting _Add Fields_ and fill in the details for your field. Add the most commonly needed fields first, in the order users expect, as you cannot reorder fields once added. 

![Zapier Digest Auth Input Form](https://cdn.zappy.app/680696e6c2d79b837600c5d1e32c9d40.png)

- Add the required _Key_, the name your API uses to reference this field.

- Fill in the optional fields, as appropriate, especially the _Label_:

  **Label**: A human-friendly name for this field. Enter what this value is called inside your app's UI.

  **Is this field required**: Check this box for the API key field, and any other fields your API requires to authenticate.

  **Type**: All input fields use the `string` text field by default; select `password` instead if you would like to obscure the data as users enter it.

  **Help Text**: Include details to assist users in authenticating with your app, especially if they may be unsure where to find the data needed within your app. Format text with [Markdown](https://zapier.com/blog/beginner-ultimate-guide-markdown/), and include a hyperlink if needed.
  
  **Default Value**: Include a value for this field to be used as a fallback. For optional fields, the default value is set on initial connection creation and used in the API call instead of missing or null values every time the Zap runs. For required fields, this value is used during connection creation, but not when the Zap runs (Zapier raises an error for missing/null values instead).

- Input fields marked as password and all authentication fields with sensitive, private data such as both username and password from Digest Auth are automatically censored at runtime. These values are stored in the Auth bundle and used in API calls, but are replaced in Zapier’s logs with a censored value like this `:censored:6:82a3be9927:`. Due to this, it is not possible to view the exact tokens or keys in Zapier's logs. To verify that the same token as was returned by the authentication, is being used in subsequent API calls; you can compare censored value characters, for example `:censored:6:82a3be9927:` would have the same value ending in 9927 when used in a subsequent call.

- Computed fields are not applicable to Basic Authentication and are only used with OAuth v2 and Session Auth.

- Each input field is listed with its label, key, type, and required status in your authentication settings. Click the field to edit it, or click the gear icon and select _Delete_ to remove a field.

![Edit or delete input fields](https://cdn.zappy.app/573a3eb19a884c44fd67b9fa421c3bf4.png)

## 2. Add a Test API Request

- Add an API call to your API that requires no configuration, typically a `/user` or `/me` call. Add the URL for the API call, and set the call type, typically a `GET`. This will test the user-entered credentials to ensure it enables a successful API call to your app. 

- The Digest input fields you configured earlier are automatically included in the URL Params and the HTTP Headers. Click _Show Options_ to remove the details where they are not needed or add any custom URL params or HTTP headers your API requires. It is typically not recommended to pass any sensitive information such as the password in the URL Params. Passing it through the headers or even the body is preferable.

![Digest Auth Test API Call](https://cdn.zappy.app/503eeb14514aa854ae06ba956b6c572c.png)

- To customize the test API request, select _Switch to Code Mode_ and write custom JavaScript code to handle your test API call and the response parsing as needed. The first time you click the toggle, Zapier will [convert your API call to code](https://platform.zapier.com/build/code-mode). If you switch back to Form Mode though, Zapier will not convert your code changes to the Form Mode, nor will any subsequent changes in the form be added to your code.

## 3. Configure a Connection Label

Review [connection label documentation](https://platform.zapier.com/build/connection-label) to optionally differentiate the app accounts users connect.  

## 4. Test your authentication

Connect a valid user account to [test authentication](https://platform.zapier.com/build/test-auth).