---
title: Authentication
order: 1
layout: post-toc
redirect_from: 
    - /quickstart/auth
    - /docs/auth
---

# Authentication

Connecting an app to Zapier starts with authentication. Users select an app they wish to use in their Zap, authenticating their account with that app to allow Zapier to access their data.

Zapier will have access to the account until the authorization expires, is revoked, or credentials are changed. Zapier will automatically refresh OAuth v2 and session authentications when refresh token functionality is enabled in the integration.

Once users authenticate an app account to Zapier, they can use any of that app's triggers/actions in their Zaps without authenticating again. Users would authenticate another connection if they wish to use additional accounts from an app with Zapier, for example if they have a work and personal account in one app. 

Zapier integration builders define how Zapier connects to your app to authenticate users, adding an API call where Zapier tests the account authentication. 

All Zapier integrations that can access or add private data for users require authentication. The only apps that don't require authentication include data feeds (such as news or weather updates) or utilities (such as file format conversion tools or public search engines). If you're building an integration for any app that stores private data and requires an account to use, your integration will require authentication.

## Zapier Supported Authentication Schemes

Zapier supports the following five authentication schemes in the Platform UI, each with their own settings:

- API Key
- OAuth v2
- Session Auth
- Basic Auth
- Digest Auth

![Zapier Authentication](https://cdn.zappy.app/37e7829169eb2e07278d512c174cd708.png)

For more custom authentication schemes, switch to the [Platform CLI](https://platform.zapier.com/manage/export-integration). 

## How to Remove or Change Type of Authentication Scheme 

You cannot change an integration’s authentication scheme. Instead, remove an existing integration’s authentication, then add a new authentication scheme.

To remove a Zapier integration's authentication scheme in the Platform UI, open the _Authentication_ page. Click the gear icon beside the existing authentication scheme, click _Delete_, then confirm to remove the authentication.

Then add your app’s new authentication scheme to the Zapier integration instead.

Never remove authentication from an existing integration with active users. If an active integration’s authentication scheme needs to be changed, clone a new major version and add the new authentication.

![Zapier Remove Authentication Scheme](https://cdn.zappy.app/a616ced2f22bdf0873b0f910fc238424.png)

## Common Authentication Error Messages

When the test API call to verify users' credentials is unsuccessful, an error message shows in the Test section of your Zapier integration. Zapier shows a simplified error message in the _Response_ tab by default.

![404 error in Zapier basic auth](https://cdn.zappy.app/f6e4616d8e457f2ccf8dd872b2a15aac.png)

The original API response with the full error message is shown in the _HTTP_ tab under _Response Content_.

![Zapier Error Response Content](https://cdn.zappy.app/2598ca338518d55cb41cebc2116bd1af.png)

The most common errors include:

### 404

The standard HTTP 404 `Not Found` error is commonly returned when:

- Test API endpoint URL is incorrect
- Test API call method is incorrect

![404 error in Zapier basic auth](https://cdn.zappy.app/4b268ddfa326ee23cb902d05acc6ac10.png)

Verify both the API endpoint URL and the call method (typically `GET`). Ensure both are set to what your API expects, then click the _Save & Continue_ button, and click the _Test Connected Account_ button again.

### 401 or 403

The standard HTTP 401 `Unauthorized` or HTTP 403 `Forbidden` error is commonly returned when:

- User account credentials are incorrect, expired, or revoked

Try authenticating your app user account with Zapier again. Click _Connect an Account_, add credentials for an active account on the app, then try the test again.

![401 error in Zapier basic auth](https://cdn.zappy.app/e8dd16ccd395d9c466d81ce669510296.png)

### 400

The standard HTTP 400 `Bad Request` error is often returned when:

- OAuth v2 Client ID and/or Secret are incorrect or expired
- Some other part of your request is malformed, particularly a token exchange request

Check the full error message from the error or Zapier's testing logs to see if it lists why the call failed, then correct that part of your authentication flow. Verify each part of your authentication flow is entered correctly, including the request headers, URL parameters, and request body for each part of your authentication flow.

![400 error Zapier authentication](https://cdn.zapier.com/storage/photos/91579ed613b77fb803ff52fb900b093b.png)

### Error Parsing Response

The _Error Parsing Response_ error is commonly returned when:

- API returns non-standard and especially non-JSON output
- Test API endpoint URL is incorrect

![Error Parsing Response in Zapier Basic Auth](https://cdn.zappy.app/7dc661d47076c1114b2581289646de48.png)

Verify the test API URL is entered correctly. If a normal webpage URL is entered in the test field, the site will return its raw HTML content to Zapier and that will likely result in this error. If you do change the URL, click _Save & Continue_, then test your connection again.

If your API call is correct and returning data in a format [Zapier does not expect](https://platform.zapier.com/build/faq#what-response-type-does-zapier-expect), you will need to switch to [Code mode](https://platform.zapier.com/build/code-mode) and add custom parsing for your API response. Under the _Test_ API call in the top of your app's Authentication settings, click _Switch to Code Mode_, then add custom JavaScript code to parse your API response.

### Authentication Failed Task Timed Out

The _Authentication Failed_ error, often including _Task Timed Out_, is commonly returned when:

- The API request does not return a response to Zapier within 30 seconds
- The API request is formatted incorrectly and the server does not respond with an error code

Check your Zapier test logs to see if it shows which URL timed out, then verify you've entered the correct URL in all of your integration authentication settings. Finally, check the API provider to see if their site or API are temporarily down.

If the request seems to be successful but the task still times out, your API call may be taking too long to respond, or could be returning more data than Zapier can parse within the time limit. Use a testing API call in authentication that returns as little data as possible, such as a `/me` call that returns the connected user's account data. Or, if your API supports pagination and/or filtering, enable that and have the API return only the most recent result. Then test again to ensure the call works successfully.

![Zapier Authentication Timed Out](https://cdn.zapier.com/storage/photos/2bc7541d4859785d23a64dc5caceec22.png)

### 500

The HTTP 500 error is the default, unformatted error that may be returned without specifying what went wrong or why. If you encounter this error, check the API endpoint URL that gave the error, and verify your API call is configured correctly with the expected URL params, HTTP headers, and Request Body.

![500 error when adding account in Zapier](https://cdn.zapier.com/storage/photos/22eb6cbc2c965dc196a3646511deeb7d.png)
