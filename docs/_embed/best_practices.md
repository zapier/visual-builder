---
title: Best Practices
order: 7
layout: post
redirect_from: /partner_api/
---

# Best Practices

## `create_url` and Prefill Options

Always link the user with the `create_url` (available in a [Zap template object](/partner_api/endpoints#zap-template)) in order to create the Zap. Optionally, you can add additional parameters to the `create_url` so that the user's Zap is prefilled with the provided custom values.

> Note: You will need to know the fields that your app requires per step. You can find the fields as definied in your Zapier integration.

Each parameter is in a flattened dictionary/object syntax. For example an object: `{a: {b: 2}}` would be flattened to: `a__b=2`. This allows you to provide countless prefills onbehalf of the user.

**Example**

Prefill Trello's board ID (field: `board`) in the second step of the Zap template:

`https://zapier.com/app/editor/template/2405?steps__1__params__board=12345`

Here's what it would look like in the editor:

![](https://cdn.zapier.com/storage/photos/1f3544e43787d1d2e0b528b08b909dcb.png)

If you'd like to provide a label for the value (e.g. a Board's name) you can do so by passing an additional parameter:

`https://zapier.com/app/editor/template/2405?steps__1__params__board=12345&steps__1__meta__parammap__board=My+Board`

![](https://cdn.zapier.com/storage/photos/86b71a90bc69e5b13024c08f1da4b812.png)
