---
title: Making Integration Changes in Platform UI and CLI
order: 6
layout: post-toc
---

# Making Integration Changes in Platform UI and CLI

Before making updates to your integration, it's important to consider the potential impact on user migration and existing Zaps. Ensuring your API and Zapier integration remains backwards compatible is crucial to avoid disruption to users. However, we acknowledge certain changes are sometimes necessary and unavoidable. In such cases, consider the best practice for implementation.

## Affects of Different Changes (Versioning Matrix)

The matrix below illustrates the impact of different changes on promotions and migrations for a public integration. Refer to our best practice to facilitate the upgrade process for yourself and your users.

Matrix Key:
* Update: Making a change to an existing component
* Replace: Deleting/deprecating an existing component and adding a new one in its place
* Breaking Change: A modification to the integration which renders existing Zaps incompatible with the new version
* Depends: A modification which may render existing Zaps incompatible with the new version, depending on the implementation
* ✓: A modification to the integration which renders existing Zaps compatible with the new version
* -: Not applicable

Several change scenarios are validated by the platform when you try to "Migrate" after a version promotion, but always be aware of the effects of any changes you make before you even begin implementing those changes.

| **Integration Change** | **Add** | **Update** | **Replace** | **Delete/Deprecate** | **Validated by platform?** |
| --- | --- | --- | --- | --- | --- |
| **Authentication schemes** | **BREAKING CHANGE** | - | **BREAKING CHANGE** | - | ✓ |
| **Authentication fields - required** | **BREAKING CHANGE** | Depends | - | ✓ | |
| **Authentication fields - optional** | ✓ | ✓ | - | ✓ | |
| **Authentication field key(s)** | - | **BREAKING CHANGE** | - | - | |
| **Authentication - token request** | - | ✓ | - | - | |
| **Authentication - test function** | - | ✓ | ✓ | - | |
| **Trigger/Action/Search - meta info (e.g.: label, description)** | - | ✓ | ✓ | - | |
| **Trigger/Action/Search - key** | - | **BREAKING CHANGE** | **BREAKING CHANGE** | - | ✓ |
| **Trigger/Action/Search - input field(s) - required** | Depends | Depends | Depends | ✓ | |
| **Trigger/Action/Search - input field(s) - optional** | ✓ | ✓ | ✓ | ✓ | |
| **Trigger/Action/Search - input field(s) - key** | - | **BREAKING CHANGE** | **BREAKING CHANGE** | - | |
| **Trigger/Action/Search - input field(s) - field type** | - | Depends | Depends | - | |
| **Trigger/Action/Search - output data - key(s)** | ✓ | **BREAKING CHANGE** | **BREAKING CHANGE** | **BREAKING CHANGE** | |
| **Trigger/Action/Search - output data - response structure** | - | **BREAKING CHANGE** | **BREAKING CHANGE** | - | |
| **Trigger/Action/Search - perform function** | - | Depends | Depends | - | |
| **Trigger type - polling/hook** | - | **BREAKING CHANGE** | - | - | ✓ |
| **Trigger (polling) - perform function** | - | Depends | Depends | - | |
| **Trigger (hook) - perform list** | - | Depends | Depends | - | |
| **Trigger (hook) - performSubscribe** | - | ✓ | ✓ | - | |
| **Trigger (hook) - performUnsubscribe** | - | ✓ | ✓ | - | |
| **Middleware** | Depends | Depends | Depends | Depends | |
| **Partner's API (overall)** | - | Depends | Depends | Depends | |
| **Product feature** | ✓ | - | - | - | |
| **Rebrand - (e.g. logo, app name)** | - | ✓ | - | - | |
| **Convert - UI to CLI** | - | Depends | ✓ | - | |
| **Convert - CLI to UI** | - | Depends | - | - | |
| **Edit - version of a converted Web Builder integration** | - | Depends | Depends | - | |

## Change Scenarios & Best Practices

Below is a list of common changes that require special attention as they can affect the ability to migrate users. Look for your change and check out the recommended best practices. 

If your change is not in this list, it's likely fine, but consider whether it changes keys, requires users to provide _new_ info, or revokes functionality.

I want to make edits to...

### Authentication

#### Changing authentication scheme

##### Change Scenario

If your API’s authentication method changes, or your app rolls out different endpoints for integration users; you would need to change the method Zapier uses to authenticate user accounts.

##### Impact to Users

Changing an integration’s authentication type (such as Basic Auth, API Key, or OAuth) to a different one is a breaking change. Migration would not be possible as all existing connected accounts would stop working if migrated. Users would need to make a new connection to your app and manually update each of their Zaps using the app.

##### Best Practices

Clone your app into a new version, deleting the existing authentication method and adding the new one. Once ready promote that version for new users to select when connecting your app to Zapier.

If users with existing authentications can remain connected with that authentication method, it is recommended to allow them to remain on the old version. Existing users would still be prompted to make a new connection to your app for any new Zaps they create as only the promoted version would be available when searching for your app by name.

If the existing authentications will cease to function at some future date, then [Deprecation](https://platform.zapier.com/docs/versions#deprecating-versions) is necessary. Please note this is significantly more disruptive to our mutual users and should be considered carefully.

> NOTE: this method is not possible with apps built in the legacy web builder. To update the authentication, you would need to update all triggers/actions/searches as well; as deleting the authentication method and re-adding it in the new builder would not be compatible with existing triggers/actions/searches built in the legacy web builder.

#### Adding a required auth field

##### Change Scenario

Breaking changes can occur when adding a new required authentication field or updating an existing optional authentication field to be required.

##### Impact to Users

Requiring new data during authentication can have significant effects:

- Existing connected accounts will not work: All existing connected accounts will no longer be functional with your integration until users re-authenticated manually.
- Manual updates are required for all Zaps: If a Zap cannot be migrated due to a breaking change, users will have to edit each Zap individually before they can start running tasks again. For example, if a user has 20 Zaps set up with your integration, they will need to manually update each one of those Zaps.

##### Best Practices

- **Add the field as optional**: Use field help text and custom error handling to validate that the newly required field is provided, while keeping it set to optional. Also, consider using custom code to set the field's default value in your API call if left blank.
- **Set a default value**: If possible, provide a default value for the required field that can be overwritten if necessary. This ensures that users who do not provide explicit values for these fields can continue to use your integration without issues.

For example in the case of updated API endpoints for geographical region or site domain, it is possible to account for an added **required** inputField with scripting to ensure existing authentications are backward compatible, allowing existing users to be migrated to the new version.

In this example code, the default URL for US region is updated when the user selects AU or CA when authenticating.

```js
let baseURL = "theUsApiBaseUrl";
switch (authData.region) {
  case "AU":
    baseURL = "theAuApiBaseUrl";
    break;
  case "CA":
    //other regions can be easily supported by adding cases like this
    baseURL = "theCaApiBaseUrl";
    break;
  default:
    console.log("Legacy credentials are in use, defaulting to US Base URL.");
}
```

#### Changing authentication field keys

##### Change Scenario

You want to change the key of one or more [authentication input fields](https://platform.zapier.com/docs/auth) required when a user authenticates your app to Zapier.

##### Impact to Users

This is a breaking change.

Unless precautions are taken, changing the key of an existing authentication field will break existing app connections. Migration would not be possible. Users would need to make a new connection to your app and manually update each of their Zaps using the app.

##### Best Practices

- We strongly encourage you to **avoid changing authentication field keys** whenever possible.

If your API endpoint needs a different property to authenticate a request, consider changing the property key instead of modifying the form field input’s key. Note that you’ll need to make this change in each trigger, action, search request, as well as authentication.

Form field input keys do not necessarily need to match the properties expected by your API.

Let’s say you have a form field input with the key `api_key` (two words) and are sending the field’s value to your API using a property with the same name, `api_key`:

![example one](https://cdn.zappy.app/7a3d828ef0d8dcd340ef03adfd79a5b1.png)

```js
params: {
  api_key: bundle.authData.api_key; // original
}
```

Then, your API changes and expects the request property to be `apikey` (one word) instead. As shown below, you can change the request property key (left) as needed (`apikey`) while still referring to the form field input (right) based on its original key (`api_key`):

![example two](https://cdn.zappy.app/8ee1ffe99f2583b1202d9c16d57b1664.png)

```js
params: {
  apikey: bundle.authData.api_key; // new - request key and field key can differ
}
```

###  Trigger/action/search keys, fields and output

#### Updates to trigger/action/search keys

##### Change Scenario

In cases where a trigger/action/search’s custom code needs to be rewritten or a new v2 is replacing an older v1.

##### Impact to Users

Deleting a trigger/action/search in a new version is a breaking change - which would prevent migration of your users to the new version. Updating an existing trigger/action/search’s custom code would allow for migration but break users’ Zaps if the output changes.

![impact example](https://cdn.zappy.app/65326a8f5fff0f9640c0d6fdc59dfa3b.png)

The triggers, actions, and searches are identified by their **key**, such as `new_contact` or `create_post`, so if you remove it, or change its **key** (possible in CLI apps only), this message appears when you attempt to migrate.

##### Best Practices

- If you have already renamed the **key** (possible in CLI apps only) for a trigger/action/search, you’ll need to switch it back to the previous **key** to proceed with migrating users.
- If you need to remove a trigger/action/search, change its visibility to **hidden** instead. Use the Visibility Options dropdown in the [UI](https://platform.zapier.com/docs/triggers#1-configure-trigger-settings), or the `hidden` key in the [CLI](https://github.com/zapier/zapier-platform/blob/main/packages/schema/docs/build/schema.md#basicdisplayschema).

![hidden](https://cdn.zappy.app/73990d8049572347aea87fc304173ecc.png)

Migrated Zaps that used the hidden trigger/action/search will now show it as Deprecated in the Zap Editor, but will continue to function as long as the endpoints remain valid.

![deprecated](https://cdn.zappy.app/61a2ac6095433d278bc412c2e59408fc.png)

Once a user selects a different trigger/action/search when editing their Zap, they will not be able to retrieve the hidden one. New users will not see any `hidden` trigger/action/search as available for selection.

- If you need to add a new trigger/action/search that replaces the hidden one, create a duplicate and give it a new **key** (such as appending `_v2` on the end), and keep the Name and Description the same if the functionality for a user is the same.

![duplicate](https://cdn.zappy.app/6231ec2b53271c7d83672f6ed232d0e3.png)

- This way existing Zaps continue to work once migrated with the previous (and now hidden) definition, and new Zaps will only be able to select the new definition.

- In cases where the endpoint in the hidden trigger/action/search will be sunset and begin to return errors in the future, the impact to users would be as follows:

Once the API has been sunset, active Zaps (turned on) using the impacted trigger/action/search will produce errors when they run. Depending on [user's email notification settings](https://help.zapier.com/hc/en-us/articles/8496289225229), owners of these Zaps will be sent email notifications about these errors.

If those Zaps exceed the error ratio **and** users have not [overridden related settings in their Zaps](https://help.zapier.com/hc/en-us/articles/8496037690637-Troubleshoot-errors-in-Zapier#i-want-my-zap-to-continue-running-even-when-there-are-errors--0-6), those Zaps will be automatically turned off.

- If you’d like to add custom errors within Zapier for the hidden trigger/action/search at the time of the endpoint sunset, you could consider the following:

Create a new version of the integration that immediately throws a `z.errors.Error` exception in the `perform` method of the impacted trigger/action/search. Learn more for apps maintained in the [UI](https://platform.zapier.com/docs/versions-best-practices#custom-error-handling) or the [CLI](https://github.com/zapier/zapier-platform/blob/main/packages/cli/README.md#zerrors).

"Promote" and then "migrate" users to this new version as close to the sunset date as possible.

The benefits of this approach are:

- Throwing an explicit exception will ensure impacted Zaps will hit the error ratio (and be turned off) at the earliest possible time.
- You can add a user-friendly message to the exception that users will see in both Zaps Runs on the [Zap History](https://help.zapier.com/hc/en-us/articles/8496291148685-View-and-manage-your-Zap-history) and also in email error notifications, e.g. "This function has been deprecated and is no longer available."
- Here's an example of how a custom error message would be displayed on an action in the Zap History:

![custom error](https://cdn.zappy.app/50807aad2a2e2ecda9044a524dafba8c.png)

#### Adding new required fields in trigger/action/search

##### Change Scenario

Your app’s API endpoint adds an additional field for filtering records (trigger/search) or an additional property for created records (action).

##### Impact to Users

Adding a new **required** input field or making a _previously_ optional input field now required, would break existing Zaps without a value for the field. There is no automated check for this when migrating so though it may be possible, it will be a breaking change for users.

##### Best Practices

Consider the following options:

1. Add new inputFields as optional

2. Use Code Mode (UI) or code in Perform (CLI) to set a default value for the inputField if users have it blank in their existing Zaps. This would only be successful if a universal default could apply to all users (would not work for custom fields for example).

3. Create a new trigger/action/search (T/A/S) with the required inputField; and [hide the previous T/A/S](https://platform.zapier.com/docs/versions-best-practices#custom-error-handling). That way, existing Zaps will continue to work with the previous (and now hidden) trigger/action/search definition, and new Zaps will be forced to provide a value for the required field.

#### Changing form field keys

##### Change Scenario

You want to change the key of one or more form field inputs within a trigger, action, or search.

##### Impact to Users

Modifying the key of a form field input is a breaking change.

Unless precautions are taken, changing the key of an existing form field input will break the field’s mapping within the step it’s used. The previously-mapped value will be dropped, resulting in missed data and/or errors.

##### Best Practices

- We strongly encourage you to **avoid changing form field input keys** whenever possible.
- Design the trigger, action, or search to **handle both the old and new keys**.

###### Avoid changing form field input keys

If your API endpoint needs a different property in the request, consider changing the property key instead of modifying the form field input’s key.

Form field input keys do not necessarily need to match the properties expected by your API.

Let’s say you have a form field input with the key `first_name` (right) and are sending the field’s value to your API using a property with the same name, `first_name` (left):

![example one](https://cdn.zappy.app/cf7d34d12c1a1c42f75a89815409d20e.png)

```js
body: {
  first_name: bundle.inputData.first_name; // original
}
```

Then, your API changes and expects the request property to be `firstname` (one word) instead. As shown below, you can change the request property key (left) as needed (`firstname`) while still referring to the form field input (right) based on its original key (`first_name`):

![example two](https://cdn.zappy.app/b6b1776d964f52eed12d64ff264b8cac.png)

```js
body: {
  firstname: bundle.inputData.first_name; // new - request key and field key can differ
}
```

###### Handle both the old and new keys

If it’s not possible to simply change a hardcoded request property’s key:

- We recommend that you design the trigger or action to handle both the old and new key

Using the same example above, let’s say that instead of hardcoding your request properties, you were spreading `bundle.inputData` into the body of the API request, so there was a one-to-one relationship between field keys and request properties.

```js
body: {
  ...bundle.inputData // original - request keys tied to field keys
}
```

Instead of changing form field input keys, you can use Code Mode (UI) or code (CLI) to modify the request.

For example, below, we create a new object, payload, with all the fields from `bundle.inputData` AND the updated property, `firstname`. Then we delete the old property, `first_name`, and send the updated objected in the request:

```js
// copy bundle, add updated property
const payload = { ...bundle.inputData, firstname: bundle.inputData.first_name };

// delete old property
delete payload.first_name;

body = {
  ...payload, // send updated payload
};
```

With this approach, or one like it, you can change the request as needed without modifying field keys and breaking users’ mappings.

#### Changing output field keys

##### Change Scenario

You may want to update or remove existing output field keys in your Zapier integration. This can happen when you need to clean up output data, remove unnecessary fields, or due to changes in your API's response data.

##### Impact to Users

If a user has mapped one of the affected fields to an input field in a subsequent step of their Zap, the change can affect that step and potentially the entire Zap's functionality. Imagine if you updated the output field key or removed an output field altogether that a user had mapped to a required field in the next step of their Zap - the step would now error every time.

##### Best Practices

To minimize disruptions to your users, follow these best practices when updating or removing existing output field keys:

1. Remove extraneous fields carefully: If you're cleaning up output data and removing non-essential fields (such as HTTP request data like request type or request URL), you should be able to safely remove them. Be cautious and avoid removing fields that users might have mapped to required or critical fields in their Zaps.

2. Maintain backward compatibility (CLI partners): If you're using the Zapier CLI, you can use custom code to ensure backward compatibility with updated response data from your API. Modify the perform methods in your code appropriately to handle these changes.

3. Update the static sample: When you have made any changes to output fields, remember to update the static sample data accordingly. This ensures that the sample data used for testing and setup by users remains accurate and up-to-date.

#### Changing output data

##### Change Scenario

Breaking changes can occur when certain changes are made to a trigger, action, or search's output data structure. Even if the output field key(s) remain the same, significant changes to the data structure or format returned from one or more of these fields can affect users’ Zaps.

Examples of potential breaking change scenarios:

- An output field representing datetime is updated to return data in ISO-8601 format instead of full date format (Thursday, April 10, 2008 6:30:00 AM)
- A `results` field in a search returns a list of all search results instead of the single, last created result
- A previously comma-separated list value is updated to return line-items

##### Impact to Users

Updated output fields from your integration steps can impact the way subsequent actions run in a user's Zap if they are mapped to input fields in those actions.

For example, if a user has set up a Formatter step to parse out the day of the week from the `added_date` field before adding it to a CRM, changing the date format to ISO-8601 will cause the Formatter to process unexpected values, which may lead to issues in the user's Zap.

Another example is a user's Zap configured with a search that always returns a single result based on the latest created date in the `results` field. If the search is updated to return all results, subsequent actions in the Zap may not be set up to handle multiple results, leading to potential problems.

##### Best Practices

1. Use custom code to add your newly formatted data to the existing output data. By doing this, you ensure that users who have already set up their Zaps with the previous data structure will not experience issues due to the changes.

_for example_  Add a created_date_ISO field with the ISO-8601 formatted created date to the output data, instead of updating the current created_date value to be in ISO-8601 format. Define clear [output field labels](https://platform.zapier.com/build/faq#output-fields) to help users differentiate the fields; updates to field labels are non-breaking.

2. Add an optional, boolean input field that users can toggle to choose between returning old and the new data structure. This way, users can decide which data structure best suits their needs for existing and new Zaps. Make sure to set a default value for the input field to automatically return data as your previous version did.

3. If you’re looking to update a search to return multiple or all search results, instead of the default one result, create a new, separate search for the purpose. This way, users can choose which one to use without encountering issues in their existing Zaps. Differentiate the searches by pluralizing the search: “Find Lead” vs “Find Lead(s)”.


### Trigger type changes (polling vs REST Hook)

##### Change Scenario

An app needs to change how it notifies Zapier of new records - changing the type of trigger - from Zapier polling an app endpoint for new items to instead a REST Hook subscription where the app notifies Zapier of new records; or vice versa.

##### Impact to Users

This is a breaking change. Edits to an existing trigger’s type will cause your users’ Zaps to stop working and they would need to create new Zaps with the new trigger type, and manually re-create their actions. Using the [Duplicate feature](https://help.zapier.com/hc/en-us/articles/15408145778829-Duplicate-your-Zap) would help, but each Zap would need to be mapped individually with the new trigger.

##### Best Practices

- Copy the trigger configuration into a new trigger and give it a new **key** (such as appending `_v2` on the end), change the type for this new trigger, and **hide** the previous trigger. This way existing Zaps continue to work with the previous (and now hidden) trigger definition, and new Zaps will use the new trigger definition.
- That is the recommended path forward whether using the visual builder or the CLI, with the only difference being using the Visibility: Hidden toggle in the visual builder and setting the `hidden` key as `true` [in the CLI](https://github.com/zapier/zapier-platform/blob/main/packages/schema/docs/build/schema.md#basicdisplayschema).

### Updating a polling trigger's Perform method

##### Change Scenario

It is generally safe to update a polling trigger's [perform method](https://github.com/zapier/zapier-platform/blob/main/packages/schema/docs/build/schema.md#basicpollingoperationschema) (CLI) or [API endpoint](https://platform.zapier.com/docs/triggers#polling-trigger) (UI), as long as the changes maintain backward compatibility in the returned response data. This means that the output fields and output data structure should remain consistent with previous version’s.

##### Impact to Users

Updating a polling trigger's perform method or API endpoint might cause deduplication issues and cause old records to trigger a Zap if any of the following changes occur:

- The [dedupe ID field](https://platform.zapier.com/build/dedupe) (usually `id`) is changed or removed from the API response.
- The perform method's endpoint is modified, resulting in fundamental changes to the dedupe ID value.

For example, if the API or endpoint previously returned dedupe IDs as integers -1,2,3,4 - and is now updated to return alphanumeric values - 1-abc, 2-bcd, 3-cde, 4-def - records that were previously processed will fire again since the new IDs aren't saved in the deduplication table that Zapier references during each poll.

##### Best Practices

- Ensure the dedupe ID key remains unchanged: If the API response changes the dedupe ID key, use [custom code](https://platform.zapier.com/build/dedupe#custom-or-multiple-id-fields) to maintain consistency and prevent deduplication issues.
- Maintain reverse chronological order: the trigger should continue to return data in reverse chronological order to prevent unintended records triggering the Zap.

### Making changes to your API

##### Change Scenario

When making changes to your API, consider how these will affect your Zapier integration. API updates can widely vary from small to significant changes and can have varying effects on your users’ Zaps.

##### Impact to Users

Though not exhaustive, here are some potential major impacts to users:

- If a new version with breaking changes to authentication is promoted, users with existing Zaps will have to manually reconnect their account on Zapier.
- If a new version with breaking changes to any trigger, action, or search is promoted, users with existing Zaps will have to manually upgrade _each_ Zap using your integration. Keep in mind: power users can have tens to hundreds of Zaps using your integration.
- Changes to a trigger, action, or search’s response data can break or negatively affect the proceeding steps of the Zap.
- Changes to response data in polling triggers can prevent Zaps from triggering on new records or cause them to trigger on old records. This can lead to missed data and undesirable results for your users.

##### Best Practices

To mitigate the impact of API changes on your Zapier users, consider the following best practices:

- Maintain general backwards compatibility on existing endpoints. This ensures that the existing Zaps continue to work as expected, and your users won't need to modify them due to API changes.
- For polling triggers - changing the number of records returned from the endpoint can significantly impact the functionality of the users' Zaps.
- Implementing pagination on an endpoint can affect how much data fetched and processed in the Zap.
- Changing the sort order of response data returned can impact Zap triggers. For polling triggers, ensure that the data is always sorted in reverse chronological order to maintain compatibility.

By adhering to these best practices, you can minimize disruptions to your Zapier users when updating or modifying your API. A well-managed API transition process ensures that your users continue to have a seamless and efficient Zapier integration experience.

### Rebrand

##### Change Scenario

The app name, description, homepage or logo has changed.

##### Impact to Users

As shown to users in the App Directory: https://zapier.com/apps.

##### Best Practices

To edit your integration details on Zapier's public app directory, email partners@zapier.com as Public apps cannot make these edits themselves.

For logo changes, please include a square, 256x256px or larger transparent PNG image that does not include the app name.

- [App logo](https://platform.zapier.com/publish/integration-brand-design-guidelines#app-logo).

For description changes, please note the 140 character limit and style guide.

- [App description copy](https://platform.zapier.com/publish/integration-brand-design-guidelines#app-description-copy).

App name changes will also be made in the slug of the app’s url in the app directory - `https://zapier.com/apps/XXX-slug-XXX/integrations`

- [App name](https://platform.zapier.com/publish/integration-brand-design-guidelines#app-name)

### Custom Error Handling in the UI

[Switching to the Zapier CLI](https://platform.zapier.com/manage/export-integration), allows you to [make use of HTTP middleware](https://github.com/zapier/zapier-platform/blob/main/packages/cli/README.md#using-http-middleware) to implement [custom error response handling](https://github.com/zapier/zapier-platform/blob/main/packages/cli/README.md#error-response-handling). This will allow you to write a single script that applies across the entire integration to detect a specific error from the API, and act accordingly.

If you prefer to build and maintain your app in the UI, custom error handling can still be implemented within the Zapier Platform. The main difference is that you’ll need to add it to each individual element of the integration (triggers, actions, searches, authentication) that could encounter the error.

In the UI, `skipThrowForStatus` is set from the Advanced tab. This allows for custom error handling for status codes above 400. Note that 401 status codes will throw a `RefreshAuthError` [regardless](https://github.com/zapier/zapier-platform/blob/main/packages/cli/README.md#user-content-error-response-handling).

![advanced settings](https://cdn.zappy.app/8cafa443c6e5844d6881f2690e4f34c5.png)

Once set, you can add [error handling](https://github.com/zapier/zapier-platform/blob/main/packages/cli/README.md#general-errors) when in Code Mode within the API Configuration for each trigger/action/search.

![code screenshot](https://cdn.zappy.app/9553266cb5a5ab7804d3f9ac1a9eed60.png)

```js
return z.request(options).then((response) => {
  if (response.status === 404) {
    throw new z.errors.Error(
      "An error was returned. Help!",
      "InvalidData",
      404
    );
  }
  return response.json;
});
```

### Editing Legacy Apps in the UI

##### Change Scenario

All existing integrations built with Zapier’s legacy web builder have been converted to the new Zapier Platform UI to use our new input form editor and integration testing features. 

##### Impact to Users

Users were not impacted when legacy web builder integrations were converted to the new UI. All apps on the new Platform run on the [zapier-platform-core NPM package.](https://www.npmjs.com/package/zapier-platform-core) When making edits to your converted integration, consider the following. 

##### Best Practices

Any custom code written in the Legacy app can be viewed and edited in the “Advanced” section of the UI, in the “Legacy Web Builder” tab. The z.legacyScripting will call these functions to drive your triggers, actions, and authentication transactions. There are no plans to sunset the Legacy Scripting upon which all converted applications are dependent. 
Legacy apps can be converted to the [CLI](https://platform.zapier.com/manage/export-integration) with the ability to better optimize existing custom code. 
When creating new trigger/action/searches, you will build in the new UI, and any custom code written in the Legacy app cannot be called. Differences when writing custom code [here.](https://platform.zapier.com/manage/maintain-converted-integration#differences-when-writing-custom-scripting-code) Existing triggers/actions built in the Legacy app and any new triggers/actions you build in the new UI will work simultaneously. 
In the new UI, custom code is written in Code Mode within each module (authentication, trigger, action, search).
See more details [here.](https://platform.zapier.com/manage/maintain-converted-integration)
To fully convert your app to the new Zapier Platform UI and eliminate any legacy references,  you’ll need to rebuild each module (authentication, trigger, action, search). Contact [Developer Support]
(https://developer.zapier.com/contact) to request a cloned “shell” version that retains the names and keys of the trigger/action/searches. You’ll need to add in endpoints and any custom code. Depending on the nature of your changes, you would want to review the best practices in this list to assess if migration of users is an option. 

### Converting UI to CLI

##### Change Scenario

The Zapier CLI (Command Line Interface) is a toolset you install and run on your local development environment. It allows you to build, test, and manage your Zapier integration through JavaScript code and terminal commands instead of building in the visual builder on the Zapier Platform. [Compare UI to CLI features.](https://platform.zapier.com/quickstart/zapier-platform) 

##### Impact to Users

At time of exporting an app to the CLI in your local environment, there is no user impact. Once you push and promote a version from the CLI, you’ll want to consider any changes made. 
When exporting an app from the UI to CLI, you can push the new CLI version (as long as no changes were made) and migrate users. 
If instead you create a brand new CLI app, migration of users may not be possible and you would want to review the best practices in this list to assess the impacts of your changes. Contact [Developer Support]
(https://developer.zapier.com/contact) for steps to push your new CLI version as a new version of the existing UI app. 
When there are breaking changes between the UI version and the new CLI version, existing users will be able to continue using the version they’re on, but must upgrade to the new version manually. Zapier does not automatically notify all existing users of a new version’s availability, but new users would see the currently promoted/Public version when searching for the app name. We also recommend announcing the changes/new integration version to your general user base via in-app or email marketing to encourage users to switch over.
It is recommended to allow users to remain on the old version until they switch over manually, as long as the endpoints are functional. If [Deprecation](https://platform.zapier.com/manage/versions-ui#deprecating-versions) is necessary, please note this is significantly more disruptive to our mutual users and should be considered carefully. 

##### Best Practices

Once an UI app version is exported to a CLI version to your local environment, it can be deleted, so there’s no risk in trying it out before promoting it to users. You’ll just lose any changes you made in the CLI version as those cannot be converted back to the UI. 
Change the version number in your local environment from the `package.json` file before you push to keep the latest private version you built in the visual builder for reference. 
If you don’t bump the version number and attempt to `zapier push` to a Public version or one with more than 5 users, you’ll see a version blocked error in the History tab to prevent a Public version from being overwritten. That error simply means the `zapier push` was not successful, it does not affect the version’s existing users. 
See more details to convert [here](https://platform.zapier.com/manage/export-integration#how-to-export-your-integration) and a setup guide [here.](https://platform.zapier.com/quickstart/platform-cli-tutorial)

### Converting CLI to UI

##### Change Scenario

Building in the UI is the easiest way for anyone with API experience to build Zapier integrations. [Compare CLI to UI features.](add link to https://platform.zapier.com/docs/vs)

##### Impact to Users

When moving an app from CLI to the VB, we **cannot** migrate users from previous versions or apps. Existing users will be able to continue using the version they’re on, but must upgrade to the new version manually. Zapier does not automatically notify all existing users of a new version’s availability, but new users would see the currently promoted/Public version when searching for the app name. We also recommend announcing the changes/new integration version to your general user base via in-app or email marketing to encourage users to switch over.
It is recommended to allow users to remain on the old version until they switch over manually, as long as the endpoints are functional. If [Deprecation](https://platform.zapier.com/manage/versions-cli#deprecate-an-older-version-of-your-integration) is necessary, please note this is significantly more disruptive to our mutual users and should be considered carefully. 

##### Best Practices

Contact [Developer Support](https://developer.zapier.com/contact) to create an **empty** version associated to your same app ID. Hiding an app and replacing it with a new app ID built in the preferred tool is [**not** supported.](https://platform.zapier.com/publish/integration-publishing-guidelines#23-replacement-integration) 
You will need to re-build the integration from scratch with feature parity to the previous CLI version, and it can then be maintained in the visual builder by your team. For Public apps, this avoids a repeat of the app review process; as well as retaining previous versions, associated bug reports and feature requests.