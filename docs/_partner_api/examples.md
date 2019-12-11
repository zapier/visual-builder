---
title: Examples
order: 7
layout: post
redirect_from: /partner_api/
---

# Examples

### See it in Action: How Unbounce Uses the API

The API allows for so much flexibility that it can be challenging to picture the end result. Here's how lead generation app, Unbounce, built Zapier integrations into the Unbounce UI. The end result? A seamless integration experience for their users who can now connect their new Unbounce leads to hundreds of apps right from their Unbounce dashboard.

Now when Unbounce users are logged in, there's a slew of Zapier-powered integrations alongside their forms.

![](https://cdn.zapier.com/storage/photos/9e769e34030c2bbcf2fb80b827d69c22.png)

When a user chooses an integration, pop-up Zap Template guides the user through setting up that Zap, with info from Unbounce pre-filled like the form, client, landing page - anything already known about the Unbounce form. 

![](https://cdn.zapier.com/storage/photos/edcf17488c8250dca213ed2083846fc5.png)

Then, once that Zap is set up and turned on, it's right there in Unbounce, where it can be edited, toggled on/off<sup>[1](#toggle-on-off-caveat)</sup> (see note below), etc. That means users can set up and manage nearly 1,000 integrations without ever leaving Unbounce.

![](https://cdn.zapier.com/storage/photos/05fec8dfe5a382bcfbcfe44c6139f14e.png)

### Other Examples

- **Facebook** lets you search for and configure a Zap from within the [Lead Ad Campaign Manager](https://cdn.zapier.com/storage/photos/73d073d363d0eae104ccdb159eaba8cd.gif).
- **Trello** leverages the Partner API to let the user manage their Zapier experience from their [dashboard within Trello.](http://blog.trello.com/zapier-power-up-for-trello)
- **Zoho Connect** lets users set up Zaps from [within the Zoho Connect app.](https://cdn.zapier.com/storage/photos/e02db0c000ed037b3385b813b3f1303c.gif)

-----

<div style="font-size: 80%">

<bold><sup id="toggle-on-off-caveat">1</sup>: Allowing a user to toggle a Zap on/off</bold>: The API does not currently have an endpoint to turn off/on a user's Zaps. If your Zapier app uses Webhook Subscriptions, you can send a <code>DELETE</code> to the webhook subscription URL and that will then pause/turn off a Zap. Other partners have also embedded the Zapier editor using iframes. Doing so allows the user to edit the Zap within your app; including turning the Zap off and on. If you decide to embed the Zap editor within your app you can listen to <code>postMessage</code> on your app that have <code>zap:pause</code> or <code>zap:unpause</code> which can help you improve interactivity with the iframe (e.g. automatically close the iframe modal).

</div>
