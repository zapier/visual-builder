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

## How to Design a Successful Zapier Integration

It starts with a Google search, perhaps, or a peek at Zapier's App Directory to find a new integration. Then the user makes a new Zap, either manually or from a Zap Template, and chooses your app. They they connect their account with your app, set up the trigger or action they need for this workflow, and tell Zapier what data to copy from other apps to your app or vise versa.

That's where your Zapier integration is used, and here, the most important thing is how it works. Effective Zapier integrations both include correct branding and deliver the triggers, actions, searches, and fields that users expect.

Each time, users expect consistent messaging and with the items they'd expect to be able to automate from your app. Here are the core considerations to keep in mind to deliver a consistent integration experience.

### Authentication

![Example OAuth v2 Authentication Screen](https://cdn.zapier.com/storage/photos/6f14340218bd51f4047afcdfc71fd9b6.png)

Authentication connects users' accounts on your app to Zapier. This part of the Zapier experience should be as smooth as possible for users. We recommend using OAuth v2 authentication if possible to simplify account connection and minimize set up time.

With OAuth v2, when users select to connect their account on your app with Zapier, they'll see a familiar popup window from your app to select their account or log in, then verify the connection. This fits the flow most modern apps use for integration authentication.

The second best option is API Key authentication. Users should be able to obtain their API key from your app without human intervention. Zapier will not allow your integration to be publicly released if your service requires users to email or call your team in order to receive an API Key or access to your API.

Basic authentication, while acceptable, is the least appropriate authentication type to use for a third party service like Zapier, as users must type their account credentials directly into Zapier's UI.

Here are additional considerations when adding authentication to your integration:

**Include Help Text**: If your authentication requires users to enter a domain name, API key, or other information that could be confusing, always include help text for those authentication input fields. Add links to your app in the help text with [Markdown](https://zapier.com/blog/beginner-ultimate-guide-markdown/).

**Link to API Key (with API Key Authentication)**: If your authentication requires an API key, include a direct URL where users can obtain their API key from your app. If there is no direct link, include as clear of directions as possible to help users find the API key.

**Use a Dedicated Endpoint for Testing**: Your Authentication Test API call should ping an endpoint such as `/me` or `/user` that tests if the authentication was successful but does not require additional input. This call should return a `2xx` error for invalid authentication. Do not use an API call that returns a `4xx` error for missing input data aside from authentication.

**Customize Your Connection Label**: Zapier includes the app name, integration version, and a number to help identify each connected account, so users can add multiple accounts of one app to Zapier. When building your integration's authentication, be sure to customize your connection label to include a username, email address, or other data aside from passwords and API keys entered during authentication or returned by your test trigger. Learn how in Zapier's [Platform UI](https://zapier.github.io/visual-builder/docs/auth#how-to-add-a-connection-label-to-authenticated-accounts) and [Platform CLI](https://zapier.github.io/zapier-platform-cli/#authentication) docs.

### Triggers



https://platform.zapier.com/docs/input-designer#dropdown


### Actions

### Searches


