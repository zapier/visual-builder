---
title: Add authentication with API Key
order: 2
layout: post-toc
redirect_from: 
    - /docs/apikey
---

# Add authentication with API Key

API Key authentication passes along a user-entered API Key with every API call. In your Zapier integration using API Key authentication, the API key—and optionally any other data your API needs—is included every time a Zap step runs.

![Zapier API Key auth example](https://cdn.zapier.com/storage/photos/19467b7d1852276b766b373373fd069c.png)
_Example API Key auth screen for users inside Zapier_

Use API Key authentication if your API primarily uses an API Key to identify accounts, especially with apps for weather, maps, content verification, file conversion, and other data tools that require a key for access to the service but do not contain user-specific content. 

Since API Key authentication allows you to create a custom input form, you can use it for any custom authentication type with username and password-based logins that don't fit other authentication scheme types.

## 1. Build input form

- Open the _Authentication_ tab in Zapier visual builder and select _API key_.

![Add API Key Auth to Zapier Integration](https://cdn.zappy.app/283f4595d4e25caee8256b2727eebb6d.png)

- Add authentication input fields where users will enter their API key and any other required authentication details. Check your API documentation for what fields are required, including user or account names, domains, and more. Note any details users may need on how to find that data in your app. API keys especially are often hidden under settings menus and you'll need to include those details in your input form's help text.

![Add fields to API key auth Zapier](https://cdn.zappy.app/8de37a192b7d50162a7a115281d4a388.png)

- Click the _Add Fields_ button and fill in the details for your field. Add the most commonly needed fields first, in the order users expect, as you cannot reorder fields once added. 

- Add the required _Key_, the name your API uses to reference this field.

![Zapier API Key Input Form](https://cdn.zappy.app/d122ac64a68b926bacd5b4e0954ead2c.png)

- Fill in the optional fields, as appropriate, especially the _Label_:

-- **Label**: A human-friendly name for this field that will be shown to users in the authentication form.

-- **Required? (checkbox)**: Check if this field is required for successful authentication.

-- **Type**: All input fields use the `string` text field by default; select `password` instead if you would like to obscure the data as users enter it.

-- **Help Text**: Include details to assist users in authenticating with your app, especially if they may be unsure where to find the data needed within your app. Format text with [Markdown](https://zapier.com/blog/beginner-ultimate-guide-markdown/), and include a hyperlink if needed.

-- **Input Format**: (optional) Help users figure out exactly what piece of data you need them to enter. For example, for a subdomain, https://{{input}}.yourdomain.com/.

-- **Default Value**: Include a value for this field to be used as a fallback. For optional fields, the default value is set on initial connection creation and used in the API call instead of missing or null values every time the Zap runs. For required fields, this value is used during connection creation, but not when the Zap runs (Zapier raises an error for missing/null values instead).

- Input fields marked as password and all authentication fields with sensitive, private data such as API keys from API Key auth are automatically censored at runtime. These values are stored in the Auth bundle and used in API calls, but are replaced in Zapier’s logs with a censored value like this `:censored:6:82a3be9927:`.

- Computed fields are not applicable to API Key authentication and are only used with OAuth v2 and Session Auth.

- Each input field is listed with its label, key, type, and required status in your authentication settings. Click the field to edit it, or click the gear icon and select _Delete_ to remove a field.

![Edit API key input fields](https://cdn.zappy.app/b27d364f2dd6ef2c1701c8b094a7ada0.png)

- Once you've added all the input fields to your authentication form, select _Continue_

## 2. Add a Test API Request

- Add an API call to your API that requires no configuration, typically a `/user` or `/me` call. Add the URL for the API call, and set the call type, typically a `GET`. This will test the user-entered API Key and any other credentials to ensure it enables a successful API call to your app. 

![Zapier test request API Key authentication](https://cdn.zappy.app/c4c58979ddcf7eb8a462ac5ff7a37348.png)

- The API Key and any additional input fields are automatically included in the URL Params and the HTTP Headers. Click _Show Options_ to remove the details where they are not needed. It is typically not recommended to pass any sensitive information such as the API Key in the URL Params. Passing it through the headers or even the body is preferable.

- To customize the test API request, select _Switch to Code Mode_ and write custom JavaScript code to handle your test API call and the response parsing as needed. The first time you click the toggle, Zapier will convert your API call to code. If you switch back to Form Mode though, Zapier will not convert your code changes to the Form mode, nor will any subsequent changes in the form be added to your code.

![Zapier code mode API Key auth](https://cdn.zappy.app/b5f336f8d8642f04d99d584f04c4e334.png)

## 3. Configure a Connection Label

Review [connection label documentation](https://platform.zapier.com/build/connection-label) to optionally differentiate the app accounts users connect.  

## 4. Test your authentication

Connect a valid user account to [test authentication](https://platform.zapier.com/build/test-auth).
