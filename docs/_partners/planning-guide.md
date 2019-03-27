---
title: How to Build a Zapier Integration
order: 1
layout: post-toc
redirect_from: /docs/
---

## How to Build a Zapier Integration

No app can do everything on its own. The best apps instead focused on their core features, then integrations let them work alongside dozens of other great apps to do the rest. That brings every app’s strong points together—and is what the Zapier platform enables.

A Zapier integration connects your app to 1,300+ of the best business and productivity apps, and puts it in front of millions of Zapier users when they need new apps.

Here are the core things to keep in mind to build a great Zapier integration.

## How to Brand Your Zapier Integration

![Zapier App Directory](https://cdn.zapier.com/storage/photos/49f490f3f9e7e612d9da70627b626fc7.png)
_The Zapier App Directory is the best way to find new apps to add to your workflows_

Your customers already recognize your app name and logo, and they’ll look for it inside Zapier. New customers who are looking for a new tool may also first discover your app through Zapier. That makes a consistent branding experience a core part of a successful Zapier integration.

The search for new apps and integrations starts at the [Zapier App Directory](https://zapier.com/apps/). Apps are ranked by popularity and category, with a search box to filter through the list.

![Zapier app directory pages](https://cdn.zapier.com/storage/photos/448439d942fa0c522b0ac25ee3e5cacd.png)
_App Directory listings help users discover new ways to connect apps_

Click on an app—or search for an app’s integrations—to see its Zapier’s app profile page. Your app’s branding plays the strongest role here as the first place many users will see your app on Zapier. They can explore details about your app and its integrations, or select another popular app to see details about how the two work together.

App profile pages include Zap Templates, predefined and curated examples of popular integration use cases with pre-mapped fields that users can set up in a few clicks.

![Zapier Explore Tab](https://cdn.zapier.com/storage/photos/26bf54b3d6882df8df6be38a84b4fc3a.png)

Inside Zapier’s account dashboard, the _Explore_ tab shows Zap Templates and Zapier content for apps users have connected to their accounts.

![Zap editor app selector](https://cdn.zapier.com/storage/photos/91688ba735515ecdaed48f6f06e7e9b6.png)

Then, inside the core Zapier app, users will again see your app name and logo in the Zap editor, where they can select the apps they want to connect in a Zap.

When you create a Zapier integration, you’ll be asked to add your app’s name, logo, description, category, along with your brand colors when the integration is launched publicly. Follow these guidelines to effectively brand your app on Zapier:

### App Name

Use the actual, unique name of your app with the same capitalization as your company uses in your core branding.

Do not add adjectives or phrases to your app name, and only include your company name if the company and app name are always used together in your branding. Do not include the word _app_ unless you always include that in your app’s branding.

**Example**:

- `Evernote`, not `Evernote Note Taking App` or `EverNote`
- `Google Sheets`, not `Sheets` or `Google Spreadsheets`

### App Logo

Zapier requires a square, transparent PNG formatted logo at least 256x256px in size (please use a bigger version if you have one available). The logo should have a transparent background; if your app has a solid, square background, round the corners 3% of the width.

Do not include the app name in the logo as it will not be legible at small sizes.

### App Description Copy

Write a short description (up to 140 characters) of your app’s core features and use case. Include your app’s name in the description, then explain what makes your app different and the reason one should use it. Use proper English and full sentences.

Do not use flowery or overstated language, and do not mention Zapier or other apps in the description. Do not simply state your app’s category.

**Example**:

- `Trello is a team collaboration tool to organize anything on a kanban board.`, not `Trello is the best project management tool.`
- `Dropbox lets you store files online, sync them to all your devices, and share them easily.`, not `A file storage app.`

### Category

Select the category that best fits your apps’ core features and use case. If your app includes features from multiple categories, choose the category that best describes your app’s primary use case today.

Categories may be updated in the future, so do not select a category that your app does not fit into today but that you anticipate it will fit in with future updates. Additionally, do not select a category that applies only to a secondary feature in your app, nor a narrow category that does not cover your app’s broader focus.

**Example**:

- _Gmail_ is primarily an app to send and receive email messages, so it fits best in the `email` category alongside services like _Microsoft Office 365_, not in the `email newsletters` category with _Mailchimp_.
- _Slack_ is primarily a team communication tool for chat, so it fits best in the `team chat` category alongside apps like _Discord_ and _ChatWork_, not in the `video calls` category even though it does include a video call tool as a secondary feature.
- _Google Contacts_ is primarily an address book that fits best with other `contacts` apps, while _HubSpot CRM_ can manage contacts but also includes deals and contact tracking which makes it a better fit for the `CRM` category.

### Colors

![Zapier primary colors in App Directory](https://cdn.zapier.com/storage/photos/d78c5f1c6ee7eb8ac9ae4501e9e103eb.png)

When you release your Zapier integration to the public, Zapier asks for two additional brand details: Your app’s primary and secondary colors.

The Primary color is the main color used in your app’s logo or branding. The secondary color is a complementary color from your CTAs or as an accent to your primary color.

Do not use pure white (`#FFFFFF`) for either color, as overlaid text would be unreadable. If your logo is black and white, use the next most common color from your branding.

Zapier uses the primary color as the background color in your app’s Zapier App Directory listing, and may additionally use it and the secondary color in the Zapier app dashboard, Zapier blog marketing materials, and other parts of Zapier’s app and content that promote your app’s integrations.

## How to Design a Successful Zapier Integration



### Auth
Triggers
Actions
Searches






## How Does Zapier Work?

All new Zapier integrations are built using Zapier Platform v3, the latest version of our development platform. You can build an integration using Zapier's Platform CLI, a command line interface to build integrations in JavaScript code from your local development environment. Or, you could build integrations using Zapier Platform UI, an online visual builder to create integrations in a form layout.

Both interfaces use the same Zapier Platform and function the same internally. In general, Zapier integrations include definitions of API calls for triggers that watch for new and updated data, searches that request specific data, and create actions that send new data to an API. Zapier bundles your app definition along with any input data received from users in life Zaps, prepares API requests, includes authentication details, and makes the API call. Zapier then parses the API response for individual fields and deduplicates the results from Trigger and Search steps that expect an array of results.

Zapier will then take action depending on the step. For triggers, if the item is new, Zapier then runs the remaining Zap steps. For searches, if an item exists, Zapier will perform resource hydration, parse its details and run subsequent steps in the Zap; if it does not exist, Zapier may stop the Zap or run a create action to add that item, depending on user selection in the Zap setup. For actions, Zapier will return the results after creating the item, and either run subsequent steps in the Zap if the Zap includes additional steps, or stop the Zap and log this run of the Zap as successful.

Here's a diagram example of how this works with a trigger step; search and create steps work similarly with their differing final steps as outlined above:

![Zapier Platform Diagram](https://cdn.zapier.com/storage/photos/54fe2e91170f3337ed8648ec29e97aaf.png)

Trigger steps's internal workflow differs if triggered with a rest hook as well.

See [Zapier's Platform CLI documentation](https://zapier.github.io/zapier-platform-cli/#getting-started) for more detail on how Zapier integrations work.

***

# How Zapier Legacy Web Builder Works

> **Note**: The following only applies to integrations built with Zapier's legacy web builder.

For integrations built with Zapier's [Platform v2]({{base_url}}versions/#version-2-2015-07-31)'s legacy web builder, the following diagrams show how Zapier trigger and action calls work.

## Triggers

To reduce visual noise, assume `KEY` or `TK` is the key you define for your trigger.

### Polling

The methods mentioned here can be seen in more detail in the [Available Methods for Polling doc](https://zapier.com/developer/documentation/v2/available-methods/#polling).

<img src="https://cdn.zapier.com/storage/photos/952e19287daf24693988e64e547d5051.png" alt="Diagram of how Polling Triggers work" style="border: none">

### REST Hooks

> The methods mentioned here can be seen in more detail in the [Available Methods for REST Hooks doc](https://zapier.com/developer/documentation/v2/available-methods/#static-and-rest-hooks).

> NOTE: This diagram excludes the [subscription process](https://zapier.com/developer/documentation/v2/rest-hooks/#step-1-subscribe-smallema-call-from-zapier-to-your-appemsmall) as that will just happen once the Zap’s turned on.

1. Your API makes an HTTP request to Zapier
2. `TK_catch_hook` is called
3. Zapier parses the received data and triggers on it

<img src="https://cdn.zapier.com/storage/photos/d88a35691254c08215cdb3c7e1ba1ca4.png" alt="Diagram of how REST Hook Triggers work" style="border: none">

### Notification REST Hooks

> The methods mentioned here can be seen in more detail in the [Available Methods for Notification REST Hooks doc](https://zapier.com/developer/documentation/v2/available-methods/#notification-rest-hooks).

> NOTE: This diagram excludes the [subscription process](https://zapier.com/developer/documentation/v2/notification-rest-hooks/#step-1-subscribe-smallema-call-from-zapier-to-your-appemsmall) as that will just happen once the Zap’s turned on.

1. Your API makes an HTTP request to Zapier (with the URL for the "GET Resource" call)
2. Zapier builds an HTTP request for the "GET Resource" call
3. `TK_pre_hook` is called
4. Zapier makes the HTTP Request for the "GET Resource" call
5. Your API receives a request and sends back a response
6. `TK_post_hook` is called
7. Zapier parses the received data and triggers on it

<img src="https://cdn.zapier.com/storage/photos/918e49e175c7e6e27d2c85f0f6487ce2.png" alt="Diagram of how Notification REST Hook Triggers work" style="border: none">

## Actions

To reduce visual noise, assume `AK` is your `ACTION_KEY` (what you define as your action’s key) and `SK` is your `SEARCH_KEY` (what you define as your search’s key).

### Writes

> The methods mentioned here can be seen in more detail in the [Available Methods for Actions doc](https://zapier.com/developer/documentation/v2/available-methods/#action-methods).

1. Zapier builds an HTTP Request
2. If `AK_write` exists, it's called (and will override steps 3 through 6)
3. `AK_pre_write` is called
4. Zapier makes the HTTP Request
5. Your API receives a request and sends back a response
6. `AK_post_write` is called
7. Zapier parses the received data, and makes it available for subsequent steps in the Zap

<img src="https://cdn.zapier.com/storage/photos/226846474b0341c4f910a509897abe75.png" alt="Diagram of how Actions work" style="border: none">

> NOTE: If you have the Custom Action Fields URL defined, there are a couple of additional calls to `AK_pre_custom_action_fields` and `AK_post_custom_action_fields` after 2 and before 3.

> NOTE 2: If this write runs as part of a `search_or_write`, there are a couple of additional calls to `SK_read_resource` OR `SK_pre_read_resource` and `SK_post_read_resource` after 6 and before 7, to make sure the output there is the same as the search.

### Searches

> The methods mentioned here can be seen in more detail in the [Available Methods for Searches doc](https://zapier.com/developer/documentation/v2/available-methods/#search-methods).

1. Zapier builds an HTTP Request
2. If `SK_search` exists, it's called (and will override steps 3 through 6)
3. `SK_pre_search` is called
4. Zapier makes the HTTP Request
5. Your API receives a request and sends back a response
6. `SK_post_search` is called
7. If a [Resource URL]({{base_url}}reference/#resource-url) is not set, Zapier skips to step 13
8. If `SK_read_resource` exists, it’s called (and will override steps 8 through 12)
9. Zapier builds an HTTP Request for the “GET Resource” call
10. `SK_pre_read_resource` is called
11. Zapier makes the HTTP Request for the "GET Resource" call
12. Your API receives a request and sends back a response
13. `SK_post_read_resource` is called
14. Zapier parses the received data, and makes it available for subsequent steps in the Zap

<img src="https://cdn.zapier.com/storage/photos/c1b25709ce79c0037a8c2c45b3e952fd.png" alt="Diagram of how Searches work" style="border: none">

> NOTE: If you have the Custom Search Fields URL defined, there are a couple of additional calls to `SK_pre_custom_search_fields` and `SK_post_custom_search_fields` after 2 and before 3