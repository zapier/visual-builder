---
title: Integration build guidelines
order: 2
layout: post-toc
redirect_from:
---

# Integration Build Guidelines

Before publishing your integration on Zapier, it is essential to ensure that your integration is well-prepared to provide a seamless and efficient user experience. The following guidelines are designed to assist you in refining your integration before submitting it for review. Adhering to these guidelines will help enhance the functionality and user interaction with your integration and will provide you with the best value and opportunities to harness Zapier as a method of obtaining new users and most commonly, boosting the lifetime value of your current customers

## Familiariasation and testing

### Familiarize yourself with Zapier

If new to Zapier, start by signing up for a free account and experimenting with [popular integrations](https://zapier.com/apps). This will help you understand how Zapier works, how your users will set up Zaps, and how your integration can best fit into Zap workflows

### Identify key use cases

Focus on the primary functionalities of your application. Review similar integrations in [Zapier’s App Directory](https://zapier.com/apps) and [recommended features](https://platform.zapier.com/build/recommended-integration-features) by app category for ideas on which items to include in your integration. Also, get feedback from your current customer base on their needs and wants from automation with your application.

### Thorough integration testing

- **Internal Testing**: Develop and test Zaps using your integration’s triggers, actions, and searches in your Zapier account. Ensure these are error-free and have successful runs in the Zap History. This gives you firsthand experience of the Zap setup process our mutual users will go through.
- **External Testing**: [Share your integration](https://platform.zapier.com/manage/sharing) with external users before submitting it for review to gather early feedback from them and make changes to the integration when necessary.

### Provision of demo accounts and resources

Provide access to a fully functional demo account and any necessary resources to facilitate the review process.

### Automatic validation checks

Review the [integration check reference documentation](https://platform.zapier.com/publish/integration-checks-reference) while building your integration to pass the automatic validation when submitting for publishing. To publish your integration, all Errors and Publishing Tasks must be validated. Warnings are non-blocking and not strictly required to proceed as they would not prevent you from promoting a version, though we do recommend you review them for the usability of your integration.

## Integration information

### Comprehensive documentation and metadata

All integration information, including the name, logo, description, and category, should be complete, accurate, and adhere to [Zapier’s branding standards](https://platform.zapier.com/publish/branding-guidelines). If your app includes features from multiple categories, choose the category that best describes your app’s primary use case today.

### Clarify non-obvious features

Detail any complex features in your publishing request notes, and include relevant documentation to support understanding and review.

### Consistency in style and branding

The terminology and features in your Zapier integration should be consistent with the terminology and features seen in your product’s UI. We strive to give users a consistent experience throughout Zapier, so your integration should also be consistent with the style used in other popular Zapier integrations. Be sure to follow [Zapier’s integration branding and design requirements](https://platform.zapier.com/publish/intergration-brand-design-guidelines) to ensure your integration suits the Zapier ecosystem well.

## Authentication

### Ease of connecting accounts

Simplify the authentication process, preferably using [OAuth v2](https://platform.zapier.com/build/oauth). For non-OAuth v2 authentication schemes, users must be able to easily generate and retrieve API keys and/or other required credentials themselves without needing assistance from your support team.

### Help texts

Provide help texts for authentication fields with guidance on where users can find their credentials if you’re not using Basic Auth. If possible, provide an embedded [link](https://www.markdownguide.org/basic-syntax/#links) using [Markdown](https://www.markdownguide.org/) in the help text straight to the page in the platform where users can find the credentials. For example, “Go to the [API details](https://my.xxxx.com/manage/api-details) screen from your Dashboard to find your API Key.“

### Input format

If authenticating to your app requires providing a value in a certain format (such as a sub-domain URL), you should specify this format with the Input Format option when adding the input field for this value.

### Handling invalid credentials

Return informative and user-friendly error messages for authentication issues. For example, “Your API Key does not appear to be valid.” is better than a generic 401 error message.

## Triggers

### Trigger design and copy

Any copy associated with a trigger should match the copy, text, and terminology used in your product’s UI. This includes the trigger’s name, description, input fields, help text, output fields, etc. For instance, since Dropbox calls directories “folders” in their product UI, the respective trigger in [their Zapier integration](https://zapier.com/apps/dropbox/integrations#triggers-and-actions) refers to “folders” instead of “directories”. If your API uses different terminology than your product’s UI, match the UI as users are most familiar with this - not the API.

Additionally, each trigger must have:

- a descriptive, titlecased name. For example, ‘New Lead’, instead of ‘New lead’.

- a descriptive key. For example, ‘new_lead’, instead of ‘trigger_1’.

- a descriptive noun that reflects the object that is being returned in the trigger. This typically is one word and should always be in the singular form. The noun is used around the Zapier platform and will be pluralized automatically to complete various messages to users such as ‘No new X found.‘

- a concise description using our standard phrasing ‘Triggers when…“ and no more than a handful of additional words. Always the description with a period/full-stop. Do not include the name of your integration nor capitalize the noun in the description such as ‘Triggers when a new Lead is created in Example CRM.’

### Trigger input fields

[Trigger input fields](https://platform.zapier.com/build/add-fields), if they exist, should be named appropriately and include help text if their purpose is ambiguous. Use appropriate naming, ordering, and field types. Avoid unnecessary complexity in ID fields and include helpful tooltips where necessary.

- **ID fields**: Users should never be expected to type in an ID as this is error prone. Your integration should not have any trigger fields labeled ‘ ID’, such as ‘Customer ID’. Instead, use Zapier’s dropdown functionality to provide users with a user-friendly list of options.

- **Help texts**: Don’t be redundant with help text, and only include it if you have something different to say from the field name such as the expected format of the value or additional instructions that would aid users in knowing what value the field expects and sometimes, how they can get those values. Redundant help text teaches users not to read any help text at all, so important information can be missed. Use [Markdown](https://www.markdownguide.org/) to [format text](https://www.markdownguide.org/basic-syntax/#emphasis) and include [links](https://www.markdownguide.org/basic-syntax/#links) to more detailed help documentation created on your site where applicable.

- **Optional trigger fields**: If a trigger field is optional, confirm the request does not throw an error in a null case where the user does not select an option.

- **Field types**: Use the most appropriate [input field type](https://platform.zapier.com/build/add-fields) for each of the input fields to show users what type of data to include. Note the Zap editor does not validate the data to ensure users added the correct item for that field type. If the field can accept multiple values, use our built in [‘List’ property](https://github.com/zapier/zapier-platform/blob/main/packages/schema/docs/build/schema.md#fieldschema) or ‘[Allow Multiples](https://platform.zapier.com/build/add-fields#allows-multiples)’ functionality rather than asking users to provide a comma-separated value in a text field.

- **Ordering**: Put required trigger input fields at the top of the form with optional fields towards the bottom by importance.

### Static webhook

Triggers using static webhooks are not allowed in public Zapier integrations. Users can replicate this functionality in their Zaps via the [Webhooks by Zapier Integration](https://zapier.com/apps/webhook/integrations). Please consider including authentication and using REST Hooks to provide users with a more streamlined experience.

### Polling triggers

Live Zaps with [polling triggers](https://platform.zapier.com/build/trigger) automatically poll the request URL for new data every 1 to 15 minutes, depending on the user’s [Zapier plan](https://zapier.com/pricing). For an effective polling trigger, the following should be done:

- Return results from the polling URL in reverse chronological order by created date, so the most recently created or updated object is returned first.

- Return a sufficient amount of items from the polling endpoint. Generally, 100 items is plenty for most integrations, but there are cases where it’s common for users to perform an action in your app that would trigger more than 100+ records at once. Note that a trigger with more than 100 new items returned in a poll will run into the [polling trigger throttle](https://platform.zapier.com/build/operating-constraints#polling-trigger-throttle-zapier).

- Use [pagination](https://platform.zapier.com/build/pagination-trigger) on trigger results when being used to populate a dynamic dropdown, if large amounts of data will be returned.

- Each result should contain a unique primary key (usually an id field) for [deduplication](https://platform.zapier.com/build/dedupe) from the polling endpoint.

### REST hook

[REST hook-based triggers](https://platform.zapier.com/build/trigger) are Zapier’s preferred implementation of triggers since they fire immediately after the triggering action is performed.Our mutual users prefer REST hook triggers over polling triggers in their Zaps. They are labelled as [Instant triggers](https://help.zapier.com/hc/en-us/articles/8496244568589-Types-of-triggers-in-Zaps) to users For an effective REST hook trigger, the following should be done:

- Hook-based triggers must allow multiple subscriptions without overwriting subscriptions. You can test this by setting up 2 Zaps with the same trigger, turning them On, and confirming both Zaps fire successfully when the triggering event is performed in your app.

- Each REST Hook trigger must also have a polling URL defined in the Perform List. This allows users to easily pull in sample resources to set up their Zaps without leaving the Zap editor. Without a corresponding polling URL, users would have to navigate off of the Zap editor to the product to create or update a resource each time they set up a Zap. Ensure that the data returned from the polling URL follows the Polling Trigger requirements above.

- Data returned from the polling URL should exactly match the data returned in the hook payload. Check that field keys from the polling URL and in the hook payload match in spelling, casing, and data structure.

### Response content

The response content is what is returned to Zapier by the trigger. The response data should include important keys in the most usable format. For example, it helps to return both the ID and pretty name of objects, any contact information, and links to the resource (ex: for a New Card in Trello trigger, a URL to link to card). Remove unnecessary fields that may seem confusing or add noise to users’ Zap setup process. For example, if the response content includes information about the request itself and the input fields provided, please remove those fields from the returned response. Also, ensure that the response content meets the below guidelines

- **Names**: Many actions in Zapier require names to be split into two fields - first/last or given/surname. This conflicts with some naming schemes around the world, but without separated name fields, your trigger may not be compatible with certain integrations. Always provide separate name fields, though feel free to return the full name as well if the response already includes this.

- **Addresses**: Likewise with names, many actions in Zapier require address components in separate fields (street, street2, city, state, zip), instead of requiring the complete address in a single field. Always provide separated address fields, though feel free to return the complete address as well if the response already includes this.

- **Date-times**: Date-time values are required to be in [ISO 8601 format](http://www.cl.cam.ac.uk/~mgk25/iso-time.html?utm_source=zapier.com&utm_medium=referral&utm_campaign=zapier#date) and should always include a time zone offset (even if it is UTC). This includes date-time values returned from the polling URL, in the hook payload, and your sample data. Avoid UNIX/Epoch timestamps. Date-time values may be modified in your API call custom code if your API returns dates in different formats. Example acceptable date-time values include:

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`2023-12-15T01:15:13Z` (or `-0000` instead of `Z`)
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`2023-12-01T12:32:01-0800`
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`2023-12-01T12:32:01-08:00`
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`2023-12-13` (for date-only values)

- **Booleans**: Set boolean values as true or false. Do not use 1 and 0 or alternative representations for boolean values.

- **Dropdown fields**: Return both the name and ID of the selected dropdown option to be used in subsequent steps of a Zap.

### Sample data

Each trigger requires [sample data](https://platform.zapier.com/build/sample-data) for instances where no result is returned during Zap setup or the user chooses to skip testing. This could be because the API is temporarily down, or because the user has no existing data in their account to return. The sample data must:

- Only represent one item, and not the entire response of the request if there are multiple items returned as a set. For example, {“key”: “value”} instead of [{“key”: “value”}, {“key”: “value2”}, … ].

- Use representative data in the expected format the values will be returned. For example, don’t set a ‘first name’ key to a value of ‘string’ or ‘1234’; set it to something like ‘Bob’.

- Only return the keys that would be returned in every response for all users of the trigger. This means if there are custom fields that will be returned for some users and not others, please do not include these in the sample data.

### Output fields

[Output fields](https://platform.zapier.com/build/sample-data) add user-friendly labels to your API’s response to facilitate mapping fields during Zap setup for users. By default, Zapier will try to make a friendly version of the response by capitalizing words and replacing underscores with spaces, but this can be customized. Add a custom output field label when:

- a field is abbreviated. For example, ‘LTV’ should be labeled ‘Lifetime Value’.
- a field has an ambiguous unit of measure. For example, ‘Duration’ should be labeled ‘Duration (in seconds)’.
- a field is represented by an ID.
- in general, it is not instantly clear what the field or value represents.

### Update triggers

Don’t offer a generic ‘Updated ’ trigger, as these are often too general for users to use in their Zaps. Instead, think under what specific scenarios the user needs an update trigger. For example, instead of offering an ‘Updated Deal’ trigger which triggers when anything changes on the deal, offer a ‘New Deal in Stage’ or ‘Updated Deal Status’ trigger that allows the user to specify which stage they want to monitor.

### Error messages

Users should never receive a success/200 response if there was an error in the request as this will not show up as an error in the Zap history. All error messages should be user-friendly and avoid technical jargon. Be as specific as possible to what caused the error.

## Actions

### Action design and copy

The copy for actions should match your product’s UI. This includes the action’s name, description, input fields, help text, etc. For instance, since Dropbox calls directories “folders” in their product UI, the Zapier integration should refer to “folders” in the respective action. If the API uses different terminology than your product’s UI, match the UI - not the API.

Additionally, each action must have:

- a descriptive, titlecased name. For example, ‘Create Lead’, instead of ‘Create lead’.

- a descriptive key. For example, ‘create_lead’, instead of ‘action_1’.

- a descriptive noun that reflects the object that is being created or updated in the action. This should typically be one word and should always be in the singular form. The noun is used around the Zapier platform and will be pluralized automatically to complete various messages to users such as ‘No new found.‘

- a concise description starting with a plural form of the action verb, and ending in a period/full-stop. For example, the description for a ‘Create Lead’ action could be ‘Creates a new lead.’ Please do not include the name of the platform nor capitalize the noun such as ‘Creates a new Lead in XXX CRM.’

### Action input fields

All action steps must include [input fields](https://platform.zapier.com/build/add-fields) to gather the data needed to create, update, or perform the intended action. These fields should be named appropriately and include help text if their purpose is ambiguous. Use appropriate naming, ordering, and field types. Avoid unnecessary complexity in ID fields and include helpful tooltips where necessary.

- **ID fields**: Users should never be expected to manually type or map an internal ID to an action field. Your integration should not have input fields labeled ‘XXX ID’. Generally, trigger and action steps of other integrations do not return internal IDs for your specific platform to be used in an action field from your Zapier integration. Use Zapier’s [dynamic dropdown](https://platform.zapier.com/build/add-fields#dynamic-dropdown) and [Search Connector](<https://platform.zapier.com/build/add-fields#dynamic-dropdown:~:text=**%203.Add%20search%20to%20a%20dynamic%20field%20(optional)**>)/[search-powered field](https://github.com/zapier/zapier-platform/blob/main/packages/cli/README.md#how-do-search-powered-fields-relate-to-dynamic-dropdowns-and-why-are-they-both-required-together) functionalities to provide users with an easier way to select or search for the appropriate resource by a more readily available value such as ‘name’, ‘email address’, ‘title’, etc.

- **Ordering**: Order action fields logically. If you are unsure, look at how the respective fields are ordered in your platform and mimic that since users will be familiar with that ordering. Required action fields should generally be listed first at the top of the Zap editor while all optional, lesser-used fields towards the bottom. Group related fields together. For example, first name and last name fields, as well as individual address component fields should be ordered consecutively. Do NOT use [line-item groups](https://platform.zapier.com/build/line-items) or the ‘[children](https://github.com/zapier/zapier-platform/blob/main/packages/schema/docs/build/schema.md#fieldschema)’ field schema key to visually group fields; these are solely intended for line-item or array functionality.

- **Required fields**: If a field is not required by your API, don’t make it required in the Zap action. Parallel the required fields from your integration as closely as possible. For example, if ‘Email Address’ is not required to create a lead in the platform, do not make the ‘Email Address’ field required in the Zap editor. If the API specifies a non-important field as required, hard-code a default value so the field is not empty if one is not provided by the user. If the action step has a case where one field OR another field is required, set both fields as optional, add help text to both fields stating that one or the other is required, and throw a user-friendly error message if neither field is filled.

- **Help texts**: Don’t be redundant with help text, and only include it if you have something different to say from the field name such as the expected format of the value or additional instructions. For example, help text for an ‘Email Address’ field stating ‘Contact’s email address’ is not necessary. Redundant help text teaches users not to read any help text at all, so important information can be missed. Use [Markdown](https://www.markdownguide.org/) to [format text](https://www.markdownguide.org/basic-syntax/#emphasis) and include [links](https://www.markdownguide.org/basic-syntax/#links) to more detailed help documentation created on your site where applicable.

- **Default values**: Set [default values](https://platform.zapier.com/build/add-fields) for input fields sparingly. If the API specifies an unimportant field as required, set a default value in case one is not provided by the user. If the field in the application is set to or shows a default value, set the same default value for the action field in the Zapier integration.

- **Field types**: Use the most appropriate [input field type](https://platform.zapier.com/build/add-fields) for each of the input fields to show users what type of data to include — note Zapier does not validate the data to ensure users added the correct item for that field type. If the field can accept multiple values, use our built-in [‘List’ property](https://github.com/zapier/zapier-platform/blob/main/packages/schema/docs/build/schema.md#fieldschema) or ‘[Allow Multiples](https://platform.zapier.com/build/add-fields#allows-multiples)’ functionality rather than asking users to provide a comma-separated list of values in a text field.

### Response content

Return information about the resource that was created, updated, or affected by the action, and not just a ‘success’ message. At a minimum, return an ID, the name or title of the resource (when pertinent), and a link to the newly created, updated, or affected resource in the platform (if available). Additionally, return any other useful data about the resource users may need in subsequent actions of a multi-step Zap.

- **Date-times**: Date-time values are required to be in standard [ISO 8601 format](http://www.cl.cam.ac.uk/~mgk25/iso-time.html?utm_source=zapier.com&utm_medium=referral&utm_campaign=zapier#date) and should always include a time zone offset (even if it is UTC). This includes date-time values returned in the response content and in your sample data. Avoid UNIX/Epoch timestamps. Date-time values may be modified in your API call custom code if your API returns dates in different formats. Example acceptable date-time values include:

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`2023-12-15T01:15:13Z` (or `-0000` instead of `Z`)
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`2023-12-01T12:32:01-0800`
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`2023-12-01T12:32:01-08:00`
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`2023-12-13` (for date-only values)

- **Booleans**: Set boolean values as true or false. Do not use 1 and 0 or alternative representations for boolean values.

- **Important Data**: The response data should include important fields in the most usable format. For example, it helps to return both the ID and pretty name of resources, any important information about the resource such as contact information, and a link to the resource in the platform (ex: Create Card in Trello action returns a URL link to the card created). Also, Returning a link to the newly created/updated/affected resource in the action’s response data helps users link to the resource in subsequent steps of a multi-step Zap and confirms the new resource was created. This is also helpful for the Zapier support team when debugging issues.

- **Unnecessary/Excess Data**: Remove non-necessary fields that may seem confusing or add unnecessary noise to users’ Zap setup process from your API call’s custom code. For example, if the response content includes information about the request itself and the input fields provided, please remove those fields from the returned response.

- **Dropdown Fields**: Return both the name and ID of the selected dropdown option to be used in subsequent steps of the Zap.

### Sample data

The ‘Test’ step on actions sends a real request on behalf of the connected account. Therefore, each action requires [sample data](https://platform.zapier.com/build/sample-data) for instances when the user does not wish to actually run the action in their account to finish setting up the Zap. The sample data must:

- Represent the expected return from the request when a record is successfully created or found.

- Use representative data in the expected format the values will be returned. For example, don’t set a ‘first name’ key value to ‘string’ or ‘1234’; set it to something like ‘Bob’.

- Reflect the keys returned in every response for all users of the action. This means if there are custom fields that will be returned for some users and not others, please do not include these key:values in the sample data.

### Output fields

[Output Fields](https://platform.zapier.com/build/sample-data) add user-friendly labels to your API’s response data to facilitate mapping fields during Zap setup for users. By default, Zapier will try to make a friendly version of your API’s response, capitalizing words, and replacing underscores with spaces, but they can also be customized. Add a custom output field label when:

- a field is abbreviated. For example, ‘LTV’ should be labeled ‘Lifetime Value’.
- a field has an ambiguous unit of measure. For example, ‘Duration’ should be labeled ‘Duration (in seconds)’.
- a field is represented by an ID.
- in general, it is not instantly clear what the field or value represents.

### Create or update functionality

If your integration must have a ‘Create-or-Update’ functionality, implement a ‘Search-or-Create’ with an ‘Update’ action versus a ‘Search’ with a ‘Create-or-Update’ action or a standalone ‘Create-or-Update’ action.

### Delete actions

Carefully consider delete actions that fully delete or remove data. To prevent data loss, action steps should preferably only add or update data.

If you have a valid use case for a delete action, consider alternative actions for items such as deactivating, unsubscribing, or canceling, instead of deleting items completely.

If you do add a delete action, make sure to include a Copy field to clarify to users that the action is irreversible once the API request is made.

### Error messages

Users should never receive a success/200 response if there was an error in the request as this will not show up as an error in the Zap history. All error messages should be user-friendly and avoid technical jargon. Be as specific as possible to what caused the error.

## Searches

### Find or create

Search actions can optionally create items if nothing is found in the search. If your integration has a ‘Create-or-Update’ action, please implement a ‘Search-or-Create’ with an ‘Update’ action versus a ‘Search’ with a ‘Create-or-Update’ action or a standalone ‘Create-or-Update’ action.

### Search design and copy

The copy for searches should match your product’s UI. This includes search name, description, input fields, help text, etc. For instance, since Dropbox calls directories “folders” in their product UI, the Zapier integration should refer to “folders” in the respective search. If the API uses different terminology than your integration’s UI, match the UI - not the API.

Additionally, each search must have:

- a descriptive, titlecased name. Use ‘Find’ over ‘Get’. For example, ‘Find Lead’, instead of ‘Get Lead’.

- a descriptive key. For example, ‘find_lead’, instead of ‘search_1’.

- a descriptive noun that reflects the object that will be returned. This should typically be one word and should always be in the singular form. The noun is used around the Zapier platform and will be pluralized automatically to complete various messages to users such as ‘No new found.‘

- a concise description starting with a plural form of the verb, which typically is ‘Finds’, and ending in a period/full-stop. For example, a valid description for a ‘Find Lead’ search is ‘Finds a new lead.’ Please do not include the name of the platform nor capitalize the noun such as ‘Finds a new Lead in XXX CRM.’

### Search input fields

[Search input fields](https://platform.zapier.com/build/add-fields) should be named appropriately and include help text if their purpose is ambiguous.

- **ID fields**: Users should never be expected to manually type or map an internal ID to a search field. Your integration should not have search fields labeled ‘XXX ID’. Trigger and action steps of other integrations do not return internal IDs for your specific app that could be used in an action field for your Zapier integration. If the user is using a trigger from your Zapier integration, the trigger should return all necessary information about the resource without the Zap needing a search step to retrieve additional, necessary information. Instead, provide search field options for more general information such as ‘name’, ‘email address’, ‘phone number’, ‘title’, etc. that is more readily available from all triggers.

- **Ordering**: Put required search fields at the top of the form with optional fields towards the bottom by importance.

- **Optional search fields**: If a search field is optional, confirm the request does not throw an error in a null case where the user does not select an option.

- **Help texts**: Don’t be redundant with help text, and only include it if you have something different to say from the field name such as the expected format of the value or additional instructions. Redundant help text teaches users not to read any help text at all, so important information can be missed. Use [Markdown](https://www.markdownguide.org/) to [format text](https://www.markdownguide.org/basic-syntax/#emphasis) and include [links](https://www.markdownguide.org/basic-syntax/#links) to more detailed help documentation created on your site where applicable.

- **Field types**: Use the most appropriate [input field type](https://platform.zapier.com/build/add-fields) for each of the input fields to show users what type of data to include — note Zapier does not validate the data to ensure users added the correct item for that field type. If the field can accept multiple values, use our built-in [‘List’ property](https://github.com/zapier/zapier-platform/blob/main/packages/schema/docs/build/schema.md#fieldschema) or ‘[Allow Multiples](https://platform.zapier.com/build/add-fields#allows-multiples)’ functionality rather than asking users to provide a comma-separated list of values in a text field.

### Response content

While “create” actions return a single object to Zapier; searches must return an array of objects. Each search must follow these requirements:

- **No Result**: Do not raise an error if there are no search results to return. If your API returns a 404 for search misses, use custom code to [return a 200 with an empty array as the response](https://platform.zapier.com/build/response-types).

- **Names**: Many actions in Zapier require names to be split into two fields - first/last or given/surname. This conflicts with some naming schemes around the world, but without a separated name field, your action may not be compatible with certain integrations in subsequent steps of a user’s Zap. Always provide separated name fields if applicable, though feel free to return the full name as well if the response already includes this.

- **Addresses**: Likewise with names, most actions in Zapier require address components in separate fields (street, street2, city, state, zip), instead of requiring the complete address in a single field. Always provide separated address fields, though feel free to return the complete address as well if the response already includes this.

- **Date-times**: Date-time values are required to be in standard [ISO 8601 format](http://www.cl.cam.ac.uk/~mgk25/iso-time.html?utm_source=zapier.com&utm_medium=referral&utm_campaign=zapier#date) and should always include a time zone offset (even if it is UTC). This includes date-time values returned in the response content and in your sample data. Avoid UNIX/Epoch timestamps. Date-time values may be modified in your API call custom code if your API returns dates in different formats.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`2023-12-15T01:15:13Z` (or `-0000` instead of `Z`)
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`2023-12-01T12:32:01-0800`
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`2023-12-01T12:32:01-08:00`
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`2023-12-13` (for date-only values)

- **Booleans**: Set boolean values as true or false. Do not use 1 and 0 or alternative representations for boolean values.

- **Important Data**: The response data should include important fields in the most usable format. For example, it helps to return both the ID and pretty name of resources, any important information about the resource such as contact information, and a link to the resource in the platform (ex: Find Card in Trello search, returns a URL link to the found card).

- **Unnecessary/Excess Data**: Remove unnecessary fields that may seem confusing or add noise to users’ Zap setup process from your API call’s custom code. For example, if the response content includes information about the request itself and the input fields provided, please remove those fields from the returned response.

### Sample data

Each search requires [sample data](https://platform.zapier.com/build/sample-data) for instances where no result is returned during Zap setup. This could be because the API is temporarily down, or because no result is returned for the specific search the user tests. The sample data must:

- Only represent one record, and not the entire return from the request if there are multiple records returned as a set. For example, {“key”: “value”} instead of [{“key”: “value”}, {“key”: “value2”}, … ].

- Use representative data in the expected format the values will be returned. For example, don’t set a ‘first name’ key value to ‘string’ or ‘1234’; set it to something like ‘Bob’.

- Reflect keys available in every response for all users of the search. This means if there are custom fields that will be returned for some users and not others, please do not include these key:values in the sample data.

### Output fields

[Output fields](https://platform.zapier.com/build/sample-data) add user-friendly labels to your API’s response data to facilitate mapping fields during Zap setup for users. By default, Zapier will try to make a friendly version of your API’s response, capitalizing words, and replacing underscores with spaces, but they can also be customized. Add a custom output field label when:

- a field is abbreviated. For example, ‘LTV’ should be labeled ‘Lifetime Value’.
- a field has an ambiguous unit of measure. For example, ‘Duration’ should be labeled ‘Duration (in seconds)’.
- a field is represented by an ID.
- in general, it is not instantly clear what the field or value represents.

## Error handling

APIs are not always available. Users do not always provide valid data for requests. Build a defensive and resilient integration. Plan for 4xx and 5xx responses. Without [proper handling](https://github.com/zapier/zapier-platform/blob/main/packages/cli/README.md#error-handling), errors can have incomprehensible messages, technical error codes, or remain unnoticed by users.

### General errors

Use `z.errors.Error` in situations where users misconfigure their Zaps and need to take action. Typically, this will be for prettifying `4xx` responses and APIs that return errors as 200 with a payload that describes the error with guidance on how to correct it.

- If a Zap raises too many error messages it will be [automatically turned off](https://help.zapier.com/hc/en-us/articles/8496037690637-Troubleshoot-errors-in-Zapier#500-series-error-codes-0-3), so only throw these if the scenario is truly an error that needs to be fixed.

- Elaborate on terse messages. ‘Your API Key is invalid.’ is better than ‘not_authenticated.’

- If the error calls out a specific field, surface that information to the user. ‘Title is not valid.’ is better than ‘Invalid Request.’

- If the error provides details about why a field is invalid, surface that information to users. ‘Title is invalid. Please only use alphanumeric characters.’ is better than ‘Title is invalid.‘

### Halting errors

Use `z.errors.HaltedError` in situations where a required pre-condition is not met. For instance, in an action to add an email address to a list where duplicates are not allowed, throw a `HaltedError` if the Zap attempted to add a duplicate. This indicates failure but is treated as a soft failure. Thus, unlike general errors, a Zap will never be turned off when this error is thrown even if it is raised more often than not.

### Stale authentication credentials

For integrations requiring a manual refresh of authorization regularly, Zapier provides `z.errors.ExpiredAuthError`, so the current operation is interrupted, the Zap is turned off (to prevent additional runs with expired credentials), and a predefined email is sent out informing the user to refresh the credentials. The runs will be [Held](https://help.zapier.com/hc/en-us/articles/20505304170637-Review-Zap-run-statuses), and the user will be able to replay them after reconnecting.

For integrations using OAuth2 with automatic refresh requests or Session Auth, use `z.errors.RefreshAuthError`. This signals Zapier to refresh the credentials and retry the failed operation.

## Code quality

### Environment variables

Do not hard code credentials such as API Keys, Client IDs, Client Secrets, etc. into your integration. Use [environment variables](https://platform.zapier.com/build/env) instead.

### Structure

If you are using the [Zapier CLI](https://github.com/zapier/zapier-platform/blob/main/packages/cli/README.md) to build the integration, ensure files are logically broken out into respective directories and the code is easy to follow. We suggest putting triggers, actions, and searches each in their directories.

### Dependencies

If you are using the [Zapier CLI](https://platform.zapier.com/reference/cli-docs), keep dependencies up to date. When notified that a dependency must be updated—for example, `zapier-platform-legacy-scripting-runner`, `zapier-platform-core`, or `zapier-platform-cli` —complete the update promptly or by the stated deadline. If requested updates are not completed by the stated deadline, Zapier reserves the right to make necessary updates on your behalf.

## Conclusion

While these guidelines are not exhaustive, they provide a robust framework to prepare your integration for a successful launch on Zapier.

Note that while not implementing these guidelines would not prevent your integration from being published, there are certain [requirements](https://platform.zapier.com/publish/integration-publishing-requirements) that **must** be met before your integration can be approved for publishing.

For any specific questions or additional support, feel free to contact the Developer Support team at Zapier via the [contact form](https://developer.zapier.com/contact).
