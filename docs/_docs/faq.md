---
title: FAQs
order: 16
layout: post-toc
redirect_from: /docs/
---

# Frequently Asked Questions

<a id="save"></a>
## Does Zapier Auto-Save Integrations?

_No_. Always remember to save your work when building integrations. Zapier asks you to save and continue in several spots while building integrations, so be sure to save at each point:

![Save auth and API calls](https://cdn.zapier.com/storage/photos/a0bfc995ebb8c292c4329ee9c4e4b485.png)

When adding authentication and API calls for triggers or actions, there are _Save & Continue_ buttons between each step. Click each one when you are finished adding details to your API call form or code mode editor.

![Save triggers and actions](https://cdn.zapier.com/storage/photos/dba285167f1d4557023803dcb5d54dc8.png)

When adding a new trigger or action, there is a _Save_ button after the Zap step details. Click that to save your new trigger or action step, before adding the input form and API configuration.

![Save input fields](https://cdn.zapier.com/storage/photos/6684ecfcfab99cb4573d1ba2b23b4966.png)

When adding a new field to an authentication, trigger, or action step's input field, click _Save_ after adding the field details.

<a id="code"></a>
## How Does Code Mode Work?

![Zapier visual builder code mode](https://cdn.zapier.com/storage/photos/5abf045cf0b8f3cce37d05d51071d6e9.png)
_Each API call pane in Zapier visual builder includes a code mode toggle_

Zapier visual builder includes a form to add API endpoint URLs and choose the API call type, then automatically includes any authentication details and input form data with the API call. You can additionally set any custom options your API may need, including custom URL params, HTTP headers, and request body items. Zapier then parses JSON encoded responses into individual output fields to use in subsequent Zap steps.

This is the best way to set up most API calls and options in Zapier integration authentication, triggers, and actions.

If your API calls need more customization, however, or your API response is in a non-JSON format, you will need to write custom JavaScript code to handle your API call and/or response parsing. Zapier visual builder includes a _Switch to Code Mode_ toggle on every API request, similar to the one pictured above, that switches that specific API call to code mode.

> **Remember:** Code Mode is a toggle. Code Mode and Form Mode are saved separately; changes to one do not affect the other. The settings in the currently visible editor are the ones Zapier uses in your integration.

The first time you switch to code mode, Zapier copies everything entered in the API request form, including any custom options added, and converts them to JavaScript code. It then changes the UI to code mode where you can add code for your API call.

In code mode, you can write JavaScript code, using Zapier's default code as a base or writing custom code. Use the `z.object` for Zapier specific features, including `z.console` to write to the console log, `z.JSON` to parse JSON, `z.errors` to take action on errors, and more. Check [Zapier's CLI Z Object docs](https://zapier.github.io/zapier-platform-cli/#z-object) for details.

Additionally, use Zapier bundles to access auth data, data from user input forms, request data, and more. Learn more in our [Zapier bundle docs](https://zapier.github.io/visual-builder/docs/advanced#bundle).

> **Note**: Code Mode does not load any default libraries. If you need to load NPM modules, use [Zapier Platform CLI](https://zapier.github.io/zapier-platform-cli/) instead.

Do note that changes are not saved automatically. Once you have added the code you want, click _Save & Continue_ to add the changes to your integration.

![Zapier code mode switch to form mode](https://cdn.zapier.com/storage/photos/ea2eb690bf92b55fab0bbad290107a97.png)
_Switch back to form mode to use the form mode settings instead of your custom code_

Once you switch to code mode, Zapier uses your custom code for that API call, and does not use the data you previously entered in the form.

If you wish to switch back to the form mode, click the _Switch to Form Mode_ button to see the form options as they were when you first switched to code mode. Zapier will save the code you entered, but will not convert it back to the form mode or use the custom code in your live integration.

You may switch back to code mode again—though this time, Zapier will show the last saved version of your code, and will not copy any changes from your API call form to the code.

## Is my Zapier Integration Using the Form or Code Mode Settings?

Zapier uses the currently visible option when running each part of your integration. If the form mode is visible for an API call in an integration's authentication, trigger, or action settings, that Zapier integration is using the data from form mode. If the code mode is visible for an API call, Zapier is using the code instead to turn that part of the integration.

To check which mode and settings Zapier is using for each API call, open that part of your Zapier integration and visually check to see if the form or code mode is visible.

<a id="cli"></a>
## Why Are Options Grayed Out For my CLI-built Integration?

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

_Coming Soon_: In an upcoming version of Zapier's visual builder, you will be able to export a CLI version of your visual builder project. This will be a one-time export that converts your visual builder integration to a CLI format that you can edit and maintain on your local development machine. You can then create and push new versions of your integration via Zapier CLI, and can manage the details from the visual builder UI or the CLI. Once you enable CLI, though, you will not be able to edit or add authentication, trigger, or action details in the visual builder UI.

<a id="response"></a>
## What Response Type Does Zapier Expect?

With every API call, including authentication and auth testing calls, triggers, searches, and create actions, Zapier expects to receive response data from the API. If your API call does not return a response, Zapier will show a timeout error.

Zapier additionally expects different data for different API calls:

- **Object** *for Authentication, Auth testing, and Create Actions*. Zapier expects to receive a single JSON formatted object with the correct details, including specific fields for Authentication calls depending on the auth scheme. Zapier will parse the individual fields and, with Create Actions, let users include their data in subsequent Zap steps.
- **Array** *for Triggers and Search Actions*. Zapier expects to receive a JSON formatted array with the results in reverse chronological order. Even if the trigger or search only returns a single item, it should be formatted as an array. Zapier will then parse the results and return the most relevant result for searches, and return all new items from Triggers that pass Zapier's deduper.

<a id="array"></a>
## I Got an "An array is Expected" error. How do I Fix That?

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
## Why Does Zapier Show `censored` Fields in Request and Response Data?

![Example censored fields in Zapier](https://cdn.zapier.com/storage/photos/9356f3af9c0a844a652868d877e22486.png)

When testing Authentication, Triggers, or Actions in Zapier visual builder, you can see the raw data Zapier sends to your API call and receives from it in the _Bundle_ and _HTTP_ tabs of the testing pane. Some of those values may not be shown; instead, you'll see a value like `:censored:6:82a3be9927:` as in the screenshot above.

Zapier automatically censors sensitive values at runtime, including all input fields marked as `password` and all authentication fields that will include sensitive, private data including username and password fields from Basic and Digest auth, API keys from API key auth, access and refresh tokens from Session and OAuth v2 authentication. These values are stored in the `Auth` bundle and used in API calls, but are replaced in Zapier's logs with a `censored` value.

<a id="cleanup"></a>
## How to Clean Up Test Authentication Accounts?

![Example account with multiple test accounts](https://cdn.zapier.com/storage/photos/7fe9f9155dafbcc5d9b461720d664d4d.png)

While building your integration, testing authentication, and customizing your app's connection label, you may quickly end up with a list of broken or old app authentications. You can clean those up and remove older accounts from your core Zapier account.

![Remove authed accounts](https://cdn.zapier.com/storage/photos/c7fe45e90f7c4c00f6ffd938d417cdd0.png)

Open your [Zapier _Connected Accounts_](https://zapier.com/app/settings/authorizations) page, and press `CMD`+`F` or `Ctrl`+`F` then search for your app's name. Click _Disconnect_ then confirm to remove any account, and repeat for each subsequent testing account you added to clean up your authentication list.

Then refresh your integration page in visual builder, and you'll only see the authentications you left running.

<a id="output"></a>
## How do Sample Data and Output Fields Work?

![Adding Sample Data to Zapier integration](https://cdn.zapier.com/storage/photos/8ab32f061aa89f3b57e8f4a5ea16a9d9.png)
_Sample Data gives Zapier example data if users don't test the trigger or action; Output Fields give your API data user-friendly names in subsequent Zap steps_

The last step in creating a new Trigger or Action for a Zapier integration is to _Define your Output_. Here, Zapier asks both for Sample Data and Output Fields. Neither are required, but both help improve the Zapier experience for your users.

![Sample Data in a Zap Step](https://cdn.zapier.com/storage/photos/d4e5d47c461efa897a907c2806aecc1d.png)

Sample Data lists the default data Zapier shows users when building a Zap using this step. By default, Zapier will ask to test the Zap step after users set it up. With Triggers, Zapier will try to fetch recently added or updated items; with Actions, Zapier will try to find or create the item using the user's data.

If users are in a hurry, though, they can click _Skip This Step_. Zapier will then show the sample data instead, both with triggers and actions, so they can map fields correctly in subsequent Zap steps without seeing their app account's live data. Or with triggers, if your app doesn't have any data for this item yet, Zapier will default to showing the sample data instead of showing an error that no items are available.

Sample Data is especially important for Triggers, and useful with Actions as well.

To include sample data in your integration, open the final step of your Zapier trigger or action's API Configuration. There, write valid JSON output data using the same field names as your API with sample response data that does not include any personally identifiable data, is safe for work copy, and is easily recognizable as sample data. Here are example sample data for a GitHub issue:

    {
      "body": "This is a sample issue",
      "html_url": "https://github.com/",
      "title": "Test Issue"
    }

![Adding Output Fields to Zapier integration](https://cdn.zapier.com/storage/photos/31d6247a888135ed334d5035ce4b0ade.png)

Output Fields add user-friendly labels to your API's response data. By default, Zapier will try to make friendly version of your API's response, capitalizing words and adding spaces instead of underscores. You can customize this further with Output Fields.

For example, if you use GitHub's API to watch for new issues, the API calls the issue name _Title_. Users may expect that field to be called _Issue_ or _Issue Title_, so you could define that add a custom name for that field.

Output Fields are equally important for both triggers and actions, as the output data from both may be used in subsequent Zap steps.

To add output fields, list the original field name from your API response in the left column, and a human friendly name for the field in the right column of your Zapier trigger or action's API configuration. Zapier will then substitute those names for those output field titles in your users' Zaps as in the screenshot above.