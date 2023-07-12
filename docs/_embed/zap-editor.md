---
title: Embed Zap editor & pre-fill Zaps
order: 4
layout: post-toc
redirect_from:
  - /embed/
  - /partner_api/
  - /partner_api/introduction
---

# Embed Zap editor & pre-fill Zaps

By embedding our Zap Editor in your product, your users can create and edit their Zaps without leaving your product.

## Example Implementation

This video shows how Paperform prefills Zaps for their embedded Zap Editor with contextual data from the platform, such as the Form ID, to make Zap setup easier for users. By doing so, Paperform reduces the number of clicks it takes for users to publish a Zap and removes mental friction of users needing to remember details for it:

<iframe allowtransparency="true" title="Wistia video player" allowFullscreen frameborder="0" scrolling="no" class="wistia_embed" name="wistia_embed" src="https://cdn.zappy.app/0625a071fbee914968480b0b58d696a8.mp4" width="640" height="360"></iframe>


## Creating Zaps from Zap Templates

Use the Partner API to query the public Zap templates featuring your integration (using the [`GET /v1/zap-templates`](./partner-api#get-v1zap-templates) endpoint) and feature them in your product. When a user chooses a Zap template they’d like to try, use the `create_url` value as the source to load in an embedded frame such as:

```html
<iframe src="https://api.zapier.com/v1/embed/trello/create/113"></iframe>
```

Where `https://api.zapier.com/v1/embed/trello/create/113` is the `create_url` value of the Zap template.

Optionally, you can add additional parameters to the `create_url` to prefill the user’s Zap with custom values (e.g., specifying a workspace for the trigger to filter by).

## Creating Zaps without Zap Templates

You can also facilitate a user's Zap creation via URL parameters instead of an existing Zap Template. This provides flexibility to redirect users to a pre-populated Zap Editor with known context from your app without publishing a Zap Template for each specific use case.

Use the generator under the "Embeds" and "Pre-filled Zaps" tabs in the developer platform to easily construct pre-filled Zaps for your embedded editor experience or as lightweight entry point into the Zap Editor from your app. See how to use the [pre-filled Zap generator](https://platform.zapier.com/embed/zap-editor#using-the-pre-filled-zap-generator) in the section below.

Similar to the [prefill](https://platform.zapier.com/embed/zap-editor#prefill-options) options for automatically defining field values for users, you can prefill apps, events, and input field values in the Zap Editor with the following URL schema:

Base URL: `https://api.zapier.com/v1/embed/{your_app}/create` - you can find `{your_app}` by using the [Prefill Generator](https://platform.zapier.com/embed/zap-editor#using-the-pre-filled-zap-generator)

URL parameters (with example values):

- Trigger app (required): `steps[0][app]=MailchimpCLIAPI@latest` 
- Trigger event: `steps[0][action]=new_member`
- Trigger field prefills: `steps[0][params][list_id]=123`
- Action app: `steps[1][app]=GoogleAdsCLIAPI@latest`
- Action event: `steps[1][action]=add_to_customer_list_v2`
- Action field prefills: `steps[1][params][list_id]=234`

Requirements:

- A trigger app is required. The `steps` index for a trigger is always `0`.
- Use `app_latest` values from the [`/apps` endpoint](https://platform.zapier.com/embed/partner-api#get-v1apps) of the Partner API to define an app. This is case-sensitive, so use exactly the value returned from the API.
- You can define 0 to many subsequent action steps. The `steps` index for actions will be `1` or greater. Please note, only users on a paid Zapier plan have access to multi-step Zaps.
- Events are defined by the `key` of the trigger, action, or search.
- Field prefills are defined by the `key` of the input field. See the below [Prefill Options](https://platform.zapier.com/embed/zap-editor#prefill-options) for more details on prefilling fields.

Examples:

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

## Using the pre-filled Zap generator

We provide a UI-based generator in your integration's developer platform to facilitate constructing pre-filled Zaps. **Pre-filled Zaps are simply URLs with field values added as parameters,** which you can use to direct users to the Zap Editor with some input fields already filled. Place these URLs inside your product or within an embedded Zap Editor to facilitate users creating and publishing Zaps.

Find the pre-filled Zap generator under the "Embed" and "Pre-filled Zaps" section of the developer platform.

![Screenshot of pre-filled Zaps tab](https://cdn.zappy.app/2a4f9c6de6c525cbcdc1b513ec88c519.png)

To create a pre-filled Zap using the generator:
- Select an app and event for both the trigger and action to see the fields you can pre-fill. If no fields appear, the event has no input fields.

![Screenshot of generator trigger step setup](https://cdn.zappy.app/87b9c4951d55298780ff209e217bb750.png)

- Select the fields you want to pre-fill:
  - If you don’t want to pre-fill the field, leave the box unchecked. In the Zap, the field will be empty or set to a default value, if there is one.
  - If there's a static value for a field that applies to every user's Zap (like the title of an email), check the field and provide the value in the text field.
  - If the values are dynamic or you don’t know them yet (like the ), replace the placeholders represented in curly brackets (i.e {TRIGGER_LIST_ID}) in the generated URL from Step 2 before using the it in your app. This could be like an account or list ID field. The placholder serves as a reminder to replace the value at runtime.
  - If the field is greyed out, it requires a complex field value and cannot be pre-filled.

![Screenshot of prefill input field options](https://cdn.zappy.app/9e845182506292214c866f3278861e8d.png)
_Note: fields denoting "(required)" are required for the Zap to be turned on, and not required to be pre-filled._

- Test the Zap! We provide a handy test button for you to make sure the resulting Zap is what you intended. You'll need to connect accounts on both steps to see the pre-filled fields.
- Copy the code and embed it inside your app to make setting up a Zap easier and faster for users.

The generator only supports creating 2-step Zaps, but you can construct multi-step Zaps by building upon the generated URL and adding [`steps` parameters with increased indeces](https://platform.zapier.com/embed/zap-editor#creating-zaps-without-zap-templates). You also cannot prefill an action field with data returned from the trigger. In this case, use [pre-filled Zaps with Zap Templates](https://platform.zapier.com/embed/zap-editor#creating-zaps-from-zap-templates)!

## Editing a Zap

Use the Partner API to load a user’s Zaps (using the [`GET /v1/zaps`](./partner-api#get-v1zaps) endpoint). When the user chooses to open or edit a Zap use the the `url` value of the Zap as the source of an embedded frame such as:

```html
<iframe src="https://zapier.com/app/editor/123456"></iframe>
```

Where `https://zapier.com/app/editor/123456` is the `url` of the Zap to be edited.

Additionally, if you’d prefer, you can open these URLs in a separate window, new tab, or popup just as well.

## Prefill Options

Prefills allow you to define the fields on behalf of the user, thus simplying the experience of setting up their Zap.

You'll use the `create_url` (available in a [Zap template object](/partner_api/endpoints#zap-template)) in order to create the Zap. Next, you will add parameters to the `create_url` so that the user's Zap is prefilled with the provided custom values.

> Note: You will need to know the fields that your app requires per step. You can find the fields as defined in your Zapier integration.

**Example**

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

## `postMessage` events

If you decide to embed the Zapier Editor within your product you can listen to [message events from `postMessage`](https://developer.mozilla.org/en-US/docs/Web/API/Window/message_event) which can help you improve the interactivity with the iframe (e.g. automatically close the iframe modal.)

The messages available include:

- `zap:unpause` = Zap turned on / published
- `zap:unpause:done` = Zap turned on / published (success)
- `zap:unpause:fail` = Zap turned on / published (failure)
- `zap:pause` = Zap turned off
- `zap:pause:done` = Zap turned off (success)
- `zap:pause:fail` = Zap turned off (failure)

## Turning off a Zap

The API does not currently have an endpoint to turn off/on a user's Zaps. If your Zapier app uses Webhook Subscriptions, you can send a `DELETE` to the webhook subscription URL and that will then pause/turn off a Zap.
