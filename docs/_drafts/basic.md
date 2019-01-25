---
title: — Basic Auth
order: 4
layout: post-toc
redirect_from: /docs/
---

## Authentication | Basic Auth

Basic Authentication lets you connect APIs to Zapier that authenticate users with a username and password. In a Zapier integration with Basic Auth, Zapier includes the name and password of the user in the API request bundle every time Zapier polls an API endpoint for new data or posts new data to an API endpoint.

![Zapier basic auth for users](https://cdn.zapier.com/storage/photos/8987788036a5a70072c9e75c4911ff6a.png)
_Example Basic Auth screen for users inside Zapier_

When you add Basic Auth to your integration, Zapier adds a pre-built form that requests a username and password whenever users authenticate with your API. Zapier then makes a test call to verify the credentials, and stores them to use with every subsequent API call Zapier makes to your app on behalf of the user. 

Use Basic Auth if your API only requires a username and password, and needs no special configuration.

## How to Add Basic Auth to a Zapier Integration

![Add Basic Auth to Zapier integration](https://cdn.zapier.com/storage/photos/d5f4146ecea9123de570743234478dfa.png)

To add Basic Auth to your Zapier integration, open the _Authentication_ tab in Zapier visual builder and select _Basic Auth_.

![Basic Auth settings](https://cdn.zapier.com/storage/photos/f29b99f3c22fa166852086d76e484774.png)

Zapier automatically adds a form where users will enter their username and password, so you don't need to configure anything for core basic auth. All you need to add is a test API call where Zapier can verify that the credentials work, and optionally a connection label to help users identify the account.

For the test API call, enter an API endpoint under the _Test_ header where Zapier can test users' credentials for your app, and set the correct call method (typically `GET`). Use an API endpoint that does not require any additional details or configuration, such as `/me` or `/user` to simply check the app authentication and retrieve details about the user.

![Basic Auth configuration in Zapier](https://cdn.zapier.com/storage/photos/6a872d65924adb5c12afe54589f387f7.png)

If your API requires any custom details in the API call, click the _Show Options_ link in the lower right, then add URL params or HTTP headers if needed.

![Zapier Basic Auth code mode](https://cdn.zapier.com/storage/photos/16d02986ea3fda8bcae045604df3872e.png)

If you need more customization, you can write custom JavaScript code to call your API and parse the output data. To do that, click the _Switch to Code Mode_ toggle. The first time you click the toggle, Zapier will convert the data from your API call form to JavaScript. If you switch back to form mode, Zapier will save your custom code but will not use it in the API call. Additionally, if you switch back to code mode again later, Zapier will not add any changes from the API call form to your code.

![Zapier Basic Auth connection label](https://cdn.zapier.com/storage/photos/7b04cb3a81e8dcb4f0508aec0e69cf2d.png)

Finally, add a connection label to your Zapier integration. Zapier always includes the app's name in each account label. You can additionally include:

- Plain text that will be included after your app's full name
- Output fields from your app's authentication test API call, referenced with {% raw %}`{{bundle.authData.field}}`{% endraw %} variables, replacing `field` for your API output field name.

### Test Authentication

![Test Zapier authentication](https://cdn.zapier.com/storage/photos/37a59dae4fe33ffc4894b1df23e7be83.png)

Once you've added the core details of how Zapier can authenticate users and test the connection, you need to try it out to set the final options. Click the _Connect an Account_ button to add your account with this app to Zapier.

Zapier will open a popup window like one your users will see when authenticating your app with Zapier. Enter your account info or API key, or authenticate through your app's site, using real account details for a personal or testing account.

> **Tip**: The account you add here will be the one you use to test any triggers and actions you add to Zapier in visual builder. It can also be used in live Zaps in Zapier, if you wish. These account details are not tied to your app definition, though, and if you add a collaborator to your Zapier integration, they will need to connect their own account for testing.

Once you've added your account, you'll see it with a connection label under the setup box. Then click _Test Connected Account_ to have Zapier run your testing API call and ensure your app connection works.

![Example Zapier authentication test response](https://cdn.zapier.com/storage/photos/d5cf1a5cbc5a8389ad3272d01ef71c06.png)

If everything works as expected, Zapier will receive response data from the API call and display it in the _Response_ tab. You can look through the JSON-formatted fields from the response and use any of the field names in your account [connection label](#label). You can also look at the _Bundle_ tab to see the data Zapier used in the API request, and the _HTTP_ tab to see the full request and response details.

![Example Zapier authentication error](https://cdn.zapier.com/storage/photos/3337e520ebab7b09de282e598ea70cfd.png)

If something didn't work, Zapier will show the error message in the _Response_ tab, with the full response content in the _HTTP_ tab if you need more detail. Update your authentication settings accordingly, click the _Save & Continue_ button, then try testing your connected account again—and repeat until your authentication works and tests correctly.

With that, your app authentication should be finished, and your integration ready to add triggers and actions.

<a id="error"></a>

## Common Basic Auth Error Messages

![404 error in Zapier basic auth](https://cdn.zapier.com/storage/photos/88b058e13a0321efdbdab3e0a046dfa5.png)

If Zapier cannot successfully make the test API call to verify users' credentials, you may see an error message in the Test section of your Zapier integration. Zapier shows a simplified error message in the _Response_ tab by default, along with a red x and a _Request Failed_ message in the top right.

![Zapier Error Response Content](https://cdn.zapier.com/storage/photos/2511421236621c8c5ea7c160f2a2ca7e.png)

You can find the original API response with the full error message in the _HTTP_ tab under _Response Content_.

The most common errors include:

### 404

![404 error in Zapier basic auth](https://cdn.zapier.com/storage/photos/88b058e13a0321efdbdab3e0a046dfa5.png)

The standard HTTP 404 `Not Found` error is commonly returned when:

- Test API endpoint URL is incorrect
- Test API call method is incorrect

If you encounter this error, double-check both the API endpoint URL and the call method (typically `GET`). Ensure both are set to what your API expects, then click the _Save & Continue_ button, and click the _Test Connected Account_ button again.

### 401

![401 error in Zapier basic auth](https://cdn.zapier.com/storage/photos/d13a9b1ff308b520ae4b29461cc754d6.png)

The standard HTTP 401 `Unauthorized` error is commonly returned when:

- User account credentials are incorrect, expired, or revoked

Try authenticating your app user account with Zapier again. Click _Connect an Account_, add credentials for an active account on the app, then try the test again.

### Error Parsing Response

![Error Parsing Response in Zapier Basic Auth](https://cdn.zapier.com/storage/photos/deebd9e07497a209479a66e7f1d465b0.png)

The _Error Parsing Response_ error is commonly returned when:

- API returns non-standard and especially non-JSON output
- Test API endpoint URL is incorrect

Double-check the test API URL is entered correctly. If a standard, non-API endpoint URL is entered in the test field, the site will return its raw HTML page to Zapier and will result in this error. If you do change the URL, click _Save & Continue_ then test your connection again.

If your API call is correct and returning data in a format Zapier does not expect, you will need to switch to code mode and add custom parsing for your API response. Under the _Test_ API call in the top of your app's Authentication settings, click _Switch to Code Mode_, then add custom JavaScript code to parse your API response.