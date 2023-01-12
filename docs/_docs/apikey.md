---
title: — API Key Auth
order: 6
layout: post-toc
redirect_from: /docs/
---

# Authentication — API Key Auth

API Key authentication lets apps verify users' account with an API key that is passed along with every API call. In a Zapier integration using API Key authentication, Zapier includes the API key—optionally along with any other data your API needs—every time a Zap step runs.

![Zapier API key auth example](https://cdn.zapier.com/storage/photos/19467b7d1852276b766b373373fd069c.png)
_Example API key auth screen for users inside Zapier_

API Key authentication works similarly to Zapier's [Basic Auth](https://platform.zapier.com/docs/basic) in that Zapier passes the credentials with every API call. Here, though, you need to build the [input form](https://platform.zapier.com/docs/input-designer) where users add their API key and any other optional information your API requires, such as their account name, site URL, and other identifying data. You can additionally include help text under each field to direct users to where they can retrieve their API key.

> **When to use API key authentication:** Use API key authentication if your API primarily uses an API key to identify accounts, especially with apps for weather, maps, content verification, file conversion, and other data tools that require a key for access to the service but do not contain user-specific content. Alternately, since API key authentication allows you to create a custom input form, you can use it to customize username and password-based logins that don't fit Zapier's default Basic auth scheme.

<a id="add"></a>

## How to Add API Key Auth to a Zapier Integration

![Add API Key Auth to Zapier Integration](https://cdn.zappy.app/283f4595d4e25caee8256b2727eebb6d.png)

To add API Key Auth to your Zapier integration, open the _Authentication_ tab in Zapier visual builder and select _API key_.

You then need to:

- Build an input form for users to enter their API key and any other required data
- Add a test API call to verify user credentials when adding new accounts
- Add a connection label to identify each added account
- Test the authentication to ensure it works and to obtain a testing login that can be used in testing subsequent Zap steps as you add them

<a id="form"></a>

## Add an API Key Input Form

![Add fields to API key auth Zapier](https://cdn.zappy.app/8de37a192b7d50162a7a115281d4a388.png)

Start by adding a form where users will enter their API key and other authentication details when connecting their app account to Zapier. Check your API documentation for what fields are required, including user or account names, domains, and more. Additionally, note any details users may need on how to find that data since API keys especially are often hidden under settings menus and you'll need to include those details in your input form's help text.

For each field that you need, click the _Add Fields_ button and fill in the details for your field. Be sure to add the most commonly needed fields first, in the order users expect, as you cannot reorder fields once added.

![Zapier API Key Input Form](https://cdn.zappy.app/d122ac64a68b926bacd5b4e0954ead2c.png)

Every input field requires a _Key_, the name your API uses to reference this field. Enter the same key name that your API uses.

Then fill in the optional fields, as appropriate, especially the _Label_:

- **Label**: A human-friendly name for this field. Enter what this value is called inside your app's UI.
- **Is this field required**: Check this box for your API key field, and for any other fields that your API requires for authentication.
- **Type**: Zapier uses the `string` text field for all input fields by default; select `password` instead if you would like to obscure the data as users enter it.
- **Help Text**: Include details to assist users in authenticating with your app, especially if they may be unsure where to find the data needed. Format text with [Markdown](https://zapier.com/blog/beginner-ultimate-guide-markdown/), and include a link if needed.
- **Default Value**: Include a value for this field to be used as a fallback. For optional fields, the default value is set on initial creation and used instead of missing or null values every time the Zap runs. For required fields, this value is used during Zap creation, but not when the Zap runs (Zapier raises an error for missing/null values instead).

> **Note:** The input field designer also includes an option for computed fields; those are not applicable to API key login and are only used with OAuth v2 and Session auth.

![Edit API key input fields](https://cdn.zappy.app/b27d364f2dd6ef2c1701c8b094a7ada0.png)

Once you've added your input fields, Zapier lists each input field with its label, key, type, and required status on your authentication settings. Click the field to edit it, or click the gear icon and select _Delete_ to remove a field.

When you've added the needed forms, click _Continue_ to add a test API call and continue setting up your app's authentication.

<a id="request"></a>

## Add a Test API Request

![Zapier test request API Key authentication](https://cdn.zappy.app/c4c58979ddcf7eb8a462ac5ff7a37348.png)

Zapier then needs a way to test the API key and other input field data users enter and ensure it enables a successful API call. For that, in step two, add an API call to your API that requires no configuration, typically a `/user` or `/me` call. Add the URL for the API call, and set the call type.

Zapier automatically includes the API key and any additional input fields you added to your input form in the URL Params. If your API needs that data as headers instead, click _Show Options_ and add the details there instead.

![Zapier code mode API Key auth](https://cdn.zappy.app/b5f336f8d8642f04d99d584f04c4e334.png)

If you need a custom API call, you can switch to code mode and write custom JavaScript code to handle your test API call and the response parsing, if needed. Click the _Switch to Code Mode_ toggle to enable it. The first time you click the toggle, Zapier will convert your API call to code. If you switch back to Form mode, though, Zapier will not convert your code changes to the form mode, nor will any subsequent changes in form mode be added to your code.

<a id="label"></a>

## Configure a Connection Label

![Zapier API Key auth connection label](https://cdn.zappy.app/0be1ac5639e1e6cf2366474b0c40910c.png)

Finally, add a connection label to help users identify each account from your app that they connect with Zapier. Zapier includes your app's name in the connection label by default, followed by any text you include in the connection label. You can add:

- Plain text that will be included in every account connection
- Any input field from your authentication form
- Output fields from your app's authentication test API call

Fields can be referenced using double curly braces. For example, a `username` field would look like {% raw %}`{{username}}`{% endraw %}. 

**Do not use the API Key (or anything sensitive) in the connection label**, since the label appears in plain text on Zapier. Use identifiable, but non-sensitive, information. Learn more in our [Connection Label documentation](https://platform.zapier.com/docs/auth#label).

When you're finished, click _Save & Continue_ to save your authentication settings.

Then, test your authentication, adding a real account to ensure Zapier can successfully connect to your app and use your test API call. Check our [Authentication Testing docs](https://platform.zapier.com/docs/auth#test) for more details, common errors you may encounter, and how to resolve those.
