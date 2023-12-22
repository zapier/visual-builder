---
title: How Zapier works
order: 1
layout: post-toc
redirect_from: 
    - /quickstart/introduction
    - /docs/zapier-intro
---

# How Zapier works

[Zapier is a tool](https://zapier.com/how-it-works) that helps you automate repetitive tasks between two or more apps, no code necessary. Our customers use Zapier to move information from one app to another automatically rather than manually. Each Zap you create starts with a trigger (something that happens in one app) and then one or more actions (something else that happens in another app).

In order to connect your app to the {{ site.partner_count }} apps on the Zaper Platform to allow your users to build Zaps, your app will need to have a publicly-accessible API which you can use to build your Zapier integration. 

For an intro to APIs in general, check out the [guide](https://zapier.com/learn/apis/). 

When you're ready to get started, [the UI tutorial](https://platform.zapier.com/quickstart/ui-tutorial) offers a great introduction to building your first Zapier integration.

## What do Zapier integrations include?

Zapier integrations are comprised of three core concepts: Authentication, Triggers and Actions. 

Authentication connects an app to Zapier. Users authenticate their account with an app to allow Zapier to access their data in that app. Once a user authenticates, Zapier will use the same authentication credentials for every API call the integration makes on the user's behalf. 

Triggers are how your app's users can start Zaps (automated workflows) whenever an item is added or updated in your app.

Actions are how your app's users can create new or update existing items in your app. 

## How does building an integration work?

All new Zapier integrations are built using Zapier Platform v3, the latest version of our developer platform. You can build integrations using Zapier Platform UI, an online visual builder to create integrations in a form layout. Or, you can use Zapier Platform CLI, a command line interface to build integrations in JavaScript code from your local development environment. 

Both interfaces use the same Zapier Platform and function the same internally, with some [differences to consider when building](https://platform.zapier.com/quickstart/ui-vs-cli).