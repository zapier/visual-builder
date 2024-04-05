---
title: Partner API
order: 3
layout: post-toc
redirect_from:
  - /partner_api/authentication
  - /partner_api/examples
  - /partner_api/changelog
  - /partner_api/errors
  - /partner_api/endpoints
  - /partner_api/best-practices
  - /embed/partner-api-examples
  - /embed/partner-api-endpoints
  - /embed/zap-editor
  - /embed/prefill-zaps


---

# Partner API

The Partner API is the best tool for complete style control over a user's Zapier experience within your app. It allows you to customize how you present Zapier within your product without sacrificing your app's look, feel, and flow.

Think of it as a native Zapier integration, helping you showcase your best Zapier-powered workflows where it's most helpful to your users (within the flow of your tool). Customize styling, streamline Zap set-up for users and expose relevant Zap information.

Embed features are available for public integrations. To enable embed features, [update your Intended Audience](https://platform.zapier.com/quickstart/private-vs-public-integrations) to public and [submit your integration for review](https://platform.zapier.com/publish/public-integration#4-submit-your-integration-for-app-review) to be published in the Zapier App Directory. 

Once your integration is public, the integration's client ID needed to call the Partner API will be revealed under the `Embed > Settings` or `Embed > Partner API endpoints` section of that integration in the [Developer Platform](https://developer.zapier.com/).

## Highlighted capabilities

- Get a list of all the apps available in Zapier’s app directory to power your own app directory and show your users all the integration possibilities with your Zapier integration.
- Have complete style control over how you present Zap templates in your product. The Partner API gives you access to the raw Zap Template data so you can give your users access to your Zap template with your product’s style, look and feel.
- Get access to all your Zap templates and give your users the ability to search to quickly find the one they need.
- Streamline Zap setup by pre-filling fields on behalf of your users.
- Show users the Zaps they have set up from right within your product, keeping them on your site longer and giving them complete confidence in your Zapier integration.
- [Embed our Zap Editor](https://platform.zapier.com/embed/zap-editor) to allow your users to create new Zaps and modify existing ones, without needing to leave your product.

## Partner API implementation examples

Jotform uses the `/apps` endpoint to power their own app directory by intertwining the thousands of public integrations on Zapier's directory with their native integrations:

<iframe allowtransparency="true" title="Wistia video player" allowFullscreen frameborder="0" scrolling="no" class="wistia_embed" name="wistia_embed" src="https://fast.wistia.net/embed/iframe/qk2x3cwnzt" width="640" height="360"></iframe>


Wufoo uses the `/zap-templates` endpoint to retrieve raw data about their Zap Templates to customize the look and feel of how they are surfaced to users within their own integration directory:

<iframe allowtransparency="true" title="Wistia video player" allowFullscreen frameborder="0" scrolling="no" class="wistia_embed" name="wistia_embed" src="https://fast.wistia.net/embed/iframe/j8t914xl0y" width="640" height="360"></iframe>


Unbounce uses the `/zaps` endpoint to display users' Zaps using their integration directly within the Unbounce platform:

<iframe allowtransparency="true" title="Wistia video player" allowFullscreen frameborder="0" scrolling="no" class="wistia_embed" name="wistia_embed" src="https://fast.wistia.net/embed/iframe/zhls72cz15" width="640" height="360"></iframe>

Explore more live examples and success stories in our [Partner Embed Gallery](https://zapier.com/developer-platform/partner-embeds).

## Embed Zap editor with Partner API

With an embedded Zap editor in your product, your users can create and edit their Zaps without leaving your app.

### Prerequisites

- Your app has passed the review process and is Published in the Zapier App Directory
- Any [Zap templates](https://platform.zapier.com/publish/zap-templates) you want to query have been reviewed and made public 

### Example implementation

This video shows how Paperform prefills Zaps for their embedded Zap editor with contextual data from the platform, such as the Form ID, to make Zap setup easier for users. By doing so, Paperform reduces the number of clicks it takes for users to publish a Zap and removes mental friction of users needing to remember details for it:

<iframe allowtransparency="true" title="Wistia video player" allowFullscreen frameborder="0" scrolling="no" class="wistia_embed" name="wistia_embed" src="https://cdn.zappy.app/0625a071fbee914968480b0b58d696a8.mp4" width="640" height="360"></iframe>


### Option 1: Create Zaps from Zap Templates

Use the Partner API to query the public Zap templates featuring your integration (using the [`GET /v1/zap-templates`](https://platform.zapier.com/embed/partner-api) endpoint) and feature them in your product. When a user chooses a Zap template they’d like to try, use the `create_url` value as the source to load in an embedded frame such as:

```html
<iframe src="https://api.zapier.com/v1/embed/trello/create/113"></iframe>
```

Where `https://api.zapier.com/v1/embed/trello/create/113` is the `create_url` value of the Zap template.

Optionally, you can add additional parameters to the `create_url` to [prefill the user’s Zap](https://platform.zapier.com/embed/prefill-zaps) with custom values (e.g., specifying a workspace for the trigger to filter by).

### Option 2: Create Zaps without Zap Templates

You can also facilitate a user's Zap creation via URL parameters instead of an existing Zap Template. This provides flexibility to redirect users to a pre-populated Zap editor with known context from your app without publishing a Zap Template for each specific use case.

[Use the generator](https://platform.zapier.com/embed/prefill-zaps) under the _Embed_ and _Pre-filled Zaps_ tabs in the Platform UI to easily construct pre-filled Zaps for your embedded editor experience or as a lightweight entry point into the Zap editor from your app. 

### Editing existing Zaps

Use the Partner API to load a user’s Zaps (using the [`GET /v1/zaps`](https://platform.zapier.com/embed/partner-api) endpoint). When the user chooses to open or edit a Zap use the the `url` value of the Zap as the source of an embedded frame like this:

```html
<iframe src="https://zapier.com/app/editor/123456"></iframe>
```

Where `https://zapier.com/app/editor/123456` is the `url` of the Zap to be edited.

If you prefer, you can open these URLs in a separate window, new tab, or popup from your app.

### `postMessage` events

If you decide to embed the Zap editor within your product you can listen to [message events from `postMessage`](https://developer.mozilla.org/en-US/docs/Web/API/Window/message_event) to help you improve the interactivity with the iframe (e.g. automatically close the iframe modal.)

The messages available include:

- `zap:unpause` = Zap turned on / published
- `zap:unpause:done` = Zap turned on / published (success)
- `zap:unpause:fail` = Zap turned on / published (failure)
- `zap:pause` = Zap turned off
- `zap:pause:done` = Zap turned off (success)
- `zap:pause:fail` = Zap turned off (failure)

### Turning off a Zap

The API does not currently have an endpoint to turn off/on a user's Zaps. If your Zapier app uses [Webhook Subscriptions](https://platform.zapier.com/build/hook-trigger), you can send a `DELETE` to the unique target URL that was provided when the subscription was created and that will then pause/turn off a Zap.

## Embed pre-fill Zaps with Partner API

Prefills allow you to define the input fields on behalf of the user, thus simplying the experience of setting up their Zap.

### Prerequisites

- You will need to know the required input fields per trigger or action step. You can find the fields as defined in your Zapier integration.

### Create Zap with pre-filled fields

Use the `create_url` (available in a [Zap template object](https://platform.zapier.com/embed/partner-api)) in order to create the Zap. 

Next, add parameters to the `create_url` so that the user's Zap is prefilled with the provided custom values.

#### Example with single app

You can prefill the name of a Trello card (field: `name`) in the second step of the Zap template:

> `https://api.zapier.com/v1/embed/trello/create/113?steps[1][params][name]=hello`

- `template=113`
- `steps[1][params][name]=hello`

Here's what it would look like in the editor:

![Zap Editor showing "hello" pre-filled into the name field of a new Zap titled Create Card in Trello](https://cdn.zappy.app/5db273249f668a1520e1632cf331a141.png)

You can prefill multiple values for the user. In this example `name` and `desc` are prefilled

> `https://api.zapier.com/v1/embed/trello/create/113?steps[1][params][name]=yoyoyo&steps[1][params][desc]=yeehaw`

- `template=113`
- `steps[1][params][name]=yoyoyo`
- `steps[1][params][desc]=yeehaw`

![Zap Editor showing "yoyoyo" pre-filled into the name field, and "yeehaw" pre-filled into the description field of a new Zap titled Create Card in Trello](https://cdn.zappy.app/35882f8b86dade9e41c13cdbd0baf03c.png)

You can provide a label for prefill dropdowns as we won't fetch all of the pages of choices until the user opens the dropdown:

> `https://api.zapier.com/v1/embed/trello/create/113?steps[1][params][board]=1234&steps[1][meta][parammap][board]=Test`

- `template=113`
- `steps[1][params][board]=1234`
- `steps[1][meta][parammap][board]=Test`

![Zap Editor showing "Test" pre-filled into the board field of a new Zap titled Create Card in Trello](https://cdn.zappy.app/fd9fd4872773018bfd15dfebea0795a4.png)

#### Example with multiple apps

Similarly, you can prefill apps, events, and input field values in the Zap Editor with the following URL schema:

Base URL: `https://api.zapier.com/v1/embed/{your_app}/create` - you can find `{your_app}` by using the [Prefill Generator](https://platform.zapier.com/embed/prefill-zaps#using-the-pre-filled-zap-generator)

##### URL parameters (with example values)

- Trigger app (required): `steps[0][app]=MailchimpCLIAPI@latest` 
- Trigger event: `steps[0][action]=new_member`
- Trigger field prefills: `steps[0][params][list_id]=123`
- Action app: `steps[1][app]=GoogleAdsCLIAPI@latest`
- Action event: `steps[1][action]=add_to_customer_list_v2`
- Action field prefills: `steps[1][params][list_id]=234`

##### Requirements

- A trigger app is required. The `steps` index for a trigger is always `0`.
- Use `app_latest` values from the [`/apps` endpoint](https://platform.zapier.com/embed/partner-api#get-v1apps) of the Partner API to define an app. This is case-sensitive, so use exactly the value returned from the API.
- You can define 0 to many subsequent action steps. The `steps` index for actions will be `1` or greater. Please note, only users on a paid Zapier plan have access to multi-step Zaps.
- Events are defined by the `key` of the trigger, action, or search.
- Field prefills are defined by the `key` of the input field. 

##### Examples

Defining a trigger and action app
> `https://api.zapier.com/v1/embed/{your_app}/create?steps[0][app]=MailchimpCLIAPI@latest&steps[1][app]=GoogleAdsCLIAPI@latest`

Defining a trigger and trigger event with no action:
> `https://api.zapier.com/v1/embed/{your_app}/create?steps[0][app]=MailchimpCLIAPI@latest&steps[0][action]=new_member`

Defining a trigger and trigger event with a prefilled value for the "Audience" input field:
> `https://api.zapier.com/v1/embed/{your_app}/create?steps[0][app]=MailchimpCLIAPI@latest&steps[0][action]=new_member&steps[0][params][list_id]=123`

Defining a trigger, trigger event, action, and action event with prefilled values for "Audience" and "Customer List" input fields:
> `https://api.zapier.com/v1/embed/{your_app}/create?steps[0][app]=MailchimpCLIAPI@latest&steps[0][action]=new_member&steps[0][params][list_id]=123&steps[1][app]=GoogleAdsCLIAPI@latest&steps[1][action]=add_to_customer_list_v2&steps[1][params][customer_list_id]=234`

Defining a multi-step Zap with a trigger and two actions:
> `https://api.zapier.com/v1/embed/{your_app}/create?steps[0][app]=MailchimpCLIAPI@latest&steps[1][app]=GoogleAdsCLIAPI@latest&steps[2][app]=FacebookLeadAdsCLIAPI@latest`

### Use the pre-filled Zap generator

The UI-based generator in the Platform UI facilitates constructing pre-filled Zaps. 

**Pre-filled Zaps are simply URLs with field values added as parameters,** which you can use to direct users to the Zap editor with some input fields already filled. Place these URLs inside your product or within an embedded Zap editor to facilitate users creating and publishing Zaps.

Find the pre-filled Zap generator under the _Embed_ and _Pre-filled Zaps_ section of the Platform UI.

![Screenshot of pre-filled Zaps tab](https://cdn.zappy.app/2a4f9c6de6c525cbcdc1b513ec88c519.png)

#### Create a pre-filled Zap using the generator

- Select an app and event for both the trigger and action to see the fields you can pre-fill. If no fields appear, the event has no input fields.

![Screenshot of generator trigger step setup](https://cdn.zappy.app/87b9c4951d55298780ff209e217bb750.png)

- Select the fields you want to pre-fill:
  - If you don’t want to pre-fill the field, leave the box unchecked. In the Zap, the field will be empty or set to a default value, if there is one.
  - If there's a static value for a field that applies to every user's Zap (like the title of an email), check the field and provide the value in the text field.
  - If the values are dynamic or you don’t know them yet, replace the placeholders represented in curly brackets (i.e {TRIGGER_LIST_ID}) in the generated URL from Step 2 before using it in your app. This could be something like an account or list ID field. The placeholder serves as a reminder to replace the value at runtime.
  - If the field is greyed out, it requires a complex field value and cannot be pre-filled.

![Screenshot of prefill input field options](https://cdn.zappy.app/9e845182506292214c866f3278861e8d.png)

_Note: fields denoting **(required)** are required for turning the Zap on, not required to be pre-filled._

- Test the Zap! Use the handy test button to make sure the resulting Zap is what you intended. You'll need to connect app accounts on both steps to see the pre-filled fields.
- Copy the code and embed it inside your app to make setting up a Zap easier and faster for users.

The generator only supports creating 2-step Zaps, but you can construct multi-step Zaps by building upon the generated URL and adding `steps` parameters with increased indeces.
 
You also cannot prefill an action field with data returned from the trigger. In this case, use [pre-filled Zaps with Zap Templates](https://platform.zapier.com/embed/zap-editor).

## Partner API endpoints

### Authentication

There are two ways to authenticate to the Partner API.

1. Your application's `client_id` which is available once you are approved for access to the API by publishing your app in Zapier's [App Directory](https://platform.zapier.com/quickstart/private-vs-public-integrations). This method only works for certain `v1` endpoints.
2. A user's access token

The authentication method you should use depends on which endpoint(s) you are using. Review each endpoint's documentation to understand which parameters are required.


#### Access token

The Zapier Partner API uses [OAuth 2.0 authentication with the authorization code grant type](https://developer.okta.com/blog/2018/04/10/oauth-authorization-code-grant-type). At the end of the Oauth authentication code flow, you'll get a user access token that you'll pass in a header with each API request.

##### Prerequisite 1: Configure a redirect URI

> You will only be able to configure redirect URIs after you've published your app as a [public integration in Zapier's App Directory](https://platform.zapier.com/quickstart/private-vs-public-integrations).


You can configure one (or multiple) **redirect URIs** in the [Zapier Developer Platform](https://developer.zapier.com/) under `Embed`→`Settings`→`Redirect URIs`

![Configure redirect URIs](https://cdn.zappy.app/f8fbb9cf76864f457a0132b7eb8db196.png)

##### Prerequisite 2: Get your Client ID and Client Secret
>Your application's **Client ID** and **Client Secret** are only available after you've published your app as a [public integration in Zapier's App Directory](https://platform.zapier.com/quickstart/private-vs-public-integrations).

You can find your **Client ID** and **Client Secret** in the [Zapier Developer Platform](https://developer.zapier.com/) under `Embed`→`Settings`→`Credentials`

![Client ID and Secret](https://cdn.zappy.app/cb3660c17a3d26b36f438ab80c0860d5.png)

---

##### 1. Determine which OAuth scopes are required for your use case
The various endpoints of the Zapier Partner API require different OAuth scopes. See the [API Reference](/api-reference/actions/get-actions) for documentation regarding which OAuth scopes are required by which endpoints.
![OAuth Scope documentation example](https://cdn.zappy.app/3667a31edfb56bc1187739d8b1303c5c.png)

##### 2. Initiate the OAuth flow and get the user's permission.
Construct a URL like the one below (with your own redirect url, client id, OAuth scopes, etc.) and open a browser to that URL.
```js
https://zapier.com/oauth/authorize
    ?response_type=code
    &client_id={YOUR_CLIENT_ID}
    &redirect_uri={YOUR_REDIRECT_URI}
    &scope={YOUR_OAUTH_SCOPES}
    &response_mode=query
    &state={RANDOM_STRING}
```
Here's an explanation for each query parameter:
* `response_type=code` - This tells the authorization server that the application is initiating the authorization code flow.
* `client_id` - The public identifier for your application. This will be the same client id that you retrieved earlier.
* `redirect_uri` - Tells Zapier's authorization server where to send the user back to after they approve the request. This should be the redirect URI that you configured earlier.
* `scope` - One or more space-separated strings indicating which permissions your application is requesting. The OAuth scopes required for specific endpoints are documented in the Partner API Reference.
* `state` - Your application generates a random string and includes it in the request. It should then check that the same value is returned after the user authorizes the app. This is used to prevent CSRF attacks.

A full example would be:
```js
https://zapier.com/oauth/authorize
  ?response_type=code
  &client_id=5672067294567789354752
  &redirect_uri=https%3A%2F%2Fyour-app.com%2Fcallback
  &scope=zap%20zap:write%20authentication
  &response_mode=query
  &state=tney4952
```

When the user visits this URL, Zapier's authorization server will present them with a prompt asking if they would like to authorize your application's request.
![OAuth prompt example](https://cdn.zappy.app/a58205b77ec7e6aa52226354af296125.png)


##### 3. Receive a Redirect at your Redirect URI
If the user approves the above request, then Zapier's authorization server will redirect the browser back to the `redirect_uri` that you specified and configured earlier. Two query string parameters, `code` and `state` will also be included.

For example, the browser would be redirected to:
```js
https://your-app.com/redirect
    ?code=dfJ2KuL0vKLRCwQIOL5NDGKQ&H9mlc
    &state=tney4952
```
* The `code` value is the **authorization code** generated by Zapier's authorization server. In the next step, you'll exchange this code for an access token. Keep in mind that authorization codes are only valid for 2 minutes, and you'll need to do the exchange within that window of time to avoid errors.
* The `state` value should match the state query parameter that you used in step 2. Your application should verify that these values match.

##### 4. Exchange authorization code for an access token
The final step is to exchange the **authorization code** that you just recieved for an **access token** that can be used to make authorized requests to the Zapier Partner API. You make the exchange with a `POST` request to Zapier's token endpoint `https://zapier.com/oauth/token/`.

Below is an example of a cURL request that can be used to do the exchange. Though, in reality, you would make the exchange request in your application code.
```cURL
curl -v -u {CLIENT_ID}:{CLIENT_SECRET} \
-d "grant_type=authorization_code&code={AUTHORIZATION_CODE}&redirect_uri={REDIRECT_URI}" \
https://zapier.com/oauth/token/
```
* `CLIENT_ID` - This will be the same client id that you retrieved earlier.
* `CLIENT_SECRET` - This is a secret known only to your application and the authorization server. It will be the same client secret that you retrieved earlier.
* `AUTHORIZATION_CODE` - This is the authorization code you received in the above step.
* `REDIRECT_URI` - This should be the redirect URI that you configured earlier.

You'll receive a response that looks like this:
```
HTTP/1.1 200 OK
Content-Type: application/json
Cache-Control: no-store
Pragma: no-cache

{
  "access_token": "jk8s9dGJK39JKD93jkd03JD",
  "expires_in": 36000,
  "token_type": "Bearer",
  "scope": "zap zap:write authentication",
  "refresh_token": "9D9oz2ZzaouT12LpvklQwNBf6s4vva"
}
```
🎉 This response contains the access token that you'll use to make API request on the user's behalf.

##### 5. Using the access token
The access token should be passed with requests an `Authorization` header. For example:
```
Authorization: Bearer jk8s9dGJK39JKD93jkd03JD
```

### Endpoints

#### GET /v1/apps

|            URL             | Protected By |
| :------------------------: | :----------: |
| **api.zapier.com/v1/apps** |  Client ID   |

> **Notes**
>
> - Your own app will not be returned.
> - Zapier built-in apps will not be returned.
> - Order of the result is by app popularity.

**Arguments**

Available parameters to the Apps resource:

| parameter                   | requirement | notes                                                                                   |
| --------------------------- | ----------- | --------------------------------------------------------------------------------------- |
| **client_id**               | Required    | Your application client ID.                                                             |
| **category**                | Optional    | Filter the results by app category slug.                                                |
| **is_in_zap_template_with** | Optional    | Fetch apps that appear in a Zap Template with your app (no value required).             |
| **title_search**            | Optional    | Filter the results with a case-insensitive search for a substring within the app title. |
| **title_starts_with**       | Optional    | Fetch apps with a title that starts with this value (case-insensitive).                 |
| **per_page**                | Optional    | (defaults to 100, max of 100) Limit the number of apps returned.                        |
| **page**                    | Optional    | (defaults to 1) The page number. Page number 1 refers to the first page in the result.  |

**Example Requests**

Get apps that can be integrated with my app.

```bash
curl -L "https://api.zapier.com/v1/apps?client_id=${client_id}"
```

Get a list of apps related to Google.

```bash
curl -L "https://api.zapier.com/v1/apps?client_id=${client_id}&category=google"
```

Get a list of apps that are included in the same Zap Template as your app.

```bash
curl -L "https://api.zapier.com/v1/apps?client_id=${client_id}&is_in_zap_template_with"
```

Get the Google Calendar app.

```bash
curl -L "https://api.zapier.com/v1/apps?client_id=${client_id}&title_search=google+calendar"
```

Get a list of apps where the title starts with Google.

```bash
curl -L "https://api.zapier.com/v1/apps?client_id=${client_id}&title_starts_with=google"
```

Get apps that can be integrated with my app, returning only 5 results per page.

```bash
curl -L "https://api.zapier.com/v1/apps?client_id=${client_id}&per_page=5"
```

**Example Response**

> Refer to the [App object](#app) reference for all the available fields.

```json
{
  "total": 3649,
  "page": 2,
  "pages": 1825,
  "per_page": 2,
  "objects": [
    {
      "uuid": "ca83afc5-ee9a-470d-b577-e7f8fd555b67",
      "title": "Slack",
      "slug": "slack",
      "description": "Slack is a platform for team communication: everything in one place, instantly searchable, available wherever you go. Offering instant messaging, document sharing and knowledge search for modern teams.",
      "image": "https://zapier-images.imgix.net/storage/services/6cf3f5a461feadfba7abc93c4c395b33_2.png?auto=format%2Ccompress&ixlib=python-3.0.0&q=50",
      "url": "https://api.zapier.com/v1/embed/apps/google-ads/integrations/slack",
      "links": {
        "mutual:zap_templates": "https://api.zapier.com/v1/zap-templates?apps=slack"
      },
      "categories": [
        {
          "slug": "team-chat"
        }
      ],
      "images": {
        "url_16x16": "https://zapier-images.imgix.net/storage/services/6cf3f5a461feadfba7abc93c4c395b33_2.png?auto=format%2Ccompress&fit=crop&h=16&ixlib=python-3.0.0&q=50&w=16",
        "url_32x32": "https://zapier-images.imgix.net/storage/services/6cf3f5a461feadfba7abc93c4c395b33_2.png?auto=format%2Ccompress&fit=crop&h=32&ixlib=python-3.0.0&q=50&w=32",
        "url_64x64": "https://zapier-images.imgix.net/storage/services/6cf3f5a461feadfba7abc93c4c395b33_2.png?auto=format%2Ccompress&fit=crop&h=64&ixlib=python-3.0.0&q=50&w=64",
        "url_128x128": "https://zapier-images.imgix.net/storage/services/6cf3f5a461feadfba7abc93c4c395b33_2.png?auto=format%2Ccompress&fit=crop&h=128&ixlib=python-3.0.0&q=50&w=128"
      },
      "app_latest": "SlackAPI"
    },
    {
      "uuid": "d74234df-0045-436e-bd5b-ee577e74e6b8",
      "title": "Google Calendar",
      "slug": "google-calendar",
      "description": "Google Calendar lets you organize your schedule and share events with co-workers and friends. With Google's free online calendar, it's easy to keep track of your daily schedule.",
      "image": "https://zapier-images.imgix.net/storage/services/62c82a7958c6c29736f17d0495b6635c.png?auto=format%2Ccompress&ixlib=python-3.0.0&q=50",
      "url": "https://api.zapier.com/v1/embed/apps/google-ads/integrations/google-calendar",
      "links": {
        "mutual:zap_templates": "https://api.zapier.com/v1/zap-templates?apps=google-calendar"
      },
      "categories": [
        {
          "slug": "calendar"
        },
        {
          "slug": "google"
        }
      ],
      "images": {
        "url_16x16": "https://zapier-images.imgix.net/storage/services/62c82a7958c6c29736f17d0495b6635c.png?auto=format%2Ccompress&fit=crop&h=16&ixlib=python-3.0.0&q=50&w=16",
        "url_32x32": "https://zapier-images.imgix.net/storage/services/62c82a7958c6c29736f17d0495b6635c.png?auto=format%2Ccompress&fit=crop&h=32&ixlib=python-3.0.0&q=50&w=32",
        "url_64x64": "https://zapier-images.imgix.net/storage/services/62c82a7958c6c29736f17d0495b6635c.png?auto=format%2Ccompress&fit=crop&h=64&ixlib=python-3.0.0&q=50&w=64",
        "url_128x128": "https://zapier-images.imgix.net/storage/services/62c82a7958c6c29736f17d0495b6635c.png?auto=format%2Ccompress&fit=crop&h=128&ixlib=python-3.0.0&q=50&w=128"
      },
      "app_latest": "GoogleCalendarAPI"
    }
  ],
  "prev_url": "https://api.zapier.com/v1/apps?per_page=2&page=1",
  "next_url": "https://api.zapier.com/v1/apps?per_page=2&page=3"
}
```

#### GET /v1/zap-templates

|                 URL                 | Protected By |
| :---------------------------------: | :----------: |
| **api.zapier.com/v1/zap-templates** |  Client ID   |

**Arguments**

Available parameters to the Zap templates resource:

| parameter     | requirement | notes                                                                                                                                                            |
| ------------- | ----------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **client_id** | Required    | Your application client ID.                                                                                                                                      |
| **templates** | Optional    | A comma separated list of specific Zap templates.                                                                                                                |
| **apps**      | Optional    | A comma separated list of Zapier Apps to match Zap templates against. **Note: Your app will always be one of the apps.**                                         |
| **limit**     | Optional    | (defaults to 5, max of 100) Limit the number of Zap templates returned.                                                                                          |
| **offset**    | Optional    | (defaults to 0) The number of Zap templates to skip before beginning to return the Zap templates. The default value is 0, which is the offset of the first item. |

**Example Requests**

Get all Zap templates for my app.

```bash
curl -L "https://api.zapier.com/v1/zap-templates?client_id=${client_id}"
```

Get all Zap templates that include my app and another.

```bash
curl -L "https://api.zapier.com/v1/zap-templates?client_id=${client_id}&apps=mailchimp"
```

**Example Response**

> Refer to the [Zap template](#zap-template) reference for all the available fields.

```json
[
  {
    "id": 51652,
    "steps": [
      {
        "id": 1,
        "uuid": "b9df4eff-f311-44f9-ac54-2901f952c6ac",
        "title": "Google Ads",
        "slug": "google-ads",
        "description": "Google Ads (formerly Google AdWords) is an online advertising platform developed by Google, where advertisers pay to display brief advertisements, service offerings, product listings, video content, and generate mobile application installs within the Google ad network to web users.",
        "image": "https://zapier-images.imgix.net/storage/services/4058ec8b47ad751cbd39bd686cf4eab7.png?auto=format%2Ccompress&ixlib=python-3.0.0&q=50",
        "hex_color": "4285F4",
        "images": {
          "url_16x16": "https://zapier-images.imgix.net/storage/services/4058ec8b47ad751cbd39bd686cf4eab7.png?auto=format%2Ccompress&fit=crop&h=16&ixlib=python-3.0.0&q=50&w=16",
          "url_32x32": "https://zapier-images.imgix.net/storage/services/4058ec8b47ad751cbd39bd686cf4eab7.png?auto=format%2Ccompress&fit=crop&h=32&ixlib=python-3.0.0&q=50&w=32",
          "url_64x64": "https://zapier-images.imgix.net/storage/services/4058ec8b47ad751cbd39bd686cf4eab7.png?auto=format%2Ccompress&fit=crop&h=64&ixlib=python-3.0.0&q=50&w=64",
          "url_128x128": "https://zapier-images.imgix.net/storage/services/4058ec8b47ad751cbd39bd686cf4eab7.png?auto=format%2Ccompress&fit=crop&h=128&ixlib=python-3.0.0&q=50&w=128"
        },
        "api": "GoogleAdsCLIAPI@3.0.0",
        "url": "https://zapier.com/apps/google-ads/integrations?utm_medium=partner_api",
        "label": "New Campaign"
      },
      {
        "id": 2,
        "uuid": "ca83afc5-ee9a-470d-b577-e7f8fd555b67",
        "title": "Slack",
        "slug": "slack",
        "description": "Slack is a platform for team communication: everything in one place, instantly searchable, available wherever you go. Offering instant messaging, document sharing and knowledge search for modern teams.",
        "image": "https://zapier-images.imgix.net/storage/services/6cf3f5a461feadfba7abc93c4c395b33_2.png?auto=format%2Ccompress&ixlib=python-3.0.0&q=50",
        "hex_color": "510f4d",
        "images": {
          "url_16x16": "https://zapier-images.imgix.net/storage/services/6cf3f5a461feadfba7abc93c4c395b33_2.png?auto=format%2Ccompress&fit=crop&h=16&ixlib=python-3.0.0&q=50&w=16",
          "url_32x32": "https://zapier-images.imgix.net/storage/services/6cf3f5a461feadfba7abc93c4c395b33_2.png?auto=format%2Ccompress&fit=crop&h=32&ixlib=python-3.0.0&q=50&w=32",
          "url_64x64": "https://zapier-images.imgix.net/storage/services/6cf3f5a461feadfba7abc93c4c395b33_2.png?auto=format%2Ccompress&fit=crop&h=64&ixlib=python-3.0.0&q=50&w=64",
          "url_128x128": "https://zapier-images.imgix.net/storage/services/6cf3f5a461feadfba7abc93c4c395b33_2.png?auto=format%2Ccompress&fit=crop&h=128&ixlib=python-3.0.0&q=50&w=128"
        },
        "api": "SlackAPI",
        "url": "https://zapier.com/apps/slack/integrations?utm_medium=partner_api",
        "label": "Send Channel Message"
      }
    ],
    "title": "Send messages to Slack channels whenever new Google Ads campaigns launch",
    "slug": "send-messages-to-slack-channels-whenever-new-google-ads-campaigns-launch",
    "status": "published",
    "description_plain": "A new Google Ads campaign can mean the start of your next marketing push, but it can also mean the start of a ton of new sales and service workflows. Zapier gives you a head start on those projects by automatically posting a new message in Slack to a specific channel you choose. Give your teams the heads up they need before your new clients come rolling in!\n",
    "description_raw": "A new Google Ads campaign can mean the start of your next marketing push, but it can also mean the start of a ton of new sales and service workflows. Zapier gives you a head start on those projects by automatically posting a new message in Slack to a specific channel you choose. Give your teams the heads up they need before your new clients come rolling in!",
    "url": "https://zapier.com/apps/google-ads/integrations/slack/51652/send-messages-to-slack-channels-whenever-new-google-ads-campaigns-launch?utm_medium=partner_api",
    "description": "<p>A new Google Ads campaign can mean the start of your next marketing push, but it can also mean the start of a ton of new sales and service workflows. Zapier gives you a head start on those projects by automatically posting a new message in Slack to a specific channel you choose. Give your teams the heads up they need before your new clients come rolling in!</p>\n",
    "create_url": "https://api.zapier.com/v1/embed/google-ads/create/51652",
    "type": "guided_zap"
  }
]
```

**Paging through results using limit and offset**

By default, this API returns the first 5 Zap templates. To get a different set of items,
you can use the `offset` and `limit` parameters in the query string.

For example, to get 20 Zap templates, skipping the first 20 results:

```bash
curl -H "Authorization: Bearer {token}" \
  -L "https://api.zapier.com/v1/zap-templates?client_id=${client_id}&limit=20&offset=20"
```

#### GET /v1/zaps

|            URL             | Protected By | Required Scopes |
| :------------------------: | :----------: | :-------------: |
| **api.zapier.com/v1/zaps** | Access Token |      `zap`      |

> **Note**
>
> 1. The zaps returned are narrowed/filtered by your Zapier app. For example, if you are Trello you'll only be returned a user's Zap that contain Trello in one of the steps of the Zap.
>
> 2. If your app is built with the [Zapier CLI](https://github.com/zapier/zapier-platform/blob/main/packages/cli/README.md) the Zaps returned are for **any** version of your app.

**Arguments**

Available parameters to the Zaps resource:

| parameter                   | requirement | notes                                                                                                                                      |
| --------------------------- | ----------- | ------------------------------------------------------------------------------------------------------------------------------------------ |
| **params\_\_{KEY}={VALUE}** | Optional    | Return Zaps that have a specific key/value set in the params (settings) of the Zap. |
| **get_params** | Optional    | Return Zaps along with their associated key/value param settings. |
| **limit** | Optional | (defaults to 5, max of 100) Limits the number of returned items |
| **offset** | Optional | (defaults to 0) the number of Zaps to skip before beginning to return the Zaps. The default value of 0, which is the offset of the first item. |

**Example Requests**

Get all Zaps in the user's account (note this will only include the OAuth app that is associated with the Zapier app).

```bash
curl -H "Authorization: Bearer {token}" -L "https://api.zapier.com/v1/zaps"
```

Get all Zaps in the user's account that have a particular Trello board (assuming the OAuth app is Trello).

```bash
curl -H "Authorization: Bearer {token}" -L "https://api.zapier.com/v1/zaps?&params__board=BOARD_ID"
```

Get all Zaps in the user's account and include Trello steps' `params` key/value pairs (assuming the OAuth app is Trello).

```bash
curl -H "Authorization: Bearer {token}" -L "https://api.zapier.com/v1/zaps?&get_params"
```

**Example Response**

> Refer to the [Zap](#zap) reference for all the available fields.

```json
{
    "next": "https://api.zapier.com/v1/zaps?limit=2&offset=4",
    "previous": "https://api.zapier.com/v1/zaps?limit=2",
    "count": 20,
    "objects": [
        {
            "id": 159061877,
            "title": "",
            "state": "off",
            "steps": [
                {
                    "type_of": "read",
                    "app": {
                        "id": 730,
                        "uuid": "c91cc1ba-d8fb-4aaa-b71a-a325f7705f78",
                        "title": "Typeform",
                        "slug": "typeform",
                        "description": "Typeform helps you ask awesomely online! If you ever need to run a survey, questionnaire, form, contest etc. Typeform will help you achieve it beautifully across all devices, every time, using its next generation platform.",
                        "hex_color": "8bcbca",
                        "image": "https://zapier-images.imgix.net/storage/services/065860c1e1210fdf4040105024099b0a.png?auto=format%2Ccompress&ixlib=python-3.0.0&q=50",
                        "images": {
                            "url_16x16": "https://zapier-images.imgix.net/storage/services/065860c1e1210fdf4040105024099b0a.png?auto=format%2Ccompress&fit=crop&h=16&ixlib=python-3.0.0&q=50&w=16",
                            "url_32x32": "https://zapier-images.imgix.net/storage/services/065860c1e1210fdf4040105024099b0a.png?auto=format%2Ccompress&fit=crop&h=32&ixlib=python-3.0.0&q=50&w=32",
                            "url_64x64": "https://zapier-images.imgix.net/storage/services/065860c1e1210fdf4040105024099b0a.png?auto=format%2Ccompress&fit=crop&h=64&ixlib=python-3.0.0&q=50&w=64",
                            "url_128x128": "https://zapier-images.imgix.net/storage/services/065860c1e1210fdf4040105024099b0a.png?auto=format%2Ccompress&fit=crop&h=128&ixlib=python-3.0.0&q=50&w=128"
                        },
                        "api": "TypeformCLIAPI@1.0.25",
                        "url": "https://zapier.com/apps/typeform/integrations?utm_source=partner&utm_medium=embed&utm_campaign=partner_api&referer=None"
                    },
                    "params": null
                },
                {
                    "type_of": "write",
                    "app": {
                        "id": 60,
                        "uuid": "b9df4eff-f311-44f9-ac54-2901f952c6ac",
                        "title": "Trello",
                        "slug": "trello",
                        "description": "Trello is a team collaboration tool that lets you organize anything and everything to keep your projects on task.",
                        "hex_color": "0079bf",
                        "image": "https://zapier-images.imgix.net/storage/services/da3ff465abd3a3e1b687c52ff803af74.png?auto=format%2Ccompress&ixlib=python-3.0.0&q=50",
                        "images": {
                            "url_16x16": "https://zapier-images.imgix.net/storage/services/da3ff465abd3a3e1b687c52ff803af74.png?auto=format%2Ccompress&fit=crop&h=16&ixlib=python-3.0.0&q=50&w=16",
                            "url_32x32": "https://zapier-images.imgix.net/storage/services/da3ff465abd3a3e1b687c52ff803af74.png?auto=format%2Ccompress&fit=crop&h=32&ixlib=python-3.0.0&q=50&w=32",
                            "url_64x64": "https://zapier-images.imgix.net/storage/services/da3ff465abd3a3e1b687c52ff803af74.png?auto=format%2Ccompress&fit=crop&h=64&ixlib=python-3.0.0&q=50&w=64",
                            "url_128x128": "https://zapier-images.imgix.net/storage/services/da3ff465abd3a3e1b687c52ff803af74.png?auto=format%2Ccompress&fit=crop&h=128&ixlib=python-3.0.0&q=50&w=128"
                        },
                        "api": "TrelloAPI",
                        "url": "https://zapier.com/apps/trello/integrations?utm_source=partner&utm_medium=embed&utm_campaign=partner_api&referer=None"
                    },
                    "params": {
                        "checklist_name": "Checklist",
                        "card_pos": "bottom"
                    }
                }
            ],
            "url": "https://zapier.com/app/editor/159061877?utm_source=partner&utm_medium=embed&utm_campaign=partner_api&referer=None",
            "modified_at": "2022-08-22T15:17:30+00:00"
        },
        {
            "id": 159061916,
            "title": "",
            "state": "off",
            "steps": [
                {
                    "type_of": "read",
                    "app": {
                        "id": 730,
                        "uuid": "c91cc1ba-d8fb-4aaa-b71a-a325f7705f78",
                        "title": "Typeform",
                        "slug": "typeform",
                        "description": "Typeform helps you ask awesomely online! If you ever need to run a survey, questionnaire, form, contest etc. Typeform will help you achieve it beautifully across all devices, every time, using its next generation platform.",
                        "hex_color": "8bcbca",
                        "image": "https://zapier-images.imgix.net/storage/services/065860c1e1210fdf4040105024099b0a.png?auto=format%2Ccompress&ixlib=python-3.0.0&q=50",
                        "images": {
                            "url_16x16": "https://zapier-images.imgix.net/storage/services/065860c1e1210fdf4040105024099b0a.png?auto=format%2Ccompress&fit=crop&h=16&ixlib=python-3.0.0&q=50&w=16",
                            "url_32x32": "https://zapier-images.imgix.net/storage/services/065860c1e1210fdf4040105024099b0a.png?auto=format%2Ccompress&fit=crop&h=32&ixlib=python-3.0.0&q=50&w=32",
                            "url_64x64": "https://zapier-images.imgix.net/storage/services/065860c1e1210fdf4040105024099b0a.png?auto=format%2Ccompress&fit=crop&h=64&ixlib=python-3.0.0&q=50&w=64",
                            "url_128x128": "https://zapier-images.imgix.net/storage/services/065860c1e1210fdf4040105024099b0a.png?auto=format%2Ccompress&fit=crop&h=128&ixlib=python-3.0.0&q=50&w=128"
                        },
                        "api": "TypeformCLIAPI@1.0.25",
                        "url": "https://zapier.com/apps/typeform/integrations?utm_source=partner&utm_medium=embed&utm_campaign=partner_api&referer=None"
                    },
                    "params": null
                },
                {
                    "type_of": "write",
                    "app": {
                        "id": 60,
                        "uuid": "b9df4eff-f311-44f9-ac54-2901f952c6ac",
                        "title": "Trello",
                        "slug": "trello",
                        "description": "Trello is a team collaboration tool that lets you organize anything and everything to keep your projects on task.",
                        "hex_color": "0079bf",
                        "image": "https://zapier-images.imgix.net/storage/services/da3ff465abd3a3e1b687c52ff803af74.png?auto=format%2Ccompress&ixlib=python-3.0.0&q=50",
                        "images": {
                            "url_16x16": "https://zapier-images.imgix.net/storage/services/da3ff465abd3a3e1b687c52ff803af74.png?auto=format%2Ccompress&fit=crop&h=16&ixlib=python-3.0.0&q=50&w=16",
                            "url_32x32": "https://zapier-images.imgix.net/storage/services/da3ff465abd3a3e1b687c52ff803af74.png?auto=format%2Ccompress&fit=crop&h=32&ixlib=python-3.0.0&q=50&w=32",
                            "url_64x64": "https://zapier-images.imgix.net/storage/services/da3ff465abd3a3e1b687c52ff803af74.png?auto=format%2Ccompress&fit=crop&h=64&ixlib=python-3.0.0&q=50&w=64",
                            "url_128x128": "https://zapier-images.imgix.net/storage/services/da3ff465abd3a3e1b687c52ff803af74.png?auto=format%2Ccompress&fit=crop&h=128&ixlib=python-3.0.0&q=50&w=128"
                        },
                        "api": "TrelloAPI",
                        "url": "https://zapier.com/apps/trello/integrations?utm_source=partner&utm_medium=embed&utm_campaign=partner_api&referer=None"
                    },
                    "params": {
                        "checklist_name": "Checklist",
                        "card_pos": "bottom"
                    }
                }
            ],
            "url": "https://zapier.com/app/editor/159061916?utm_source=partner&utm_medium=embed&utm_campaign=partner_api&referer=None",
            "modified_at": "2022-08-22T15:17:30+00:00"
        }
    ]
}
```

#### GET /v1/profiles/me

|            URL                    | Protected By | Required Scopes     |
| :-------------------------------: | :----------: | :-----------------: |
| **api.zapier.com/v1/profiles/me** | Access Token |      `profile`      |

**Example Requests**

Get user information related to the given `access_token`.

```bash
curl -H "Authorization: Bearer {token}" -L "https://api.zapier.com/v1/profiles/me"
```

**Example Response**

> Refer to the [Profile](#profile) reference for all the available fields.

```json
{
    "id": 88998899,
    "first_name": "Jacob",
    "last_name": "Corwin",
    "email": "jacob.corwin@gmail.com",
    "email_confirmed": true,
    "timezone": null,
    "full_name": "Jacob Corwin"
}
```

#### GET /v1/categories

|               URL                | Protected By |
| :------------------------------: | :----------: |
| **api.zapier.com/v1/categories** |     None     |

**Arguments**

Available parameters to the categories resource:

| parameter  | requirement | notes                                                                                                                                                  |
| ---------- | ----------- | ------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **limit**  | Optional    | (defaults to 10, max of 100) Limit the number of categories. returned.                                                                               |
| **offset** | Optional    | (defaults to 0) The number of categories items to skip before returning new categories. The default value is 0, which is the offset of the first item. |

**Example Requests**

Get a list of app categories

```bash
curl -L "https://api.zapier.com/v1/categories"
```

**Example Response**

> Refer to the [AppCategory](#appcategory) reference for all the available fields.

```json
{
    "next": "https://api.zapier.com/v1/categories?offset=10&limit=10",
    "previous": null,
    "count": 90,
    "objects": [
        {
            "id": 7,
            "title": "Accounting",
            "slug": "accounting",
            "description": "Tools for accounting and finance.",
            "url": "https://zapier.com/api/v4/app-directory/categories/accounting/",
            "type_of": "curated",
            "featured_entry_slug": "accounting-automation",
            "role": "child"
        },
        {
            "id": 77,
            "title": "Ads & Conversion",
            "slug": "ads-conversion",
            "description": "Tools to track and reach an audience online.",
            "url": "https://zapier.com/api/v4/app-directory/categories/ads-conversion/",
            "type_of": "curated",
            "featured_entry_slug": "improve-ppc-campaigns",
            "role": "child"
        },
        {
            "id": 106,
            "title": "AI Tools",
            "slug": "ai-tools",
            "description": "Unlock the potential of artificial intelligence in your workflow with these AI integrations. These apps use AI to tackle everything from natural language processing to image classification, providing you with unparalleled automation power.",
            "url": "https://zapier.com/api/v4/app-directory/categories/ai-tools/",
            "type_of": "curated",
            "featured_entry_slug": "use-openai-gpt-3-to-write-emails",
            "role": "child"
        },
        {
            "id": 87,
            "title": "All",
            "slug": "all",
            "description": "Contains all the services.",
            "url": "https://zapier.com/api/v4/app-directory/categories/all/",
            "type_of": "auto",
            "featured_entry_slug": null,
            "role": "parent"
        },
        {
            "id": 57,
            "title": "Amazon",
            "slug": "aws",
            "description": "Tools from Amazon to host and manage sites and applications on the Amazon cloud.",
            "url": "https://zapier.com/api/v4/app-directory/categories/aws/",
            "type_of": "curated",
            "featured_entry_slug": "what-you-should-automate",
            "role": "child"
        },
        {
            "id": 24,
            "title": "Analytics",
            "slug": "analytics",
            "description": "Tools to measure and report on success",
            "url": "https://zapier.com/api/v4/app-directory/categories/analytics/",
            "type_of": "curated",
            "featured_entry_slug": "automate-analytics-tools",
            "role": "child"
        },
        {
            "id": 31,
            "title": "App Builder",
            "slug": "app-builder",
            "description": "Tools to build a custom app with forms and databases.",
            "url": "https://zapier.com/api/v4/app-directory/categories/app-builder/",
            "type_of": "curated",
            "featured_entry_slug": null,
            "role": "child"
        },
        {
            "id": 95,
            "title": "App Families",
            "slug": "app-families",
            "description": "",
            "url": "https://zapier.com/api/v4/app-directory/categories/app-families/",
            "type_of": "curated",
            "featured_entry_slug": null,
            "role": "parent"
        },
        {
            "id": 105,
            "title": "Artificial Intelligence",
            "slug": "artificial-intelligence",
            "description": "Unlock the potential of artificial intelligence in your workflow with these AI integrations. These apps use AI to tackle everything from natural language processing to image classification, providing you with unparalleled automation power.",
            "url": "https://zapier.com/api/v4/app-directory/categories/artificial-intelligence/",
            "type_of": "curated",
            "featured_entry_slug": "gpt-3-prompt",
            "role": "parent"
        },
        {
            "id": 86,
            "title": "Beta",
            "slug": "beta",
            "description": "Beta services.",
            "url": "https://zapier.com/api/v4/app-directory/categories/beta/",
            "type_of": "auto",
            "featured_entry_slug": null,
            "role": "child"
        }
    ]
}
```

#### Data Objects

##### App

| attribute       | type   | notes                                                                                                                                                 |
| --------------- | ------ | ----------------------------------------------------------------------------------------------------------------------------------------------------- |
| **uuid**        | String | The unique canonical identifier to the app.                                                                                                           |
| **description** | String | Plain text description of the app.                                                                                                                    |
| **links**       | Object | Link to get mutual Zap templates from Zapier's Partner API.                                                                                           |
| **title**       | String | The name of the app.                                                                                                                                  |
| **url**         | String | An absolute url to the Zapbook Apps page.                                                                                                             |
| **image**       | String | The app's logo in large format.                                                                                                                       |
| **images**      | Object | Thumbnails for the app image. <br><small>Available sizes (and respective keys):<br> `url_128x128`, `url_64x64`, `url_32x32`, and `url_16x16`.</small> |
| **slug**        | String | A URL/SEO friendly ID for the app.                                                                                                                    |
| **categories**  | Object | A list of categories this app belongs to.                                                                                                             |
| **app_latest**  | String | An identifier for the app's production version.                                                                                                       |

```json
{
  "uuid": "ca83afc5-ee9a-470d-b577-e7f8fd555b67",
  "description": "Slack is a platform for team communication: everything in one place, instantly searchable, available wherever you go. Offering instant messaging, document sharing and knowledge search for modern teams.",
  "links": {
    "mutual:zap_templates": "https://api.zapier.com/v1/zap-templates?apps=slack"
  },
  "title": "Slack",
  "url": "https://zapier.com/partner/embed/apps/trello/integrations/slack",
  "image": "https://cdn.zapier.com/storage/developer/57b336375384ab62cc06e7e83d5c3622_2.png",
  "images": {
    "url_16x16": "https://cdn.zapier.com/storage/developer/57b336375384ab62cc06e7e83d5c3622_2.16x16.png",
    "url_32x32": "https://cdn.zapier.com/storage/developer/57b336375384ab62cc06e7e83d5c3622_2.32x32.png",
    "url_128x128": "https://cdn.zapier.com/storage/developer/57b336375384ab62cc06e7e83d5c3622_2.128x128.png",
    "url_64x64": "https://cdn.zapier.com/storage/developer/57b336375384ab62cc06e7e83d5c3622_2.64x64.png"
  },
  "slug": "slack",
  "categories": [
    {
      "slug": "team-chat"
    },
    {
      "slug": "top-100"
    }
  ]
}
```

##### AppCategory

| attribute               | type                                      | notes                                                                                                                                                                                                                                                            |
| ----------------------- | ----------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **id**                  | String                                    | Unique identifier for the category.                                                                                                                                                                                                                              |
| **title**               | String                                    | Plain text description of the category.                                                                                                                                                                                                                          |
| **slug**                | String                                    | URL/SEO friendly ID for the Zap template API.                                                                                                                                                                                                                  |
| **description**         | String |  Detailed explanation of the app category.
| **url**                 | String                                    | An absolute url to the Zapbook Apps page.                                                                                                                                                                                                                        |
| **type_of**             | String                                    | Category type. 'Curated' categories are maintained by Zapier staff, 'Automatically Generated' categories are maintained by automation and populated with the 'rebuild_special_categories' command, 'Other' categories are manually created for various purposes. |
| **featured_entry_slug** | String                                    | Alternative slug for the category.                                                                                                                                                                                                                               |
| **role**                | String                                    | Indicates if the category is a 'parent' or a 'child'.                                                                                                                                                                                                            |

```json
{
    "id": 104,
    "title": "AI Tools",
    "slug": "ai-tools",
    "description": "Unlock the potential of artificial intelligence in your workflow with these AI integrations. These apps use AI to tackle everything from natural language processing to image classification, providing you with unparalleled automation power.",
    "url": "https://zapier.com/api/v4/app-directory/categories/ai-tools/",
    "type_of": "curated",
    "featured_entry_slug": null,
    "role": "parent"
}
```

##### Profile

| attribute           | type            | notes                                                 |
| ------------------- | --------------- | ----------------------------------------------------- |
| **id**              | Number          | The ID of the User.                                   |
| **first_name**      | String          | User's first name.                                    |
| **last_name**       | String          | User's last name.                                     |
| **email**           | String          | User's email.                                         |
| **email_confirmed** | Boolean         | Says if the user confirmed the email to Zapier.       |
| **timezone**        | String          | User's timezone.                                      |
| **full_name**       | String          | User's full name                                      |

```json
{
    "id": 88998899,
    "first_name": "Jacob",
    "last_name": "Corwin",
    "email": "jacob.corwin@gmail.com",
    "email_confirmed": true,
    "timezone": null,
    "full_name": "Jacob Corwin"
}
```

##### Zap

| attribute       | type            | notes                                                 |
| --------------- | --------------- | ----------------------------------------------------- |
| **id**          | Number          | The ID of the Zap.                                    |
| **modified_at** | Date            | The last modified date time.                          |
| **state**       | String          | One of `'on'`, `'off'`, or `'draft'`                  |
| **steps**       | Array<Zap Step> | An array steps in the Zap. See [Zap Step](#zap-step). |
| **title**       | String          | The name of the Zap, if any, otherwise `null`.        |
| **url**         | String          | An absolute url to the Zap (to edit).                 |

```json
{
  "id": 125,
  "modified_at": "2017-03-22T09:38:11-05:00",
  "state": "on",
  "steps": [{ "See Step object definition ..." }],
  "title": "Create Trello cards from new Typeform entries",
  "url": "https://zapier.com/app/editor/125"
}

```

##### Zap Step

| attribute   | type   | notes                                                                      |
| ----------- | ------ | -------------------------------------------------------------------------- |
| **type_of** | String | One of `'read'`, `'write'`, `'filter'`, `'search'`, or `'search_or_write'` |
| **app**     | App    | The app for the step. See [App object](#app).                              |

```json
{
  "app": {
    // ... See the App object definition ...
  },
  "type_of": "read"
}
```

##### Zap Template

| attribute             | type       | notes                                                                                                                         |
| --------------------- | ---------- | ----------------------------------------------------------------------------------------------------------------------------- |
| **id**                | Number     | The ID of the Zap Template                                                                                                    |
| **create_url**        | String     | An absolute URL used to create the Zap.                                                                                       |
| **description**       | String     | The HTML-rendered description provided when the Zap template was created.                                                     |
| **description_plain** | String     | Plain text (HTML tags stripped) description. **Note: `\r` and `\n` replaced with space character. Artifacts may be present.** |
| **description_raw**   | String     | The [Markdown][https://www.markdownguide.org/getting-started/] description provided when the Zap template was created.                                              |
| **slug**              | String     | A URL/SEO friendly ID for the Zap template.                                                                                   |
| **steps**             | Array<App> | An array of two or more steps in the Zap template. See [App object](#app).                                                    |
| **title**             | String     | The name of the Zap template.                                                                                                 |
| **status**            | String     | The status of the Zap template (choices: `draft`, `published`).                                                               |
| **url**               | String     | An absolute url to the Zapbook Zap template Page.                                                                             |

```json
{
  "create_url": "https://zapier.com/webintent/create-zap?template=10127&utm_campaign=Zap%20Templates%20Partners%20API&embedded=true&referrer=FacebookLeadsAPI&utm_source=partners&utm_medium=api&selected_apis=FacebookLeadsAPI,MailchimpCLIAPI@1.0.10",
  "description": "<p>Facebook Lead Ads are an...",
  "description_plain": "Facebook Lead Ads ... ",
  "description_raw": "**Facebook Lead Ads** are an ...",
  "slug": "subscribe-new-facebook-lead-ads-mailchimp-list",
  "status": "published",
  "steps": [
    {
      // ... see App object definition ...
    }
  ],
  "title": "Subscribe new Facebook Lead Ad leads to a MailChimp list",
  "url": "https://zapier.com/apps/inside-sales-box/integrations/zoho-crm/12084/add-new-leads-created-in-inside-sales-box-to-zoho-crm"
}
```

### Errors
Zapier uses HTTP response codes to indicate the success or failure of an API request.

| Code    | Status            | Explanation                                                                |
| ------- | ----------------- | -------------------------------------------------------------------------- |
| **200** | OK                | Successful request.                                                        |
| **400** | Bad Request       | Invalid request, or invalid parameters .                                   |
| **403** | Authentication    | Not authorized.                                                            |
| **404** | Not Found         | The resource requested was not found.                                      |
| **429** | Too Many Requests | Too many requests were performed within a window of time. Try again later. |
| **5xx** | Server Error      | A fatal error occurred while processing the request. Try again.            |

All errors will be JSON object with a String array of errors:

```json
{
  "errors": ["Malformed request"]
}
```

### Changelog
- 2023-05-25

  - Added query parameters to `v1/apps`

    - The endpoint `/v1/apps` supports query parameters `title_search`, `title_starts_with`, `category`, and `is_in_zap_template_with` for more refined app search results.

  - Added query parameter to `v1/zaps`

    - The endpoint `/v1/zaps` supports the query parameters `get_params`.

  - Added endpoint `/v1/categories`

    - The new endpoint `/v1/categories` returns a list of supported zap categories.

- 2023-03-30

  - Added attribute to `v1/apps`

    - The endpoint `/v1/apps` exposes the `app_latest` string attribute representing the SelectedAPI and production version for each app.

- 2022-08-29

  - Removed restriction to `v1/zaps`

    - The endpoint `/v1/zaps` now performs param filtering on both triggers and actions.

- 2022-05-23
  
  - Added attribute to `v1/zaps`
  
    - The endpoint `/v1/zaps` exposes the `uuid` attribute to each step app. This attribute is a UUID v4 string.

- 2021-08-03
  
  - Added attribute to `v1/zap-templates`
  
    - The endpoint `/v1/zap-templates` exposes the `uuid` attribute to each step. This attribute is a UUID v4 string.

- 2021-07-29
  
  - Added `v1/profiles/me`
  
    - The endpoint return information about the user whose `access_token` is authorized.
  
    - Check the endpoint [documentation](https://platform.zapier.com/partner_api/endpoints#get-v1profilesme) for the payload structure.

  - Added pagination to `v1/zaps`
  
    - The endpoint `/v1/zaps` supports `limit`/`offset` query parameters to paginate the results.
  
    - `count`/`next`/`previous` have been added to the response payload.

- 2021-06-01
  
  - [DEPRECATION] After July 5, 2021, the endpoint `v1/zap-template/me` will no longer exist.

- 2021-05-13

  - Added attributes to existing endpoint payloads

    - The endpoint `/v1/apps` exposes the `uuid` attribute for each app that is returned. This attribute is a UUID v4 string.

    - The endpoint `/v1/zap-templates` exposes the `label` attribute to each step. A `null` placeholder value is used if the label is unable to be resolved.

  - Updated example endpoint payloads

    - The example payloads for endpoints `/v1/apps` and `/v1/zap-templates` have been updated to reflect these new attributes.

- 2021-01-14

  - Introducing rate limiting

    - The endpoints are now rate limit protected. The limit is set to 9,000 requests per hour for an individual endpoint.

- 2018-05-31

  - New `/apps` endpoint

    - This is a new endpoint that returns a list of apps in Zapier's App Directory.

- 2018-03-19

  - Updated `/zap-templates` and `/zap-templates/me`

    - These endpoints now accept an `offset` parameter to support pagination through results.

- 2018-02-12

  - Faster `/zap-templates` lookup.

    - Sub-second responses to the `/v1/zap-templates` even when requesting up to 100 Zap templates.

- 2017-10-16

  - `/zaps`

    - The endpoint will now return **all** Zaps regardless of the [Zapier CLI App's version](https://github.com/zapier/zapier-platform-cli) that was used when creating the Zap.