---
title: Add authentication with Digest Auth
order: 5
layout: post-toc
redirect_from: /build/
---

# Add authentication with Digest Auth

Digest Auth in Zapier follows the [RFC 7616](https://tools.ietf.org/html/rfc7616) standard. It includes an authentication form where users enter their username and password, optionally along with any additional data your API requires for authentication. Zapier then makes an unauthenticated API call, gets the nonce from your server, and uses it to encrypt and pass the authentication data to your server with each API call.

![Zapier digest auth form](https://cdn.zapier.com/storage/photos/3c842632d017aa50ba6470201d02f416.png)

When users add a new app account with Digest Auth to Zapier, they'll see an input form. Zapier then uses that data with each API request to authenticate the user.

> **When to use Digest Auth**: Use Digest Auth if your application uses the [RFC 7616](https://tools.ietf.org/html/rfc7616) authentication standard, where users enter their username and password where they can be passed encrypted to your API with the nonce key your app sends to Zapier on the first API call.

<a id="add"></a>
## How to Add Digest Auth to a Zapier Integration

![Add Digest Auth to Zapier Integration](https://cdn.zappy.app/fccd6ab8ba9c837158907d39eef1f288.png)

To add Digest Auth to a Zapier integration, open your integration's _Authentication_ page in Zapier visual builder, and select _Digest Auth_ from the dropdown.

You will then need the following to add Digest Auth to your integration:

- An input form where users add their login credentials. Zapier includes a form that requests username and password by default; you can add fields for any additional info needed
- A Test API endpoint where Zapier can make an API call to test the credentials
- A Connection Label to help users identify each account they authenticate

<a id="form"></a>
## Add a Digest Auth Input Form

![Zapier Digest Auth Input Form](https://cdn.zappy.app/680696e6c2d79b837600c5d1e32c9d40.png)

By default, Zapier includes an input form with Digest auth that requests a username and password. You can then add additional fields if your API requires them for authentication.

In Step 1's _Configure your Fields_ section, click _Add Fields_ to add a new field to your input form, which will show up underneath the default username and password fields. There, add the following details:

- **Key**: The internal name for your field, used to reference this field in Zapier API calls. For convenience, use the same key as your API uses for this field.
- **Label**: A human friendly name for this field that will be shown to users in the authentication form
- **Required Checkbox**: Check if this field is required for successful authentication
- **Help Text**: Add [Markdown](https://zapier.com/blog/beginner-ultimate-guide-markdown/) formatted details on what users should enter in this field, optionally with a link to your site to help users find the data
- **Default Value**: If your API request can accept standard data that works for every user, you can add a default value. Zapier will store and use the value on all API calls if set as non-required; if in a required field, Zapier will only use this value during account creation.

Add one field for each item your API needs for digest auth in addition to the username and password.

Save each field after adding it, then click _Continue_ when every field your API needs has been added.

<a id="test"></a>
## Add a Test API Call

![Digest Auth Test API Call](https://cdn.zappy.app/503eeb14514aa854ae06ba956b6c572c.png)

Digest Auth doesn't require any special API calls for authentication, so the only other details you need to add is a test API call. Zapier will use this test API call to verify that your user's credentials work—and will then use them to authenticate every subsequent API call.

Enter an API endpoint that doesn't require additional detail or configuration, such as a `/user` or `/me` call if available. Set the correct HTTP call. Zapier will include the default Digest authentication settings, but if your API needs additional detail or configuration, click the _Show Options_ button on the right to add custom URL params or HTTP headers. Optionally, click the _Switch to [Code Mode](https://platform.zapier.com/build/code-mode)_ toggle to write custom JavaScript code to handle your app's authentication and response bundle parsing.

<a id="label"></a>
## Add a Connection Label

![Zapier API Key auth connection label](https://cdn.zappy.app/0526347a17577147c712d0814b4995d5.png)

Finally add a connection label to identify each account users add from your app to Zapier. Zapier includes your app's name in the connection label by default, followed by the version number, then any text you include in the connection label. You can include:

- Plain text that will be included in every account connection
- Any input field from your authentication form
- Output fields from your app's authentication test API call

Fields can be referenced using double curly braces. For example, a `username` field would look like {% raw %}`{{username}}`{% endraw %}. 

Learn more in our [Connection Label documentation](https://platform.zapier.com/build/auth#label).

Click _Save & Continue_ when finished to save your authentication settings.

Then, test your authentication, adding a real account to ensure Zapier can successfully connect to your app and use your test API call. Check our [Authentication Testing docs](https://platform.zapier.com/build/auth#test) for more details, common errors you may encounter, and how to resolve those.
