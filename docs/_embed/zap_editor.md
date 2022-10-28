---
title: Zap Editor
order: 2
layout: post
redirect_from:
  - /embed/
  - /partner_api/
  - /partner_api/introduction
---

# Embedding the Zap Editor

By embedding our Zap Editor in your product, your users can create and edit their Zaps without leaving your product.

## Creating a new Zap

Use the Partner API to query the public Zap templates featuring your integration (using the [`GET /v1/zap-templates`](./partner-api#get-v1zap-templates) endpoint) and feature them in your product. When a user chooses a Zap template they’d like to try, use the `create_url` value as the source to load in an embedded frame such as:

```html
<iframe src="https://api.zapier.com/v1/embed/trello/create/113"></iframe>
```

Where `https://api.zapier.com/v1/embed/trello/create/113` is the `create_url` value of the Zap template.

Optionally, you can add additional parameters to the `create_url` to prefill the user’s Zap with custom values (e.g., specifying a workspace for the trigger to filter by).

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
