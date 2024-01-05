---
title: Embed Zap editor with Partner API
order: 5
layout: post-toc
redirect_from:
---

# Embed Zap editor with Partner API

With an embedded Zap editor in your product, your users can create and edit their Zaps without leaving your app.

## Prerequisites

- Your app has passed the review process and is Published in the Zapier App Directory
- Any [Zap templates](https://platform.zapier.com/publish/zap-templates) you want to query have been reviewed and made public 

## Example implementation

This video shows how Paperform prefills Zaps for their embedded Zap editor with contextual data from the platform, such as the Form ID, to make Zap setup easier for users. By doing so, Paperform reduces the number of clicks it takes for users to publish a Zap and removes mental friction of users needing to remember details for it:

<iframe allowtransparency="true" title="Wistia video player" allowFullscreen frameborder="0" scrolling="no" class="wistia_embed" name="wistia_embed" src="https://cdn.zappy.app/0625a071fbee914968480b0b58d696a8.mp4" width="640" height="360"></iframe>

## Option 1: Create Zaps from Zap Templates

Use the Partner API to query the public Zap templates featuring your integration (using the [`GET /v1/zap-templates`](https://platform.zapier.com/embed/partner-api) endpoint) and feature them in your product. When a user chooses a Zap template they’d like to try, use the `create_url` value as the source to load in an embedded frame such as:

```html
<iframe src="https://api.zapier.com/v1/embed/trello/create/113"></iframe>
```

Where `https://api.zapier.com/v1/embed/trello/create/113` is the `create_url` value of the Zap template.

Optionally, you can add additional parameters to the `create_url` to [prefill the user’s Zap](https://platform.zapier.com/embed/prefill-zaps) with custom values (e.g., specifying a workspace for the trigger to filter by).

## Option 2: Create Zaps without Zap Templates

You can also facilitate a user's Zap creation via URL parameters instead of an existing Zap Template. This provides flexibility to redirect users to a pre-populated Zap editor with known context from your app without publishing a Zap Template for each specific use case.

[Use the generator](https://platform.zapier.com/embed/prefill-zaps) under the _Embed_ and _Pre-filled Zaps_ tabs in the Platform UI to easily construct pre-filled Zaps for your embedded editor experience or as a lightweight entry point into the Zap editor from your app. 

## Editing existing Zaps

Use the Partner API to load a user’s Zaps (using the [`GET /v1/zaps`](https://platform.zapier.com/embed/partner-api) endpoint). When the user chooses to open or edit a Zap use the the `url` value of the Zap as the source of an embedded frame like this:

```html
<iframe src="https://zapier.com/app/editor/123456"></iframe>
```

Where `https://zapier.com/app/editor/123456` is the `url` of the Zap to be edited.

If you prefer, you can open these URLs in a separate window, new tab, or popup from your app.

## `postMessage` events

If you decide to embed the Zap editor within your product you can listen to [message events from `postMessage`](https://developer.mozilla.org/en-US/docs/Web/API/Window/message_event) to help you improve the interactivity with the iframe (e.g. automatically close the iframe modal.)

The messages available include:

- `zap:unpause` = Zap turned on / published
- `zap:unpause:done` = Zap turned on / published (success)
- `zap:unpause:fail` = Zap turned on / published (failure)
- `zap:pause` = Zap turned off
- `zap:pause:done` = Zap turned off (success)
- `zap:pause:fail` = Zap turned off (failure)

## Turning off a Zap

The API does not currently have an endpoint to turn off/on a user's Zaps. If your Zapier app uses [Webhook Subscriptions](https://platform.zapier.com/build/hook-trigger), you can send a `DELETE` to the unique target URL that was provided when the subscription was created and that will then pause/turn off a Zap.
