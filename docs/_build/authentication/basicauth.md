---
title: Add authentication with Basic Authentication
order: 3
layout: post-toc
redirect_from: 
    - /docs/basic
---

# Add authentication with Basic Authentication

APIs using Basic Authentication will authenticate users with a username and password. In your Zapier integration using Basic Auth, Zapier includes the username and password credentials in the API request bundle every time Zapier polls an API endpoint for new data or posts new data to an API endpoint.

![Zapier basic auth for users](https://cdn.zapier.com/storage/photos/8987788036a5a70072c9e75c4911ff6a.png)
_Example Basic Auth screen for users inside Zapier_

Use Basic Auth if your API requires a username and password or other basic fields, needs no special configuration, and specifically if your API leverages "[HTTP Basic Authentication](https://en.wikipedia.org/wiki/Basic_access_authentication)". For further customization of your login flow or to request additional data from users, [API Key authentication](https://platform.zapier.com/docs/apikey) may be a better fit. 

## 1. Build an input form 

- Open the _Authentication_ tab in Zapier visual builder and select _Basic Auth_.

![Add Basic Auth to Zapier integration](https://cdn.zappy.app/a8f5698b7c1fd2556eb6b6dc0a983155.png)

- The pre-built input form for Basic Authentication includes a username and password field already.

- Add additional fields if your API documentation requires it by selecting _Add Fields_ and fill in the details for your field. Add the most commonly needed fields first, in the order users expect, as you cannot reorder fields once added. 

![Add fields to Basic Auth Zapier](https://cdn.zappy.app/c17e6838cf27ed5704f561c75625864f.png)

- Add the required _Key_, the name your API uses to reference this field.

- Fill in the optional fields, as appropriate, especially the _Label_:

-- **Label**: A human-friendly name for this field that will be shown to users in the authentication form.

-- **Required? (checkbox)**: Check if this field is required for successful authentication.

-- **Type**: All input fields use the `string` text field by default; select `password` instead if you would like to obscure the data as users enter it.

-- **Help Text**: Include details to assist users in authenticating with your app, especially if they may be unsure where to find the data needed within your app. Format text with [Markdown](https://zapier.com/blog/beginner-ultimate-guide-markdown/), and include a hyperlink if needed.

-- **Input Format**: (optional) Help users figure out exactly what piece of data you need them to enter. For example, for a subdomain, https://{{input}}.yourdomain.com/.

-- **Default Value**: Include a value for this field to be used as a fallback. For optional fields, the default value is set on initial connection creation and used in the API call instead of missing or null values every time the Zap runs. For required fields, this value is used during connection creation, but not when the Zap runs (Zapier raises an error for missing/null values instead).

![Zapier Basic Auth Input Form](https://cdn.zappy.app/f4346b3456ea0080862db2eae7108050.png)

- Input fields marked as password and all authentication fields with sensitive, private data such as both username and password from Basic Auth are automatically censored at runtime. These values are stored in the Auth bundle and used in API calls, but are replaced in Zapier’s logs with a censored value like this `:censored:6:82a3be9927:`. Due to this, it is not possible to view the exact tokens or keys in Zapier's logs. To verify that the same token as was returned by the authentication, is being used in subsequent API calls; you can compare censored value characters, for example `:censored:6:82a3be9927:` would have the same value ending in 9927 when used in a subsequent call. 

- Computed fields are not applicable to Basic Authentication and are only used with OAuth v2 and Session Auth.

- Each input field is listed with its label, key, type, and required status in your authentication settings. Click the field to edit it, or click the gear icon and select _Delete_ to remove a field.

![Edit Basic Auth input fields](https://cdn.zappy.app/a207e9be179e401dadfa9d5422e4df5c.png)

- Once you've added all the input fields to your authentication form, select _Continue_

## 2. Add a Test API Request

- Add an API call to your API that requires no configuration, typically a `/user` or `/me` call. Add the URL for the API call, and set the call type, typically a `GET`. This will test the user-entered credentials to ensure it enables a successful API call to your app. 

- The username and password input fields are automatically included in the URL Params and the HTTP Headers. Click _Show Options_ to remove the details where they are not needed. It is typically not recommended to pass any sensitive information such as the password in the URL Params. Passing it through the headers or even the body is preferable.

![Basic Auth configuration in Zapier](https://cdn.zappy.app/a910a8114e18b545a93bf1e2e735e5a1.png)

- To customize the test API request, select _Switch to Code Mode_ and write custom JavaScript code to handle your test API call and the response parsing as needed. The first time you click the toggle, Zapier will convert your API call to code. If you switch back to Form Mode though, Zapier will not convert your code changes to the Form Mode, nor will any subsequent changes in the form be added to your code.

![Zapier Basic Auth code mode](https://cdn.zappy.app/6ec17f1acd3def0addad6dfc9167acec.png)

## 3. Configure a Connection Label

Review [connection label documentation](https://platform.zapier.com/build/connection-label) to optionally differentiate the app accounts users connect.  

## 4. Test your authentication

Connect a valid user account to [test authentication](https://platform.zapier.com/build/test-auth).