---
title: Frequently asked questions
order: 21
layout: post-toc
redirect_from: /docs/faq
---

# Frequently asked questions

<a id="save"></a>

## Does Zapier auto-save integrations?

_No_. Always remember to save your work when building integrations. Zapier asks you to save and continue in several spots while building integrations, so be sure to save at each point:

![Save auth and API calls](https://cdn.zappy.app/197afa28db0a58da34f339553ea4631f.png)

When adding authentication and API calls for triggers or actions, there are _Save & Continue_ buttons between each step. Click each one when you are finished adding details to your API call form or code mode editor.

![Save triggers and actions](https://cdn.zappy.app/57809cc1b678825d0f2e96909270d3d8.png)

When adding a new trigger or action, there is a _Save_ button after the Zap step details. Click that to save your new trigger or action step, before adding the input form and API configuration.

![Save input fields](https://cdn.zappy.app/84ae560095048083c876d3a2274743f4.png)

When adding a new field to an authentication, trigger, or action step's input field, click _Save_ after adding the field details.

<a id="code"></a>

## Why are options grayed out for my CLI-built integration?

![Zapier CLI integration in visual builder](https://cdn.zappy.app/1bf0fc78333fa9a48d6ed3b234f3e717.png)

The Zapier Command Line Interface (CLI) is a separate SDK available to install on your local development machine to create Zapier integrations. It lets you work in code rather than a web based UI for more advanced integrations.

Integrations created in the CLI cannot be edited in the visual builder UI. You can’t add triggers or actions, edit code or configurations, for instance. Zapier's platform site lists every integration you build, in the visual builder or CLI, but disables the core editing options for CLI-built integrations. These options will be grayed out in the UI.

You _can_ manage the other details of your CLI integration from the UI, however, including:

- Invite testers and collaborators
- Monitor integration usage
- Change environment variables
- Submit your integration to be made publicly available
- Promote a new integration version to public
- Migrate users between versions

You can [export a CLI version of your builder project to a CLI format](https://platform.zapier.com/manage/export-integration) that you can edit and maintain on your local development machine. You can then create and push new versions of your integration via Zapier CLI, and can manage the details from the visual builder UI or the CLI. Once you enable CLI, though, you will not be able to edit or add authentication, trigger, or action details in the visual builder UI.

If your app was originally built on our legacy platform, any custom code you wrote there will be accessible in a ‘scripting.js’ file in your exported CLI app.

<a id="response"></a>

## Can I add files/attachments to a Trigger/Action using the Platform UI Visual Builder?

No. If you'd like to work with file attachments in your app, you'll need to convert your app from the [Visual Builder to the CLI platform](https://platform.zapier.com/manage/export-integration) instead.

<a id="files"></a>

## What response type does Zapier expect?

With every API call, including authentication and auth testing calls, triggers, searches, and create actions, Zapier expects to receive response data from the API. If your API call does not return a response, Zapier will show a timeout error.

Zapier additionally expects different data for different API calls:

- **Object** _for Authentication, Auth testing, and Create Actions_. Zapier expects to receive a single JSON formatted object with the correct details, including specific fields for Authentication calls depending on the auth scheme. Zapier will parse the individual fields and, with Create Actions, let users include their data in subsequent Zap steps.
- **Array** _for Triggers and Search Actions_. Zapier expects to receive a JSON formatted array with the results in reverse chronological order. Even if the trigger or search only returns a single item, it should be formatted as an array. Zapier will then parse the results and return the most relevant result for searches, and return all new items from Triggers that pass Zapier's deduper.

<a id="array"></a>

## I got an "An array is expected" error. How do I fix that?

With you add a polling trigger or search action to a Zap, the Zapier platform expects to get a bare array of the new or found items, sorted in reverse chronological order. APIs will instead return a result _object_ that contains the array of items the trigger needs.

{% raw %}
For example, for a "Find Issue" search action with GitHub's API, we might start with a `https://api.github.com/repos/{{bundle.inputData.owner}}/ {{bundle.inputData.repo}}/issues/{{bundle.inputData.issue_number}}` request:
{% endraw %}

![](https://cdn.zappy.app/a5516cc30abee4f84a58ac5b7b3dfc76.png)

Test it, though, and Zapier will show an error message like the one below:

![](https://cdn.zappy.app/2461b0e7f49ecf5aed90d429a59ad2bf.png)

Dig into the API response in the HTTP tab, and you'll see that what was returned was an _object_ that contains the array of items we need, not the array itself:

![](https://cdn.zappy.app/d569e3a05f643a9a199b5d85dc4a4fc2.png)

What we need to return to Zapier is that array of channels. To do that we need to switch to "[Code Mode](https://platform.zapier.com/build/code-mode)" in our request. That lets us provide a JavaScript function to handle our request, where we can make needed changes to the structure or content of the result before we return data to the Zapier platform.

For this request, wrap the response with an array instead of the default `return results`, to have Zapier return an array of issues.

![](https://cdn.zappy.app/3bec13fa502f47ff1e5f9bfded052b4d.png)

> Remember: "Code Mode" is a toggle; if you switch back to Form Mode your code will be ignored! [Learn more](#code).

Now, retest the request and it should run successfully.

![](https://cdn.zappy.app/af56c7fed5183aed462d2e7efbf78f8c.png)

<a id="censored"></a>

## Why does Zapier show `censored` fields in request and response data?

![Example censored fields in Zapier](https://cdn.zappy.app/1ace9c1a32b101b30d8600db73c5dd10.png)

When testing Authentication, Triggers, or Actions in Zapier visual builder, you can see the raw data Zapier sends to your API call and receives from it in the _Bundle_ and _HTTP_ tabs of the testing pane. Some of those values may not be shown; instead, you'll see a value like `:censored:6:82a3be9927:` as in the screenshot above.

Zapier automatically censors sensitive values at runtime, including all input fields marked as `password` and all authentication fields that will include sensitive, private data including username and password fields from Basic and Digest auth, API keys from API key auth, access and refresh tokens from Session and OAuth v2 authentication. These values are stored in the `Auth` bundle and used in API calls, but are replaced in Zapier's logs with a `censored` value.

<a id="cleanup"></a>

## How do I clean up test authentication accounts?

![Example account with multiple test accounts](https://cdn.zappy.app/943cd7b0ee2ada32492c834157a2eccb.png)

While building your integration, testing authentication, and customizing your app's connection label, you may quickly end up with a list of broken or old app authentications. You can clean those up and remove older accounts from your core Zapier account.

![Remove authed accounts](https://cdn.zappy.app/b31f5c7f712c1a585e727b729248615a.png)

Open your [Zapier _Connected Accounts_](https://zapier.com/app/connections) page, and find your app's name (you may need to use the search box or `CMD`+`F` (Mac) or `Ctrl`+`F` (PC)). Click the app name. Once on the app's connections page, identify the connection to remove and click the three dots, then _Delete_, and confirm the deletion. Repeat for each subsequent testing account you added to clean up your authentication list.

Then refresh your integration page in the Visual Builder, and you'll only see the authentications that were not deleted.

<a id="output"></a>

## How do Sample Data and Output Fields work?

![Adding Sample Data to Zapier integration](https://cdn.zappy.app/293b09e9593b591de3c735988f1a5f19.png)
_Sample Data gives Zapier example data if users don't test the trigger or action. Output Fields give your API data user-friendly names in subsequent Zap steps._

The last step in creating a new Trigger or Action for a Zapier integration is to _Define your Output_. Zapier asks both for Sample Data and Output Fields. Sample Data is especially important for Triggers, and useful with Actions as well. Output Fields are equally important for both triggers and actions, as the output data from both may be used in subsequent Zap steps.

### Sample Data

![Sample Data in a Trigger step with no available data](https://cdn.zappy.app/05e9be8a62a663f42ab25cf2b17591b8.png)
![Sample Data in an Action step](https://cdn.zappy.app/42353c3702ca94af6000e3efb926a3f2.png)

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

The user's Zap will error unexpectedly when they try to add the person to their CRM because `job_title` is a required field in the CRM but there's no data in it. Because this result is confusing, there are several [integration checks](https://platform.zapier.com/publish/integration-checks-reference) that require sample and live data to match.

### Output Fields

Output Fields add user-friendly labels to your API's response data. Zapier uses a basic human-friendly transformation of field names by default, capitalizing words and adding spaces instead of underscores. You can customize this further with Output Fields.

For example, if you use GitHub's API to watch for new issues, the API calls the issue name `title`. Users may expect that field to be called _Issue_ or _Issue Title_, so you could define the Output Field as having the name _Issue Title_, rather than the default transformation of "Title".

You can learn more about how Zapier uses sample data and output fields in [triggers](https://platform.zapier.com/build/triggers#define-sample-data-and-output-fields) and [actions](https://platform.zapier.com/build/action#define-sample-data-and-output-fields).

<a id="resthooktesting"></a>

## How do I define REST Hooks?

See [Triggers: REST Hook Trigger](https://platform.zapier.com/build/triggers#rest-hook-trigger) for details.
