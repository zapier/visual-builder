---
title: How to Build a Zapier Integration
order: 1
layout: post-toc
redirect_from: /docs/
---

# How to Build a Zapier Integration

No app can do everything on its own. The best apps are instead focused on their core features, then rely on integrations with dozens of other great apps to do the rest. That is what the Zapier platform enables. It brings the best of every app together.

A Zapier integration connects your app to 1,300+ of the best business and productivity apps so millions of Zapier users can add it to their workflows.

Here are the core things to keep in mind to build a great Zapier integration.

## How to Brand Your Zapier Integration

![Zapier App Directory](https://cdn.zapier.com/storage/photos/49f490f3f9e7e612d9da70627b626fc7.png)
_The Zapier App Directory is the best way to find new apps to add to your workflows_

Your customers already recognize your app name and logo, and they’ll look for it inside Zapier. Zapier users who have never used your app may discover it through Zapier when looking for a new tool. That makes consistent branding a core part of a successful Zapier integration.

The search for new apps and integrations starts at the [Zapier App Directory](https://zapier.com/apps/). Apps are ranked by popularity and category, with a search box to filter through the list.

![Zapier app directory pages](https://cdn.zapier.com/storage/photos/448439d942fa0c522b0ac25ee3e5cacd.png)
_App Directory listings help users discover new ways to connect apps_

Each app includes a standalone app profile page. Your app’s branding plays the strongest role here as it's the first place many users will see your app on Zapier. They can explore details about your app and its integrations, or select another popular app to see how the two can work together in Zapier.

App profile pages include Zap Templates, predefined and curated examples of popular integration use cases with pre-mapped fields that users can set up in a few clicks.

![Zapier Explore Tab](https://cdn.zapier.com/storage/photos/26bf54b3d6882df8df6be38a84b4fc3a.png)

Inside Zapier’s account dashboard, the _Explore_ tab shows Zap Templates and Zapier content for apps users have connected to their accounts.

![Zap editor app selector](https://cdn.zapier.com/storage/photos/91688ba735515ecdaed48f6f06e7e9b6.png)

Then, inside the core Zapier app, users will again see your app name and logo in the Zap editor, where they can select the apps they want to connect in a Zap.

When you create a Zapier integration, you’ll be asked to add your app’s name, logo, description, category, along with your brand colors when the integration is launched publicly. Follow these guidelines to effectively brand your app on Zapier:

### App Name

Use the actual, unique name of your app with the same capitalization your company uses in your core branding.

Do not add adjectives or phrases to your app name, and only include your company name if the company and app name are always used together in your branding. Do not include the word _app_ unless you always include that in your app’s branding.

**Example**:

- `Evernote`, not `Evernote Note Taking App` or `EverNote`
- `Google Sheets`, not `Sheets` or `Google Spreadsheets`

### App Logo

Upload a square, transparent PNG format logo for your app at least 256x256px in size (please use a bigger version if you have one available). If your app has a solid, square background, round the corners 3% of the width and set the background as transparent. If your icon is not square, make a square transparent image and center your icon inside the transparent square.

Do not include the app name or other copy in the logo as it will not be legible at small sizes.

**Example**:

![Evernote icon on Zapier](https://cdn.zapier.com/storage/photos/eb96efb9ebe4055595f17f49d7733005.png)

Evernote's elephant icon is included in a transparent square rectangle.

![Todoist icon on Zapier](https://cdn.zapier.com/storage/photos/2961bb94baab4009288c24cba96a69ba.png)

Todoist's icon includes transparent, rounded corners.

### App Description Copy

Write a short description (up to 140 characters) of your app’s core features and use cases. Include your app’s name in the description, then explain what makes your app different and the reason one should use it. Use proper English and full sentences.

Do not use flowery or overstated language, and do not mention Zapier or other apps in the description. Do not simply state your app’s category.

**Example**:

- `Trello is a team collaboration tool to organize anything on a kanban board.`, not `Trello is the best project management tool.`
- `Dropbox lets you store files online, sync them to all your devices, and share them easily.`, not `A file storage app.`

### Category

Select the category that best fits your app's core features and use case. If your app includes features from multiple categories, choose the category that best describes your app’s primary use case today.

You may update your app's category anytime if needed, so do not select a category that fits your future ambitions for the app instead of its features today. Additionally, do not select a category that applies only to a secondary feature in your app or a narrow category that does not cover your app’s broader focus.

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

## How to Design Successful Zapier Integrations

It starts with a Google search, perhaps, or a peek at Zapier's App Directory to find a new integration. Then the user makes a new Zap, either manually or from a Zap Template, and chooses your app. They they connect their account with your app, set up the trigger or action they need for this workflow, and tell Zapier what data to copy from other apps to your app or vise versa.

That's where your Zapier integration is used, and here, the most important thing is how it works. Effective Zapier integrations both include correct branding and deliver the triggers, actions, searches, and fields that users expect.

Each time, users expect consistent messaging and with the items they'd expect to be able to automate from your app. Here are the core considerations to keep in mind to deliver a consistent integration experience:

- [Authentication](#authentication)
- [Zap Steps](#zap-steps)
- [Triggers](#triggers)
- [Create Actions](#create-actions)
- [Search Actions](#search-actions)
- [Output Data](#output-data)

## Authentication

![Example OAuth v2 Authentication Screen](https://cdn.zapier.com/storage/photos/6f14340218bd51f4047afcdfc71fd9b6.png)
_OAuth v2 authentication lets users authenticate accounts similar to how they would in other apps_

Authentication connects users' accounts on your app to Zapier. This part of the Zapier experience should be as smooth as possible for users. We recommend using OAuth v2 authentication if possible to simplify account connection and minimize set up time.

> Use OAuth v2 authentication if possible.

With OAuth v2, when users select to connect their account on your app with Zapier, they'll see a familiar popup window from your app to select their account or log in, then verify the connection. This fits the flow most modern apps use for integration authentication.

The second best option is API Key authentication. Users should be able to obtain their API key from your app without human intervention. Zapier will not allow your integration to be publicly released if your service requires users to email or call your team in order to receive an API Key or access to your API.

Basic authentication, while acceptable, is the least appropriate authentication type to use for a third party service like Zapier, as users must type their account credentials directly into Zapier's UI.

Here are additional considerations when adding authentication to your integration:

**Include Help Text**: If your authentication requires users to enter a domain name, API key, or other information that could be confusing, always include help text for those authentication input fields. Add links to your app in the help text with [Markdown](https://zapier.com/blog/beginner-ultimate-guide-markdown/).

**Link to API Key (with API Key Authentication)**: If your authentication requires an API key, include a direct URL where users can obtain their API key from your app. If there is no direct link, include as clear of directions as possible to help users find the API key.

**Use a Dedicated Endpoint for Testing**: Your Authentication Test API call should ping an endpoint such as `/me` or `/user` that tests if the authentication was successful but does not require additional input. This call should return a `2xx` error for invalid authentication. Do not use an API call that returns a `4xx` error for missing input data aside from authentication.

**Customize Your Connection Label**: Zapier includes the app name, integration version, and a number to help identify each connected account, so users can add multiple accounts of one app to Zapier. When building your integration's authentication, be sure to customize your connection label to include a username, email address, or other data aside from passwords and API keys entered during authentication or returned by your test trigger. Learn how in Zapier's [Platform UI](https://zapier.github.io/visual-builder/docs/auth#how-to-add-a-connection-label-to-authenticated-accounts) and [Platform CLI](https://zapier.github.io/zapier-platform-cli/#authentication) docs.

## Zap Steps

Every Zapier integration includes at least one trigger or action, and ideally will include several triggers, actions, and searches to let users do as much with the app through Zapier as possible. Triggers, actions, and searches—together called _Zap Steps_—all have their own unique considerations, but also have some common things to keep in mind.

Follow the following guidelines whenever creating a trigger, create action, or search action:

**Include 3 important triggers, actions, and searches at launch**, and up to 2 more unimportant items. Think through the use cases where users would use your Zapier integration, and try to build Zap steps that fit those needs. You can add additional Zap steps later based on user feedback. Triggers and actions are most important; searches could be added later as advanced features.

**Use a descriptive name**. Each trigger, action, and search must include a name in title case, along with a simple description of what that step does. Start with the phrase "Triggers when", "Creates a new", or "Finds a" for triggers, create actions, and search actions, respectively, followed by three to five words additional words.

**Only include input field help text if needed**. Do not include redundant help text in input fields that repeats the name of the field. Use field help text to tell users what to do, for example "Choose the directory to watch for new files". Always use active voice. If links or formatting are needed, use [Markdown](https://zapier.com/blog/beginner-ultimate-guide-markdown/).

**Use the same name for items as used in your app**, in Zap step names, descriptions, input fields, and input field help text. If the API calls an item something different from the app's UI, match the UI's copy.

**Order input fields logically**, in the same order as they would appear in your app. An action step to create a contact should likely request the contact's name and email first; an email action step should likely request the email recepiant, subject, and message body first. Mimic the order fields are included in your app if possible. Add optional, less-important fields towards the bottom of the input field form.

**Only mark critical fields as required**. If your API call will not be successful without a field, be sure to mark it as required. Otherwise, leave all non-required fields marked as optional.

**Never make users type in an ID number**. Instead, use [Zapier's dynamic dropdown](https://platform.zapier.com/docs/input-designer#dropdown) functionality to show ID numbers and user-friendly names in a list, or add a search action to find the ID number automatically.

**Never ask users to type in a comma separated list**. Instead, use [Zapier's allows multiples](https://platform.zapier.com/docs/input-designer#allows-multiples) functionality to let users enter multiple values and let Zapier turn them into a list.

**Always include a sample data response** so users can successfully set up a Zap even if their app account doesn't include data to test the Zap step.

## Triggers

![Zapier Triggers](https://cdn.zapier.com/storage/photos/dc5aa8f1f3b78a9b192d87b729cbe0cc.png)
_Triggers use new or updated items from apps to start Zap workflows_

Triggers let Zapier watch for new or updated items in your app. Every Zap starts with a trigger, and every Zapier integration should include triggers if the app lets users create items or follow new updates from the app.

Most apps include triggers for new and updated items that users add to their account in the app (contacts, projects, documents, messages, and more). Apps such as monitoring or news apps could include triggers for new events or data. The only apps that would not need triggers are utilities such as conversion tools where there is never new data to act upon.

**Design triggers around how users interact with your app**, not based on which API endpoints are available.

For example, imagine a "New Payments" trigger in an invoice app. Most users care about successful payments, not pending ones. Use a filter in the API call, perhaps, to have Zapier trigger only on successful payments.

Or imagine a “New Email” trigger in an email app. Users may want to watch for specific email messages, so include a trigger field to filter which emails trigger the Zap.

**Include workflow scenarios**, where some action inside your app triggers a Zap. In an email or chat app, a “New Starred Email” trigger lets users do something in your app to triggers a Zap. This helps users build automated workflows that start with an action on their part.

![Update filter in Zapier](https://cdn.zapier.com/storage/photos/4763f54f5baef4f65afd8cf25186696b.png)

**Watch for specific updates**. Don't include a generic "Item Updated" trigger. Think instead about the scenario where users would want to watch for updated items. They may want to watch for deal status changes in a CRM, or email address changes in from contacts. Include filters so users can watch for the specific updates that are important to their work.

**Use REST Hooks whenever possible**. Zaps with [REST hook](http://resthooks.org) triggers run automatically when new data is available, which matches users' expectations from automation. Polling triggers, instead, run `GET` calls every 5 to 15 minutes, depending on the user's Zapier plan, and static webhooks are not supported (as users could instead use Zapier's built-in [Webhooks app](https://zapier.com/apps/webhook/integrations)).

**Only include Trigger input fields where necessary**. Many triggers need no fields, as they simply watch for new or updated items without any additional input from users. If your trigger would return a large amount of data to Zapier and cause the Zap to run too often, include input fields to let users filter and only run the Zap on the data they want.

**Use smart defaults for input fields**. If your API requires a trigger field, use the default value where possible. For example, Dropbox' **New File** trigger watches for new files in the root directory by default. That helps users successfully set up Zaps even if they don't customize the input field.

**Return a reverse chronological ordered array**, ordered by creation or update date. If your API returns items in a different order, you will need to add custom code to your trigger to reorder the response data.

**Make sure your API returns an ID field**. Otherwise, Zapier looks through response data for the shortest field key with `ID` in the key name. If that doesn't exist, Zapier does a hash over every field key and value as a fallback, which can provide unexpected results.

## Actions

![Zapier Action steps](https://cdn.zapier.com/storage/photos/0705da1d3c6b8654f82c32e7e475a748.png)
_Actions add, update, or find items based on data from previous Zap steps_

Actions let Zapier create or update items in your app, or find existing items with a _[Search](#searches)_ action. After a Zap's trigger has found new data, Zapier runs the Zap's subsequent action steps to add or update items with that data.

Triggers are focused on data has been added in your app. Actions are focused on adding data to your app. Most actions create or update a single item, each with multiple details from input fields.

**Focus on popular use cases**. Think about what users would want to automatically create in your app, and build actions for those specific items. Think about everything they would need to create in a workflow—would they need to create folders along with new files? Would they need to add a customer for a new order? That will help you find other actions that may need added.

**Do not add Delete actions**. Deleting data automatically can let users accidentally delete data they didn't intend to delete. Instead, offer less permanent actions such as options to deactivate, unsubscribe, or tag a user in a certain way (where users could then easily delete those items from inside your app).

**Only add Update actions for clear use cases**. Updating items with detailed fields such as contact details are easy, as users can simply add the updated data via Zapier. Updating a longer, single item such as a note or document is harder or impossible to implement, and thus should not be used in a Zapier integration. Update actions should be separate from create actions.

**Actions may create multiple items if needed**, using the same data, though you will likely need to customize the API call code to create both items at once. Only do this for linked items, such as if an app stores customers and customer addresses separately.  If the multiple objects that need to be created are top-level, complex objects in your app, they should be separate actions within Zapier. You can then link the two with a drop-down menu in the action to select the paired item, add a search action for users to find the specific item they need, and then let them match the items with the [_Use a Custom Value_ option](https://zapier.com/help/using-custom-values-dropdown/) in Zapier.

## Searches

![Search in Zapier](https://cdn.zapier.com/storage/photos/4caeafb091addc1d873615ff63e4b20d.png)

Searches let Zapier find items in your app based on input fields. Searches often aren't necessary for new Zapier integrations, but are great to add over time as users request more advanced features.

Searches may enable more advanced actions, where users can find an item then use it in subsequent steps in Zapier. For example, Freshbooks users can first use a Search step to find a client, then use the client ID number that Zapier found to add an invoice for that client in a subsequent step.

**Add searches for items users will need to lookup and use in subsequent steps**. Generic searches that return multiple items aren't useful in Zapier. Only add searches where one individual item will be returned by default, and where that item will likely be needed in another Zap step.

**Include a single search field for most searches**. Users need an input field to tell Zapier what to find, but multiple fields may be confusing. If possible, use the most precise way to find the item. For example, an email address will be most likely to return a unique customer or contact.

**Add help text for advanced searches**. If your app supports advanced searches, such as Airtable or Gmail's custom search syntax, then add help text and a [Markdown](https://zapier.com/blog/beginner-ultimate-guide-markdown/) formatted link to your app's docs to help users create the search query.

![Search or Create in Zapier](https://cdn.zapier.com/storage/photos/d010b0f37b0f06c6f91fa2e2d8478b63.png)

**Add matching Create actions where possible**, then enable the _Search or Create_ functionality in your Search action so Zapier can let users create the item if Zapier doesn't find it. That lets users keep from adding duplicate data to your app, and lets their Zap continue to work even if the search comes back without data.

## Output Data

