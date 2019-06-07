---
title: — Basic Auth
order: 4
layout: docs
redirect_from: /docs/
---

# Authentication — Basic Auth

Basic Authentication lets you connect APIs to Zapier that authenticate users with a username and password. In a Zapier integration with Basic Auth, Zapier includes the name and password of the user in the API request bundle every time Zapier polls an API endpoint for new data or posts new data to an API endpoint.

![Zapier basic auth for users](https://cdn.zapier.com/storage/photos/8987788036a5a70072c9e75c4911ff6a.png)
_Example Basic Auth screen for users inside Zapier_

When you add Basic Auth to your integration, Zapier adds a pre-built form that requests a username and password whenever users authenticate with your API. Zapier then makes a test call to verify the credentials, and stores them to use with every subsequent API call Zapier makes to your app on behalf of the user. 

> **When to use Basic Auth:** Use Basic Auth if your API only requires a username and password, needs no special configuration, and specifically if your API leverages "[HTTP Basic Authentication](https://en.wikipedia.org/wiki/Basic_access_authentication)". If you need further customization of your login flow or need additional data from users, [API key authentication](https://platform.zapier.com/docs/apikey) works the same as Basic auth but includes a customizable form where you can request additional authentication data from users.

<a id="add"></a>
## How to Add Basic Auth to a Zapier Integration

![Add Basic Auth to Zapier integration](https://cdn.zapier.com/storage/photos/d5f4146ecea9123de570743234478dfa.png)

To add Basic Auth to your Zapier integration, open the _Authentication_ tab in Zapier visual builder and select _Basic Auth_.

![Basic Auth settings](https://cdn.zapier.com/storage/photos/f29b99f3c22fa166852086d76e484774.png)

Zapier automatically adds a form where users will enter their username and password, so you don't need to configure anything for core basic auth. 

All you need to add is a test API call where Zapier can verify that the credentials work, and optionally a connection label to help users identify the account.

<a id="test_request"></a>
## Configure a Test Request

For the test API call, enter an API endpoint under the _Test_ header where Zapier can test users' credentials for your app, and set the correct call method (typically `GET`). Use an API endpoint that does not require any additional details or configuration, such as `/me` or `/user` to simply check the app authentication and retrieve details about the user.

![Basic Auth configuration in Zapier](https://cdn.zapier.com/storage/photos/6a872d65924adb5c12afe54589f387f7.png)

If your API requires any custom details in the API call, click the _Show Options_ link in the lower right, then add URL params or HTTP headers if needed.

![Zapier Basic Auth code mode](https://cdn.zapier.com/storage/photos/16d02986ea3fda8bcae045604df3872e.png)

If you need more customization, you can write custom JavaScript code to call your API and parse the output data. To do that, click the _Switch to Code Mode_ toggle. The first time you click the toggle, Zapier will convert the data from your API call form to JavaScript. If you switch back to form mode, Zapier will save your custom code but will not use it in the API call. Additionally, if you switch back to code mode again later, Zapier will not add any changes from the API call form to your code.

<a id="label"></a>
## Configure a Connection Label

![Zapier Basic Auth connection label](https://cdn.zapier.com/storage/photos/196e9987836a34e4528a0b8ebd9dbd25.png)

Finally, add a connection label to your Zapier integration. Zapier always includes the app's name in each account label. You can additionally include:

- Plain text that will be included after your app's full name
- The username that users enter in the Zapier authentication form when adding your app—enter {% raw %}`{{bundle.authData.username}}`{% endraw %} to include that
- Output fields from your app's authentication test API call, referenced with {% raw %}`{{bundle.inputData.field}}`{% endraw %} variables, replacing `field` for your API output field name.

Learn more in our [Connection Label documentation](https://platform.zapier.com/docs/auth#label).

Click _Save & Continue_ when finished to save your authentication settings.

Then, test your authentication, adding a real account to ensure Zapier can successfully connect to your app and use your test API call. Check our [Authentication Testing docs](https://platform.zapier.com/docs/auth#test) for more details, common errors you may encounter, and how to resolve those.
