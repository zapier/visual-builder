---
title: Handle Authentication
order: 5
layout: post
redirect_from: /quick-start/
---

## Build Your Integration

### Handle Authentication

![Zapier Example OAuth Authentication](https://cdn.zapier.com/storage/photos/6234e3eb4aa23975b9f89139ebffe3ac.gif)

_Many Zapier integrations use OAuth2 authentication to connect user accounts, including Zapier's built-in GitHub integration_

The first thing to set up is authentication. Your integration defines how Zapier’s platform authenticates with the API and what data needs to be collected from users to allow access to their accounts. Zapier supports most popular authentication schemes, including basic auth with username and password, API key auth, digest, session, and OAuth v2.

Whenever someone uses your integration in a Zap, they'll first select your app, then will connect their account. That's where the authentication flow comes in. Zapier shows a popup window where users login and select their account with OAuth2, or where they can enter account details with basic auth.

### 1. Select Your Authentication Scheme

![Zapier Visual Builder select auth](https://cdn.zapier.com/storage/photos/a2855758dabdb228966b1bad7238814a.png)

_Zapier supports a wide range of authentication schemes—select the best one for your app_

We'll use basic auth in this sample GitHub integration to keep things simple. Click the _Authenticstion_ tab in Zapier visual builder, then select _Basic Auth_ from the menu. Zapier will create a form with input fields to collect the username and password automatically.

> _If you want to use [OAuth](https://zapier.github.io/visual-builder/docs/oauth){:target="_blank"} or another authentication scheme, check our [auth docs](https://zapier.github.io/visual-builder/docs/auth) for more details and use them instead of the steps below._

### 2. Add Authentication Details

![Zapier Visual Builder Basic Auth](https://cdn.zapier.com/storage/photos/f245b3d5504000186a035e040aab02d5.png)

_Zapier automatically creates a form for Basic Auth—all you need to add is a test API call to ensure those credentials work_

With Basic authentication, you only specify an API endpoint to test the user’s credentials. To do that, add GitHub’s user API call `https://api.github.com/user ` to the _Test_ field.

![Example connection label](https://cdn.zapier.com/storage/photos/f2c3d557023ce2a65b41122da34c1fdd.png)

_Add a connection label, and users' accounts in Zapier will be personalized to easily distinguish between multiple accounts._

You can also add details to the account. Whenever a new account is authenticated with Zapier, Zapier adds a _Connection Label_ so users can identify accounts and add multiple accounts if desired. Customize this label with output fields from the API call (learn more in our [connection label docs](https://zapier.github.io/visual-builder/docs/auth#how-to-add-a-connection-label-to-authenticated-accounts)).

For GitHub, add {% raw %}`{{bundle.authData.username}}`{% endraw %} to the _Connection Label_ to include users’ GitHub username along with the app name that Zapier automatically includes.

### 3. Test The Authentication

![Basic Auth example](https://cdn.zapier.com/storage/photos/97847990532583a4885b5479817e3a32.gif)

_Basic Auth in Zapier shows a form where users enter their username and password—unlike OAuth2 above where Zapier sends users to your site to authenticate_

Then test the authentication. Click _Connect an Account_, and enter your GitHub username and password or personal access token. You can now use this GitHub account to test triggers and actions as you build them into your integration. 

When others use your integration, they'll see a similar login flow to connect their GitHub account to Zapier—only there, the popup window will open from the Zap editor.