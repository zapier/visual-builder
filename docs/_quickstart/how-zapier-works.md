---
title: How Zapier works
order: 1
layout: post-toc
redirect_from: /quickstart/
---

# How Zapier works

Your app can't do everything. It shouldn't. Despite every new feature request, the best thing is a clear focus on what makes your app unique.

For everything else, there are Zapier integrations. [Zapier](https://zapier.com/) is the most popular way to automate tasks through customized workflows with {{ site.partner_count }} web apps. Using Zaps, what we call automated Zapier workflows, Zapier watches for new or updated data in connected apps, then use that data to do tasks in that or other connected apps. Zaps let your app rely on other best-in-class tools to do the extra things your users want, freeing your app to focus on its core features.

Build a Zapier integration, and you’ll clear dozens of your app’s top feature requests at once. You don’t need to build custom integrations with every app. One Zapier integration connects your app to every other Zapier integrated app, with more added every day.

And it’s not much harder than building a form.

## What is a Zapier integration?

Zapier integrations are different from standalone apps. Say you were building a new email app. You would either use Gmail and Exchange’s APIs to connect to their services, or would build in support for IMAP, SMTP, and/or POP3 protocols. Your app would likely need a database to store every email message, a UI to manage folders, and an editor to write or view HTML email messages. It would need to support every core feature an email service like Gmail offers.

Zapier integrations are far simpler. Instead of a complete application for every part of an API, Zapier integrations are instead a curated set of an API’s most important features.

Zapier runs in the background, automatically watching for new or updated items in connected apps then using that data to find, create, and/or update items in apps.

Take Gmail’s API for example. It includes API calls to check forwarding and IMAP settings, see the history of a mailbox, undelete messages, and more—along with the more popular options to watch mailboxes for new emails, create new draft messages, and send emails. What should go in Gmail’s Zapier integration?

You first would add Gmail authentication, likely using Zapier's OAuth v2 tool to quickly let users connect their Gmail account through a Gmail standard login experience.

You then would add triggers, the API calls that would tell Zapier when new items came into Gmail. Users would want to watch for new emails, and might also want to watch for new draft emails, labels, and attachments.

Then add actions, API calls that let Zapier do something with Gmail. Users would want to send email messages, and likely also want to create new labels and draft messages. You would want to add a search action to find email messages.

Those core features would let users automate their inbox and fit it into their ecosystem of apps. Extra Gmail API calls to see the mailbox history or check IMAP settings wouldn’t be nearly as useful, and couldn’t fit well into a Zap.

Your app’s Zapier integration will be the same. Think through your app’s core API calls. Those that surface new data would be great for triggers; if they support lookups and filtering, they may also make great search actions. The API calls to create or update things in your app would make great actions. And the API calls for settings, deleting data, or seldom-used features would likely be best left out—they're not things users would want to automate on a regular basis.

## What do Zapier integrations include?

Zapier integrations require three core things: Authentication, curated API features, and forms.

Start with Authentication. Most apps require authentication, from API keys or usernames and passwords to OAuth login flows. When building a Zapier integration, first tell Zapier how to authenticate your apps’ users. Set this once and Zapier will use the same authentication scheme for every API call it makes. The same goes for users: Once they’ve authenticated your app in Zapier, they can use any of its triggers and actions without authenticating again (unless they wish to add a second account).

Next, decide which parts of your app fit best with Zapier. Anything to watch for new data, find existing data, or add new data would likely fit in well. Figure out which of these are most important to your users and would fit best into automated workflows, and list the API calls and input data needed.

Then turn that input data into forms. Triggers often don’t need extra detail—the API call is enough to get the newest data from your app, and you only need more info to filter that new data (say, to watch for emails with specific labels or from certain mailboxes). Actions, on the other hand, _always_ need data to create new things, the email addresses and names and dates and prices and more Zapier uses to create messages, invoices, events, tasks, and everything else in apps. For that, you need a form. Inside Zapier, users always see a form to fill in data, either with plain text or mapped input fields from previous steps.

You build that form in Zapier Input Designer when creating Zapier actions (and triggers, when they need to filter for specific data). List the data your API endpoints need to create and find items, and make matching form fields in your Zapier integration actions. That together with the action API call will let a simple form in Zapier create anything in your app.

Repeat that for every trigger and action your Zapier integration needs. Then test your integration—and get 10 or more others to help you test it—and you can release your Zapier integration to the world.

## How does Zapier work?

All new Zapier integrations are built using Zapier Platform v3, the latest version of our development platform. You can build an integration using Zapier's Platform CLI, a command line interface to build integrations in JavaScript code from your local development environment. Or, you could build integrations using Zapier Platform UI, an online visual builder to create integrations in a form layout.

Both interfaces use the same Zapier Platform and function the same internally. In general, Zapier integrations include definitions of API calls for triggers that watch for new and updated data, searches that request specific data, and create actions that send new data to an API. Zapier bundles your app definition along with any input data received from users in life Zaps, prepares API requests, includes authentication details, and makes the API call. Zapier then parses the API response for individual fields and deduplicates the results from Trigger and Search steps that expect an array of results.

Zapier then takes action depending on the step. For triggers, if the item is new, Zapier then runs the remaining Zap steps. For searches, if an item exists, Zapier will perform resource hydration, parse its details and run subsequent steps in the Zap; if it does not exist, Zapier may stop the Zap or run a create action to add that item, depending on user selection in the Zap setup. For actions, Zapier will return the results after creating the item, and either run subsequent steps in the Zap if the Zap includes additional steps, or stop the Zap and log this run of the Zap as successful.

Here's a diagram example of how this works with a trigger step; search and create steps work similarly with their differing final steps as outlined above:

![Zapier Platform Diagram](https://cdn.zapier.com/storage/photos/54fe2e91170f3337ed8648ec29e97aaf.png)

Trigger steps's internal workflow differs if triggered with a rest hook as well.

See [Zapier's Platform CLI documentation](https://zapier.github.io/zapier-platform-cli/#getting-started) for more detail on how Zapier integrations work.


