---
title: Integration publishing requirements
order: 2
layout: post-toc
redirect_from: 
    - /partners/integration-review-guidelines
    - /publish/integration-publishing-guidelines
---

# Integration publishing requirements

We are excited you are creating an integration for the [Zapier Platform](https://zapier.com/developer-platform). We are here to help you understand our platform and its requirements to successfully prepare your Zapier integration for publishing. Thousands of partners have built integrations on the Zapier Platform, so our mutual users can set up Zaps as easily and quickly as possible.

Your Zapier integration can pass the review for publishing process quickly and smoothly when it meets these requirements. The requirements help maintain quality and consistency for all integrations listed in our [App Directory](https://zapier.com/apps). Please review them carefully before submitting for review to ensure your integration is compliant.

The requirements are arranged into multiple sections: [General](https://platform.zapier.com/publish/integration-publishing-requirements#1-general), [Meta](https://platform.zapier.com/publish/integration-publishing-requirements#2-meta), [Authentication](https://platform.zapier.com/publish/integration-publishing-requirements#3-authentication), [Triggers](https://platform.zapier.com/publish/integration-publishing-requirements#4-triggers), [Actions](https://platform.zapier.com/publish/integration-publishing-requirements#5-actions), [Searches](https://platform.zapier.com/publish/integration-publishing-requirements#6-searches), [Error Handling](https://platform.zapier.com/publish/integration-publishing-requirements#7-error-handling), and [Code](https://platform.zapier.com/integration-publishing-requirements#8-code).

## Key considerations

* Because the Zapier Platform is always changing and improving to keep up with the needs of our customers, this is a living document.
* If you prefer your integration to be accessible to a limited group of users, or if the Zapier integration review requirements do not align with your needs, you might want to consider maintaining your integration as private. Learn more about [private vs public integrations](https://platform.zapier.com/quickstart/private-vs-public-integrations).
* We encourage diversity on the Zapier Platform, provided your integration respects users with varying viewpoints and ensures a high-quality user experience. Any integration found to contain or exhibit behaviour deemed inappropriate, discriminatory or crossing acceptable boundaries will be rejected.
* We reserve the right to remove users from the Zapier Platform and remove integrations from Zapier if there is evidence of not following these requirements or the [Platform Agreement](https://zapier.com/platform/tos). This includes attempts to exploit the review process, illicitly acquire user data, or manipulate test users.


## Pre-submission checklist

Before submitting your [Zapier integration for app review](https://platform.zapier.com/publish/public-integration), familiarize yourself with the criteria the Zapier team uses during app reviews:

* Confirm your integration is fully developed and has undergone thorough testing. This includes creating test Zaps on your end that check for bugs, edge cases, and errors.
* Focus on primary use cases. Review similar integrations in [Zapier’s App Directory](https://zapier.com/apps) for inspiration on which [recommended features](https://platform.zapier.com/build/recommended-integration-features) to include in your integration.
* Ensure all integration information and metadata is complete and accurate. Be sure to follow [Zapier’s standards for integration branding](https://platform.zapier.com/publish/integration-brand-design-guidelines) to fit into the Zapier ecosystem.
* Provide an active demo account and login credentials, plus any other resources that might be needed to review your integration (e.g. login credentials to your product under integration-testing@zapier.com as the username/email and dummy credit card credentials used to test making purchases, if applicable to your integration). The review may need to test triggers, actions, or searches in your integration, so please provide access to the appropriate platforms and resources to do so.
* Test early with real users. Use the [invite links to beta test](https://platform.zapier.com/manage/share-integration) the integration.
* Enable backend services so they’re live and accessible during review.
* Include detailed explanations of non-obvious features in the publishing request notes, including supporting documentation where appropriate. Integrations with unclear aspects may be rejected during the review.
* Your developer should review the [integration check reference documentation](https://platform.zapier.com/publish/integration-checks-reference) while building your integration in order to pass the automatic validation when submitting for publishing. 

## 1. General

### 1.1 Familiarity with Zapier
If you haven’t used Zapier before, [sign up](https://zapier.com/sign-up/) for a free account and try a few popular integrations before building your integration. This will help you understand how Zapier works, how your users will set up Zaps, and how your integration can best fit into Zap workflows.

### 1.2 Key use cases
Your triggers, actions, and searches should focus on the main use cases of your platform. Check similar integrations in [Zapier’s App Directory](https://zapier.com/apps) and [recommended features](https://platform.zapier.com/build/recommended-integration-features) by app category to for ideas on which items to include in your integration.

### 1.3. Integration testing
Test your integration early and often, both internally and externally during the build stage. This will help you catch bugs and identify any usability issues that you otherwise will be asked to address during the review process, extending the time to launch.

#### 1.3.1 Internal Testing
* Create test Zaps in your Zapier account with each of the triggers, actions, and searches in your integration, and run them, so each have some successful runs in the Zap History. This gives you firsthand experience of the Zap setup process our mutual users will go through, and lets you validate that triggers, actions, and searches look and work as intended. We may ask you to share your test Zaps with us when you submit your integration for review.

#### 1.3.2 External testing with real users
* Share your integration's [invite link](https://platform.zapier.com/manage/share-integration) before you request a review to gather early feedback from beta users. 

### 1.4 Consistency in style
The terminology and features in your Zapier integration should be consistent with the terminology and features seen in your product's own UI. We strive to give users a consistent experience throughout Zapier, so your integration should also be consistent with the style used in other popular Zapier integrations. Be sure to follow [Zapier’s integration branding and design requirements](https://platform.zapier.com/publish/intergration-brand-design-guidelines) to ensure your integration suits the Zapier ecosystem well.

### 1.5 Valid test account
The Zapier team verifies each trigger, action and search in the integration to verify they function consistently with the platform. Please set up a valid test account on your platform and share the test credentials via the publishing form. Further requirements for the test account:

* Create the test account with email integration-testing@zapier.com, to give access to the Forgot Password flow.
* Make sure the account includes all the features enabled needed to test out each Zap step with any special configurations set. All paid/premium features required for testing should be unlocked.
* Ensure the account is non-expiring and not under a trial to avoid any interruption during your review and going forward even after your integration goes live. This is required to give Zapier support staff a view of your app's user interface for troubleshooting and testing while supporting our mutual users.
* Provide a demo video or detailed documentation to the Zapier team if testing any features requires an environment that is difficult to replicate or requires specific hardware.
* Supply any other necessary credentials/resources and configure the test account so it’s ready to test. For example,  providing dummy payment data if your integration requires making payments, or configuring your plugin/embed on a test site. Do not give super admin access or enable any features or settings on the test account that are only available to internal employees, and not available to users.

### 1.6 Completeness and platform consistency
Submit your integration for review only when it is complete and ready to be published. Thoroughly test for edge cases, and do not submit with known bugs. Both your product and integration need to work consistently without errors. Products not yet fully launched to the public (app is invite-only or for beta users only) and integrations using sandbox/test/dev environments or endpoints will be asked to remain private until they are ready to be publicly available. Once the app is published, it is visible in the Zapier App Directory and it would be expected that any of our mutual users would be able to connect the application to Zapier.

See the following item regarding “Repeated Submission” for more information. We will not allow incomplete or error-ridden integrations to become public.

### 1.7 Repeated submission
Submitting multiple integrations that are essentially the same ties up the Zapier process and risks the rejection of all the integrations. Please do not flood the Zapier team with multiple, consecutive submissions of the same integration while going through the review process. Violating this policy will result in slower review times for your integration or further penalties.

### 1.8 Misleading or malicious functionality
Your integration must perform as advertised and should not give users the impression the integration is something it is not. If your integration appears to promise certain features and functionalities, it needs to deliver. Do not create a Zapier integration that can be used to spam, phish, or send unsolicited messages to users. If you attempt to cheat the system (for example, by trying to trick the review process, steal user data, or fake real users) your integration will be removed from Zapier and you could be expelled from submitting any integrations in the future. False information and features, including inaccurate data or joke functionalities, such as fake phone calls or SMS are prohibited.

### 1.9 Objectionable content
Integrations should not include content that is discriminatory, defamatory, offensive, mean-spirited, or insensitive with regards to gender, religion, sexual orientation, age, race, national/ethnic origin, or other targeted groups.

## 2. Meta

### 2.1 Integration ownership
The Zapier team needs to ensure the account owning the integration has proper access to associated platform and API, either by working for, being associated with, or being contracted by the company whose integration is in review. This is so we can reach out with questions or support issues during the review and after the integration is public. If it’s not obvious to us the owning account is associated with your integration's company (largely by email domain), we will request proof via an email from a matching domain as the platform or confirmation from someone at the company.

Scenarios which integrations are permitted on the Zapier Platform by status, ownership, and intention:

| Private | Public | Not Allowed |
|---|---|---|
|Anyone that accepts [Zapier Terms of Service](https://zapier.com/platform/tos) can build a private integration.|Integrations by developers who work for the company owning the API or have been contracted by the API owner can go public.|Integrations by developers who are building on an API they own but for a competing product with Zapier.|
|Integrations by developers building on a private API with no intention of going public, are permitted to remain private/invite-only indefinitely. |Integrations by developers who work for or third-party developers (preferably a [trusted developer](https://platform.zapier.com/quickstart/trusted-developers)) hired by the company owning the API and intended to go public, are permitted as private before going public.| Integrations by developers who do not own the API used in the integration or who have not been given explicit permission by the owners of the API. | Integrations by developers who are building on a public API they do not own, and routing traffic to their own servers. Exceptions apply when building on an approved third-party API.|
| Integrations by developers building on a public API they do not own and intend to share with their team (within their company or organization, family and friends, etc.) are only permitted to be private.| | |
| Integrations by developers building on a public API they do not own and intend to sell access to the integration, are only permitted to be private. | | |
| Integrations by developers building with sandbox/test/dev environments or endpoints are only permitted to be private.| | |

### 2.2 Developer information
Ensure all information provided in the Publishing form is accurate and up-to-date. This helps us reach out to the appropriate contacts when questions or support issues arise. 

#### 2.2.1 Homepage URL
* The Homepage URL submitted via the Publishing form should be the homepage URL of the application's marketing site.

### 2.3 Replacement integration
The integration should not already have an equivalent that is public in our App Directory. Each integration published within the Zapier App Directory should represent a distinct, independent app - to ensure the best experience for our mutual customers. If you’re trying to replace an existing (Legacy) integration, check out the guide on [versions](https://platform.zapier.com/manage/versions) and how to deploy changes. Creating separate integrations for the same app brand is not allowed.

### 2.4 Multiple integrations
Do not create separate integrations for functionality that share the same authentication method and interact with the same API. Consolidate the functionality into one, high-level integration.

### 2.5 Name
Use the actual, unique name of your app with the same capitalization your company uses in your core branding. Trademark/copyright identifiers such as a TM suffix aren’t allowed in the app name, though they can be added to the description.

Do not add adjectives or phrases to your app name, and only include your company name if the company and app name are always used together in your branding. Do not include the word "app" unless you always include that in your app’s branding.

### 2.6 Logo
The logo must be a square, transparent PNG at least 256x256px in size. Please use a bigger version if you have one available. If your app has a solid, square background, round the corners 3% of the width and set the background as transparent. If your icon is not square, make a square transparent image and center your icon inside the transparent square. Do not include the app name or other copy in the logo as it will not be legible at small sizes.

### 2.7 Description
Write a short description (up to maximum of 140 characters) of your app’s core features and use cases in the form of `<Integration Name> is a...`. The copy should not include links or mentions of Zapier. Do not use flowery or overstated language, or make make it appear your integration is associated with or endorsed by Zapier.

**Example**:

- `Trello is a team collaboration tool to organize anything on a kanban board.`, not `Trello is the best project management tool.`
- `Dropbox lets you store files online, sync them to all your devices, and share them easily.`, not `A file storage app.`

###  2.8 Category and role
Select the category that best fits your app’s core features and use case. If your app includes features from multiple categories, choose the category that best describes your app’s primary use case today.

You may update your app’s category anytime if needed, so do not select a category that fits your future ambitions for the app instead of its features today. Additionally, do not select a category that applies only to a secondary feature in your app or a narrow category that does not cover your app’s broader focus.

Be sure to select the integration owner’s relationship with your integration in the Role field.

### 2.9 Language
We do not have native support for language other than English on the Zapier Platform. The description of your integration, trigger/action/search names, field names, output field labels, help texts, and error messages must be in English. The data returned from your API and passed back to Zapier can be in the native language of your product.

## 3. Authentication

### 3.1 Connecting accounts
Make connecting new accounts on Zapier easy for users. [OAuth v2](https://platform.zapier.com/build/oauth) is the preferred authentication scheme.

* For non-OAuth v2 authentication schemes, users must have the ability to easily generate and retrieve API keys and/or other required credentials themselves without needing assistance from your support team. 
* Provide help text with guidance on where users can find their credentials if you’re not using Basic Auth. If possible, provide an embedded link using Markdown in the help text straight to the page in the platform where users can find the credentials. For example, “Go to the [[API details](https://www.example.com/manage/api-details)](https://my.xxxx.com/manage/api-details) screen from your <Integration Name> Dashboard to find your API Key.“
* If authenticating to your app requires providing a value in a certain format (such as a sub-domain URL), you should specify this format with the *Input Format* option when adding the input field for this value.

### 3.2. Invalid credentials
When authenticating with invalid credentials, make sure a user-friendly error message is returned containing information a non-technical user can understand. For example, "Your API Key does not appear to be valid." is better than a generic 401 error message.

### 3.3 Connection label
[Connection labels](https://platform.zapier.com/build/auth#how-to-add-a-connection-label-to-authenticated-accounts) for authenticated accounts helps users who connect more than one account to their Zapier account distinguish between accounts. Easily identifiable values such as account name, email address, and name are suitable Connection Labels, but avoid using sensitive information or non-easily identifiable values such as API Keys, API Secrets, and lengthy IDs as Connection Labels. 

### 3.4 HTTPS endpoints
For security purposes, all API endpoints used by in integration must use HTTPS versus HTTP. We also require the authentication or login portal to the platform to be hosted on HTTPS.

## 4. Triggers

### 4.1 Copy

Any copy associated with a trigger should match the copy, text, and terminology used in your product’s UI. This includes the trigger’s name, description, input fields, help text, output fields, etc. For instance, since Dropbox calls directories "folders" in their product UI, the respective trigger in [their Zapier integration](https://zapier.com/apps/dropbox/integrations#triggers-and-actions) refers to "folders" instead of "directories". If your API uses different terminology than your product’s UI, match the UI as users are most familiar with this - not the API.

Additionally, each trigger must have:

* a descriptive, titlecased name. For example, ‘New Lead’, instead of ‘New lead’.
* a descriptive key. For example, ‘new_lead’, instead of ‘trigger_1’.
* a descriptive noun that reflects the object that is being returned in the trigger. This typically is one word and should always be in the singular form. The noun is used around the Zapier platform and will be pluralized automatically to complete various messages to users such as ‘No new <noun> found.‘
* a concise description using our standard phrasing ‘Triggers when...“ and no more than a handful of additional words. Always the description with a period/full stop. Do not include the name of your integration nor capitalize the noun in the description such a ‘Triggers when a new Lead is created in Example CRM.’ 

### 4.2 Trigger input fields
[Trigger input fields](https://platform.zapier.com/build/add-fields), if they exist, should be named appropriately and include help text if their purpose is ambiguous.

#### 4.2.1 ID fields
* Users should never be expected to type in an ID as this is error prone. Your integration should not have any trigger fields labeled ‘<Object Name> ID’, such as ‘Customer ID’. Instead, use Zapier’s [dropdown](https://platform.zapier.com/build/add-fields#dynamic-dropdown) functionality to provide users with a user-friendly list of options.

#### 4.2.2 Help text
* Don't be redundant with help text, and only include it if you have something different to say from the field name such as the expected format of the value or additional instructions. Redundant help text teaches users not to read any help text at all, so important information can be missed.

#### 4.2.3 Optional trigger fields

* If a trigger field is optional, confirm the request does not throw an error in a null case where the users does not select an option.

#### 4.2.4 Field types

* Use the most appropriate [input field type](https://platform.zapier.com/build/add-fields) for each of the input fields to show users what type of data to include. Note the Zap editor does not validate the data to ensure users added the correct item for that field type. 

* If the field can accept multiple values, use our built in [‘List’ property](https://github.com/zapier/zapier-platform/blob/main/packages/schema/docs/build/schema.md#fieldschema) or ‘[Allow Multiples’](https://platform.zapier.com/build/add-fields#allows-multiples) functionality rather than asking users to provide a comma-separated value in a text field.

#### 4.2.5 Ordering
* Put required trigger input fields at the top of the form with optional fields towards the bottom by importance.

### 4.3 Static webhooks
                        
Triggers using static webhooks are not allowed in public Zapier integrations. Users can replicate this functionality on Zapier via our built in [Webhooks integration](https://zapier.com/apps/webhook/integrations). Please consider including authentication and using REST Hooks to provide users with a more streamlined experience.

### 4.4 Polling Triggers
Live Zaps with [polling triggers](https://platform.zapier.com/build/trigger) automatically poll the request URL for new data every 1 to 15 minutes, depending on the user’s [Zapier plan](https://zapier.com/pricing).

* Return results from the polling URL in reverse chronological order by created date, so the most recently created or updated object is returned first. 
* Return a sufficient amount of items from the polling endpoint. Generally, 100 items is plenty for most integrations, but there are cases where it’s common for users to perform an action in your app that would trigger more than 100+ records at once. Note that a trigger with more than 100 new items returned in a poll will run into the [polling trigger throttle](https://platform.zapier.com/build/operating-constraints#polling-trigger-throttle-zapier).
* Use [pagination](https://platform.zapier.com/build/trigger#how-to-use-pagination) on the trigger results if large amounts of data will be returned.
* Each result should contain an explicit `id` field for [deduplication](https://platform.zapier.com/build/dedupe) from the polling endpoint.

### 4.5 REST Hooks
[REST hook-based triggers](https://platform.zapier.com/build/trigger) are Zapier’s preferred implementation of triggers, since they fire immediately after the triggering action is performed. Here’s a [post](https://zapier.com/engineering/introducing-resthooksorg/) further describing why we and our mutual users prefer REST hook triggers over polling triggers.

#### 4.5.1 Multiple subscriptions

* Hook based triggers must allow multiple subscriptions without overwriting subscriptions. You can test this by setting up 2 Zaps with the same trigger, turning them On, and confirming  both Zaps fire successfully when the triggering event is performed in your app.

#### 4.5.2 Polling URL
* Each REST Hook trigger must also have a polling URL defined in the `Perform List`. This allows users to easily pull in sample resources to set up their Zaps without leaving the Zap editor. Without a corresponding polling URL, users would have to navigate off of the Zap editor to the product to create or update a resource each time they setup a Zap.
* Ensure the data returned from the polling URL follows the Polling Trigger requirements above.
* Data returned from the polling URL should exactly match the data returned in the hook payload. Check that field keys from the polling URL and in the hook payload match in spelling and casing.

### 4.6 Response content

#### 4.6.1 Names
* Many actions in Zapier require names to be split into two fields - first/last or given/surname. This conflicts with some naming schemes around the world, but without a separated name field, your trigger may not be compatible with certain integrations. Always provide separated name fields, though feel free to return the full name as well if the response already includes this.

#### 4.6.2 Addresses
* Likewise with names, many actions in Zapier require address components in separate fields (street, street2, city, state, zip), instead of requiring the complete address in a single field. Always provide separated address fields, though feel free to return the complete address as well if the response already includes this.

#### 4.6.3 Date-times
* Date-time values are required to be in [ISO 8601 format](http://www.cl.cam.ac.uk/~mgk25/iso-time.html?utm_source=zapier.com&utm_medium=referral&utm_campaign=zapier#date) and should always include a time zone offset (even if it is UTC). This includes date-time values returned from the polling URL, in the hook payload, and in your sample data. Avoid UNIX/Epoch timestamps. Date-time values may be modified in your API call custom code if your API returns dates in different formats. Example acceptable date-time values include:

    * `2023-12-15T01:15:13Z` (or `-0000` instead of `Z`)
    * `2023-12-01T12:32:01-0800`
    * `2023-12-01T12:32:01-08:00`
    * `2023-12-13` (for date-only values)

#### 4.6.4 Booleans
* Set boolean values as `true` or `false`. Do not use `1` and `0` or alternative representations for boolean values.

#### 4.6.5 Important data
* The response data should include important keys in the most usable format. For example, it helps to return both the ID and pretty name of objects, any contact information, and links to the resource (ex: for a New Card in Trello trigger, a url `link to card).

#### 4.6.6 Unnecessary/excess data
* Remove unnecessary fields that may seem confusing or add noise to users’ Zap setup process. For example, if the response content includes information about the request itself and the input fields provided, please remove those fields from the returned response.

#### 4.6.7 Dropdown fields

* Return both the name and ID of the selected dropdown option to be used in subsequent steps of a Zap. 

### 4.7 Sample Data

Each trigger requires [sample data](https://platform.zapier.com/build/sample-data) for instances where no result is returned during Zap setup or the user chooses to skip testing. This could be because the API is temporarily down, or because the user has no existing data in their account to return. The sample data must:

* Only represent one item, and not the entire response of the request if there are multiple items returned as a set. For example, {"key": "value"} instead of [{"key": "value"}, {"key": "value2"}, ... ]. 
* Use representative data in the expected format the values will be returned. For example, don’t set a ‘first name’ key to a value of ‘string’ or ‘1234’; set it to something like ‘Bob’.
* Only return the keys that would be returned in every response for all users of the trigger. This means if there are custom fields that will be returned for some users and not others, please do not include these in the sample data.

### 4.8 Output fields

[Output fields](https://platform.zapier.com/build/sample-data) add user-friendly labels to your API’s response to facilitate mapping fields during Zap setup for users. By default, Zapier will try to make a friendly version of the response by capitalizing words and replacing underscores with spaces, but this can be customized. Add a custom output field label when:

* a field is abbreviated. For example, ‘LTV’ should be labeled ‘Lifetime Value’.
* a field has an ambiguous unit of measure. For example, ‘Duration’ should be labeled ‘Duration (in seconds)’.
* a field is represented by an ID.
* in general, it is not instantly clear what the field or value represents.


### 4.9 Update triggers
Don't offer a generic 'Updated <object name>' trigger, as these are often too general for users to use in their Zaps. Instead, think under what specific scenarios the user needs an update trigger. For example, instead of offering an 'Updated Deal' trigger which triggers when anything changes on the deal, offer a 'New Deal in Stage' or 'Updated Deal Status' trigger that allows the user to specify which stage they want to monitor.

### 4.10 Error Messages
Users should never receive a success/200 response if there was an error in the request as this will not show up as an error in the Zap history. All error messages should be user-friendly and avoid technical jargon. Be as specific as possible to what caused the error.

## 5. Actions

### 5.1 Copy

The copy for actions should match your product’s UI. This includes the action’s name, description, input fields, help text, etc. For instance, since Dropbox calls directories "folders" in their product UI, the Zapier integration should refer to "folders" in the respective action. If the API uses different terminology than your product’s UI, match the UI - not the API.

Additionally, each action must have:

* a descriptive, titlecased name. For example, ‘Create Lead’, instead of ‘Create lead’.
* a descriptive key. For example, ‘create_lead’, instead of ‘action_1’.
* a descriptive noun that reflects the object that is being fired in the trigger. This should typically be one word and should always be in the singular form. The noun is used around the Zapier platform and will be pluralized automatically to complete various messages to users such as ‘No new <noun> found.‘
* a concise description starting with a plural form of the action verb, and ending in a period/fullstop. For example, the description for a ‘Create Lead’ action could be ‘Creates a new lead.’ Please do not include the name of the platform nor capitalize the noun such a  ‘Creates a new Lead in XXX CRM.’

### 5.2 Action input fields
All action steps *must* include [input fields](https://platform.zapier.com/build/add-fields) to gather the data needed to create, update, or perform the intended action.

#### 5.2.1 ID fields

* Users should never be expected to manually type or map an internal ID to an action field. Your integration should not have input fields labeled ‘XXX ID’. Generally, trigger and action steps of other integrations do not return internal IDs for your specific platform to be used in an action field from your Zapier integration. Use Zapier’s [dynamic dropdown](https://platform.zapier.com/build/add-fields#dynamic-dropdown) and [Search Connector](https://platform.zapier.com/build/add-fields#dynamic-dropdown:~:text=**%203.Add%20search%20to%20a%20dynamic%20field%20(optional)**)/[search-powered field](https://github.com/zapier/zapier-platform/blob/main/packages/cli/README.md#how-do-search-powered-fields-relate-to-dynamic-dropdowns-and-why-are-they-both-required-together) functionalities to provide users with an easier way to select or search for the appropriate resource by a more readily-available value such as ‘name’, ‘email address’, ‘title’, etc.

#### 5.2.2 Ordering
* Order action fields logically. If you are unsure, look at how the respective fields are ordered in your platform and mimic that since users will be familiar with that ordering. 
* Required action fields should generally be listed first at the top of the Zap editor.
* Place all optional, lesser-used fields towards the bottom.
* Group related fields together. For example, first name and last name fields, as well as individual address component fields should be ordered consecutively. Do NOT use [line-item groups](hhttps://platform.zapier.com/build/line-items) or the [‘children’](https://github.com/zapier/zapier-platform/blob/main/packages/schema/docs/build/schema.md#fieldschema) field schema key to visually group fields; these are solely intended for line-item functionality.

#### 5.2.3 Required fields
* If a field is not required by your API, don't make it required in the Zap action. Parallel the required fields from your integration as closely as possible. For example, if 'Email Address' is not required to create a lead in the platform, do not make the 'Email Address' field required in the Zap editor. If the API specifies a non-important field as required, hard-code a default value so the field is not empty if one is not provided by the user.
* If the action step has a case where one field OR another field is required, set both fields as optional, add help text to both fields stating that one or the other is required, and throw a user-friendly error message if neither field is filled.

#### 5.2.4 Help text
* Don't be redundant with help text, and only include it if you have something different to say from the field name such as the expected format of the value or additional instructions. For example, help text for an 'Email Address' field stating 'Contact's email address' is not necessary. Redundant help text teaches users not to read any help text at all, so important information can be missed. You may use [Markdown](https://zapier.com/blog/beginner-ultimate-guide-markdown/) formatting in help text.

#### 5.2.5 Default values

* Set [default values](https://platform.zapier.com/build/add-fields) for input fields sparingly, but when:

* the API specifies an unimportant field as required, set a default value in case one is not provided by the user.
* the field in the platform is set to or shows a default value, set the same default value for the action field in the Zapier integration.

#### 5.2.6 Field types

* Use the most appropriate [input field type](https://platform.zapier.com/build/add-fields) for each of the input fields to show users what type of data to include — note Zapier does not validate the data to ensure users added the correct item for that field type.

* If the field can accept multiple values, use our built in [‘List’ property](https://github.com/zapier/zapier-platform/blob/main/packages/schema/docs/build/schema.md#fieldschema) or ‘[Allow Multiples’](https://platform.zapier.com/build/add-fields#allows-multiples) functionality rather than asking users to provide a comma-separated lis of values in a text field.

### 5.3 [Response content](https://platform.zapier.com/build/response-types)

Return information about the resource that was created, updated, or affected by the action, and not just a 'success' message. At a minimum, return an ID, the name or title of the resource (when pertinent), and a link to the newly created, updated, or affected resource in the platform (if available). Additionally, return any other useful data about the resource users may need in subsequent actions of a multi-step Zap.

#### 5.3.1 Date-times
* Date-time values are required to be in standard [ISO 8601 format](http://www.cl.cam.ac.uk/~mgk25/iso-time.html?utm_source=zapier.com&utm_medium=referral&utm_campaign=zapier#date) and should always include a time zone offset (even if it is UTC). This includes date-time values returned in the response content, and in your sample data. Avoid UNIX/Epoch timestamps. Date-time values may be modified in your API call custom code if your API returns dates in different formats. Example acceptable date-time values include:

    * `2023-12-15T01:15:13Z` (or `-0000` instead of `Z`)
    * `2023-12-01T12:32:01-0800`
    * `2023-12-01T12:32:01-08:00`
    * `2023-12-13` (for date-only values)

#### 5.3.2 Booleans
* Set boolean values as `true` or `false`. Do not use `1` and `0` or alternative representations for boolean values.

#### 5.3.3 Important data

* The response data should include important fields in the most usable format. For example, it helps to return both the ID and pretty name of resources, any important information about the resource such as contact information, and a link to the resource in the platform (ex: Create Card in Trello action returns a url link to the card created).

* Returning a link of the newly created/updated/affected resource in the action’s response data helps users link to the resource in subsequent steps of a multi-step Zap and confirms the new resource was created. This is also helpful for Zapier support team when debugging issues.

#### 5.3.4 Unnecessary/excess data
* Remove non-necessary fields that may seem confusing or add unnecessary noise to users’ Zap setup process from your API call’s custom code. For example, if the response content includes information about the request itself and the input fields provided, please remove those fields from the returned response.

#### 5.3.5 Dropdown fields

* Return both the name and ID of the selected dropdown option to be used in subsequent steps of the Zap. 

### 5.4 Sample data

The ‘Test’ step on actions sends a real request on behalf of the connected account. Therefore, each action requires [sample data](https://platform.zapier.com/build/sample-data) for instances when the user does not wish to actually run the action in their account to finish setting up the Zap. The sample data must:

* Represent the expected return from the request when a record is successfully created or found. 
* Use representative data in the expected format the values will be returned. For example, don’t set a ‘first name’ key value to ‘string’ or ‘1234’; set it to something like ‘Bob’.
* Reflect the keys returned in every response for all users of the action. This means if there are custom fields that will be returned for some users and not others, please do not include these key:values in the sample data.

### 5.5 Output fields

[Output Fields](https://platform.zapier.com/build/sample-data) add user-friendly labels to your API’s response data to facilitate mapping fields during Zap setup for users. By default, Zapier will try to make friendly version of your API’s response, capitalizing words, and replacing underscores with spaces, but they an also be customized. Add a custom output field label when:

* a field is abbreviated. For example, ‘LTV’ should be labeled ‘Lifetime Value’.
* a field has an ambiguous unit of measure. For example, ‘Duration’ should be labeled ‘Duration (in seconds)’.
* a field is represented by an ID.
* in general, it is not instantly clear what the field or value represents.

### 5.6 Create or update functionality
If your integration must have a ‘Create-or-Update’ functionality, implement a ‘Search-or-Create’ with an ‘Update’ action versus a ‘Search’ with a ‘Create-or-Update’ action or a standalone ‘Create-or-Update’ action.

### 5.7 Delete actions
Avoid delete actions which make it easy for users to accidentally delete data they didn’t intend to remove. Instead, offer less permanent actions such as options to deactivate, unsubscribe, or tag a user in a certain way (where users could then easily delete those items from inside your app).

## 6. Searches

### 6.1 Find or create

Search actions can optionally create items if nothing is found in the search. If your integration has a ‘Create-or-Update’ action, please implement a ‘Search-or-Create’ with an ‘Update’ action versus a ‘Search’ with a ‘Create-or-Update’ action or a standalone ‘Create-or-Update’ action.

### 6.2 Copy
The copy for searches should match your product’s UI. This includes search name, description, input fields, help text, etc. For instance, since Dropbox calls directories "folders" in their product UI, the Zapier integration should refer to "folders" in the respective search. If the API uses different terminology than your integration's UI, match the UI - not the API.

Additionally, each search must have:

* a descriptive, titlecased name. Use ‘Find’ over ‘Get’. For example, ‘Find Lead’, instead of ‘Get lead’.
* a descriptive key. For example, ‘find_lead’, instead of ‘search_1’.
* a descriptive noun that reflects the object that will be returned. This should typically be one word and should always be in the singular form. The noun is used around the Zapier platform and will be pluralized automatically to complete various messages to users such as ‘No new <noun> found.‘
* a concise description starting with a plural form of the verb, which typically is ‘Finds’, and ending in a period/fullstop. For example, a valid description for a ‘Find Lead’ search is ‘Finds a new lead.’ Please do not include the name of the platform nor capitalize the noun such a  ‘Finds a new Lead in XXX CRM.’

### 6.3 Search fields
[Search input fields](https://platform.zapier.com/build/add-fields) should be named appropriately and include help text if their purpose is ambiguous.

#### 6.3.1 ID fields
* Users should never be expected to manually type or map an internal ID to a search field. Your integration should not have search fields labeled ‘XXX ID’. Trigger and action steps of other integrations do not return internal IDs for your specific app that could be used in an action field for your Zapier integration. And if the user *is* using a trigger from your Zapier integration, the trigger should return all necessary information about the resource without the Zap needing a search step to retrieve additional, necessary information. Instead, provide search field options for more general information such as ‘name’, ‘email address’, ‘phone number’, ‘title’, etc. that is more readily-available from all triggers.

#### 6.3.2 Help text
* Don't be redundant with help text, and only include it if you have something different to say from the field name such as the expected format of the value or additional instructions. Redundant help text teaches users not to read any help text at all, so important information can be missed.

#### 6.3.3 Optional search fields
* If a search field is optional, confirm the request does not throw an error in a null case where the users does not select an option.

#### 6.3.4 Field types
* Use the most appropriate [input field type](https://platform.zapier.com/build/add-fields) for each of the input fields to show users what type of data to include — note Zapier does not validate the data to ensure users added the correct item for that field type. 
* If the field can accept multiple values, use our built in [‘List’ property](https://github.com/zapier/zapier-platform/blob/main/packages/schema/docs/build/schema.md#fieldschema) or ‘[Allow Multiples’](https://platform.zapier.com/build/add-fields#allows-multiples) functionality rather than asking users to provide a comma-separated list of values in a text field.

#### 6.3.5 Ordering
* Put required search fields at the top of the form with optional fields towards the bottom by importance.

### 6.4 Response content
While create actions return a single object to Zapier; searches must return an array of objects. Each search must follow these requirements:

#### 6.4.1 No result

* Do not raise an error if there are no search results to return. If your API returns a 404 for search misses, use custom code to return a 200 with an empty array as the response.

#### 6.4.2 Names
* Many actions in Zapier require names to be split into two fields - first/last or given/surname. This conflicts with some naming schemes around the world, but without a separated name field, your action may not be compatible with certain integrations in subsequent steps of a user's Zap. Always provide separated name fields if applicable, though feel free to return the full name as well if the response already includes this.

#### 6.4.3 Addresses
* Likewise with names, most actions in Zapier require address components in separate fields (street, street2, city, state, zip), instead of requiring the complete address in a single field. Always provide separated address fields, though feel free to return the complete address as well if the response already includes this.

#### 6.4.4 Date-times
* Date-time values are required to be in [ISO 8601 format](http://www.cl.cam.ac.uk/~mgk25/iso-time.html?utm_source=zapier.com&utm_medium=referral&utm_campaign=zapier#date) and should always include a time zone offset (even if it is UTC). This includes date-time values returned in the response content, and in your sample data. Avoid UNIX/Epoch timestamps. Date-time values may be modified in your API call custom code if your API returns dates in different formats. Example acceptable date-time values include:

    * `2023-12-15T01:15:13Z` (or `-0000` instead of `Z`)
    * `2023-12-01T12:32:01-0800`
    * `2023-12-01T12:32:01-08:00`
    * `2023-12-13` (for date-only values)

#### 6.4.5 Booleans
* Set boolean values as `true` or `false`. Do not use `1` and `0` or alternative representations for boolean values.

#### 6.4.6 Important Data
* The response data should include important fields in the most usable format. For example, it helps to return both the ID and pretty name of resources, any important information about the resource such as contact information, and a link to the resource in the platform (ex: Find Card in Trello search, returns a url link to the found card).

#### 6.4.7 Unnecessary/Excess Data
* Remove unnecessary fields that may seem confusing or add noise to users’ Zap setup process from your API call’s custom code. For example, if the response content includes information about the request itself and the input fields provided, please remove those fields from the returned response.

### 6.5 Sample Data
Each search requires [sample data](https://platform.zapier.com/build/sample-data) for instances where no result is returned during Zap setup. This could be because the API is temporarily down, or because no result is returned for the specific search the user tests. The sample data must:

* Only represent one record, and not the entire return from the request if there are multiple records returned as a set. For example, {"key": "value"} instead of [{"key": "value"}, {"key": "value2"}, ... ]. 
* Use representative data in the expected format the values will be returned. For example, don’t set a ‘first name’ key value to ‘string’ or ‘1234’; set it to something like ‘Bob’.
* Reflect keys available in every response for all users of the search. This means if there are custom fields that will be returned for some users and not others, please do not include these key:values in the sample data.

### 6.6 Output fields
[Output fields](https://platform.zapier.com/build/sample-data) add user-friendly labels to your API’s response data to facilitate mapping fields during Zap setup for users. By default, Zapier will try to make friendly version of your API’s response, capitalizing words, and replacing underscores with spaces, but they an also be customized. Add a custom output field label when:

* a field is abbreviated. For example, ‘LTV’ should be labeled ‘Lifetime Value’.
* a field has an ambiguous unit of measure. For example, ‘Duration’ should be labeled ‘Duration (in seconds)’.
* a field is represented by an ID.
* in general, it is not instantly clear what the field or value represents.

## 7. [Error handling](https://platform.zapier.com/manage/error-handling)
APIs are not always available. Users do not always provide valid data for requests. Build a defensive and resilient integration. Plan for 4xx and 5xx responses. Without proper handling, errors can have incomprehensible messages, technical error codes, or remain unnoticed by users.

### 7.1 General errors
Use `z.errors.Error` in situations where users misconfigure their Zaps and need to take action. Typically, this will be for prettifying `4xx` responses and APIs that return errors as `200` with a payload that describes the error with guidance on how to correct it.

* If a Zap raises too many error messages it will be [automatically turned off](https://help.zapier.com/hc/en-us/articles/8496037690637-Troubleshoot-errors-in-Zapier#500-series-error-codes-0-3), so only throw these if the scenario is truly an error that needs to be fixed.
* Elaborate on terse messages. 'Your API Key is invalid.' is better than 'not_authenticated.' 
* If the error calls out a specific field, surface that information to the user. ‘Title is not valid.’ is better than ‘Invalid Request.’
* If the error provides details about why a field is invalid, surface that information to users. ‘Title is invalid. Please only use alphanumeric characters.’ is better than ‘Title is invalid.‘

### 7.2 Halting errors
Use `z.errors.HaltedError` in situations where a required pre-condition is not met. For instance, in an action to add an email address to a list where duplicates are not allowed, throw a `HaltedError` if the Zap attempted to add a duplicate. This          indicates failure, but is treated as a soft failure. Thus, unlike general errors, a Zap will never be turned off when this error is thrown even if it is raised more often than not.

### 7.3 Stale authentication credentials
* For integrations requiring manual refresh of authorization on a regular basis, Zapier provides `z.errors.ExpiredAuthError`, so the current operation is interrupted, the Zap is turned off (to prevent additional runs with expired credentials), and a predefined email is sent out informing the user to refresh the credentials. The runs will be [Held](https://help.zapier.com/hc/en-us/articles/20505304170637-Review-Zap-run-statuses), and the user will be able to replay them after reconnecting.
* For integrations using OAuth2 with automatic refresh requests or Session Auth, use `z.errors.RefreshAuthError`. This signals Zapier to refresh the credentials and retry the failed operation.

## 8. Code

### 8.1 Environment variables
Do not hard code credentials such as API Keys, Client IDs, Client Secrets, etc. into your integration. Use [environment variables](https://platform.zapier.com/build/env) instead. 

### 8.2 Structure
If you are using the [Zapier CLI](https://github.com/zapier/zapier-platform/blob/main/packages/cli/README.md) to build the integration, ensure files are logically broken out into respective directories and the code is easy to follow. We suggest putting triggers, actions, and searches each in their own directories.

If you have any questions or concerns about our integration publishing requirements, contact Zapier via the [contact form](https://developer.zapier.com/contact).

### 8.3 Dependencies
If you are using the [Zapier CLI](https://platform.zapier.com/reference/cli-docs), keep dependencies up to date. When notified that a dependency must be updated—for example, `zapier-platform-legacy-scripting-runner`, `zapier-platform-core`, or `zapier-platform-cli`—complete the update in a timely manner or by the stated deadline. If requested updates are not completed by the stated deadline, Zapier reserves the right to make necessary updates on your behalf.