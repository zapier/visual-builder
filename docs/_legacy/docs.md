---
title: Legacy Web Builder Docs
order: 3
layout: post-toc
redirect_from: /legacy/
---

# Legacy Web Builder Docs

Zapier's Web Builder was the original way to build Zapier integrations since it was launched in 2012 and updated in [2014](https://zapier.com/blog/connect-any-service-zapier-new-and-improved-developer-platform). Since then, we've deeply updated our platform, and the latest Zapier Platform v3 lets you build integrations with all of Zapier's features in an online visual builder or with our CLI.

If you have an existing integration that was built with Zapier's older Web Builder, we're slowly migrating these integrations to the [Zapier Platform UI](https://platform.zapier.com/quickstart/introduction).

Here is our full archived documentation for the original Zapier Web Builder to help maintain existing integrations.

> **Note**: If you're building a new Zapier integration, use the new [Zapier Platform](https://platform.zapier.com/quickstart/introduction) instead.

### App Integrations

A Developer App (App for short) is an implementation of your app's API—what we now call a Zapier integration. It's the thing you build to make Zapier support your app.

A Zapier Integration is composed of four main parts:

- [Authentication](#authentication) (usually) which lets us know what credentials we need to ask users for and where to include them in the requests we make to your API.
- [Triggers](#triggers), which read data **from** your API.
- [Actions](#actions), which send data **to** your API.
- [Searches](#searches), which find specific records **in** your API.
- Code written in [scripting](#scripting) that lets you handle any mismatches between what Zapier needs and what your API generates.

---

## Authentication

Your API probably has some kind of authentication needs in order for us to talk to it on behalf of a user. Zapier supports the following authentication schemes: Basic Auth, Digest Auth, API Keys, Session-based Auth or OAuth V2.

### Basic Auth

Classic Basic Auth, as [documented on MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Authentication#Basic_authentication_scheme).

Users provide Zapier their username and password to authenticate with your API.

This is also the scheme you want to use if your API relies on Basic Auth, but with atypical values for the username and password. For instance, an API that uses an API Key as the username and a dummy value as the password would still want to select Basic Auth for their App. We'll use this as the example.

1. Customize the Authentication Fields:

   ![](https://cdn.zapier.com/storage/photos/7453d104c8a4586c30b21f91cbfd0bd6.png)

2. [Map](#authentication-mappings/#basic-auth) the fields to a `username` and `password` property:

   ![](https://cdn.zapier.com/storage/photos/96d976f520638bb82a83ed15690bce87.png)

3. The user will be asked to provide values:

   ![](https://cdn.zapier.com/storage/photos/d7d8a3cb2332a2fccaebff4f4bf7f5b6.png)

4. We will prepare all requests to the API with an header like:

   ```html
   Authorization: Basic WkFQSUVSIExPVkVTIFlPVTpYT1hP
   ```

See also [Authentication Mappings](#authentication-mappings/#basic-auth) and [Basic Auth via CLI](https://zapier.github.io/zapier-platform-cli/#basic).

### Digest Auth

Digest Auth, as [documented by RFC7616](https://tools.ietf.org/html/rfc7616#section-3.1).

Users will provide Zapier their username and password, and we will handle all the [nonce](https://en.wikipedia.org/wiki/Cryptographic_nonce) and quality of protection details automatically.

The setup and user experience is identical to _Basic Auth_.

See also: [Digest Auth via CLI](https://zapier.github.io/zapier-platform-cli/#digest)

### API Keys

Typically, you'll provide your users with an API Key inside your app somewhere. Many times these are provided on the user's settings or accounts page. These keys can be given to Zapier by the user so that we may make authenticated requests to access that user's information on their behalf.

1. Select either _API Key (Headers)_ or _API Key (Query String)_, depending on how the API expects to receive the keys.

2. Customize the Authentication Fields:

   ![](https://cdn.zapier.com/storage/photos/7453d104c8a4586c30b21f91cbfd0bd6.png)

3. [Map](#authentication-mappings/#api-key-query-string) the fields to the headers or query string parameters the API expects:

   ![](https://cdn.zapier.com/storage/photos/e872817ff0986e3948802ee9c62514f4.png)

4. The user will be asked to provide values:

   ![](https://cdn.zapier.com/storage/photos/d7d8a3cb2332a2fccaebff4f4bf7f5b6.png)

5. We will prepare all requests to the API with an header like:

   ```html
   X-Secret: WkFQSUVSIExPVkVTIFlPVTpYT1hP
   ```

See also [Authentication Mappings](#authentication-mappings/#api-key-query-string) and [API Key auth via CLI](https://zapier.github.io/zapier-platform-cli/#custom).

### Session-based Auth

This type can be used for almost any authentication where user provided credentials get exchanged for some kind of session token.

1. Customize the Authentication Fields:

   ![](https://cdn.zapier.com/storage/photos/81c1870ffb905d182f4b366b5b5c21fc.png)

2. Write a [`get_session_info()`](#scripting/#get_session_info) method that handles the exchange of the authentication fields for the session token and returns an object like:

   ```javascript
   {
     user_token: "WkFQSUVSIExPVkVTIFlPVTpYT1hP";
   }
   ```

3. [Map](#authentication-mappings/#session-auth) the fields and/or the properties returned by [`get_session_info()`](#scripting/#get_session_info) to parameters the API expects, and select if it expects them as headers or query string parameters:

   ![](https://cdn.zapier.com/storage/photos/90e28d2ac63d469c879c5e1a63621d6a.png)

4. The user will be asked to provide values:

   ![](https://cdn.zapier.com/storage/photos/265d27fa64e33b5e75af87a7d90a3893.png)

5. We will call [`get_session_info()`](#scripting/#get_session_info) the first time or when we receive a 401 HTTP status or [`InvalidSessionException`](#scripting/#updating-session-credentials) is thrown.

6. We will prepare all requests to the API with an header like:

   ```html
   X-Token: WkFQSUVSIExPVkVTIFlPVTpYT1hP
   ```

See also [`get_session_info()`](#scripting/#get_session_info), [Authentication Mapping](#authentication-mappings/#session-auth) and [Session auth via CLI](https://zapier.github.io/zapier-platform-cli/#session).

### OAuth v1

The flow we respect matches [Twitter's](https://dev.twitter.com/oauth/3-legged) and [Trello's](https://trello.com/docs/gettingstarted/oauth.html) implementation of the 3-legged oauth flow.

Note that OAuth v1 is not officially supported on Zapier; we highly recommend using OAuth 2 if possible!

That said, because OAuth v1 has been a popular authentication mechanism, we have a sample implementation if you want to try it, respecting OAuth v1 "revision a".

### Initial Setup:

First, you'll need to select _OAuth v1_ as your Authentication Type. In most cases you can continue with the default Authentication Fields. The final step is to configure OAuth V1:

![OAuth parameters](https://cdn.zapier.com/storage/photos/4620d15bd155dfca914ac41899284519.png)

**Capture extra data from token response**

If your app returns extra data through the token response (user id for example) you can grab those extra parameters using the **Extra Requested Fields** option.

### How we authenticate with your OAuth service

We attempt a 3 legged OAuth 1 process that has 3 high level steps:

1. Obtain temporary oauth_token and oauth_secret from your app
2. Get user to authorize Zapier access to your app
3. Exchange the temporary oauth_token for an authorized oauth_token

### 1. Requesting Temporary Credentials From Your App:

When a user goes to add a new account for your app, we make a request behind-the-scenes to ask your app for a request token and secret. Your app should respond back with a valid `oauth_token` and `oauth_token_secret`. Additionally, our request contains an `oauth_callback` URL that your app will use in a later step.

The signed POST request to your application's `request_token_url` will look like this:

```
POST https://example.com/api/1.0/oauth/request_token
Authorization: OAuth
oauth_nonce="ZAPIER-GENERATED-NONCE",
oauth_callback="ZAPIER-OAUTH-CALLBACK",
oauth_signature_method="HMAC-SHA1",
oauth_timestamp="ZAPIER-GENERATED-TIMESTAMP",
oauth_consumer_key="<Your consumer key>",
oauth_signature="ZAPIER-GENERATED-SIGNATURE",
oauth_version="1.0"

```

Your app should validate the request and return with the temporary response token, like so:

```
oauth_token_secret=TEMP-OAUTH-TOKEN-SECRET&oauth_token=TEMP-OAUTH-TOKEN&oauth_callback_confirmed=true

```

### 2. Redirecting the User to Your App:

With token in hand, we redirect the user to the `authorization_url` you provided, so that they can grant access to Zapier.

![User grants access](https://cdn.zapier.com/storage/photos/ad57fd3749261016bd595066837cb392.png)

```
302 https://example.com/api/v1/oauth/authenticate?oauth_token=<oauth_token>
```

### 3. Redirecting the User Back to Zapier:

After the user clicks allow, your app redirects the user to `oauth_callback` (from Step 1), along with an `oauth_verifier` parameter in the query string.

`302 <oauth_callback>?oauth_verifier=<oauth_verifier>`

### 4. Exchanging Temporary Credentials for Token Credentials:

We use that `oauth_verifier` to make a POST to the `access_token_url` you provided.

```bash
POST https://example.com/api/1.0/oauth/access_token \
    -H Accept: application/json \
    -d 'consumer_key=<consumer_key>&
        consumer_secret=<consumer_secret>&
        oauth_verifier=<oauth_verifier>&
        oauth_token=<oauth_token>&
        oauth_token=<oauth_token_secret>
```

Your service should then provide an access_token and access_token_secret, along with any extra parameters that you may have included in the optional _Capture extra data from token response_ step.

While we ask for a JSON response, the response can be JSON, XML or query string encoded. For example, any of the below are valid responses:

With `Content-Type: application/json`:

```javascript
{
  "oauth_token": "1234567890abcdef",
  "oauth_token_secret": "1234567890abcdef",
}
```

With `Content-Type: application/xml`:

```xml
<AnyRootElem>
  <oauth_token>1234567890abcdef</oauth_token>
  <oauth_token_secret>1234567890abcdef</oauth_token_secret>
</AnyRootElem>
```

With `Content-Type: text/plain`:

`oauth_token=1234567890abcdef&oauth_token_secret=1234567890abcdef`

### 5. Using the Token Credentials

We sign all requests using your secret and the new `oauth_token` and `oauth_token_secret`. We're talking standard HMAC-SHA1, RSA is not supported. However, you can use [scripting](#scripting) to modify request parameters (including headers) as you see fit.

For example, if a POST request to your API expects `Content-Type:application/x-www-url-form-encoded` instead of the standard `application/x-www-form-urlencoded` then you can use a custom script to modify the request that we make. In an app with a trigger `create_ticket` the Scripting API would look like so:

![Edit app script](https://cdn.zapier.com/storage/photos/acab90e3f065deeac8e08db4c48b4b30.png)

```
var Zap = {
    create_ticket_pre_write: function(bundle) {
        bundle.request.headers['Content-Type'] = 'application/x-www-url-form-encoded';
        return bundle.request;
    }
}
```

### Example:

We highly recommend looking at each of [Bitbucket's](https://confluence.atlassian.com/display/BITBUCKET/oauth+Endpoint), [Twitter's](https://dev.twitter.com/oauth/3-legged) and [Trello's](https://trello.com/docs/gettingstarted/oauth.html) authentication documentation for some great examples of how OAuth 1a can be implemented. Our system is designed to match their industry standard implementation pattern. Additionally, [oauth1a spec](http://oauth.net/core/1.0a/#anchor9) and [oauth bible](http://oauthbible.com/#oauth-10a-three-legged) can be extremely useful in understanding the 3 legged oauth flow.

### OAuth v2

While the official OAuth V2 spec offers lots of options, the flow we respect matches [GitHub's](http://developer.github.com/v3/oauth) and [Facebook's](https://developers.facebook.com/docs/authentication/server-side) implementation of the `authorization_code` grant type flow. We do not support other forms of OAuth at this time.

> **A complete OAuth V2 example is available on our [Formstack example](#rest-hooks-example) page.** Check that out for more detail in a real world example!

### Initial Setup

First, you'll need to select `OAuth V2` or `OAuth V2 (w/refresh)` as your auth type, and then provide the following parameters:

![OAuth parameters](https://cdn.zapier.com/storage/photos/cef0cb3af6bf1c793a7d724e97e75222.png)

We'll automatically create the required `access_token` and `refresh_token` (optional) auth fields for you. They look something like this in the developer interface - **the access_token field is required at minimum**:

![](https://cdn.zapier.com/storage/photos/008ec6005cbaed25a12873da53866691.png)

> **Hint:** Does your app need to change the URL based on the user's subdomain or domain? Simply add another authentication field (right alongside `access_token` from the above screenshot) that has the key like `subdomain` and then use it like {% raw %}https://{% templatetag openvariable %}subdomain{% templatetag closevariable %}.yourwebsite.com/api/token{% endraw %} in all your URLs.

### 1. Redirecting the User to Your App

We'll redirect the user to an `authorize_url` (provided by you), along with a query string which contains a `redirect_uri` (provided by us), `scope` (optional, provided by you) and `client_id` (provided by you).

`302 <authorize_url>?client_id=<client_id>&scope=<scope>&redirect_uri=https://zapier.com/app/login?next=/dashboard/auth/oauth/return/AppIDAPI/`

### 2. Redirecting the User Back to Zapier

After the user clicks allow, you should redirect the user to the `redirect_uri` along with a `code` parameter in the query string.

> **Note:** _Don't_ hardcode the `redirect_uri` on your side, as it will change as you deploy new versions of your app. If your app goes public, we'll assign you a permanent ID, but some users may be using older versions even after that point.

`302 <redirect_uri>?code=<code>`

We use that `code` to make a POST to the `access_token_url` (provided by you) along with the `code`, matching `redirect_uri` (provided by us), `client_id` (provided by you), and `client_secret` (provided by you) as a form encoded request.

```bash
POST <access_token_url>?client_id=<client_id>&client_secret=<client_secret>&code=<code>&grant_type=authorization_code&redirect_uri=https://zapier.com/app/login?next=/dashboard/auth/oauth/return/AppIDAPI/ \
    -H Accept: application/json
```

> Zapier will try two ways to get the token: POST with data in querystring, if that returns a `4xx`, we will retry a POST with the data in the form-encoded body. You can always override this behavior with the Scripting though!

While we ask for a JSON response, the response can be JSON, XML or query string encoded as where the value you return is `access_token`. For example, any of the below are valid responses:

With `Content-Type: application/json`:

```javascript
{
  "access_token": "1234567890abcdef",
  "refresh_token": "1234567890abcdef" // optional
}
```

With `Content-Type: application/xml`:

```xml
<AnyRootElem>
  <access_token>1234567890abcdef</access_token>
  <refresh_token>1234567890abcdef</refresh_token> <!-- optional -->
</AnyRootElem>
```

With `Content-Type: text/plain`:

`access_token=1234567890abcdef&refresh_token=1234567890abcdef`

> We automatically pull and store `access_token` and `refresh_token` from the JSON, XML, or query string data, but if you want to pull and store more fields, you can set them up in your auth setup under _Extra Requested Fields_:

![](https://cdn.zapier.com/storage/photos/8ac33bf6ba69b36f46733af4a3fe4792.png)

### 3. Authorizing Requests to Your App

By default, we append the `access_token` to the querystring for all requests, as well as in an Authorization header, however, you can use [scripting](#scripting) to modify request parameters as you see fit (IE: place the `access_token` in a special header). This is called the `bearer` token type.

An example of the default with `access_token_placement` set to `header`:

```bash
GET https://api.example.com/v2/tickets.json \
    -H Authorization: Bearer 1234567890abcdef
```

And now with `access_token_placement` set to `querystring`:

`GET https://api.example.com/v2/tickets.json?access_token=1234567890abcdef`

### 4. Refreshing Tokens (optional)

Optionally, if your app supports refresh tokens, we natively support that.

You'll need to select `OAuth V2 (w/refresh)` and provide us the `refresh_token_url` in addition to the previous requirements. When we encounter a `401` status code, we'll attempt to refresh like so:

```bash
POST <refresh_token_url> \
    -H Accept: application/json \
    -d 'client_id=<client_id>&
        client_secret=<client_secret>&
        grant_type=refresh_token&
        refresh_token=<refresh_token>'
```

> Zapier will try two ways to get the token: POST with data in the form-encoded body, if that returns a `4xx`, we will retry a POST with the data in querystring. Note that this is the exact reverse of how we try to get the initial access token. You can always override this behavior with the Scripting though!

We will only attempt to refresh an access token when we encounter a `401` status code from your API.

If your API does not signal expired tokens with a `401`, use [scripting](#scripting) to manually set the status code header to `401` upon conditions of your choosing. Or, you can raise a `RefreshTokenException` in your `post_XXXX` function call to kick off a new refresh.

The resulting `access_token` will be updated in our system and the previous, failed call will be attempted once more.

We prefer and advocate one of two patterns around expiring refresh tokens:

1.  Never expire refresh tokens except on password changes or user revocation.
2.  In the last 10% window of a refresh token's life (IE: last 9 days of a 90 day lifetime), give a brand new refresh_token along with the normal access_token refresh.

We fully support each pattern. While option 1 is definitely more common, option 2 works very nicely and has the effect of eventually cleaning up unused oauth tokens.

If you cannot adhere to one of the above patterns and you app requires manual refresh of tokens on a regular basis, you should check for this condition and notify users via scripting. With `throw new ExpiredAuthException('Your reason.');`, the current call is interrupted, the zap is turned off (to prevent more calls with expired auth), and a predefined email is sent out informing the user to refresh the credentials.

### Some Examples

We highly recommend looking at each of [GitHub's](http://developer.github.com/v3/oauth), [Facebook's](https://developers.facebook.com/docs/authentication/server-side) and [Podio's](https://developers.podio.com/authentication/server_side) (with refresh tokens) authentication documentation for some great examples of how OAuth V2 can be implemented. Our system is designed to match their industry standard implementation pattern.

**A complete OAuth V2 example is available on our [Formstack example](#rest-hooks-example) page.** Check that out for more detail in a real world example!

### Authentication Field Options

Authentication fields are simply what you need from the user to get started authenticating their API calls. For example, when a user tries to authenticate your service:

![auth fields for user](https://cdn.zapier.com/storage/photos/e092bbbc68bb48b87bc5b90e0fc0f138.png)

You can see what it will be powered by a developer set up like:

![auth fields in developer](https://cdn.zapier.com/storage/photos/b4f0b14bb0dfada46a245a7da8135240.png)

Additionally, these user-provided variables will be passed in with the `bundle` for usage in [scripting](#scripting). For example, the above screenshots would translate to:

```javascript
{
  "account_name": "myaccount",
  "api_key": "123456789"
}
```

You can use [Auth Mappings](#authentication-mappings) to put your Auth Fields to use in Basic Auth, Digest Auth, HTTP headers and query strings.

Let's look at each of the options you define for a single Auth Field.

### Key

This is somewhat arbitrary but you should pick a good, short key name because you'll need to include it elsewhere in the developer interface as {% raw %}{% templatetag openvariable %}key{% templatetag closevariable %}{% endraw %} using the [variable syntax](#variable-syntax). Needs to be at least two characters long, start with an alpha, and only contain `a-z`, `A-Z`, `0-9` or `_`.

Example: <br/> (you may not need all of these)

- `api_key` an API Key which you give to your users somewhere inside your service. Allows Zapier to authenticate on their behalf
- `account_name` an account name which you use to build the API Request URL (perhaps as a subdomain: https://&#123;&#123;account_name&#125;&#125;.example.com/api/v1)

### Label

This will show up just above the text input field as a human-readable name. You don't need to be super descriptive here; you can provide more details and information about this field in the Help Text field.

Example: <br/> API Key, Account Name

![label help default](https://cdn.zapier.com/storage/photos/96522edc71e94085537c1fa70480adb8.png)

### Required

Pretty easy concept; most all auth fields should be required. You really shouldn't ask for non-essential information as an auth field.

### Help Text

Smaller text which appears under the Label of the field. You can type longer directions here. A common pattern for Auth Field Help Text is to tell the user where in your interface they can find their API Key.

Example: <br/> The API Key for your account, you can find this by going to your Basecamp Profile page, clicking settings, then API Keys.

### Default

If you specify a default value, the actual field will be pre-filled with this value when the user goes to add a new authentication for your service. If the user clears out a required auth field which had a default set, they will receive an error. Optional fields that are missing a value will use the default every time.

Most auth fields will not have a default.

Examples: <br/> `choice_b` (if you use the choices feature detailed below)
<br/> `1` (if you use the `raw|label` syntax detailed below)

If you are using the `raw|label` syntax and provide a default value, you should also provide a placeholder that corresponds to the raw value's label. Otherwise, your users will see the raw value in the dropdown.

For example, if you use `1` as your raw label, you should provide `Option 1` as a placeholder.

### Static Dropdowns

You can create a dropdown-style select box by giving us a comma-separated list of choices. This works well in conjunction with the default value option above.

Example: <br/> `choice_a,choice_b,choice_c` or `Yesterday, Today, Tomorrow`

![simple static dropdown](https://cdn.zapier.com/storage/photos/7641c6b42a5034432f63274226e84414.png)

If you would like to provide a label for the raw value of each choice, you can also use the raw|label,raw|label syntax instead.

Example: <br/>`1|Option 1,2|Option 2`

![simple static dropdown as key-value pairs](https://cdn.zapier.com/storage/photos/524ad1774802cc81d95cb2e3f23972d6.png)

### Subdomain Format

If you need the user to supply an account name (or similar) which gets translated into a subdomain (or similar) URL format, we recommend you take advantage of this feature. It helps guide the user with what to type in.

Example: <br/> {% raw %}https://,{% templatetag openvariable %}input{% templatetag closevariable %},.yourdomain.com/{% endraw %} will create:

![subdomain format](https://cdn.zapier.com/storage/photos/8cb23a041bd6bf522d14c6ca3829e70c.png)

> Note: don't forget the commas!

### Authentication Mappings

Auth mappings tell us how to interpret the credentials or tokens your user provides, as usable Basic Auth, Digest Auth, HTTP headers and query strings. Let's use an example where there are two auth fields available to us: `account_name` and `api_key`.

### Basic Auth

Your app might use `api_key` as the username and password is ignored:

{% raw %}```javascript
{
"username": "{% templatetag openvariable %}api_key{% templatetag closevariable %}",
"password": "x"
}

````{% endraw %}

Or maybe, where `account_name` is the username and `api_key` is the password:

{% raw %}
```javascript
{
  "username": "{% templatetag openvariable %}account_name{% templatetag closevariable %}",
  "password": "{% templatetag openvariable %}api_key{% templatetag closevariable %}"
}
```{%  %}

In any case, the *Auth Mapping* should provide a `username` and `password` field, which we will use to generate an header like:

`Authorization: Basic WkFQSUVSIExPVkVTIFlPVTpYT1hP`

This will be added to all prepared requests to your server.

### Digest Auth

Your app might have `account_name` as the username and `api_key` as the password:

{% raw %}
```javascript
{
  "username": "{% templatetag openvariable %}account_name{% templatetag closevariable %}",
  "password": "{% templatetag openvariable %}api_key{% templatetag closevariable %}"
}
```{% endraw %}

This will produce an header similar to *Digest Auth*, but using a server provided nonce. We handle the computation of the response, so you don't have to think about realms, nonces, or qop's.

### API Key (Query String)

Your app might expect the API key as `secret` parameter in the query string:

{% raw %}
```javascript
{
  "secret": "{% templatetag openvariable %}api_key{% templatetag closevariable %}"
}
```{% endraw %}

Which will append `?secret=0123456789` to the end of all URLs.

### API Key (Headers)

Say your app expects two headers called `X-Account-Name` and `X-API-Key`:

{% raw %}
```javascript
{
  "X-Account-Name": "{% templatetag openvariable %}account_name{% templatetag closevariable %}",
  "X-API-Key": "{% templatetag openvariable %}api_key{% templatetag closevariable %}"
}
```{% endraw %}

This will add headers like:

```html
X-Account-Name: myfancyaccount
X-API-Key: 0123456789
````

### Session Auth

With Session Auth, you can map the Authentication Fields as well as what is returned by your [`get_session_info()`](#scripting/#get_session_info) scripting method. In most cases, this method will return a token and this is the only value your API needs for further requests.

Let's say our method makes a request which sends our `account_name` and `api_key` and receives the following object:

```javascript
{
  token: "WkFQSUVSIExPVkVTIFlPVTpYT1hP",
  name: "John Doe"
}
```

If your app expects to receive the token in an header named `X-Token` the auth mapping could be:

{% raw %}

````javascript
{
  "X-Token": "{% templatetag openvariable %}token{% templatetag closevariable %}"
}
```{% endraw %}

And we would set *Auth Placement* to *Header*:

![](https://cdn.zapier.com/storage/photos/a4ad34fec2ce7232c77e528b79f398b0.png)

This will add a header like:

```html
X-Token: WkFQSUVSIExPVkVTIFlPVTpYT1hP
````

If your app expects the token as Query String parameter, select _Querystring_ for _Auth Placement_ instead.

---

## Triggers

**Triggers** answer the question: _What events can my users listen for with Zapier?_ They are things like:

- New Contact _(EG: Highrise or Salesforce)_
- New Email _(EG: Gmail or IMAP)_
- New Issue _(EG: GitHub or Pivotal Tracker)_

You can think of a Trigger as a GET or read. It involves Zapier receiving data from your app.

For example, say your app has a "New Ticket Opened" trigger. We will watch for new tickets in a user's account. The data we trigger off of might look like this:

```javascript
[
  {
    id: 123456,
    owner_id: 654,
    date_created: "Mon, 25 Jun 2012 16:41:54 -0400",
    description: "Add our app to Zapier"
  }
];
```

_Note: The data in the response must be an array, even for a single data point._

These key/values are available for users to map into the [action](#actions) as they see fit.

What a user sees:

![](https://cdn.zapier.com/storage/photos/f52aa243c8d08c98cfd332e04e169820.png)

What a developer sees:

![](https://cdn.zapier.com/storage/photos/0ca98ee10ff4ddb3c3ca06286c7be07c.png)

See also: [Triggers in the CLI](https://zapier.github.io/zapier-platform-cli/#triggerssearchescreates)

There are four ways Zapier can obtain data from your API.

- [Polling](#polling) - repeatedly hit a REST endpoint looking for new data.
- [Static Webhooks](#static-webhooks) - gives the user a URL to enter into your app. Hooks carry the full object.
- [REST Hooks](#rest-hooks) work similar to static webhooks, but our system handles the subscriptions through your REST API.
- [Notification REST Hooks](#notification-rest-hooks) are "lightweight" REST Hooks as they only contain a callback URL to retrieve the object.

### Polling

Polling is the process of repeatedly hitting the same endpoint looking for new data. We don't like doing this (its wasteful), vendors don't like us doing it (again, its wasteful) and users dislike it (they have to wait a maximum interval to trigger on new data). However, it is the one method that is ubiquitous, so we support it.

It is also closely tied into how we handle [deduplication](#deduplication).

That said, we support [REST Hooks](#rest-hooks), so if you like to make your users and servers happy, implement hooks!

> If you don't use classic `GET` with your API to retrieve lists of objects - you can use our [scripting API to customize the polling request with a different method and body](#scripting/#trigger-pre-poll-examples).

### Static Webhooks

Static webhooks are a very simple version of webhooks wherein the user of your service will have to take action to enable a webhook. Usually, this is done copying a url that Zapier provides during the Zap setup process (like `https://zapier.com/hooks/catch/123/n/456789/`). If you would like your app to go public, you should use [REST hooks](#rest-hooks).

While Static webhooks are very useful for rapid prototyping, we don't accept apps for inclusion in the Zapbook that are solely Static webhooks. Users can use our built in Webhook app to do the same things that a purely Static webhook app can do. You should look at [REST Hooks](#rest-hooks) as the next step after you've proved the concept privately with Static webhooks.

_To get a taste of how static webhooks work, check out our built-in [generic webhook service](https://zapier.com/apps/webhook/integrations)._

### Setup the Webhooks

To get started simply create a new trigger on your app, choosing static webhook as the type. You can follow the [Hubspot example](#static-webhooks-example-app) to see a detailed walk through of how to do this.

Once defined in your app, static webhook triggers will appear like this to users when they create a Zap:

![static webhook user display](https://cdn.zapier.com/storage/photos/2a06f4e0432eb9bfc77bb263c740a2a3.png)

### Using the Webhooks

For as long as the Zap exists, requests made to that URL will be associated with your app and the user. That means requests made during the setup process (while the Zap is paused) will still get stored, making it easier for users to debug. However, requests will **not** trigger any actions until the Zap is turned on.

Also, it is important to know that by default, we do our best to inspect and pull out all relevant information in a request. If you use [scripting](scripting) to further refine the hook data, you'll see it passed in as `bundle.cleaned_request`. For example, a request might have a `cleaned_request` similar to:

```bash
POST https://zapier.com//hooks/catch/123/n/456789/?hello=world \
    -H Content-Type: application/x-www-form-urlencoded \
    -d 'some_json=%7B%22foo%22%3A%22hooray!%22%7D&some_xml=%3Cbar%3Eyay!%3C%2Fbar%3E'
```

```javascript
{
  "queryset": {
    "hello": "world",
  },
  "some_json": {
    "foo": "hooray!"
  },
  "some_xml": {
    "bar": "yay!"
  }
}
```

> _Note:_ We only support simple query strings at the moment. `&foo[hello]=world` will be parsed to the JavaScript object `{ "foo[hello]": "world" }` and not `{ "foo": { "hello": "world" } }`.

Of course, more simplistic examples like straight JSON or XML are handled as you'd expect.

### Catching Single Objects vs. Lists

Some webhooks send single objects, while some are batched as lists of objects for efficiency reasons. Though Zapier supports both, we highly recommend using [scripting](#scripting) if you are dealing with batched lists. We do our best via `cleaned_request` to interpret lists where possible, but if your list is hidden in a subkey, we won't capture it properly.

For example, a generically supported list:

```bash
POST https://zapier.com//hooks/catch/123/n/456789/?hello=world \
    -H Content-Type: application/json \
    -d '[{"name":"bryan","age":27},{"name":"mike","age":23}]'
```

Would result in two triggers...

```javascript
{
  "name": "bryan",
  "age": 27
}
```

...and...

```javascript
{
  "name": "mike",
  "age": 23
}
```

Notice that the query string `hello=world` is ignored? That is because we assumed the data list was more important and we didn't want to maim the data contained therein.

Check out an example where we would ignore a subkeyed list:

```bash
POST https://zapier.com//hooks/catch/123/n/456789/?hello=world \
    -H Content-Type: application/json \
    -d '{"data":[{"name":"bryan","age":27},{"name":"mike","age":23}]}'
```

Because the list isn't at the root, by default, we'll interpret this as a single object. That means we'll only trigger once for this object:

```javascript
{
  "queryset": {
    "hello": "world",
  },
  "some_json": [
    {
      "name": "bryan",
      "age": 27
    },
    {
      "name": "mike",
      "age": 23
    }
  ]
}
```

This is where you'd need to break out [scripting](#scripting) to do some refinement. Check out the examples we provide in the [scripting examples](#scripting/#catching-webhooks-example).

### Testing Webhooks

Normally, a user will just log back into your service and force an event by performing the action that causes a webhook to be emitted. This can be a little annoying to the user during setup, so alternatively you can send a `X-Hook-Test: true` and we will _never_ trigger an action for real, we'll just cache the payload for our UI. This means when the user enables webhooks in your app, just send some sample data across.

### REST Hooks

Below is our simple standard to stop the [Polling Madness](#polling)&#8482;. This is a suggested pattern for you to implement. It was chosen because there are many examples of REST APIs providing resources around GETing, POSTing and DELETEing webhooks just like any other REST resource.

The big benefit to REST Hooks is consumers wouldn't need to poll for changes, but could instead wait for hooks to deliver the payload. Additionally, producers can provide real-time updates with fewer devoted resources (compared to polling).

The gist is: we POST a subscription to e.g. `/api/hooks` requesting to receive hooks at some target URL. Every time the event happens, ping us at the target URL with the payload.

After we're done, we can cleanup with a DELETE (.e.g. `/api/hooks/:id`).

_Though we highly recommend this native pattern, you can override all the methods below with [scripting](#scripting). This means you can bend our pattern to match an existing pattern of your own._

#### Your Checklist

- enumerate the events you'd like to make available as triggers
- create a _subscribe_ REST endpoint for hooks. For example: `POST /api/hooks`
- when each event happens, loop over and notify each active subscription (or batch events of same type). Note that each user may have multiple active subscriptions to the same event.
- respect `410` responses on payload delivery and remove subscriptions
- create a _unsubscribe_ REST endpoint for hooks. For example: `DELETE /api/hooks/:id`
- add a polling URL for your REST Hook trigger for the best user experience

You need to set the _subscribe_ and _unsubscribe_ REST endpoints under _Manage Trigger Settings_:

![Manage Trigger Settings](https://cdn.zapier.com/storage/photos/cac12cadc6fc74713ea8a5c66cd5bfe7.png)

Read on for a step by step through the endpoints involved...

### Step 1: Subscribe <small>_(a call from Zapier to your app)_</small>

```bash
POST <subscribe_endpoint> \
    -H Authenticated: Somehow \
    -H Content-Type: application/json \
    -d '{"target_url": "https://hooks.zapier.com/<unique_path>",
         "event": "user_created"}'
```

> You may notice a duplicate property `subscription_url`. That's legacy terminology. You can safely ignore it and use `target_url` only.

This endpoint reuses whatever auth standard you have across the rest of your API (IE: Basic Auth, API Key, OAuth2, etc...). We'd send along a **unique**, **auto-generated** subscription URL and the event we'd like to subscribe to. These three items would be persisted on your backend (the authenticated user, target_url, and event).

The value for the **subscribe_endpoint** field can be specified within the "Manage Trigger Settings" option in your app's dashboard.

The value for the **event** field can be specified within the Trigger's setup:
![](https://cdn.zapier.com/storage/photos/69f25c6bb6cee40efb96fea32271b36c.png)

If you prefer, you can modify this request to provide additional information (like any trigger fields) by defining a `pre_subscribe` scripting method. See the [documentation](/developer/documentation/v2/scripting/#pre_subscribe) and [examples](/developer/documentation/v2/scripting/#rest-hook-subscription-examples) for more details.

On a successful subscribe, return a `201` status code. You should store data about the hook you just created via the `post_subscribe` scripting method (return an object like `{"id": 1234}`). You'll need this data later to unsubscribe, unless you use the subscription URL as the unique identifier, which is uncommon).

> Generally, subscription URLs should be unique. Return a `409` status code if this criteria isn't met (IE: there is a uniqueness conflict).

> Your service should permit a user to connect multiple webhook URLs to their account

> We support validation of the [receiver's intent to subscribe](http://resthooks.org/docs/security). When you send the `X-Hook-Secret` header, we'll reply to confirm we intended to subscribe.

> Also, we'll provide `X-Hook-Test: true` in the header if the subscription hook is setup during the editor phase of a Zap -- this means the user is just testing the Zap. You might use this to send your own test hook immediately after subscription to help the user test the Zap (please add `X-Hook-Test: true` in your hook as well).

### Step 2: Sending Hooks <small>_(a call from your app to Zapier)_</small>

```bash
POST https://hooks.zapier.com/<unique_path> \
    -H Content-Type: application/json \
    -d <json payload>
```

This hook could provide any amount of data or payload in either JSON or XML (or form-encoded). See [static webhooks](#static-webhooks/#using-the-webhooks) on how we'll do our best to parse the response.

Usually Zapier expects an array of objects. If your API only sends a single object, wrap it in a single element array:

```json
[{ "firstName": "Tom", "lastName": "Smith" }]
```

On a successful hook, we'll return a `200` status code, content is irrelevant.

> If Zapier responds with a `410` status code you should immediately remove the subscription to the failing hook (unsubscribe). Additionally, excessive failures (multiple `4xx` or `5xx` failures) can be handled at your discretion. It is the client's responsibility to resubscribe if needed after failures.

### Step 3: Unsubscribe <small>_(a call from Zapier to your app)_</small>

```bash
DELETE <unsubscribe_endpoint> \
    -H Authenticated: Somehow \
    -H Content-Type: application/json \
    -d <content built/omitted in pre_unsubscribe scripting method>
```

If you've properly stored identification data about the hook (like its unique ID) from the `post_subscribe` scripting method, you should use our`pre_unsubscribe` scripting method to formulate the DELETE call. In that call you have access to your previously stored data under the`bundle.subscribe_data` variable.

[Some example code is provided to make this as easy as possible.](#scripting/#rest-hook-subscription-examples) A heads up: you will need to use that code if you intend to do a DELETE call. You'll be able to access `bundle.subscribe_data` to build the URL in `pre_unsubscribe`. The default behavior is slightly different and listed below.

The value for the **unsubscribe_endpoint** field can be specified within the "Manage Trigger Settings" option in your app's dashboard.

However, the **current default** does not perform a DELETE. For example, if you omit the `pre_unsubscribe` function entirely, we will attempt a default unsubscribe call:

```bash
POST <unsubscribe_endpoint> \
    -H Content-Type: application/json \
    -d '{"target_url": "https://hooks.zapier.com/<unique_path>"}'
```

On a successful unsubscribe, return a `200` status code, content is irrelevant.

It is worth remembering that the subscription URL should effectively be unique (this could be enforced by your app as well) which also allows us to clean up unrecognized hooks (we also recommend not requiring authentication for such an endpoint).

### Optional: Reverse Unsubscribe <small>_(a call from your app to Zapier)_</small>

```bash
DELETE <target_url> \
    -H Content-Type: application/json
```

If you'd like to allow users to manage their subscriptions from inside your app (or maybe you are cleaning up after a user deletes their account or revokes credentials) you can issue a `DELETE` to the unique target URL which was generated when the subscription was created -- this will pause the Zap on Zapier's end.

### Required to Go Public: Set a polling URL

In the trigger setup, there is a field to define a polling URL. This URL will be used when users are setting up a Zap and must test it. Without this defined, the user must always go to your app, create a new data point, and have it send the hook to Zapier. This is not ideal, and in some cases may be particularly undesirable (if for example other Zaps are already set up on that hook, it would trigger them).

Setting up a polling URL fixes this. The polling URL is only used during this testing phase, not during the regular operation of the Zap. If you need to script special behavior, you can do so using the standard `pre_poll` and `post_poll` methods on the trigger key.

**Note**: Please ensure that the data format that returns from the Polling URL is the same as what returns from the REST Hook, so users can correctly map fields.

### Notification REST Hooks

Below is the same pattern as our [REST Hooks](#rest-hooks), but with a twist (and an extra step!). Instead of delivering the payload with each hook, it just delivers a resource URL where the payload resides. This helps us move big requests into a queue with everything else which lets us batch bigger requests. The URL can be one-time use or time sensitive as well.

#### Your Checklist

- enumerate the events you'd like to make available as triggers
- create a _subscribe_ REST endpoint for hooks. For example: `POST /api/hooks`
- when each event happens, loop over and notify each active subscription (or batch events of same type)
- respect `410` responses on payload delivery and remove subscriptions
- create a _unsubscribe_ REST endpoint for hooks. For example: `DELETE /api/hooks/:id`

You need to set the _subscrube_ and _unsubscribe_ REST endpoints under _Manage Trigger Settings_:

![Manage Trigger Settings](https://cdn.zapier.com/storage/photos/cac12cadc6fc74713ea8a5c66cd5bfe7.png)

Read on for a step by step through the endpoints involved...

### Step 1: Subscribe <small>_(a call from Zapier to your app)_</small>

```bash
POST <subscribe_endpoint> \
    -H Authenticated: Somehow \
    -H Content-Type: application/json \
    -d '{"target_url": "https://hooks.zapier.com/<unique_target_url>",
         "event": "user_created"}'
```

This endpoint reuses whatever auth standard you have across the rest of your API (IE: Basic Auth, API Key, OAuth2, etc...). We'd send along a **unique**, **auto-generated** subscription URL and the event we'd like to subscribe to. These three items would be persisted on your backend (the authenticated user, target_url, and event). **A subscription is created when a user turns their Zap on.**

If you prefer, you can modify this request to provide additional information (like further filtering or other metadata) via our `pre_subscribe` scripting method.

On a successful subscribe, return a `201` status code. You should store data about the hook you just created via the `post_subscribe` scripting method (return an object like `{"id": 1234}`). You'll need this data later to unsubscribe, unless you use the subscription URL as the unique identifier, which is uncommon).

> Generally, subscription URLs should be unique. Return a `409` status code if this criteria isn't met (IE: there is a uniqueness conflict).

### Step 2: Sending Hooks <small>_(a call from your app to Zapier)_</small>

```bash
POST https://hooks.zapier.com/<unique_target_url> \
    -H Content-Type: application/json \
    -d {"resource_url": "<resources_url>"}
```

This hook must include a `resource_url` or we will not perform a followup GET and thus Zaps will not trigger. If you are currently sending an `id`, but not a `resource_url`, you can modify the trigger's `catch_hook` in scripting to add a `resource_url` key that uses this `id`.

On a successful hook, we'll return a `200` status code, content is irrelevant.

> If Zapier responds with a `410` status code you should immediately remove the subscription to the failing hook (unsubscribe). Additionally, excessive failures (multiple `4xx` or `5xx` failures) can be handled at your discretion. It is the clients responsibility to resubscribe if needed after failures.

> The maximum hook size is 100MB. Any payloads that exceed this limit will see a `413` status code.

### Step 3: Consuming <small>_(a call from Zapier to your app)_</small>

```bash
GET <resources_url> \
    -H Authenticated: Somehow \
    -H Content-Type: application/json
```

This is an old fashioned REST hit to a standard endpoint, it requires the same authentication as the rest of the API. It can return a list or a single object.

_If you don't want to perform this extra step, look at [REST Hooks](#rest-hooks)!_

### Step 4: Unsubscribe <small>_(a call from Zapier to your app)_</small>

```bash
DELETE <unsubscribe_endpoint> \
    -H Authenticated: Somehow \
    -H Content-Type: application/json \
    -d <content built/omitted in pre_unsubscribe scripting method>
```

If you've properly stored identification data about the hook (like its unique ID) from the `post_subscribe` scripting method, you should use our `pre_unsubscribe` scripting method to formulate the DELETE call. In that call you have access to your previously stored data under the`bundle.subscribe_data` variable. **Unsubscribing occurs when a user turns their Zap off.**

[Some example code is provided to make this as easy as possible.](#scripting/#rest-hook-subscription-examples) A heads up: you will need to use that code if you intend to do a DELETE call. You'll be able to access `bundle.subscribe_data` to build the URL in `pre_unsubscribe`. The default behavior is slightly different and listed below.

However, the **current default** does not perform a DELETE. For example, if you omit the `pre_unsubscribe` function entirely, we will attempt a default unsubscribe call:

```bash
POST <unsubscribe_endpoint> \
    -H Content-Type: application/json \
    -d '{"target_url": "https://hooks.zapier.com/<unique_target_url>"}'
```

On a successful unsubscribe, return a `200` status code, content is irrelevant.

It is worth remembering that the subscription URL should effectively be unique (this could be enforced by your app as well) which also allows us to clean up unrecognized hooks (we also recommend not requiring authentication for such an endpoint).

### Trigger Options

You can define your triggers via your app's dashboard. When you create a new trigger, you'll be prompted with several options. Below we list all complete definitions of what each option is for.

### Name

This is a human readable label a user would see when browsing the directory and adding your app. Make it short but descriptive.

Example: <br/> `New Ticket Created` or `New Email with Label`

### Noun

This is the object that the trigger is most closely associated with. It will be a noun you used in the Name field. We rely on an accurate noun to generate human-friendly sentences for users.

Example: <br/> "New Ticket Created" would have "Ticket" as the noun. "New Email with Label" would use "Email" or "Labeled Email".

### Key

This is a field only really used internally for both [dynamic dropdown](#dynamic-dropdowns) and [scripting](#scripting) references. Needs to be at least two characters long, start with an alpha, and only contain `a-z`, `A-Z`, `0-9` or `_`.

Example: <br/> `new_ticket`, or `newEmailLabel`

### Help Text

A longer description of what this trigger actually watches for.

Example: <br/> `Triggers when a new email occurs with a label of your choice.`

Demo: <br/> _the user will see **Name** and **Help Text** like below:_

![label and help](https://cdn.zapier.com/storage/photos/d4fd7c63b1f2fe58946a4184a4bce722.png)

### Hide

If you create a trigger solely to be used in a [dynamic dropdown](#dynamic-dropdowns) and it will never be helpful to users, you can mark it as hidden. We will never show the trigger in the UI and users will not be able to pick it.

This usually comes up with [test triggers](#test-triggers#), where the test trigger is for an endpoint that always returns the same data (a user profile, for instance).

### Paging

When defining a trigger to power a [dynamic dropdown](#dynamic-dropdowns) you can use the [Scripting API](#scripting) to implement paging by relying on `bundle.meta.page`.

This flag must be set in order to enable paging in the dynamic dropdowns powered by this trigger. If set, the user will see the option in the dropdown to load more choices: “Don’t see your choices? Try loading more than {x}.”

![paging](https://cdn.zapier.com/storage/photos/45654fc7f3e6d105cee15cf4d06ebf60.png)

Otherwise, the user will see standard language: “Check {your app} and reload the data”

> Note: Paging is **not used** in normal trigger polling calls.

### Polling: URL

Where in your API can we poll for this trigger? Your URL route can include [variables](#variable-syntax) (from [authentication fields](#authentication-fields) and [trigger fields](#trigger-fields)), as well as query parameters. Query parameters are helpful for telling your API to sort things in reverse-chronological order, [a requirement we have](#deduplication).

> Important: this endpoint should return JSON encoded _list_ of _objects_. If the list is nested in an object with meta information we will do our best to find it. If we can't or your API only returns a single object, then you will need to use a `_post_poll` [scripting method](#scripting/#trigger-methods) to take the response and transform it to a list.

Example: <br/> {% raw %}`https://example.com/api/v1/users/{% templatetag openvariable %}id{% templatetag closevariable %}/contacts.json?sort=desc&on=date_created`{% endraw %}

#### A Warning about encoding URL params

We will not automatically encode any URL variables, so you're responsible for encoding any if they require that. For example, emails _might_ include a `+` sign, so if you have {% raw %}`https://example.com/api/v1/users?email={% templatetag openvariable %}email{% templatetag closevariable %}`{% endraw %} you'll want to encode that in your [`TRIGGER_KEY_pre_poll`](#available-methods/#polling) (or remove it from there and add it to the `bundle.request.params`), otherwise you'll get a "space" where the `+` sign is.

A better approach is to not even include it in the URL (it'll be added and encoded automatically in that case).

#### Optimizing for a fast response

If you run into errors like `Scripting payload too large` then your API's response is too big. Here are some tips to prevent that:

Define a `KEY_pre_poll` scripting method and:

- When `bundle.meta.frontend` is `true`, modify the prepared request to include the relevant parameter that instructs your API to limit to the most recent 3 results. That's all we need when we poll for recent samples in the Editor.
- When `bundle.meta.frontend` is **not** `true`, modify the prepared request to include the relevant parameter that instructs your API to limit to results for the last 12 hours. We poll every 5 to 15 minutes, but this allows for some downtime on either side.
- If the API endpoint is one that may see a lot of results in a short time, try narrowing the above window of 12 hours or in addition add a sensible limit. Be aware that this may cause users to miss tasks, although without they would miss even more if the results are too large to process.

### Custom Trigger Result Fields URL

This allows you to dynamically define user-friendly labels for data returned by triggers as well as fields that may not be found in all live samples. These labels are shown to users in the Zap Editor when they map fields from this trigger to the _Edit Template_ step for actions or searches.

> Note: Unlike actions and searches, triggers don't support Custom Trigger Fields for the _Edit Template_ step of the trigger.

Example: <br/> {% raw %}`http://api.example.com/v2/fields.json` or `http://{% templatetag openvariable %}account{% templatetag closevariable %}.example.com/api/v1/fields.json`{% endraw %}

If your polling trigger returns:

```javascript
[
  {
    id: 1,
    q_1: "Yes"
  }
];
```

You can return in the custom fields URL something like:

```javascript
[
  {
    label: "Are you happy with your service?",
    key: "q_1",
    important: true,
    type: "unicode"
  }
];
```

And users will see _Are you happy with your service?_ instead of \*Q 1" when they map this field.

> Read more about [custom field formatting here](#trigger-fields-custom).

### Webhook: Event Name

A part of our [REST Hooks](#rest-hooks), this lets you namespace the name of event that this trigger identifies with.

### Webhook: Static Webhook

A part of our [static webhooks](#static-webhooks), this simply toggles the ability to receive webhooks and disables polling.

### Webhook: Static Webhook Directions

A part of our [static webhooks](#static-webhooks), when static webhooks are in use this lets you define specialized directions for setup. It also supports [Markdown](http://daringfireball.net/projects/markdown/syntax) so you can provide links or other specialized HTML formatting.

### Trigger Fields

**Trigger Fields** answer the question: _How can a user filter Triggers?_ Almost exclusively these are [dynamic dropdowns](#dynamic-dropdowns), but some real world examples are:

- Search Term _(EG: Twitter Tweet Search)_
- Label _(EG: Gmail Inbox)_
- Parent Object _(span relationships via [dynamic dropdowns](#dynamic-dropdowns))_
- Repo for an Issue _(EG: Github)_
- Notebook for a Note _(EG: Evernote)_

> Imagine an endpoint like `https://example.com/api/v1/prospects.json` - that would require no trigger fields at all. However an endpoint like `https://example.com/api/v1/list/1234/prospects.json` - that would require at least a trigger field to select the list ID (and it would be a [dynamic dropdown](#dynamic-dropdowns) at that!).

What a user sees:

![](https://cdn.zapier.com/storage/photos/96781c9b488d9677330773efa7a04a3e.png)

What a developer sees:

![](https://cdn.zapier.com/storage/photos/dcf94179c0896e194dc396dcf337b365.png)

When you attempt to add a trigger field, you'll be prompted to provide some options which are outlined below.

Use the Scripting API to modify the request to your [Polling URL](#scripting/#polling) or [Subscribe URL](#scripting/#rest-hooks-and-notification-rest-hooks) to include these fields or use them in the [post poll](https://zapier.com/developer/documentation/v2/scripting/#polling) or [catch hook](#scripting/#static-and-rest-hooks) methods to filter the response from your API.

### Trigger Field Options

### Key

A key for your internal use. It is available for [variable syntax](#variable-syntax) in the Trigger URL field (as well as in [scripting](#scripting)). Needs to be at least two characters long, start with an alpha, and only contain `a-z`, `A-Z`, `0-9` or `_`.

Example: <br> `project` or `search_term`

### Label

A human readable Label shown in the UI as a user builds a Zap.

Example: <br> `Room` or `Title`

![label help default](https://cdn.zapier.com/storage/photos/96522edc71e94085537c1fa70480adb8.png)

### Help Text

Human readable description of a trigger field, useful for describing some detail you couldn't list in the Label.

Example: <br> `Choose which project to watch for new messages.` or `Define a search term for finding Tweets.`

### Default

A default value for a field. The behavior varies between required and optional fields. For required fields, the default will be set once when the user first creates the Trigger, but it is not guaranteed after that (we raise an error on missing/null values instead). For optional fields, it is set on initial creation and used in place of missing or null values every time the Zap runs.

### Type

The type we will try to coerce to. Falls back to unicode (text) if coercion fails.

### Required

If checked a user will not be able to continue without entering some value.

### Dynamic Dropdown

Use an existing [Trigger](#triggers) to load in values for selection, using the machine readable value your API consumes (like `id` or `hash`) while showing a human readable version to the user (like `name` or `itemName`).

In our experience, most trigger fields are dynamic dropdowns.

Refer to our [dynamic dropdown docs](#dynamic-dropdowns) for a more in depth explanation.

Example: <br> `TRIGGERKEY.id.name` or `TRIGGERKEY.hash.itemName`

![dynamic dropdown](https://cdn.zapier.com/storage/photos/9a6185121c22d1397dad62c819333f0e.png)

### Static Dropdown

A comma separated string that will be turned into a select field for limiting the choices a user can provide to a trigger field.

Example: <br> `choice_a,choice_b,choice_c` or `Yesterday, Today, Tomorrow`

![simple static dropdown](https://cdn.zapier.com/storage/photos/7641c6b42a5034432f63274226e84414.png)

If you would like to provide a label for the raw value of each choice, you can also use the raw|label,raw|label syntax instead.

Example: <br> `1|Option 1,2|Option 2`

![simple static dropdown as key-value pairs](https://cdn.zapier.com/storage/photos/524ad1774802cc81d95cb2e3f23972d6.png)

### List

Indicates if this field can hold multiple values. For example, this could be useful if you want to allow users to only trigger on new contacts with one or more tags applied. List fields gain the +/- icons to the side.

![list field example](https://cdn.zapier.com/storage/photos/580a778c672cf2a686b4b1463ad8f84e.png)

### Trigger Results Fields (Custom)

Sometimes, the data returned by a trigger is hard to use in a Zap because of how the keys are named. When a user goes to map fields in an action, the trigger data's keys are used to identify which field is which. If those keys are something unintelligible like UUIDs rather than human-readable data points like `"name"` or `"email"`, the user may not be able to identify which fields to map in their action.

To remedy this, we have Custom Trigger Result Fields, an additional HTTP GET to a URL you provide in your trigger definition that tells us additional metadata about the data the trigger will return, such as human-readable labels to display when mapping fields. All you need to do to enable custom trigger result fields is:

- Provide a _Custom Trigger Result Fields URL_ for the trigger in question.
- Ensure the URL route returns data in the below format, or manipulate to fit with [a `_post_custom_trigger_fields` scripting method](#scripting/#key_post_custom_trigger_fields).

```javascript
[
  {
    "type": "unicode", // unicode, int, or bool
    "key": "json_key", // the key in the trigger data
    "label": "Pretty Label", // the human-readable label to display
  },
  ...
]
```

> Note: Unlike actions and searches, triggers don't support Custom Trigger Fields for the _Edit Template_ step of the trigger.

### Trigger Sample Results

To help give users a clean experience when creating Zaps, we ask that you paste a sample JSON dictionary of a single item from your API into Zapier.

We will use this sample JSON for two things:

1. To detect a list of hard-coded key names which the user can pick from during Zap (and Zap template) setup
2. To use as a hard-coded fallback for sample data so that we can provide fields to insert during Zap setup (if your API returns 0 results)

> Sample results will NOT be used for a user's Zap testing step. That step requires data to be received by an event or returned from a polling URL. If a user chooses to "Skip Test", then the sample result, if provided, will be used.

Here is the sample JSON for something like a new email message, and how it shows up in our user-facing Editor:

```javascript
{
  "to_name": "Mike Knoop",
  "to_address": "mike@zapier.com",
  "from_name": "Bryan Helmig",
  "from_address": "bryan@zapier.com",
  "subject": "Testing out this new Zap!",
  "message": {
    "no_html": "Let me know it it works.",
    "html": "<div>Let me know if it works.</div>"
  }
}
```

_Note: Even though your API endpoint has to return an array, the sample JSON here must be of a single object._

We will parse this sample and provide dropdowns like this to the user:

![samples](https://cdn.zapier.com/storage/photos/81640b3a54542c0a503bfd3bc4ef8927.png)

By default, we can handle flat dictionaries and dictionaries within dictionaries (via our `__` delimiter in keys).

When the user is inserting fields in the Zap editor, and your API returns no results (`[]`) then we will use your hard-coded fallback JSON if it exists.

<!-- NO LONGER VALID: ![sample](https://cdn.zapier.com/storage/photos/97739db25b44a01d209d8488f640372b.png)-->

> Your hard-coded JSON provided above will _not_ be run through the Scripting API (either for key enumeration or sample data fallback) so if you use the Scripting API to add or modify fields on top of your normal API response, you'll want to make sure you perform the same manipulations manually before pasting in the JSON above.

> Note - our system often does a sample "poll" or pulls cached values for a live example - samples are just a part of that system. If you need to omit bad fields from usage - you'll need to ensure the poll or webhook or whatever does not included the bad fields either!

### Test Triggers

A test trigger is a regular [trigger](#triggers) with a special responsibility. The test trigger is the trigger Zapier will use to verify the authentication credentials users provide when they first attempt to access your API through Zapier. If your API returns a `2XX` status code, we will assume the credentials are valid. Anything else (or an empty response that isn't a `204`), and we will assume the credentials are bad.

You can only mark one trigger as the test trigger. A test trigger can be made for any endpoint in your API that:

1.  Requires authentication
1.  Is guaranteed to always return some data (or a 204 for empty responses)

Some examples of good endpoints to use for the test trigger:

- A url like `/ping` that is meant solely to test authentication
- An endpoint that returns a user's profile
- An endpoint for high-level objects in your API that users are virtually guaranteed to have (i.e. contacts if you are a CRM, tickets if you are a support center)

### Setting one up

In your app, you'll need to choose a trigger that performs a "simple test" when its Polling URL is used to access an endpoint that requires valid authorization/credentials.

If your trigger is intended to be solely used for authentication testing, then you can mark it hidden.

**Important** make sure that the test trigger doesn't have any "Required" trigger fields (because they'll be empty when we perform the auth test)

### Errors

When your test trigger fails, a message will be displayed to the user like:

> The app returned "Email Missing". This usually happens when your Zap is missing a required field or a field value isn't in a recognized format.
>
> We made a request to example.com and received (400) Bad Request.

For "Email Missing" we try to extract the error message from the response body:

1. We check to see if you send back JSON. If so, we look for a `message` field, or similar in the JSON object.
2. We check to see if you send back an XML file (i.e., xml in the Content-Type header). If so, we do a similar lookup for an error message in the body.
3. We then check to see if you sent back a plain text response(i.e., Content-Type: text/plain). If so, we check that the content is < than 180 characters and use it verbatim.
4. Finally, we fall back to displaying the response status text or code.

Based on the response status code we then try to add a more general explanation and possible resolution.

Alternatively, you can compose a custom error message by raising an `ErrorException` in your Scripting. More information in the [Available Exceptions section](https://zapier.com/developer/documentation/v2/available-exceptions) of our docs.

> Heads up! This style is only valid for the legacy web builder. Zapier's [CLI platform](https://github.com/zapier/zapier-platform/blob/master/packages/cli/README.md#error-handling) and [visual builder](https://zapier.github.io/visual-builder/docs/auth#common-authentication-error-messages) expect standard HTTP Errors to be thrown.

### Testing

To select your test trigger, use the button "Manage Trigger Settings":

![](https://cdn.zapier.com/storage/photos/3fe4eea685b9eb25f72b9414d8e94db5.png)

Scroll down to the bottom of the page, and select the appropriate trigger:

![](https://cdn.zapier.com/storage/photos/dddb3d5f5ba166fbe581ff214a7385e7.png)

---

## Actions

Actions answer the question: _What should my users be able to create via Zapier?_ They are things like:

- Create ToDo Task _(EG: Basecamp)_
- Create Chat Message _(EG: Campfire or Hipchat)_
- Create Issue _(EG: GitHub or Pivotal Tracker)_

You can think of Actions as POSTs, writes, or the creation of a resource. It involves Zapier sending data to your app.

What a user sees:

![](https://cdn.zapier.com/storage/photos/be352755276c2c7466e0ce9d20225235.png)

What a developer sees:

![](https://cdn.zapier.com/storage/photos/357d93e05364353029a6c813876215ed.png)

See also: [Actions in the CLI](https://zapier.github.io/zapier-platform-cli/#triggerssearchescreates)

You can define your actions via your app's dashboard. When you create a new action, you'll be prompted with several options. Below are complete definitions of what each option is for.

### Action Options

### Name

This is a human readable label a user would see when browsing the directory and adding your app. Make it short but descriptive.

Example: <br/> `Create Issue`, `Send Alert` or `Unsubscribe User`

### Noun

This is the object that the action is most closely associated with. It will be a noun you used in the Name field. We rely on an accurate noun to generate human-friendly sentences for users.

Example: <br/> "Create Issue" would have "Issue" as the noun. "Unsubscribe User" would use "User".

### Key

This is a field only really used internally for both [dynamic dropdowns](#dynamic-dropdowns) and [scripting](#scripting) references. Needs to be at least two characters long, start with an alpha, and only contain `a-z`, `A-Z`, `0-9` or `_`.

Example: <br/> `create_issue`, `ticket` or `newNote`

### Help Text

This some human readable explanatory text, usually something that clarifies what the action does.

Example: <br/> `Creates a new issue in a selected repository.`

_The user will see **Name** and **Help Text** like below:_

![label and help](https://cdn.zapier.com/storage/photos/2e4efad4d532f9b62a36ba6806c62e4e.png)

### Action Endpoint URL

Define the URL where we will, by default, `POST` the payload to. You can also make use of [variable syntax](#variable-syntax) where [auth fields](#authentication-fields) and [action fields](#action-fields) will be injected.

Example: <br/> {% raw %}`http://api.example.com/v2/clients.json` or `http://{% templatetag openvariable %}account{% templatetag closevariable %}.example.com/api/v1/projects.json`{% endraw %}

> What about the payload? You can define those in [action fields](#action-fields), anything you put there and check "Send in JSON?" will be included in the JSON according to its key!

#### A Warning about encoding URL params

We will not automatically encode any URL variables, so you're responsible for encoding any if they require that. For example, emails _might_ include a `+` sign, so if you have {% raw %}`https://example.com/api/v2/clients.json?email={% templatetag openvariable %}email{% templatetag closevariable %}`{% endraw %} you'll want to encode that in your [`ACTION_KEY_pre_write`](#available-methods/#action-methods) (or remove it from there and add it to the `bundle.request.params`), otherwise you'll get a "space" where the `+` sign is.

A better approach is to not even include it in the URL (it'll be added and encoded automatically in that case)

### Custom Action Fields URL

This allows you to dynamically define action fields that are user set (IE: custom fields). They get passed into the POST'ed JSON just like normal action fields (or into [scripting](#scripting)).

Example: <br/> {% raw %}`http://api.example.com/v2/fields.json` or `http://{% templatetag openvariable %}account{% templatetag closevariable %}.example.com/api/v1/fields.json`{% endraw %}

> Read more about [custom field formatting here](#action-fields-custom).

### Hide

Usually you'll want to leave this unchecked. If you check it, we'll completely hide the action from the enduser. This can be useful if an action is incomplete, but you need to deploy your app in it's current state. This option is also a way to hide actions that become deprecated in your API.

### Action Fields

Action Fields answer the question: what details can a user provide when setting up an Action?

These details might include:

- Title _(EG: Note Title in Evernote)_
- Description _(EG: Issue Description in Github)_
- Parent Object _(span relationships via [dynamic dropdowns](#dynamic-dropdowns))_
- Repo for an Issue _(EG: Github)_
- Notebook for a Note _(EG: Evernote)_
- Message Body _(EG: Chat Body in Campfire or Hipchat)_

What a user sees:

![](https://cdn.zapier.com/storage/photos/4019995bb52ff25afef161fde9bbde0e.png)

What a developer sees:

![](https://cdn.zapier.com/storage/photos/83ffa44eb76b6f3338f3b05ad63945cb.png)

Each action should have at least one action field, because, hey, it really makes no sense to POST nothing to an endpoint!

You can also dynamically load custom action fields by inspecting a custom field endpoint of your own. [Learn more.](#action-fields-custom)

### Action Field Options

### Key

A key for you and your API's consumption. This is available for [variable syntax](#variable-syntax) in the Action URL field as well as being added to the POSTed JSON (optional). Needs to be at least two characters long, start with an alpha, and only contain `a-z`, `A-Z`, `0-9` or `_`.

Example: <br>`room`

We'll take double underscores and convert them to nested dictionaries before we POST JSON.

Example:<br>
`project__title` converts to `{"project": {"title": "some value"} }`

### Label

A human readable Label shown in the UI as a user works to complete an Action.

Example:<br>
`Room` or `Title`

![label help default](https://cdn.zapier.com/storage/photos/96522edc71e94085537c1fa70480adb8.png)

### Help Text

Human readable description of an action field, useful for describing some detail you couldn't list in the Label.

Example:<br>
`Choose which room to send the message to.` or `Add a title to the note.`

### Default

A default value for a field. The behavior varies between required and optional fields. For required fields, the default will be set once when the user first creates the Action, but it is not guaranteed after that (we raise an error on missing/null values instead). For optional fields, it is set on initial creation and used in place of missing or null values every time the Zap runs.

### Type

The type we will try to coerce to on the backend. Fails silently to ensure that tasks aren't dropped on coercion errors.

You can get a full list of supported types and the coercion implied here: [Field Types](#field-types).

### Required

If checked a user will not be able to continue without entering some value.

### Dynamic Dropdown

Use an existing [Trigger](#triggers) to load in values for selection, using the machine readable value your API consumes (like `id` or `hash`) while showing a human readable version to the user (like `name` or `itemName`).

Refer to our [dynamic dropdown docs](#dynamic-dropdowns) for a more in depth explanation.

Example:<br>
`TRIGGERKEY.id.name` or `TRIGGERKEY.hash.itemName`

![dynamic dropdown](https://cdn.zapier.com/storage/photos/9a6185121c22d1397dad62c819333f0e.png)

### Static Dropdowns

A comma separated string that will be turned into a select field for limiting the choices a user can provide to an action field.

Example:<br>
`choice_a,choice_b,choice_c` or `Yesterday, Today, Tomorrow`

![simple static dropdown](https://cdn.zapier.com/storage/photos/7641c6b42a5034432f63274226e84414.png)

If you would like to provide a label for the raw value of each choice, you can also use the raw|label,raw|label syntax instead.

Example:<br>
`1|Option 1,2|Option 2`

![simple static dropdown as key-value pairs](https://cdn.zapier.com/storage/photos/524ad1774802cc81d95cb2e3f23972d6.png)

### Search Connector

Use an existing [Search](#searches) to find a value based on user input. Set the key of this field to the **same** key as the field in the search you want to use in executing the search. The second part of the definition is the attribute of the returned object that is sent to your service _in place of_ this field.

Example:<br>
`SEARCHKEY.id`

The above definition sets the field as an input to SEARCHKEY (as long as the field key matches a field key within SEARCHKEY), and the `id` field from the first result returned from SEARCHKEY is used as the value for this field.

The user does not see anything different for this type of field, so make sure to explain in the help text what kind of input you expect here.

**Note**: Any field with a search connector specified [must also have a dynamic dropdown specified](https://zapier.com/developer/documentation/v2/dynamic-dropdowns). This is because search connectors are meant to save the user from having to find and copy an ID value into a field. When the search connector is combined with the dynamic dropdown, we'll prefill the ID found by the search step into the dynamic dropdown for the user.

### Parent Key

Ok, parent key is a little tricky, but it can be really helpful if you want to support line items (an array of sub-objects). When an action has one or more fields that have a parent key, we treat all those fields as the schema for building sub-objects, which we combine into a list and nest under the parent key.

For example, say you define two fields `amount` and `quantity` and give them both the parent key `line_items`. Now imagine a user has a trigger that provides this data:

```json
{
  "sale": {
    "items_sold": [
      {
        "cost": "$3.00",
        "# sold": 12
      },
      {
        "cost": "$2.55",
        "# sold": 1
      }
    ]
  }
}
```

**NOTE:** The kind of data you receive ultimately depends on what the app's trigger providing the data returns. This means that if the app's trigger a customer's using doesn't provide line items, we'll transform arrays into CSV strings. There's really nothing you can do about this, but when testing, [make sure the app you're using to test triggers supports line items](https://zapier.com/help/field-types/#arrays).

The user could map `cost` into your amount field and `# sold` into the action's quantity field, like this:

![parent key UI example](https://cdn.zapier.com/storage/photos/d5fdafaf1958b06214b64c00d5d67c44.png)

Zapier would produce this JSON for POSTing:

```json
{
  "line_items": [
    {
      "amount": "$3.00",
      "quantity": 12
    },
    {
      "amount": "$2.55",
      "quantity": 1
    }
  ]
}
```

Zapier will _automatically_ expand fields with the same `parent_key` into a nested list of objects according to how the source data comes in (we'll make as many objects inside the list as the original source). All you need to do is provide the same `parent_key` and expect an array of objects under that `parent_key`.

### Send to Action Endpoint URL in JSON body

If checked, we'll include the user-provided value in the POSTed JSON on the provided key (or nested key if double underscores `__` are present).

If you utilize the `pre_poll` or `ACTIONKEY_pre_poll` methods via [scripting](#scripting) you can get complete control over the JSON output beyond simple exclusion/inclusion.

### List

Indicates if this field can hold multiple values. For example, this could be useful if you want to allow users to add tags to a new contact, and you want them to be able to add more than one. List fields gain the +/- icons to the side.

![list field example](https://cdn.zapier.com/storage/photos/3792d7a3a0d5cdd2100afd4ab2c12104.png)

## Field Types

The following is a list of the field types we use internally. Normally, you'd choose one of these fields when creating your [action fields](#action-fields) or [trigger fields](#trigger-fields) via the type dropdown:

![field types](https://cdn.zapier.com/storage/photos/fb18cf5e7fb4f3da14862f381d6ce00f.png)

However, if you're using [Custom Fields](#action-fields-custom) you might want to know the available field types. The key column corresponds to the `type` key found in the code example here: [Action Fields Custom](#action-fields-custom).

### Unicode

Unicode fields are essentially one-line text fields that can support unicode characters. There is no coercion done for this type.

![](https://cdn.zapier.com/storage/photos/9c5aa3e3eb41a1fcc7d0ee16d8e2075e.png)

> Unicode fields are represented by a `type: unicode` key.

### Textarea

Think of this as a multi-line unicode field. It's really only used to give the user a textarea in the UI instead of a one-line input field. There is no coercion done for this type.

![](https://cdn.zapier.com/storage/photos/b53b2c9bc902723203adce06f5efb69c.png)

> Textarea fields are represented by a `type: text`. key

### Integer

Suitable for whole integer numbers, we'll coerce any text down into an integer by stripped non-numeric values from the string. A negative sign (-) in front is also allowed.

![](https://cdn.zapier.com/storage/photos/a5c97c71cc03d2fd5264a108a06326e5.png)

> Integer fields are represented by a `type: int` key.

### Float

![](https://cdn.zapier.com/storage/photos/7cc8cd0c85f50dbd575556ce3686ed57.png)

Like integers, this will coerce any text down to a floating point number with the addition of allowed characters like `.` and `,`.

> Float fields are represented by a `type: float` key.

### Boolean

We apply some natural language parsing to try and coerce any text into `True` or `False`. This UI field is also replaced with a dropdown allowing the user to specifically pick "Yes" or "No" explicitly.

![](https://cdn.zapier.com/storage/photos/f34016804fa46dd9a72bab3e1e0ad188.png)

> Boolean fields are represented by a `type: bool` key.

### DateTime

Our most complex coercion. We'll attempt to convert any given value into an ISO-8601 formatted string. The parser is quite robust, supporting epoch timestamps, ISO-8601 and even natural language parsing! You can use `moment.js` via [Scripting](#scripting) to parse and replace if your servers expect a different format sent to it.

![](https://cdn.zapier.com/storage/photos/c6feadb88b90546d41a95f4d7f83b07e.png)

> DateTime fields are represented by a `type: datetime` key.

### Dictionary/Object

This is a fairly complex shortcut to a widget that allows a user to provide a series of key/value pairs, perfect for providing completely unstructured and custom metadata (do **not** use this if your API provide definitions for that metadata, look into custom fields instead!).

![](https://cdn.zapier.com/storage/photos/ff7dbcd6f85d2a2c3b406a651102c21a.png)

> Dictionary/Object fields are represented by a `type: dict` key.

### File

This field represents a file object itself – not a text field describing a file. If a URL is provided by a user, we will download the data at that URL and provide the resulting file object to your app. If non-URL text is entered here, we will create a .txt file containing the field contents and provide that file to your app. A deeper dive into files from a developer perspective can be found here: [Files](#files)).

![](https://cdn.zapier.com/storage/photos/000ef76bf48080b6f529e38b8951189a.png)

> File fields are represented by a `type: file` key.

### Copy

Copy can be used to bring extra attention to important help text. No user input will be provided with copy – it is simply static text.

![](https://cdn.zapier.com/storage/photos/fcde7fdb0917565f645ed5798d03a643.png)

> Copy fields are represented by a `type: copy` key.

There are also a few other special things, related to types, you can do.

### Static Dropdown

You can provide a `choices` array which will be mapped automatically into a dropdown in the Zap Editor. In the developer UI you should simply provide us with a hard-coded list of comma-separated values for the "choices" option when defining a field. If you're using [scripting](#scripting), you'll want to provide these choices to us manually. Here is a code sample and what it looks like:

```javascript
[
  {
    type: "integer",
    key: "priority",
    label: "Priority",
    helpText:
      "Low Priority alerts do not send a notification. Medium Priority alerts send one notification. High Priority alerts send one notification every hour.",
    choices: {
      0: "Low Priority",
      1: "Medium Priority",
      2: "High Priority"
    }
  }
];
```

![field choices](https://cdn.zapier.com/storage/photos/f968a75ac7138efa098f9fe77df64e24.png)

You can also provide an array of just labels for choices if you like. This will be equivalent to providing an object where every key matches its value.

### Lists

Say you wanted to allow the user to specify multiple values for a single field. Maybe, a list of tags to apply or a list of email addresses to send to. You can use our `list` feature to enable "+" and "-" buttons in the Zap Editor which users can use to specify more than one value. `list` fields can be any `type` except `dict` or `file`.

You can make a field a list by checking the appropriate box in the UI. For custom fields, you can use [Scripting](#scripting) to alter the field definition to include `list: true` like this:

```javascript
[
  {
    type: "unicode",
    key: "to",
    label: "To",
    help_text: "What email addresses should this email be sent to?",
    list: true
  }
];
```

![field list](https://cdn.zapier.com/storage/photos/cbb6393e207e2dc26da7f51bfa1ac5cc.png)

### Dynamic Dropdowns

Sometimes, API endpoints require clients to specify a parent object in order to create or access the child resources. Imagine having to specify a company id in order to get a list of employees for that company. Since people don't speak in auto-incremented ID's, it is necessary that Zapier offer a simple way to select that parent using human readable handles.

Our solution is to present users a dropdown that is populated by making a live API call to fetch a list of _parent_ objects. We call these special dropdowns **dynamic dropdowns**.

> Tip: We used to call the dynamic dropdowns "prefills"!

Here is what a user sees as a dynamic dropdown:

![prefill](https://cdn.zapier.com/storage/photos/dd31fa761e0cf9d0abc9b50438f95210.png)

In order for a dynamic dropdown to work, we must have a working [trigger](#triggers) set up for the parent object. Zapier will query for that dynamic dropdown, parse out an identifier and a human readable handle for each record, and then offer the user a dropdown. Once they make a selection, we store the identifier for use later when reading or writing child objects.

The dynamic dropdown syntax is split into three parts:

- Which trigger is this dynamic dropdown referring to?
- Which piece of data is the unique identifier?
- Which piece of data is a human readable representation?

We combine those into one field: `TRIGGERKEY.identifier_key.human_readable_key`.

For example, let's say you have a trigger called Project which offers the following data (remember, triggers are expected to return a list of JSON objects with an ID field):

```javascript
[
  {
    "id": 4287243,
    "owner_id": 4632,
    "date_created": "Mon, 25 Jun 2012 16:41:54 -0400",
    "title": "My secret project!",
    "description": "It's a Facebook for dogs!"
  }
  ...
]
```

You want to let users read just the messages from that project as a trigger. As you are making the **message trigger** you'd need to create a `project` [trigger field](#trigger-fields) with the following dynamic dropdown value:

Example: <br/> `new_project.id.title`

> Note: `new_project` is a fictional key for the Project trigger. You'll set your specific trigger key when you create your trigger. `id` is the identifier from the above project data. The human readable representation key `title` is located there as well.

Notice that a dynamic dropdown is really nothing more than a [trigger field](#trigger-fields)/[action field](#action-fields) that is populated by another trigger.

For fields where it's expected that the value will change, such as an Update Project action where the user will want to update different projects based off the trigger value, we recommend [pairing the dynamic dropdown with a search connector](https://zapier.com/developer/documentation/v2/action-fields/#search-connector). We will prefill the ID from the search into the dynamic dropdown so the customer can easily set this Zap up.

#### Accessing Nested Keys

If the keys that you need to access to construct the compound dynamic dropdown key are nested, use double underscore syntax to access the nested keys.

For example, if the response data to the trigger powering the dynamic dropdown was structured like this:

```javascript
[
  {
    "id": 42,
    "meta": {
      "label": "Answer to the Ultimate Question",
      "description": "It's an older meme, sir, but it checks out",
    },
  }
  ...
]
```

You would probably want your dropdown key to look like this (note the double underscore between `meta` and `label` to handle the nesting): <br/>`TRIGGERKEY.id.meta__label`

> Note: This double underscore syntax to handle nesting is really useful other places, too — like for [connection labels](#appdevguide-auth/#setting-a-connection-label)!

### Action Fields (Custom)

![](https://cdn.zapier.com/storage/photos/2902a6405a49b23f3898d280514b9095.png)

A natural extension of normal hard coded [action fields](#action-fields) are dynamic action fields, or custom fields. Custom fields are very commonly used in services that allow users to create their own data fields. Examples include contacts in CRMs, form management apps, or ticket fields in helpdesk software. These apps will assign a generated unique key to the field, while storing information about the field, such as its human readable label and data type, separately. Working with this data requires an extra step to retrieve that field metadata in order to allow users to make sense of the information.

All you need to do to enable custom fields is:

- Provide a Custom Action Fields URL for your action (found in the "Where To Send Data" section of the Action setup).
- Ensure the URL route returns data in the below format, or manipulate it to fit with [scripting](#scripting/#key_custom_action_fields).
- You can choose from several internal types, documented here: [Field Types](#field-types).

```javascript
[
  {
    "type": "unicode",
    "key": "json_key", // the field "name", will be used to construct a label if none is provided
    "required": false, // whether this field must be filled out. defaults to true
    "label": "Pretty Label", // optional
    "help_text": "Helps to explain things to users.", // optional
    "placeholder": "Helps to show format of expected value to users.", // optional
    "default": "Sets the initial value.", // optional
    "choices": { // optional
        "raw": "label"
    } // can also be a flat array if raw is the label
    "prefill": "contact.id.name", // optional, defines a dynamic dropdown
    "searchfill": "contact.id" // optional, defines a search connector
  }
  ...
]
```

### Custom Action Result Fields

If your action **returns** custom fields you'll also want to configure a source for labels so other actions in multi-step Zaps can display those fields properly and allow users to correctly use the data in the Zap editor.

- Provide a Custom Action Result Fields URL for the action. (This will likely be the same endpoint you used for Custom Action Fields)
- Ensure that the URL route returns data in the below format, or manipulate it to fit with [scripting](#scripting). Extra data will be ignored, but we require at least the following to properly format your action results.

```javascript
[
    {
        "type": "unicode",
        "key": "json_key", // the field "name", will be used to construct a label if none is provided
        "label": "Pretty Label",
    },
    ...
]
```

> Using parent_key or type=dict (or both) is not currently supported in custom fields.

### Action Sample Results

(This works similar to [trigger sample results](#trigger-sample-results)

To help give users a smooth experience when creating multi-step Zaps, we ask that you paste a JSON object that contains the fields (along with sample values), so that your user can map those fields into the next step.

We will use this sample JSON for two things:

1. To detect a list of hard-coded key names which the user can pick from during Zap (and Zap template) setup
2. To use as a hard-coded fallback for sample data so that we can provide fields to insert during Zap setup (if your API returns 0 results)

> These results will NOT be used for a user's Zap testing step. That step requires data to be received when performing the action.

Here is the sample JSON for something like a newly created email message, and how it shows up in our user-facing Editor:

```javascript
{
  "labelIds": "DRAFT",
  "id": "150f2791b6723cb5",
  "threadId": "150f2791b6723cb5"
}
```

We will parse this sample and provide dropdowns like this to the user:

![samples](https://cdn.zapier.com/storage/photos/0facee1c1497d0db62440c1404f1fdaf.png)

By default, we can handle flat dictionaries and dictionaries within dictionaries (via our `__` delimiter in keys).

When the user is inserting fields in the Zap editor, and your API returns no results (`[]`) then we will use your hard-coded fallback JSON if it exists.

> Your hard-coded JSON provided above will _not_ be run through the Scripting API (either for key enumeration or sample data fallback) so if you use the Scripting API to add or modify fields on top of your normal API response, you'll want to make sure you perform the same manipulations manually before pasting in the JSON above.

---

## Searches

**Searches** answer the question: _What records can I lookup by a particular query?_ They are things like:

- Find a Contact
- Find a Product
- Find an Issue

Searches can be useful on their own, or they can be combined with Actions to perform "Get or Create" style logic.

What a user sees:

![](https://cdn.zapier.com/storage/photos/10007490d50413c435666036699f453b.png)

What a developer sees:

![](https://cdn.zapier.com/storage/photos/c8612e5a2731a88f27f87b97dd5e6087.png)

See also: [Searches in the CLI](https://zapier.github.io/zapier-platform-cli/#triggerssearchescreates)

You can define your searches via your app's dashboard. When you create a new search, you'll be prompted with several options. Below we list all complete definitions of what each option is for.

### Search Options

### Name

This is a human readable label a user would see when browsing the directory and adding your app. Make it short but descriptive.

Example: <br/> `Find Contact` or `Find Ticket`

### Noun

This is the object that the search is most closely associated with. It will be a noun you used in the Name field. We rely on an accurate noun to generate human-friendly sentences for users.

Example: <br/> "Find Contact" would have "Contact" as the noun. "Find Completed Sale" would use "Sale" or "Completed Sale".

### Key

This is a field only really used internally for both [dynamic dropdown](#dynamic-dropdowns) and [Scripting](#scripting) references. Needs to be at least two characters long, start with an alpha, and only contain `a-z`, `A-Z`, `0-9` or `_`.

Example: <br/> `find_contact`, or `findContact`

### Help Text

A longer description of what this Search actually looks for. Point out any un-standard behavior as far as how searching happens.

Example: <br/> `Finds a contact by email address.`

### Hide

Usually you'll want to leave this unchecked. If you check it, we'll completely hide the search from the enduser. This can be useful if a search is incomplete, but you need to deploy your app in it's current state. This option is also a way to hide searches that become deprecated in your API.

### Search Endpoint

Define the URL route where we will, by default, `GET` for a list of results. Note that the results _must_ be an array, otherwise your search may fail. If there are no results, we expect an empty array. If your API returns a single object, you can use scripting to wrap the object in an array in a `_post_search` method. You can also make use of [variable syntax](#variable-syntax) where [auth fields](#auth-fields) and [search fields](#search-fields) will be injected.

Example: <br/> `http://api.example.com/v2/clients.json` or {% raw %}`http://{% templatetag openvariable %}account{% templatetag closevariable %}.example.com/api/v1/projects.json`{% endraw %}

> Note we'll only use the first object in the array for now, so if you can add optional fields to help narrow the search down, it's a great idea.

#### A Warning about encoding URL params

We will not automatically encode any URL variables, so you're responsible for encoding any if they require that. For example, emails _might_ include a `+` sign, so if you have {% raw %}`https://example.com/api/v2/leads?email={% templatetag openvariable %}email{% templatetag closevariable %}`{% endraw %} you'll want to encode that in your [`SEARCH_KEY_pre_search`](#available-methods/#search-methods) (or remove it from there and add it to the `bundle.request.params`), otherwise you'll get a "space" where the `+` sign is.

A better approach is to not even include it in the URL and to instead _only_ use `bundle.request.params` in this case since `bundle.request.params` will be encoded automatically.

### Custom Search Fields URL

This allows you to dynamically define search fields that are user set (IE: custom fields).

Example: <br/> {% raw %}`http://api.example.com/v2/fields.json` or `http://{% templatetag openvariable %}account{% templatetag closevariable %}.example.com/api/v1/fields.json`{% endraw %}

> Read more about [custom field formating here](#search-fields-custom).

### Resource URL

The URL we can use to fetch the full details of a Search result or (in the case of a Search or Action when no results are found) Create result. This is helpful because most searches only return a subset of a result's fields. It also ensures that regardless of it having found or created, the same data is returned.

If you leave this optional field blank, the raw Search or Create result will be used. You should only use this if the Search result has all relevant fields and you either configure no Search or Action or it returns the same fields as well.

You can make use of [variable syntax](#variable-syntax) where [auth fields](#auth-fields) and search result fields (not the actual [search fields](#search-fields)) will be injected.

Assuming your search would return something like:

```json
[
  {
    "id": 124
  }
]
```

And you configured this field with {% raw %}`https://api.example.com/v2/leads/{% templatetag openvariable %}id{% templatetag closevariable %}.json`{% endraw %} then we'd GET `https://api.example.com/v2/leads/124.json` to get the full result of the found or created item.

### Search Fields

Search Fields answer the question: what details can a user provide when setting up a Search?

These details might include:

- Name to query for a Contact _(EG: Salesforce)_
- Repo to restrict search to for an Issue _(EG: Github)_
- Notebook for a Note _(EG: Evernote)_

What a user sees:

![](https://cdn.zapier.com/storage/photos/7205a710c9e7a9a34a4235c52ff665ef.png)

What a developer sees:

![](https://cdn.zapier.com/storage/photos/69a1f969ea53cb987a4186432d11a227.png)

Each Search should have at least one Search Field, because otherwise we won't know what to include in the query.

You can also dynamically load custom Search Fields by inspecting a custom field endpoint of your own. [Learn more.](#search-fields-custom)

### Search Field Options

### Key

A key for you and your API's consumption. This is available for [variable syntax](#variable-syntax) in the Search URL field as well as in [Scripting](#scripting). Needs to be at least two characters long, start with an alpha, and only contain `a-z`, `A-Z`, `0-9` or `_`.

Example: <br>`room`

### Label

A human readable Label shown in the UI as a user works to complete a Search.

Example:<br>
`Email` or `Name`

![label help default](https://cdn.zapier.com/storage/photos/96522edc71e94085537c1fa70480adb8.png)

### Help Text

Human readable description of a Search field, useful for describing some detail you couldn't list in the Label.

Example:<br>
`Specify the first name to search by.` or `Restrict the search to contacts in this category.`

### Default

A default value for a field. The behavior varies between required and optional fields. For required fields, the default will be set once when the user first creates the Search, but it is not guaranteed after that (we raise an error on missing/null values instead). For optional fields, it is set on initial creation and used in place of missing or null values every time the Zap runs.

### Type

The type we will try to coerce to on the backend. Fails silently to ensure that tasks aren't dropped on coercion errors.

You can get a full list of supported types and the coercion implied here: [Field Types](#field-types).

### Required

If checked a user will not be able to continue without entering some value.

### Dynamic Dropdown

Use an existing [Trigger](#triggers) to load in values for selection, using the machine readable value your API consumes (like `id` or `hash`) while showing a human readable version to the user (like `name` or `itemName`).

Refer to our [dynamic dropdown docs](#dynamic-dropdowns) for a more in depth explanation.

Example:<br>
`TRIGGERKEY.id.name` or `TRIGGERKEY.hash.itemName`

![dynamic dropdown](https://cdn.zapier.com/storage/photos/9a6185121c22d1397dad62c819333f0e.png)

### Static Dropdowns

A comma separated string that will be turned into a select field for limiting the choices a user can provide to a Search field.

Example:<br>
`choice_a,choice_b,choice_c` or `Yesterday, Today, Tomorrow`

![simple static dropdown](https://cdn.zapier.com/storage/photos/7641c6b42a5034432f63274226e84414.png)

If you would like to provide a label for the raw value of each choice, you can also use the raw|label,raw|label syntax instead.

Example:<br>
`1|Option 1,2|Option 2`

![simple static dropdown as key-value pairs](https://cdn.zapier.com/storage/photos/524ad1774802cc81d95cb2e3f23972d6.png)

### List

Indicates if this field can hold multiple values. For example, this could be useful if you want to allow users to search for a contact by name, but limit the search to contacts with one or more tags applied. List fields gain the +/- icons to the side.

![list field example](https://cdn.zapier.com/storage/photos/580a778c672cf2a686b4b1463ad8f84e.png)

### Search or Create

Search or Create allows users to combine your Searches and your Actions together into one flow. Each Search may be associated with one Action, which represents the creation of the same type of object that search is used to look up. (Practical example [here](https://zapier.com/developer/documentation/v2/search-or-create-example))

Example use cases might include:

- Find or create a new customer _(EG: Salesforce)_
- Notebook for a Note _(EG: Evernote)_

What a user sees:

![](https://cdn.zapier.com/storage/photos/6e1006df30e029df1c4880c3090d7fb4.png)

What a developer sees:

![](https://cdn.zapier.com/storage/photos/7c12e7cbdaaf76ad2c5c33c47eecb6cc.png)

The user's UI is built using a combination of the `label` above and the related `label` and `noun` from the single Search and Action.

At this point, when the user selects the checkbox to do a Find or Create, they will be given the option to fill in both the fields for the search, as well as the fields for the create.

When the Zap runs, if an element is found during the Search, it will be used. If not, a new item will be created.

> Errors like a 404 will not be interpreted as a "miss" on search and will not trigger a follow up create - explicitly return `[]` when no records are found.
> If your API can't do that, use scripting to return an empty list `[]` (note a `_post_search` won't work, you'll have to replace `_search` completely)

This type of connection should be used in cases where the search is likely to yield one correct result, and unlikely to yield incorrect results. Good use cases include searching by keys like `email` or `phone number`, or other uniquely identifying information that the user might have.

After every successful Search or Create - we'll attempt to grab a fresh record via the [Resource URL](#searches/#resource-url).

### Search Fields (Custom)

A natural extension of normal hard coded [search fields](#search-fields) are dynamic search fields, or custom fields. Custom fields are very commonly used in services that allow users to create their own data fields. Examples include contacts in CRMs, form management apps, or ticket fields in helpdesk software. These apps will assign a generated unique key to the field, while storing information about the field, such as its human readable label and data type, separately. Working with this data requires an extra step to retrieve that field metadata in order to allow users to make sense of the information.

All you need to do to enable custom fields is:

- Provide a Custom Search Fields URL for your search action.
- Ensure the URL route returns data in the below format, or manipulate it to fit with [Scripting](#scripting).
- You can choose from several internal types, documented here: [Field Types](#field-types).

```javascript
[
    {
        "type": "unicode",
        "key": "json_key", // the field "name", will be used to construct a label if none is provided
        "required": false, // whether this field must be filled out. defaults to true
        "label": "Pretty Label", // optional
        "help_text": "Helps to explain things to users.", // optional
        "choices": { // optional
            "raw": "label"
        } // can also be a flat array if raw is the label
     },
     ...
 ]
```

### Custom Search Result Fields

If your search action **returns** custom fields you'll also want to configure a source for labels so other actions in multi-step Zaps can display those fields properly and allow users to correctly use the data in the Zap editor.

- Provide a Custom Search Result Fields URL for the search action. (This will likely be the same endpoint you used for Custom Search Fields)
- Ensure that the URL route returns data in the below format, or manipulate it to fit with [Scripting](#scripting). Extra data will be ignored, but we require at least the following to properly format your search action results.

```javascript
[
    {
        "type": "unicode",
        "key": "json_key", // the field "name", will be used to construct a label if none is provided
        "label": "Pretty Label",
    },
    ...
]
```

> Right now `parent_key` and `type=dict` is not supported in custom fields.

### Search Sample Results

(This works similar to [trigger sample results](#trigger-sample-results)

To help give users a smooth experience when creating multi-step Zaps, we ask that you paste a JSON object that contains the fields (along with sample values), so that your user can map those fields into the next step.

We will use this sample JSON for two things:

1. To detect a list of hard-coded key names which the user can pick from during Zap setup
2. To use as a hard-coded fallback for sample data so that we can provide fields to insert during Zap setup (if your API returns 0 results)

> These result is primarily used when the user picks "Skip Test" when testing their Zap. Zapier will try to use a live API result, first.

Here is the sample JSON for something like an search for a Trello Card, and how it shows up in our user-facing Editor:

```javascript
{
  "name": "Some Card",
  "url": "https://trello.com/c/YZSaTvjM/59-some-card",
  "id": "5642335fa1041c95e73f290b",
  "idList": "55159df870b769081c4a8e82",
  "pos": 65535
}
```

We will parse this sample and provide dropdowns like this to the user:

![samples](https://cdn.zapier.com/storage/photos/b4944d943c0e6362a269937cc7683493.png)

By default, we can handle flat dictionaries and dictionaries within dictionaries (via our `__` delimiter in keys).

When the user is inserting fields in the Zap editor, and your API returns no results (`[]`) then we will use your hard-coded fallback JSON if it exists.

> Your hard-coded JSON provided above will _not_ be run through the Scripting API (either for key enumeration or sample data fallback) so if you use the Scripting API to add or modify fields on top of your normal API response, you'll want to make sure you perform the same manipulations manually before pasting in the JSON above.

---

## How to Launch an Integration

### Deploy

Once your app is live (Public or Invite-Only), you'll probably want to make changes to it and add features or fix bugs. While you cannot make changes to a live app, you can **clone** an app and then make changes to the clone.

The first step is to click on the **Deployment** tab, and click the button **Make a Copy of Your App by Cloning**:

![deployment tab](https://cdn.zapier.com/storage/photos/33152753d89d0cded407d67c09387d04.png)

In the new/cloned app, make your changes. Be sure to leave this app in the **Private** status!

When you've finished testing your changes, and are ready to update the existing/public app, go into the new/cloned app, click on the **Deployment** tab, and click the button to **Deploy and Replace an Existing App**.

> Once you have deployed your new/cloned app to replace an existing app, all zaps will be updated to use this new app. Read on for important notes on handling breaking app changes.

> Do you need to change the name of your invite-only or public app? Please [contact us](mailto:partners@zapier.com) and we'll perform a manual deployment.

A screen will ask you which app you want to replace. Select the existing/live app:

![select app](https://cdn.zapier.com/storage/photos/45db411d9bf081d9954f3c0d147e979a.png)

The system will run an audit and show you the results:

![deploy page](https://cdn.zapier.com/storage/photos/48aca3cc40273674cff94b58e4268338.png)

In the screenshot you can see an error for **New Item**, with the error of _Polling triggers should always have sample data_. This simply means you need to provide a sample result for a polling trigger.

Usually you can just make some changes and ensure there is a symmetry between old and new versions of the app. If there is a breaking change that resolves a bug, please [contact us](mailto:partners@zapier.com) and we'll perform a manual deployment.

There are a number of situations where making changes in your app may cause the existing Live Zaps to stop working. If any of those situations are detected, the system will not allow you to complete the deploy/replace process. Please visit [this page of Deploy Errors](https://zapier.com/developer/documentation/v2/deploy-errors) and try a workaround.

If your app is Invite-Only, your cloned app's OAuth redirect URI will become active upon migration (it will contain a new ID #), and the old OAuth redirect URI will no longer function.
**Please plan accordingly.** Contact us for a solution to this problem if it is difficult to manage - we can set a permanent redirect URI for your app.

#### How to Handle Breaking Changes

The best approach is to copy the Triggers/Actions/Searches you want to update. Mark the originals hidden and append "(Legacy)" to their labels. On the copies, make the needed updates (it also helps to update their keys to something instructive, like append "\_v2" to the original key). Once you deploy, new Zaps will only have the copies available and old Zaps will continue to work unaffected.

If you're working on an entirely new version of your app/integration, which doesn't preserve any compatibility with the existing app/integration, you can [learn more about the process of getting the new app deployed here.](https://zapier.com/developer/documentation/v2/migrating-your-zapier-integration)

#### Deploy in process

If all goes well and you have no warnings when trying to deploy, a deploy process will start asynchronously and you can come back to the **Deployment** tab to check on its progress.

### Monitoring

You can access Monitoring by clicking the "Monitoring" tab on your App's details.

![](https://cdn.zapier.com/storage/photos/6ea3644f8c93f0058849bdf7086b3cfc.png)

This section is meant to allow you to quickly understand if your app is OK or not, by checking and comparing types of events (ideally you want to see a lot of 2xx - green, and no errors - red).

**NOTE:** The monitoring information is less useful for services/endpoints that consistently return an `HTTP 200` status, and contain a payload with an error message.

If you have access to it, you can click on a data point in the chart and get details about up to 500 events for the chosen period.

If you have too many events, you can use the filters on the right side to filter which events will be displayed on the list once you click a data point.

This is useful for mainly for debugging purposes.

### Clone

Once your app is live (Public or Invite-Only), you'll probably want to make changes to it and add features or fix bugs. While you cannot make changes to a live app, you can **clone** an app and then make changes to the clone.

To clone your app, click on the **Deployment** tab in your app editor, and click the button **Make a Copy of Your App by Cloning**:

![deployment tab](https://cdn.zapier.com/storage/photos/1f74f5bbc1882abfee42fd15a1c477fe.png)

A cloned app will begin in Private mode, which allows you to make your edits. If you wish to use the cloned app to replace your previous app (either Public or Invite-Only), you'll want to [deploy a replacement](#deploy).

---

## Dates in Zapier

### Datetimes in Triggers

For triggers, please supply any date-related fields in [ISO-8601](https://en.wikipedia.org/wiki/ISO_8601) format. We do our best to parse a variety of datetime formats.

Examples of valid [ISO-8601](https://en.wikipedia.org/wiki/ISO_8601)-formatted values:

- `2018-05-17T13:04:00-0700` (time zone offset must be specified)
- `2018-05-17T13:04:00-07:00` (time zone offset specified with a colon)
- `2018-05-17T13:04:00-0000` (UTC time zone)
- `2018-05-17T13:04:00Z` (`Z` can be used instead of `-0000`)
- `2018-05-17` (single date without a time may be used, but note that a time of "midnight" may be implicitly applied if the value is used in subsequent steps)

### Datetimes in Actions

For actions, datetimes are normalized to an [ISO-8601](https://en.wikipedia.org/wiki/ISO_8601) formatted string. For details, see the [datetime field type](#field-types/#datetime). An example: a user has a Zap between Wufoo and Mailchimp. The Wufoo "new entry" trigger supplies a UNIX epoch timestamp field. If the user maps the datetime field from Wufoo into Mailchimp, it will be supplied to Mailchimp as a string, formatted like `2015-03-05T01:00:00Z`.

If you need a different date format (like epoch as int) - you'll need to use our scripting platform to do a conversion using the globally available [Moment.js](https://momentjs.com) library (web builder apps only). If you're building using our CLI, you can use any library of your choosing.

---

## Files in Zapier

Zapier supports some limited file operations via both triggers and actions, though they behave a bit differently depending on what you want to do. At a high level, this is what you can expect:

### Triggers via URLs/Dehydration

> This is how you'd surface a file hosted by your app, so other apps can consume it.

If your files aren't private (IE: they have a public route), just provide the URL in the normal payload (right alongside `id`, `name`, etc.). Our system is smart enough to download public URLs when they get used like a file!

However, if the files are behind authentication, you can define a route for us to retrieve the file at some time in the future and we'll attempt the normal style of authentication:

```javascript
var Zap = {
  your_trigger_post_poll: function(bundle) {
    var records = z.JSON.parse(bundle.response.content);
    return _.map(records, function(record) {
      // if you just do url, we'll include any standard authentication headers
      record.file = z.dehydrateFile(
        "https://yoursite.com/files/download/" + record.id
      );
      return record;
    });
  }
};
```

You can also define a more specific request if there is more data you need to provide to activate the download, like a special key or checksum:

```javascript
var Zap = {
  your_trigger_post_poll: function(bundle) {
    var records = z.JSON.parse(bundle.response.content);
    return _.map(records, function(record) {
      // if you provide the full request, we will NOT include
      // any standard authentication headers
      var url = "https://yoursite.com/files/download/" + record.id;
      record.file = z.dehydrateFile(
        url,
        {
          method: "post",
          headers: {
            "X-Download-Key": record.key
          }
        },
        {
          name: record.fileName, // if blank we will guess/inspect!
          length: record.size // if blank we will guess/inspect!
        }
      );
      return record;
    });
  }
};
```

And we'll handle the rest!

### Actions via Multipart

> This is how you'd accept binary data to be uploaded to your app, the data is coming from some other app.

Downloading files is a little simpler than uploading them, so files in actions is a bit more involved. By default we attempt multipart uploading and include the original JSON right alongside, but you can (of course) tweak this with the developer platform.

Let's assume your API can accept JSON as well as JSON + multipart for attachments, if you set up this action:

![](https://cdn.zapier.com/storage/photos/05bf2cf6a68f34733832a963f7d678c9.png)

You can expect this request to be sent by default (no scripting required at all):

```
POST https://yoursite.com/files/upload

Content-Type: multipart/form-data; boundary=f94636b7375c4a37862029d4dc8bafe7


--f94636b7375c4a37862029d4dc8bafe7
Content-Disposition: form-data; name="data"
Content-Type: application/json; charset=utf-8

{"path": "/user/provided/path", "delete_date": "2014-10-10T13:59:36"}
--f94636b7375c4a37862029d4dc8bafe7
Content-Disposition: form-data; name="file_to_upload"; filename="user-provided-file.pdf"
Content-Type: application/pdf

<BINARY DATA HERE>
--f94636b7375c4a37862029d4dc8bafe7--
```

> The `name="data"` key for the JSON subtype in `multipart/form-data` is the default, though the rest of the multipart files will respect your action field keys.

### Limited Customization Via Scripting

If you have some other method of uploading files, you'll need to break out the scripting platform. Probably the most common way to tweak the upload is with the classic `pre_write` method.

A popular alternative pattern is likely just a pure `multipart/form-data`, no JSON at all. We support that just fine, just remove the `Content-Type` and return an object as `request.data`:

```javascript
var Zap = {
  your_action_pre_write: function(bundle) {
    // bundle.request.files is an object of strings: arrays
    // bundle.request.files.file_to_upload is an array:
    // * first item is the filename, if any
    // * second item is a zapier.com endpoint that will stream the file
    // * third item is the mimetype, if any

    bundle.request.headers["Content-Type"] =
      "application/x-www-form-urlencoded";
    // leave request data as object, not string!
    bundle.request.data = z.JSON.parse(bundle.request.data);
    // we will mix request.data and request.files together
    return bundle.request; // let zapier complete it
  }
};
```

That pure `multipart/form-data` raw request will now look like this:

```
POST https://yoursite.com/files/upload

Content-Type: multipart/form-data; boundary=0c61d2f9bd1a4675a2db6afe21f230f1


--0c61d2f9bd1a4675a2db6afe21f230f1
Content-Disposition: form-data; name="path"

/user/provided/path
--0c61d2f9bd1a4675a2db6afe21f230f1
Content-Disposition: form-data; name="delete_date"

2014-10-10T13:59:36
--0c61d2f9bd1a4675a2db6afe21f230f1
Content-Disposition: form-data; name="file_to_upload"; filename="user-provided-file.pdf"
Content-Type: application/pdf

<BINARY DATA HERE>
--0c61d2f9bd1a4675a2db6afe21f230f1--
```

> All name keys respect the keys provided.

### Advanced Streaming via Scripting

At this time we do not support advanced streaming of files via the scripting platform (for example, uploading a file to receive an attachment ID that gets mixed into the normal JSON for POSTing). We may support that in the future, please [let us know](https://developer.zapier.com/contact) if you have questions!

---

<a id="variable-syntax"></a>

## Zapier Variable Syntax

If you've used [Django](https://www.djangoproject.com) or [Mustache](http://mustache.github.com) (or many other templating engines), you are probably well versed in the variable syntax we use. This also happens to be the exact same syntax our users use to map data from triggers into [Action Fields](#action-fields) (though they get a dropdown interface to do it).

Given the following context (think [authentication fields](#authentication-fields) or data from triggers):

```javascript
{
  "id": 123456,
  "owner": "Larry",
  "title": "Hello world!",
  "description": "It's a beautiful day!"
}
```

And the following template (think [authentication mapping](#authentication-mappings) or [action fields](#action-fields)):

{% raw %}```javascript
{
"talking_user": "{% templatetag openvariable %}owner{% templatetag closevariable %}",
"chat_message": "{% templatetag openvariable %}title{% templatetag closevariable %} and of course {% templatetag openvariable %}description{% templatetag closevariable %}"
}

````{% endraw %}

We will generate the following output:

```javascript
{
  "talking_user": "Larry",
  "chat_message": "Hello world! and of course It's a beautiful day!"
}
````

The keys to put between the {% raw %}{% templatetag openvariable %}{% templatetag closevariable %}{% endraw %} come from the keys you specify when you setup [action fields](#action-fields), [trigger fields](#trigger-fields), and [authentication fields](#authentication-fields).

---

<a id="versions"></a>

## Legacy Web Builder Versions

Below is a changelog of the major releases of the Zapier Legacy Web Builder Platform. Each release has a summary of the new features added and any breaking changes that were made.

### Version 2 (2015-07-31)

This is a backward incompatible update to the Developer Platform. It adds several new features and fixes some of the limitations of the first version.

- Apps can now have [Searches](#searches). A Search is used to find individual records by a field (say finding a contact by name).
- Searches can be linked with Actions to create a [Search or Create](#search-or-create) flow, giving the user a way to search for an item, and if it doesn't exist, create it.
- Searches can be used to power action fields, similar to Dynamic Dropdowns. Users input data to the field which is used to search for items, and a given data element returned from the search result (such as `id`) is used in place of their input.
- Fields can now have the “List” property defined through the UI. Before this was only possible to set via Scripting.
- Action fields have a “Parent Key” option that enables line item support.
- Fields now have a "Placeholder" option that operates solely as an HTML5 style placeholder - it is only for helping the user understand what will happen if they enter nothing in the given field.
- **Breaking Change** Scripting can no longer access `trigger_data` from `bundle` in `pre_write` and `post_write`.
- **Breaking Change** Scripting can no longer access `trigger` and `action` from `bundle.zap`.
- **Breaking Change** Scripting code now runs under JS strict mode (`'use strict';`), so developer should verify their code still executes correctly (the built in code editor runs jshint - so check there!)
- **Breaking Change** Data mapped into Action Fields is always coerced according to the field's type
- **Breaking Change** Data entering actions is no longer flattened into a string. This means lists and dictionaries will pass through to actions intact rather than being converted to CSV and 'key|value' respectively. If there is existing Scripting code that does any sort of parsing on those values, it will need to be updated to handle the new structure (likely this means deleting code that was expanding the strings back into arrays and dictionaries).
- **Breaking Change** We now automatically include a `state` parameter on the Authorization URL for apps that use OAuth2.
- **Bug Fix** Trigger fields passed into custom fields, REST hook and catch hook methods are always coerced according to the field's type

### Version 1 (2012-08-01)

The initial launch of the platform.
