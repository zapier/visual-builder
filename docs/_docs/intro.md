---
title: Intro
order: 1
layout: post-toc
redirect_from: /docs/
---

## Zapier Intro

Your app shouldn’t do everything. It can’t. Despite every feature request that comes in, the best thing for your app is a clear focus on what makes it unique.

For everything else, there are Zapier integrations. [Zapier](https://zapier.com/) is the most popular way to automate tasks through customized workflows with 1,300+ web apps. Using Zaps, what we call automated Zapier workflows, Zapier can watch for new or updated data in a connected app, then use that data to do anything you need in that or other connected apps. Zaps let your app rely on other best-in-class tools to do the extra things your users want, freeing you to focus on your app’s core features.

Build a Zapier integration, and you’ll clear dozens of your app’s top feature requests at once. You don’t need to build custom integrations with every app. One Zapier integration connects your app to every other Zapier integrated app, with more added every day.

And it’s not much harder than building a form.

## What is a Zapier Integration?

Zapier integrations are different from standalone apps. Say you were building a new email app. You would either use Gmail and Exchange’s APIs to connect to their services, or would build in support for IMAP, SMTP, and/or POP3 protocols. Your app would likely need a database to store every email message, with a UI to manage folders, tags, attached files, and write or view HTML email messages. It would need to support every core feature an email service like Gmail offers.

Zapier integrations are far simpler. Instead of building a complete application that supports every part of your app’s API, Zapier integrations are instead a curated set of an API’s most important features.

Zapier runs in the background, automatically watching for new or updated items in connected apps then using that data to find, create, and/or update items in apps.

Take Gmail’s API for example. It includes API calls to check forwarding and IMAP settings, see the history of a mailbox, undelete messages, and more—along with the more popular options to watch mailboxes for new emails, create new draft messages, and send emails. What should go in Gmail’s Zapier integration?

You first would add Gmail authentication, likely using Zapier's OAuth v2 tool to quickly let users connect their Gmail account through a Gmail standard login experience.

You then would add triggers, the API calls that would tell Zapier when new items came into Gmail. We would definitely want to watch for new emails, and might also want to watch for new draft emails, labels, and attachments. You’d also want actions, API calls that let Zapier do something with Gmail. We would want to send email messages, and likely would also want to create new labels, and drafts. And you would want a search action to find email messages.

Those core features would let users automate their inbox and fit it into their ecosystem of apps. Extra Gmail API calls to see the mailbox history or check IMAP settings wouldn’t be nearly as useful, and couldn’t fit well into a Zap.

Your app’s Zapier integration will be the same. Think through your app’s core API calls. Those that surface new data would be great for triggers; if they support lookups and filtering, they may also make great search actions. The API calls to create or update things in your app would make great actions. And the API calls for settings, deleting data, or seldom-used features would likely be best left out—they're not things users would want to automate on a regular basis.

## What do Zapier Integrations Include?

Zapier integrations require three core things: Authentication, curated API features, and forms.

Start with Authentication. Most apps require authentication, ranging from an API key to access shared data from weather or statistics apps to username-and-password powered Basic auth or OAuth v2 for apps with private user data. When building a Zapier integration, first tell Zapier how to authenticate your apps’ users. Set this once and Zapier will use the same authentication scheme for every API call it makes. The same goes for users: Once they’ve authenticated your app in Zapier, they can use any of its triggers and actions without authenticating again (unless they wish to add a second account).

Next, decide which parts of your app fit best with Zapier. Anything to watch for new data, find existing data, or add new data would likely fit in well. Figure out which of these are most important to your users and would fit best into automated workflows, and list the API calls and input data needed.

Then turn that input data into forms. Triggers often don’t need any extra detail—the API call is enough to get the newest data from your app, and you only need more info to filter that new data (say, to watch for emails with specific labels or from certain mailboxes). Actions, on the other hand, _always_ need data to create new things, the email addresses and names and dates and prices and more Zapier uses to create messages, invoices, events, tasks, and everything else in apps. For that, you need a form. Inside Zapier, users always see a form to fill in data, either with plain text or mapped input fields from previous steps.

You build that form in Zapier Input Designer when creating Zapier actions (and triggers, when they need to filter for specific data). List the data your API endpoints need to create and find items, and make matching form fields in your Zapier integration actions. That together with the action API call will let a simple form in Zapier create anything in your app.
