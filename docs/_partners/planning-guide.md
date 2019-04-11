---
title: How to Design a Zapier Integration
order: 6
layout: post-toc
redirect_from: /docs/
---

# How to Design a Zapier Integration

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

Each Zap step must return data to Zapier to use in subsequent steps. By default, the output data is the direct response from your API—but in some cases, you may need to customize the response data to make it work well with Zapier. Here are general principles for output data from your Zap steps:

**Separate data where possible**, to make it as widely usable as possible in subsequent Zap steps. Names should be split into separate first/last or given/surname pairs, along optionally with a full name field. Addresses should be separated into their individual components.

<a id="date"></a>
**Format Date-time values in [ISO 8601](http://www.cl.cam.ac.uk/~mgk25/iso-time.html#date) standard including time zone offset**, even for UTC times. Avoid UNIX or Epoch timestamps. Dates may be modified with [Moment.js](http://momentjs.com) in your API call custom code if your API returns dates in different formats. Example acceptable date-time values include:

- `2018-12-15T01:15:13Z` (or `-0000` instead of `Z`)
- `2018-12-01T12:32:01-0800`
- `2018-12-01T12:32:01-08:00`
- `2018-12-13` (for date-only values)

**Optionally include an additional human-friendly date** especially for scheduling or calendar app integrations where the date is important for users.

**Set boolean values as `true` or `false`**. Do not use `1` and `0` for boolean values.

**Include the value name and ID in lists and dropdown menus** to help users know which item to choose.

**Consider removing non-necessary fields that may seem confusing to users** in your API call's custom code.

### Actions

**Return data about the item that was created**, not just a `success` message. Action responses should include IDs, details about the new item including a link if possible, and any other useful data about the record.

**Return `4xx` errors for unsuccessful actions**. If your API returns a `2xx` error, add custom code to your API call to replace it with a correct error.

### Searches

**Never raise an error for no Search results.** If the search does not find results, it should return an empty list instead. Your API call should never return a `404` for searches without results. If your API shows an error, use custom code in your API call to return an empty list instead of the error.

***

# Integration Design Examples

Each app has its own unique features, but there are also a number of similarities between apps in similar categories. Here are some examples to keep in mind when designing a [form](#form), [CRM](#crm), or [project management](#pm) app integration:

<a id="form"></a>
## Add a Form or Survey App to Zapier

Form and Survey apps—along with similar apps for polls, applications, and mobile data collection—are ideal apps to integrate with Zapier. Whenever someone fills out the form, that new data needs to go somewhere. Zapier can connect that form to create new contacts, document templates, messages, and more.

Here are things to keep in mind when adding a form-based app to Zapier.

### Triggers

#### Add a New Entry/Response Trigger

![Form app on Zapier](https://cdn.zapier.com/storage/photos/419a35068b794c36a9253a31a309e21d.png)

The most common trigger for a form or survey app is a "New Form Entry/Submission" or "New Survey Response" respectively.

Using our standard "New xxx" naming pattern makes it clear to users that Zapier only retrieves new entries, not existing ones.

#### Let Users Select a Specific Form

![Select Form in Zapier](https://cdn.zapier.com/storage/files/f951d24a065e5a2c56665e51002e7e17.gif)

Most users will have many forms or surveys in your app, so your Zapier integration needs a field where they can choose which form or survey they want to receive results from.

Add a [dynamic dropdown](https://platform.zapier.com/docs/input-designer#how-to-add-dynamic-and-custom-fields) that retrieves the form names exactly as they are listed in your app. Consider ordering the dropdown list by the most recently added to make it easier for users to find the form they need.

You could make the form selector required, so the trigger only watches for results from this one form, which is the recommended option. Or, you could make the field optional so it would trigger for responses to any form; if so, add help text to let users know what to expect if they do not select a form.

### Format Trigger Response

#### Question and Answer Fields

![Example Form field names](https://cdn.zapier.com/storage/photos/554f4fc4856a555714398088f7a162b2.png)

Each form field or survey question needs to include the same name as that form field shows in your app.

For example, in a form that asks for contact information, the question/field “What’s your email?” might internally use an ID like `1839dod38k01` or a generic label such as `Question 1`.

Make sure to include the field's friendly name that the user added in your app, so they'll recognize which field to use when mapping data to action steps. Zapier can also show the raw field ID beside the friendly name.

For example, a common use case is to log responses in spreadsheets, with each answer field mapped to different columns. Using `q_1_answer` as a key name for a question is sensible, but it's not intuitive for users. Specify the full question instead.

Consider including the question number as a prefix to the label as well, to make it even easier for users to find specific questions and fields.

#### Multiple Choice Fields

![Multiple Choice Fields](https://cdn.zapier.com/storage/photos/033953ce0537c18a6efbe47f783ddf5a.png)

If a multiple choice question is based on a spectrum of values (e.g., from "not really" to "very"), it’s sometimes useful to return the choice values (such as `1` to `5`) as well as the actual answer. This can be especially useful for tracking responses in a spreadsheet.

#### Multi-select Fields

![multi-select field](https://cdn.zapier.com/storage/photos/e922d705c9f9d61c46f32b31ba03e53f.png)

If a user can select multiple responses (perhaps in a list of checkboxes or buttons as above), it can be challenging to use this data with Zapier.

![multi-select as individual fields](https://cdn.zapier.com/storage/photos/a71b26a4a333fa9cb6b4a8c77607c426.png)

Consider returning these responses individually. Split each individual response to those questions into its own field, with data if it is selected and a blank response if not selected. This is often easier to map into Zap steps because users can map all responses into one field separated by the correct delimiter, or can take action on specific responses.

![multi-select as comma separated fields](https://cdn.zapier.com/storage/photos/02fd5f03f00a7e3c6953c95366013473.png)

Or, return all the selected values in a single, comma separated response. Users can then easily split the responses themselves with Zapier's [Formatter](https://zapier.com/help/formatter/#using-split-text) tool, or could map the responses together to another field.

#### Date Fields

![Date field from form](https://cdn.zapier.com/storage/photos/291cb5f3b048bcf6cda769f93408128d.png)

Return the timestamp when the response was completed, at a minimum, in [ISO 8601 format](https://platform.zapier.com/partners/planning-guide#date). Also return any dates users can select in the form or survey in ISO 8601 format.

Consider also including a human-friendly date for the response completion and any other selected dates from the form.

#### File Attachments

If users can attach files to form responses, include those in the response data as well. Zapier can request the full file via [file dehydration](https://zapier.github.io/zapier-platform-cli/#file-dehydration), or your app can return a URL for the file.

### Technical Configuration

#### REST Hooks

If possible, use [REST Hooks](https://platform.zapier.com/docs/triggers#rest-hook-trigger) for your trigger, as they will send new form entries to Zapier as soon as the form is filled out. If you have a lot of form entries in a short space of time, webhooks can make your integration more robust, as with polling, there is a chance the number of new entries will exceed your page size of polling results. Additionally, with REST hooks, Zapier won't repeatedly poll your API to check for new responses.

The format of the key/values in a hook should match the format for a polling URL item.

#### Polling URL

If using a Polling trigger, or for the _Perform List_ URL for REST hook triggers, the Polling URL should return the most recent form entry for the chosen form. That lets users set up a Zap using a real entry they recognize.

If there are no entries, you should return an empty list rather than a hard coded sample. We recommend this because every form/survey will be unique to each user, so there’s no way to provide usable static sample data for forms.

#### Sample Results

Zapier requests sample results for every trigger and action, so users can still set up Zaps even if the test API call returns no data. However, with a form app and their dynamic fields from users, it's impossible to define sample fields that work for every form.

Instead, include the bare set of common form fields from every result, such as the form ID and timestamp.

### Form or Survey Integration Test Checklist

Once you’ve built a “New Form Entry” trigger, make Zaps for the following items to ensure your integration works well:

* A form that already has completed entries, where you should check that your polling URL is returning the latest form entry first (reverse chronological)
* A brand new form that has no entries, where you should make sure your form sends an appropriate error
* A form that is composed of required and optional questions, where you should make sure all the questions are mappable regardless of whether the latest response only had a few questions answered.
* A form that has questions with multi select answers, where you should choose one or more options to check that all the values come through

Then submit new entries to your form to check that the Zaps run as expected when turned on.

<a id="crm"></a>

## Add a CRM or Contacts App to Zapier

CRM—or customer relationship management—apps are more than just a list of contact details. They're detailed databases that link contacts with companies, companies with deals, and more. That makes them a bit more tricky to integrate with Zapier than many other apps where each bit of data stands alone.

Here are things to keep in mind to make your CRM integration deliver the experience your users expect.

### Triggers

#### Include Triggers For Every Common Item

Users typically expect the following types of triggers for CRM apps. If your app uses a different name for these items, use the name that appears in your UI so your customers know exactly what to expect:

* New Contact (also: Person, Lead)
* New Deal (also: Opportunity)
* New Company (also: Organization)
* New Tag
* New Note
* New Tag Added to Contact
* New Contact in View (also: Filter)—useful to trigger when contacts meet specific criteria
* New Deal in Stage (also: Group, Segment, or Contact in Stage)—useful to trigger when a deal progresses, if your CRM includes a way to track deal stages

#### Use Separate New and Updated Triggers

Use "New x" triggers only for new items. If you want a way to track updated items, add "Updated x" triggers for those items. That way users can build Zaps that fit their workflows depending on if a contact is new or updated.

## Include Filter Options

![Filter options in a CRM](https://cdn.zapier.com/storage/photos/5dddfc827be95b7125cec7c27ab716bc.png)

Some apps, such as Pipedrive and Salesforce, let users add custom filters or views. If your app has this ability we recommend displaying an optional [dynamic dropdown](https://platform.zapier.com/docs/input-designer#how-to-add-dynamic-and-custom-fields) of the user’s filters. That way, they can use existing filters instead of re-creating them in Zapier.

Ordering the dropdown list by most recently added so users can easily find the filter or view they need.

### Technical Configuration

#### REST Hooks

We recommend you use [REST Hooks](https://platform.zapier.com/docs/triggers#rest-hook-trigger) if possible, so new contacts start Zaps as soon as they're added. This is especially helpful if users import hundreds of contacts to your app, which a paging trigger's API response may not be able to handle.

#### Update Triggers

Updated triggers should run whenever an item has new data added, or when relational data is added or removed. If you are using REST hook triggers, which we recommend, ensure that when relational data is reapplied your app sends Zapier that updated record.

If you are using polling triggers, this may cause issues with [how Zapier perform deduplication](https://platform.zapier.com/legacy_web_builder/dedupe), as we don’t consider the status, stage, or tag to be newly applied to that contact anymore. You may need to customize your API call's code to add a timestamp to the id field you’re using for deduplication so that the Zap triggers anew.

### Trigger Response Format

#### Polling URL

The polling URL should return the most recent record created, so users can set up their Zap using a real entry they recognize.

If there are no recent new records, return an empty array. Zapier will then encourage the user to create a sample then re-test their trigger and finish mapping their Zap.

#### Obtaining Linked Information 

Records in CRMs don't stand alone—they are only one part of a linked ecosystem of data. Getting the full context of linked information is useful. For example, if your trigger is "New Contact" and newly added contacts are linked to organizations, users expect to get full organization data, too.

Linked information should include both IDs to easily map them to your app’s action steps, as well as human-readable data such as individual fields for their name and contact info.

If your record API endpoint does not automatically return additional linked data beyond the ID or name of the record, you will need to add custom code to your trigger API call to fetch the linked record as well.

#### Custom Fields

If your customers typically use custom fields, make sure Zapier pulls in every custom field with [pagination](https://platform.zapier.com/docs/triggers#how-to-use-pagination).

#### Tags

If possible, return tags on records as an array of strings or a comma-delimited list in a single string, so users will be able to easily map them into other apps.

### Searches

#### Include Common Search Actions

Users typically expect to have the following searches for a CRM integration:

* Find Contact (also: Person, Lead)
* Find Deal (also: Opportunity)
* Find Company (also: Organization)

Each should find an existing record, and return it in the same format that the trigger returns records. This ensures that the user gets a consistent experience and can use data from triggers and searches the same way.

### Offer Multiple Search Options

![Infusionsoft Zapier Search Options](https://cdn.zapier.com/storage/files/5395ac18091a4fe7506d5b5e4a8ced60.gif)

If possible, let users search for items by a search key as well as a search value. The search key should be a static dropdown of different fields users can search by, followed by a text input field where users can add the text or item they wish to search for.

For a "Find Contact" search, for example, consider letting users search by Email, ID, or Name.

### Prevent Deduplication Problems

If your CRM doesn’t allow multiple records that have the same value for a field (such as email), consider offering only a single search query for that field instead of providing multiple options. This prevents users from searching on a different field, trying to create a new record, and then being told that a record with that email already exists.

### Offer Parity Across Triggers

Ensure that the field(s) you offer for search are fields that are returned by the trigger steps. For example, a user might use a *New Contact* trigger, and then want to find out more information about the organization the contact is associated with by using a *Find Organization* search. If the *New Contact* trigger only provides the associated organization ID, it doesn’t make sense for the *Find Organization* search to only allow searches for the organization name.

In the same vein, include linked information in search results as in triggers.

#### Error Handling

![Halt a Zap instead of showing an error](https://cdn.zapier.com/storage/files/a57ed995196cb44caf4dd813ac6c60aa.gif)

If a record cannot be found, ensure that it returns a halted exception instead of an error. That way, you can pair the search with a _Create_ action to let users search for items and create them if they don't exist.

*→ Learn more about [searches and creates](https://platform.zapier.com/docs/search-create).*

### Actions

#### Include Common Create Actions

Users typically expect to have the following types of create actions for CRM apps, with either *Create* or *Add* as the first word in the title:

* Create Contact (also: Person, Lead)
* Create Deal (also: Opportunity)
* Create Company (also: Organization)
* Create Note

It’s also useful to include Update actions, as information on records in CRMs tend to change frequently. Any Update action you include should have a corresponding Search action to make it easier for users to update the correct record. For example, an *Add Contact to Stage* create action needs to be paired with a *Find Contact* search.

* Update Contact (also: Deal, Person, Opportunity, Lead)
* Update Company (also: Organization)
* Add Tag to Contact
* Add Contact to Stage (also: Group, Segment)
* Add Contact to Workflow (also: Sequence, Follow-up, Campaign)

You don't need to add all of these actions in the first version of your integration, but over time these are all actions that may be good to add into your integration

#### Allow Linked Records

![Linked Record](https://cdn.zapier.com/storage/photos/19fad8f7f1b3ae44be4425760901329c.png)

Your CRM integration will be especially powerful if users can link other record types when creating a record. For example, in your app’s UI, users may be able to create a contact and link it to existing companies or stages. Offer the same through Zapier, with [dynamic dropdown](https://platform.zapier.com/docs/input-designer#dropdown) to fetch the linked record options and let users select them. Also, link it to a search, so users can either manually select an item, have Zapier find the correct item for this record, or map an ID from a previous step to this field.

That said, do not have one action create multiple items. When a user creates a new contact through Zapier, this should only create new contacts, and should not also create other linked records at the same time. Instead, include a separate action to create the other linked record, along with a contact update action to link the contact after the other record is created. This reduces the chance for errors and record redundancy.

#### Bring in All Custom Fields

Custom fields should be displayed with a human-readable label instead of the internal ID. If the custom fields are radio selects, booleans, or can only accept certain values, add them as [static or dynamic dropdowns](https://platform.zapier.com/docs/input-designer#dropdown) in Zapier.

#### Support Workflows

![CRM workflows in Zapier](https://cdn.zapier.com/storage/photos/ce412bf1bf164bdcde6f624c3ec59fe8.png)

If your app has the lets new records get automatically added to in-app workflows, sequences, follow-ups, or campaigns, make sure records created by Zapier will also get automatically added to workflows. You can also add a boolean field to your action input field to let users select if they want this contact added to a workflow, or include a dynamic dropdown to select the workflow they want.

### CRM Integration Test Checklist

Once you've built your CRM integration, create Zaps for the following scenarios to test your integration and ensure it works as expected:

* Add a record with many custom fields, and make a Zap to watch for new records to make sure each field comes in and what they look like in subsequent steps.
* Make a multi-step Zap (we recommend one trigger, search, and action step) where every step uses your app integration, to check the ease of linking one step to another.
* If you have the option to link records in your integration's actions, check to see that these are linked correctly when creating records.

<a id="pm"></a>
## Add a Project Management or Tasks App to Zapier

You often can't automate the work in your projects, but you can automatically add tasks, spin up new projects, and keep track of what's done with a Zapier product management app integration. Here are the things your users will expect in your integration

### Triggers

#### Include Popular Triggers

Be sure to include at least the following triggers, depending on what your app supports:

* New Project
* New Task (also: Todo, Subtask, Card)
* New File
* New Comment (also: Note)
* New Event
* New Account (also: Member)

![new activity trigger](https://cdn.zapier.com/storage/photos/77fad901c962b2ef853f01c88e4b1d7c.png)

You could also consider including a _New Activity_ trigger, with options to let users choose which type of activity should trigger the Zap. That can be helpful in fitting project management activity into wider workflows.

Then, consider adding update triggers as well. More than in most other apps, users really want to see updates triggers in project management integrations because updates affect their work. They need to know if the task deadline changed, if details were added or the scope was redefined, or if someone completed something. And if they're using multiple task apps, they need Zaps that can move the changes. Here are some popular update triggers to include:

* Updated Project
* Updated Task (also: Todo, Subtask, Card)
* Updated Event
* Completed Task
* Completed Project
* Project moved to Stage (also: Project Changed Status)

#### Watch Out For Permissions

Project Management apps are typically used in a team, so it’s important to ensure that Zaps also trigger on teammates’ activity. For example, if user A creates a Zap that collects comments on projects, they’ll want to know if user B comments on projects as well. 

Permissions may also fluctuate depending on if someone is an admin/creator of a record or not. Typically users expect to be able to automate off any record that is shared with them, regardless if they’re an admin/creator or not, so we strongly recommend ensuring that any trigger behavior encompasses all updates that are visible to a logged-in user in the UI. For example, if I can see that a teammate has made an update to a Project that we are all assigned to, their updates should trigger Zaps connected to my account as well.

If this is not possible with your API, we recommend making this clear in the Trigger description. For example, for a _New Note_ trigger, add help text such as "Triggers when the connected user account adds a note to a project."

## Include Trigger Options

![Trigger Options](https://cdn.zapier.com/storage/photos/4fad8819e9d09ca9fc3b590afe64d947.png)

Add Trigger options so users can select which records they want to receive. For example, a *New Task* trigger could trigger when tasks are added to any project *or* to one specific project. Include [dynamic dropdowns](https://platform.zapier.com/docs/input-designer#how-to-add-dynamic-and-custom-fields) to fetch accounts, projects, lists, and other items users would want to filter.

Order the dropdown list by most recently added to make it easier for users to find their current project.

#### Obtain Linked Information

![Linked Data in Podio Zapier](https://cdn.zapier.com/storage/photos/8ec62dd77f8278ff1626b9c2cf1be47d.png)

Project Management apps, much like CRM apps, are powerful thanks to linked data. Users expect triggers to include any data linked to an item as well. If the data is visible in that item in your app, they expect to use it in Zapier as well. For example, a "New Task" trigger should include details about the task's project as well.

Linked information should include IDs to map to your app’s action steps, as well as human-readable data including the project name and description.

If your API doesn't return linked data by default, add custom code to your API call to make a secondary request for the linked data.

### Searches

#### Include Popular Searches

Users typically expect to be able to find the broader items that organize their projects, including:

* Find Project
* Find Account (also: Member)
* Find Event

Users will typically want to find top-level records so they can add child-level details. For example, a Project can have many Tasks, and some projects may have the same or similar tasks. Users are more likely to want a *Find Project* search so they can add tasks to projects, rather than a Find Task search which may not return the precise item they need.

Searches should find an already existing record, and return it in the same format and with the same data as triggers use, for a consistent experience.

#### Offer Multiple Search Options

![Project Management Search Options](https://cdn.zapier.com/storage/photos/df5c2a77049abfa967e32f043d14811e.png)

If possible, offer multiple ways to search for items, with a dropdown menu to select the search key and a text field to enter what to find. For example, a *Find Project* search should let users search by project ID and name. The former is useful for searching based on data in previous steps, where the latter is useful to find projects with human input.

Additionally, project name searches should exact matches first. It’s likely that users will have similarly named projects, for example, "Promotional Advertisement November" and “Promotional Advertisement September.” Be sure to note how your app returns search results in the help text, as in the Asana screenshot above.

### Actions

#### Include Popular Create Actions

Users typically expect to be able to create everything they could in your app. Use *Create* or *Add* to prefix each action:

* Create Project
* Create Task (also: Todo, Subtask, Card)
* Create File
* Create Comment (also: Note)
* Create Event

Because projects are very dynamic and are often organized across several apps, we strongly recommend adding updates actions as well, such as:

* Update Project
* Complete Task (also: Todo, Subtask, Card. You might try "Update Task Status" if it’s appropriate for your API as well.)
* Update Event

#### Let User Link Records

![Create Action Search](https://cdn.zapier.com/storage/photos/acd4cd6c45be3b17d74b597c1327f282.png)

Your integration will be especially powerful if users can link other record types when creating a record. For example, in your app’s UI, users may be able to create an Event and link it to existing Project. They will want to do the same in Zapier, so include a [dynamic dropdown](https://platform.zapier.com/docs/input-designer#dropdown) where they can select items to link. Also try to include searches for each linked record type to let Zapier automatically find the correct item to link for users.

Only create one record with one Zapier action, though. When a user creates a new Event through Zapier, this should only create new Events, and should not also create other linked records at the same time. This reduces opportunity for error as well as record redundancy for the user.

### Project Management Integration Test Checklist

Once you've built your project management app integration, set up a few Zaps to test out popular scenarios:

* Connect your integration with [other project management apps](https://zapier.com/apps/categories/project-management), to see if the data your integration returns blends well with our common apps. Companies frequently use integration to copy tasks and projects across a blend of project management apps to keep track of work between teams.
* If your integration supports events or tasks with due dates, try connecting them to a popular [calendar or scheduling app](https://zapier.com/apps/categories/calendar) to see if they integrate well.
* If your integration has many nested items (such as projects containing sub-projects with tasks and sub-tasks), try setting up a few Zaps to see if the behavior across nested objects is the same as parent objects. Data returned should always be the same format; if your API doesn’t enable access to nested objects, note that in the help text for that trigger/search/action.