---
title: FAQs
order: 16
layout: post-toc
redirect_from: /docs/
---

# Frequently Asked Questions

<a id="save"></a>
## Does Zapier auto-save integrations?

_No_. Always remember to save your work when building integrations. Zapier asks you to save and continue in several spots while building integrations, so be sure to save at each point:

![Save auth and API calls](https://cdn.zapier.com/storage/photos/a0bfc995ebb8c292c4329ee9c4e4b485.png)

When adding authentication and API calls for triggers or actions, there are _Save & Continue_ buttons between each step. Click each one when you are finished adding details to your API call form or code mode editor.

![Save triggers and actions](https://cdn.zapier.com/storage/photos/dba285167f1d4557023803dcb5d54dc8.png)

When adding a new trigger or action, there is a _Save_ button after the Zap step details. Click that to save your new trigger or action step, before adding the input form and API configuration.

![Save input fields](https://cdn.zapier.com/storage/photos/6684ecfcfab99cb4573d1ba2b23b4966.png)

When adding a new field to an authentication, trigger, or action step's input field, click _Save_ after adding the field details.

<a id="code"></a>
## How does Code Mode work?

![Zapier visual builder code mode](https://cdn.zapier.com/storage/photos/5abf045cf0b8f3cce37d05d51071d6e9.png)
_Each API call pane in Zapier visual builder includes a code mode toggle_

The Zapier visual builder includes a form to add API endpoint URLs and choose the API call type, then automatically includes any authentication details and input form data with the API call. You can also set any custom options your API may need, including custom URL params, HTTP headers, and request body items. Zapier then parses JSON-encoded responses into individual output fields to use in subsequent Zap steps.

This is the best way to set up most API calls and options in Zapier integration authentication, triggers, and actions.

If your API calls need more customization, however, or your API response is in a non-JSON format, you will need to write custom JavaScript code to handle your API call and/or response parsing. The Zapier visual builder includes a _Switch to Code Mode_ toggle on every API request, similar to the one pictured above, that switches that specific API call to code mode.

> **Remember:** Code Mode is a toggle. Code Mode and Form Mode are saved separately; changes to one do not affect the other. The settings in the currently visible editor are the ones Zapier uses in your integration.

The first time you switch to code mode, Zapier copies everything entered in the API request form, including any custom options added, and converts them to JavaScript code. It then changes the UI to code mode, where you can add code for your API call.

In code mode, you can write JavaScript code, using Zapier's default code as a base or writing custom code. Use the `z.object` for Zapier specific features, including `z.console` to write to the console log, `z.JSON` to parse JSON, `z.errors` to take action on errors, and more. Check [Zapier's CLI Z Object docs](https://zapier.github.io/zapier-platform-cli/#z-object) for details. 

Additionally, use Zapier bundles to access auth data, data from user input forms, request data, and more. Learn more in our [Zapier bundle docs](https://platform.zapier.com/docs/advanced#bundle).

> **Note**: If you were familiar with our legacy Web Builder environment, we used to include several 3rd party libraries, like lodash, and made them available on the z object. Those libraries are not included in the new version of the UI tool. If you need access to additional modules you can easily move your project to the [Zapier CLI](https://zapier.github.io/zapier-platform-cli) and take advantage of npm to bring in any additional libraries you need.

> Note that, in Code Mode you can import from Node's standard library with `z.require`, for example, `z.require('querystring')` or `z.require('crypto')`. We strongly recommend you keep it simple when coding in the UI tool. The CLI is much better suited to building and testing complex code. And be sure you know what you're doing - we can't guarantee that everything you might use from the standard library will be supported in our platform's runtime.

There is a time limit of 30 seconds for each trigger and action, so keep your custom code as light and quick as feasible. If code takes longer than 30 seconds to run, it will time out, and users' Zaps will not be successful.

Do note that changes are not saved automatically. Once you have added the code you want, click _Save & Continue_ to add the changes to your integration.

![Zapier code mode switch to form mode](https://cdn.zapier.com/storage/photos/ea2eb690bf92b55fab0bbad290107a97.png)
_Switch back to form mode to use the form mode settings instead of your custom code_

Once you switch to code mode, Zapier uses your custom code for that API call, and does not use the data you previously entered in the form.

If you wish to switch back to the form mode, click the _Switch to Form Mode_ button to see the form options as they were when you first switched to code mode. Zapier will save the code you entered, but will not convert it back to the form mode or use the custom code in your live integration.

You may switch back to code mode again—though this time, Zapier will show the last saved version of your code, and will not copy any changes from your API call form to the code.

## Is my Zapier integration using the Form or Code Mode settings?

Zapier uses the currently visible option when running each part of your integration. If the form mode is visible for an API call in an integration's authentication, trigger, or action settings, that Zapier integration is using the data from form mode. If the code mode is visible for an API call, Zapier is using the code instead to turn that part of the integration.

To check which mode and settings Zapier is using for each API call, open that part of your Zapier integration and visually check to see if the form or code mode is visible.

<a id="cli"></a>
## Why are options grayed out for my CLI-built integration?

![Zapier CLI integration in visual builder](https://cdn.zapier.com/storage/photos/c631ca2cd91ab43b0bc4d22f641eb4d6.png)

The Zapier Command Line Interface (CLI) is a separate SDK available to install on your local development machine to create Zapier integrations. It lets you work in code rather than a web based UI for more advanced integrations.

Integrations created in the CLI cannot be edited in the visual builder UI. You can’t add triggers or actions, edit code or configurations, for instance.  Zapier's platform site lists every integration you build, in the visual builder or CLI, but disables the core editing options for CLI-built integrations. These options will be grayed out in the UI.

You _can_ manage the other details of your CLI integration from the UI, however, including:

- Invite testers and collaborators
- Monitor integration usage
- Change environment variables
- Submit your integration to be made publicly available
- Promote a new integration version to public
- Migrate users between versions

You can [export a CLI version of your builder project to a CLI format](https://platform.zapier.com/docs/export) that you can edit and maintain on your local development machine. You can then create and push new versions of your integration via Zapier CLI, and can manage the details from the visual builder UI or the CLI. Once you enable CLI, though, you will not be able to edit or add authentication, trigger, or action details in the visual builder UI.

If your app was originally built on our legacy platform, any custom code you wrote there will be accessible in a ‘scripting.js’ file in your exported CLI app.

<a id="response"></a>

## Can I add files/attachments to a Trigger/Action using the Platform UI Visual Builder?

No. If you'd like to work with file attachments in your app, you'll need to convert your app from the [Visual Builder to the CLI platform](https://platform.zapier.com/docs/export) instead. 

<a id="files"></a>

## What response type does Zapier expect?

With every API call, including authentication and auth testing calls, triggers, searches, and create actions, Zapier expects to receive response data from the API. If your API call does not return a response, Zapier will show a timeout error.

Zapier additionally expects different data for different API calls:

- **Object** *for Authentication, Auth testing, and Create Actions*. Zapier expects to receive a single JSON formatted object with the correct details, including specific fields for Authentication calls depending on the auth scheme. Zapier will parse the individual fields and, with Create Actions, let users include their data in subsequent Zap steps.
- **Array** *for Triggers and Search Actions*. Zapier expects to receive a JSON formatted array with the results in reverse chronological order. Even if the trigger or search only returns a single item, it should be formatted as an array. Zapier will then parse the results and return the most relevant result for searches, and return all new items from Triggers that pass Zapier's deduper.

<a id="array"></a>
## I got an "An array is expected" error. How do I fix that?

With you add a polling trigger or search action to a Zap, the Zapier platform expects to get a bare array of the new or found items, sorted in reverse chronological order. APIs will instead return a result _object_ that contains the array of items the trigger needs.

For example, for a "New Channel" trigger with Slack's API, we might start with a `http://slack.com/api/channels.list` request:

![](https://cdn.zapier.com/storage/photos/1f84a3519ad4e78c3567cdbff8a4c1d3.png)

Test it, though, and Zapier will show an error message like the one below:

![](https://cdn.zapier.com/storage/photos/55f500a240d571c5d81be4a28fff109b.png)

Dig into the API response, and you'll see that what was returned was an _object_ that contains the array of items we need, not the array itself:

```
{
    "ok": true,
    "channels": [
        {
            "id": "01234",
            "name": "general",
            "is_channel": true,
            "created": 1390943394,
            "is_archived": false,
            "is_general": true,
            "unlinked": 0,
            ....
```

What we need to return to Zapier is that array of channels. To do that we need to switch to "Code Mode" in our request. That lets us provide a JavaScript function to handle our request, where we can make needed changes to the structure or content of the result before we return data to the Zapier platform.

For this request, use `return results.channels` in line 18, instead of the default `return results`, to have Zapier return the array of results from `channels`.

![](https://cdn.zapier.com/storage/photos/e1d09e9fdf952ef5f5b031bd705e5802.png)

> Remember: "Code Mode" is a toggle; if you switch back to Form Mode your code will be ignored! [Learn more](#code).

Now, retest the request and it should run successfully. Note the response this time is a bare array:

![](https://cdn.zapier.com/storage/photos/33098c9f9c1584295e074c1dc8a40e72.png)

<a id="censored"></a>
## Why does Zapier show `censored` fields in request and response data?

![Example censored fields in Zapier](https://cdn.zapier.com/storage/photos/9356f3af9c0a844a652868d877e22486.png)

When testing Authentication, Triggers, or Actions in Zapier visual builder, you can see the raw data Zapier sends to your API call and receives from it in the _Bundle_ and _HTTP_ tabs of the testing pane. Some of those values may not be shown; instead, you'll see a value like `:censored:6:82a3be9927:` as in the screenshot above.

Zapier automatically censors sensitive values at runtime, including all input fields marked as `password` and all authentication fields that will include sensitive, private data including username and password fields from Basic and Digest auth, API keys from API key auth, access and refresh tokens from Session and OAuth v2 authentication. These values are stored in the `Auth` bundle and used in API calls, but are replaced in Zapier's logs with a `censored` value.

<a id="cleanup"></a>
## How do I clean up test authentication accounts?

![Example account with multiple test accounts](https://cdn.zapier.com/storage/photos/7fe9f9155dafbcc5d9b461720d664d4d.png)

While building your integration, testing authentication, and customizing your app's connection label, you may quickly end up with a list of broken or old app authentications. You can clean those up and remove older accounts from your core Zapier account.

![Remove authed accounts](https://cdn.zapier.com/storage/photos/c7fe45e90f7c4c00f6ffd938d417cdd0.png)

Open your [Zapier _Connected Accounts_](https://zapier.com/app/connections) page, and find your app's name (you may need to use the search box or `CMD`+`F` (Mac) or `Ctrl`+`F` (PC)). Click the app name. Once on the app's connections page, identify the connection to remove and click the three dots, then _Delete_, and confirm the deletion. Repeat for each subsequent testing account you added to clean up your authentication list.

Then refresh your integration page in the Visual Builder, and you'll only see the authentications that were not deleted.

<a id="output"></a>
## How do Sample Data and Output Fields work?

![Adding Sample Data to Zapier integration](https://cdn.zapier.com/storage/photos/8ab32f061aa89f3b57e8f4a5ea16a9d9.png)
_Sample Data gives Zapier example data if users don't test the trigger or action. Output Fields give your API data user-friendly names in subsequent Zap steps._

The last step in creating a new Trigger or Action for a Zapier integration is to _Define your Output_. Zapier asks both for Sample Data and Output Fields. Sample Data is especially important for Triggers, and useful with Actions as well. Output Fields are equally important for both triggers and actions, as the output data from both may be used in subsequent Zap steps.

### Sample Data

![Sample Data in a Zap Step](https://cdn.zapier.com/storage/photos/d4e5d47c461efa897a907c2806aecc1d.png)

In the Zap Editor, Zapier will attempt to retrieve or create existing data to test Triggers and Actions. If users are in a hurry when building a Zap, or don't have any data available, they can skip these test steps. Zapier will then show the sample data instead, so they can map fields correctly in subsequent Zap steps without seeing their account's live data.

Make sure to provide JSON-formatted sample data using the same field names as your API. The sample response data should not include any personally identifiable data, have copy that is safe for work, and be easily recognizable as sample data.

When providing sample data, it's also important that it only include fields that are present every time a Zap runs. When a field is provided in the sample, it can be mapped into a field in a later action.

If that field isn't available when the user's Zap runs, the action field will be empty, which can cause errors or unexpected results for users. For example, suppose your sample data looks like this:

```json
{
  "id": 1,
  "first_name": "Jane",
  "last_name": "Suarez",
  "email_address": "janesz@example.com",
  "job_title": "Executive Director"
}
```

A user might map the `job_title` information into a required field in another app, such as a CRM. Then, when the Zap runs, `job_title` is only included in the live result if it happens to be available, and the data the Zap receives looks like this:

```json
{
  "id": 5,
  "first_name": "Jacob",
  "last_name": "Giotto",
  "email_address": "jacob@example.com"
}
```

The user's Zap will error unexpectedly when they try to add the person to their CRM because `job_title` is a required field in the CRM but there's no data in it. Because this result is confusing, there are several [integration checks](./integration-checks-reference) that require sample and live data to match.

### Output Fields

Output Fields add user-friendly labels to your API's response data. Zapier uses a basic human-friendly transformation of field names by default, capitalizing words and adding spaces instead of underscores. You can customize this further with Output Fields.

For example, if you use GitHub's API to watch for new issues, the API calls the issue name `title`. Users may expect that field to be called _Issue_ or _Issue Title_, so you could define the Output Field as having the name _Issue Title_, rather than the default transformation of "Title".

You can learn more about how Zapier uses sample data and output fields in [triggers](/docs/triggers#define-sample-data-and-output-fields) and [actions](/docs/actions#define-sample-data-and-output-fields).

