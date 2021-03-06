---
title: Examples
order: 2
layout: post
redirect_from: /partner_api/
---

# Examples

## Featured: How Unbounce Uses the API

The API allows for so much flexibility that it can be challenging to picture the end result. Here's how lead generation app, Unbounce, built Zapier integrations into the Unbounce UI. The end result? A seamless integration experience for their users who can now connect their new Unbounce leads to hundreds of apps right from their Unbounce dashboard.

Now when Unbounce users are logged in, there's a slew of Zapier-powered integrations alongside their forms (see the [Apps endpoints](/partner_api/endpoints#get-v1apps) and [Zap templates endpoint](/partner_api/endpoints#get-v1zap-templates)).

![](https://cdn.zapier.com/storage/photos/9e769e34030c2bbcf2fb80b827d69c22.png)

When a user chooses an integration, pop-up Zap Template guides the user through setting up that Zap, with info from Unbounce pre-filled like the form, client, landing page - anything already known about the Unbounce form (See the [Embedding guide](/partner_api/embedding#iframe)). 

![](https://cdn.zapier.com/storage/photos/edcf17488c8250dca213ed2083846fc5.png)

Then, once that Zap is set up and turned on, it's right there in Unbounce, where it can be edited, toggled on/off<sup>[1](#toggle-on-off-caveat)</sup> (see note below), etc. That means users can set up and manage nearly 1,000 integrations without ever leaving Unbounce (see the [Zaps endpoint](/partner_api/endpoints#get-v1zaps)).

![](https://cdn.zapier.com/storage/photos/05fec8dfe5a382bcfbcfe44c6139f14e.png)

## Other Examples

- **Facebook** lets you search for and configure a Zap from within the Lead Ad Campaign Manager.

![](https://cdn.zapier.com/storage/photos/73d073d363d0eae104ccdb159eaba8cd.gif)

- **Zoho Connect** lets users set up Zaps from within the Zoho Connect app.

![](https://cdn.zapier.com/storage/photos/e02db0c000ed037b3385b813b3f1303c.gif)


- **MeisterTask** provides an intuitive, styled interface to search for any MeisterTask Zap Template.

![](https://cdn.zapier.com/storage/photos/570103e337edbe2b20b62ffba9f5dd7c.gif)

- **Typeform** uses Zapier to extend their integrations directory automatically, with Zapier as a fallback if no direct integrations are available.

![](https://cdn.zapier.com/storage/photos/bcec803a9b13f20e1a6453f17dee1314.gif#_ga=2.228121565.1797870667.1575912186-681011286.1567692739)

- **Trello** leverages the Partner API to let the user manage their Zapier experience from their [dashboard within Trello.](http://blog.trello.com/zapier-power-up-for-trello)


-----

<div style="font-size: 80%">

<bold><sup id="toggle-on-off-caveat">1</sup>: Allowing a user to toggle a Zap on/off</bold>: The API does not currently have an endpoint to turn off/on a user's Zaps. If your Zapier app uses Webhook Subscriptions, you can send a <code>DELETE</code> to the webhook subscription URL and that will then pause/turn off a Zap. Other partners have also embedded the Zapier editor using iframes (see the <a href="/partner_api/embedding)">Embedding guide</a>). Doing so allows the user to edit the Zap within your app; including turning the Zap off and on. If you decide to embed the Zap editor within your app you can listen to <code>postMessage</code> on your app that have <code>zap:pause</code> or <code>zap:unpause</code> which can help you improve interactivity with the iframe (e.g. automatically close the iframe modal).

</div>
