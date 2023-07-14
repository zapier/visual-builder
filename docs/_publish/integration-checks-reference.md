---
title: Integration check reference
order: 5
layout: post-toc
redirect_from: /docs/integration-checks-reference
---

# Integration Checks Reference

We run your integration through a set of automated checks to ensure it's working properly and giving our users (and yours) the best possible experience. 

To [publish your integration](https://platform.zapier.com/publish/public-integration), all Errors and Publishing Tasks should be validated. You can address any Warnings after [submitting your integration for review](https://platform.zapier.com/publish/public-integration#4-submit-your-integration-for-app-review).

If your integration will remain private, it isn't necessary to clear validation checks. You can [invite others to test your integration](https://platform.zapier.com/build/test-integration#how-to-invite-others-to-test-new-integrations) before publication.

To help better address a check in communication, each check is given a unique ID, consisting of a capital letter and three digits, such as `D001`.

You don't need to know the implication of the initial capitial letter. But if you're curious, they are:

Area | Description
--- | ---
<b><u>C</u></b>ompatibility | Only apply when your integration is public, these checks verify how the new version is backward compatible with the currently public version. They ask questions like "would this change break existing Zaps, Zap Templates, or connected accounts?"
<b><u>D</u></b>efinition | Definition of the integration, including auth and trigger/search/action configurations. Some of these checks could block you from saving/pushing if the violation results in a broken trigger/search/action.
<b><u>M</u></b>arketing | Public-facing information, such as the app title, description, and logo. The intent of these rules is to give Zapier users a consistent style among texts and images across all public integrations. They're more likely to block you from going public.
Connected <b><u>A</u></b>ccounts | Connected accounts that are linked to your integration. We verify these to ensure the authentication is working.
<b><u>S</u></b>tats | Usage stats, such as the number of users your integration has. These are more likely to block you from going public.
<b><u>T</u></b> - Zap History | Data from runs in your Zap History, produced by live (enabled) Zaps. These are more likely to block you from going public. The "T" checks are named as such for historical reasons. Zapier now shows tasks in the Zap History.
<b><u>U</u></b>ser | Things in the developer's (your) account, such as Terms of Service acceptance.
<b><u>L</u></b>ifecycle | The lifecyle state of your integration or its versions, such as the visibility (private, pending, or public) and the version state (deprecated, non-production, or production).
<b><u>Z</u></b>ap | Things related to Zaps, such as the trigger samples you pulled into the Zap editor.

When the checks are run, we'll give a brief blurb summarizing the violation (with a check ID) along with a link to this page. This will act as a full reference explaining each error and giving examples for each.

{% raw %}

---

<a name="A001"></a><a name="A00001"></a>

## A001 - A Connected Account Exists

To ensure you've tested auth, we require you to set up at least one
connected account.

---

<a name="C001"></a><a name="C00001"></a>

## C001 - Try To Avoid Hiding/Removing Public Triggers/Searches/Creates

During promotion, we compare features of your currently public version with your soon-to-be-public version.

When you hide/remove a trigger in a new version, Zap Templates that use that trigger become invalid. Try to avoid this when you can. The same applies for searches and creates.

---

<a name="C002"></a><a name="C00002"></a>

## C002 - Try To Avoid Removing Input Fields

During promotion, we compare features of your currently public version with your soon-to-be-public version.

When you change/remove the `key` property of an `input_field`, Zap Templates that use that field become invalid. Try to avoid this when you can.

---

<a name="C003"></a><a name="C00003"></a>

## C003 - Try To Avoid Removing Sample Data

During promotion, we compare features of your currently public version with your soon-to-be-public version.

When you change/remove the `key` property of an item in your `sample`, Zap Templates that use that field become invalid. Try to avoid this when you can.

---

<a name="D001"></a><a name="D00001"></a>

## D001 - Asks for API Key in Action Instead of in Auth

Some integrations incorrectly have `api_key` or similar as an an action field in an
action instead of centrally used in auth. This is worse because action fields
typically aren't treated with the same level of security as auth fields are (e.g.
scrubbed from logs) and aren't action specific. Additionally, the ability to test
the validity of auth doesn't exist for action fields, so anything auth related
should be put into an auth field instead.

---

<a name="D002"></a><a name="D00002"></a>

## D002 - Provide Link in Help Text for Auth Fields

It's often not obvious where a user can find their API credentials for a service. If
you use a pasted API key as an authentication method, it's strongly encouraged that
you link the user to the page (or relevant help doc) that has their key.

✘ an example of an **incorrect** implementation:

```
API key is found on the "API Details" page in settings
```

✔ an example of a **correct** implementation:

```
Go to the [API Details](https://my.site.com/manage/api-details) screen from your
Website Dashboard to find your API Key.
```

---

<a name="D003"></a><a name="D00003"></a>

## D003 - Connection Label Should Be Set

A Connection Label helps a customer remember which account they connected.
It should be short and easily identifiable.

For both [Platform UI](https://platform.zapier.com/build/auth#how-to-add-a-connection-label-to-authenticated-accounts)
and [CLI](https://platform.zapier.com/reference/cli_docs#authentication), the connection
label is a string. You can use any data returned by your test function.

For instance, if a successful run of the auth test returns the following data:

```json
{
  "name": "Malcom Reynolds",
  "email": "youcanttaketheskyfromme@serenity.com",
  "job": "Captain"
}
```

Your connection label could be the following:

```
{{name}} - {{email}}
```

The most important role of the label is to uniquely identify the connection.

✘ an example of an **incorrect** connection label:

```
"Slack"
```

✔ an example of a **correct** connection label:

```
{{user}} @ {{team}}
```

---

<a name="D004"></a><a name="D00004"></a>

## D004 - ID Fields Should Have Dynamic Dropdowns

We've found that instead of instructing users to paste an item `id` into Zapier,
providing them with a [dynamic dropdown](https://platform.zapier.com/reference/cli_docs#dynamic-dropdowns)
greatly increases the likelihood of the user setting up Zaps correctly. Users will
still be able to map custom fields, but this gets them started on the right foot.

Read more about implementing dynamic dropdowns below:

- Platform UI: https://platform.zapier.com/build/input-designer#dropdown
- Platform CLI: https://platform.zapier.com/reference/cli_docs#dynamic-dropdowns

---

<a name="D005"></a><a name="D00005"></a>

## D005 - Dynamic Dropdown Connects to a Non-Existing Trigger

[Dynamic dropdowns](https://platform.zapier.com/reference/cli_docs#dynamic-dropdowns)
allow you to connect an input field to an existing trigger. The dropdown won't work
if the trigger key you specify doesn't exist.

---

<a name="D006"></a><a name="D00006"></a>

## D006 - REST Hook Trigger Needs a Polling URL

When users are setting up a hook-based (aka instant) Trigger, it's important to have
a polling fallback. For example, imagine a Zap that triggers on a new Slack message.
If testing relies on the sending of a webhook, the test won't complete without the user
sending an actual message in a Slack channel, which is disruptive.

Instead, during testing, the Perform List (`performList`) operation fetches a
(real) recent message using the provided URL for polling and uses it as the test result.
The polling URL is only used for tests.

It's very important that the structure of an object from a webhook and from a poll
are identical. Typically, this means modifying a poll result so that it looks like a
hook. If a poll has fields that a hook doesn't, the user may map them to a later
step, and when the Zap runs live, the value will be blank. This can cause errors
or unexpected results for users.

Let's walk through an example. Say we have a `New Contact` REST Hook trigger. When a
new contact is created, Zapier gets a webhook that looks like this:

```json
{
  "id": 1,
  "firstName": "Bruce",
  "lastName": "Wayne",
  "job": "Batman"
}
```

The accompanying polling URL would look something like `https://site.com/contacts/list`
and return:

```json
{
  "results": [
    {
      "id": 1,
      "firstName": "Bruce",
      "lastName": "Wayne",
      "job": "Batman",
      "friends": [2, 3, 4]
    },
    {
      "id": 2,
      "firstName": "Alfred",
      "lastName": "Pennyworth",
      "job": "Butler",
      "friends": [1, 3]
    }
  ]
}
```

To match the polling result to the hook result, you would modify this response to
remove the `friends` information, and return only the array of contacts, not the
enclosing object.

The polling result is not used when a user skips testing the Zap step. In that case,
Zapier uses the sample data.

See [Sample Data](./faq#output) for more details on this.

---

<a name="D007"></a><a name="D00007"></a>

## D007 - All URLs Should Be HTTPS

When handling customer data (which all Zapier functions do), it's strongly
encouraged that all communication take place securely. Using SSL is a big part
of that, so ensure your URLs have HTTPS as their protocol.

If you need help setting up an SSL certificate for your API, we suggest
[Let's Encrypt](https://letsencrypt.org/).

✘ an example of an **incorrect** setup:

```text
http://example.com/messages/subscribe
```

✔ an example of a **correct** implementation:

```text
https://example.com/messages/subscribe
```

---

<a name="D008"></a><a name="D00008"></a>

## D008 - Invalid Markdown Link

A valid markdown link consists of a pair of square brackets with the link text
paired with a pair of parens that have the link itself. See the
[markdown cheatsheet](https://daringfireball.net/projects/markdown/syntax#link) for
more info.

If you want to show a full link without actually linking to it, use backticks. This
makes it clear to the user that they don't need to click the link, it's just used as
an example. Any link used in plain text needs to either be a proper link or in
backticks.

✘ examples of an **incorrect** implementation:

```
See [Google(https://google.com)
```

```
See https://google.com
```

✔ examples of a **correct** implementation:

```
See [Google](https://google.com)
```

```
See `https://google.com`
```

If you see this error, you should look through both the description for the
trigger/action/search and the help text for any fields that might have bad links.

---

<a name="D009"></a><a name="D00009"></a>

## D009 - Requires at Least One Search Field

When making a search step, it's important to have a field to search on! Common
examples for searching for a user are by name, email, and username.

---

<a name="D010"></a><a name="D00010"></a>

## D010 - Missing "ID" Field in Static Sample Data

For polling triggers, the deduper uses the `id` field to decide if it's seen an
object before. It can be any sort of string, but it's important that it's unique.
If your object is returned with a differently named `id` field (such as
`contact_id`), write code to rename it. Hooks are not deduped, so they're not
required to have an `id`.

This check is similiar to `T002`. This check validates the static samples in
your integration definition, while `T002` validates the live polling results
in the Zap History.

✘ an example of an **incorrect** implementation:

```json
{
  "contact_id": 4,
  "contact_name": "David"
}
```

✔ an example of a **correct** implementation:

```json
{
  "id": 4,
  "contact_name": "David"
}
```

---

<a name="D011"></a><a name="D00011"></a>

## D011 - Redundant Help Text

Help text is optional and meant to provide non-obvious information or links for the
user. If the label and help text are the same, they are considered redundant.

✘ an example of an **incorrect** implementation:

```json
{
  "label": "Subdomain",
  "help_text": "subdomain"
}
```

✔ an example of a **correct** implementation:

```json
{
  "label": "Subdomain",
  "help_text": "Where you (and your users) can access your forms, e.g., https://<SUBDOMAIN>.typeform.com"
}
```

---

<a name="D012"></a><a name="D00012"></a>

## D012 - Static Sample Is Required

When a user sets up a trigger or action (create or search), they need sample data to be returned in order to have
fields available to map in the subsequent steps. If testing the trigger returns no
live results, we use static sample data as a fallback.

It's very important that the structure of an object from the actual trigger/action and in
the sample data are identical. Otherwise, users could map fields that don't exist
in the live results, which results in a broken Zap.

See [Sample Data](./faq#output) for more details on this.

---

<a name="D013"></a><a name="D00013"></a>

## D013 - Connects to a Non-Existing Search

[Search-Powered Fields](https://platform.zapier.com/cli_docs/docs#search-powered-fields)
prompt users to set up a search step to populate the value of the field. It won't
work if the search key you specify doesn't exist.

---

<a name="D014"></a><a name="D00014"></a>

## D014 - Has a Search Connector, but No Dynamic Dropdown

By design, to get the "Add a Search Step" button, an action needs both a search
connector and a (valid) dynamic dropdown. If you can't provide a valid dropdown, you
can instead point to a dummy trigger that always returns an empty array.

✘ an example of an **incorrect** setup:

```json
{
  "key": "update_thing",
  "search": "thing.id"
}
```

✔ an example of a **correct** implementation:

```json
{
  "key": "update_thing",
  "search": "thing.id",
  "dynamic": "things.id.name"
}
```

---

<a name="D015"></a><a name="D00015"></a>

## D015 - Search-Or-Create Connects to a Non-Existing Action/Search

The search or create key you specify in `searchOrCreates` must reference to an
existing search or action. Otherwise, it won't work.

---

<a name="D016"></a><a name="D00016"></a>

## D016 - Consists Only a Static Webhook

Static Webhooks, while convenient to build, leave a lot to be desired from our side.
For this reason, Zapier doesn't allow integration that are a single static hook. To
fix this, add more triggers/searches/actions.

---

<a name="D017"></a><a name="D00017"></a>

## D017 - Static Hook Is Discouraged

When a REST Hook trigger is missing a Subscribe or Unsubscribe endpoint, it is
presented to users as a Static Webhook. As static webhooks are complicated to set up
correctly, we no longer support adding new static webhook triggers to a public
integration. Please set up Subscribe and Unsubscribe requests for this trigger,
or use a Polling trigger type instead.

---

<a name="D018"></a><a name="D00018"></a>

## D018 - Titlecased Label

In order to have a consistent style across trigger/action/search labels, they're
required to be presented in title case. If you fail this check, a passing version of
your label will be shown.

✘ an example of an **incorrect** implementation:

```
new contact
```

✔ an example of a **correct** implementation:

```
New Contact
```

---

<a name="D021"></a><a name="D00021"></a>

## D021 - Trigger Description Requirements

Trigger descriptions must start with `Triggers when ` and end with a `.`.


✘ examples of an **incorrect** implementation:

```
Whenever there's a new contact, this goes?
```

```
Triggers whenever there's a new contact.
```

✔ examples of a **correct** implementation:

```
Triggers when there's a new contact.
```

---

<a name="D022"></a><a name="D00022"></a>

## D022 - Creates Should Try to Have Static Input Fields

When making Zap Templates, it's helpful to have input fields that are common
for all users. Without any, it's hard to create templates. If possible,
add some static input fields that all users will be able to use.

---

<a name="D023"></a><a name="D00023"></a>

## D023 - ISO-8601 Date/Time Format in Static Sample

To ensure Zapier can correctly parse dates and times, you should always use ISO-8601
format to represent dates or times. Timezone info should also be present if it
contains time.

This check is similiar to `T003`. This check validates the static samples in
your integration definition, while `T003` validates the live results
in the Zap History.

✘ examples of an **incorrect** implementation:

```
01 Aug 2019
```

```
01 Aug 2019 06:50:30
```

```
2019-08-01T06:50:30
```

✔ examples of a **correct** implementation:

```
2019-08-01
```

```
2019-08-01T06:50:30-0500
```

```
2019-09-15T09:59:59Z
```

---

<a name="D024"></a><a name="D00024"></a>

## D024 - Static Sample Respects Output Field Definition

If you define output fields for a trigger/action/search, they should be consistent
with the static sample data. The specific checks are:

* "required" fields must be in the sample
* field values in the sample match their field type

✘ an example of an **incorrect** implementation:

```
static sample: {"id": "1"}
output fields: [
    {"key":  "id", "type": "integer"},
    {"key": "email", "type": "string", "required": true}
]
```

✔ an example of a **correct** implementation:

```
static sample: {"id": 1, "email": "john@example.com"}
output fields: [
    {"key":  "id", "type": "integer"},
    {"key": "email", "type": "string", "required": true}
]
```

---

<a name="L001"></a><a name="L00001"></a>

## L001 - Version Is Deprecated

You can't promote a deprecated version.

---

<a name="L002"></a><a name="L00002"></a>

## L002 - Version Was Already Submitted

You can't submit a version you've already submitted. If your integration was pushed
back and you want to resubmit for another review, you should make changes on a
**new** version and submit that.

---

<a name="L003"></a><a name="L00003"></a>

## L003 - Version Is Already Production

This could happen if you're promoting a version that is already production.

---

<a name="L004"></a><a name="L00004"></a>

## L004 - Changes From Partners Are Blocked

This is necessary when Zapier team pushes changes to a partner-owned integration.
Partners would have to coordinate with Zapier team via partners@zapier.com
to lift the restriction for subsequent changes from them.

---

<a name="M001"></a><a name="M00001"></a>

## M001 - App Category Is Required

To correctly categorize your integration on Zapier, please choose the category that
fits best your app. You can specify a category for your integration in the
Integration Settings page.

---

<a name="M002"></a><a name="M00002"></a>

## M002 - Description Is Invalid

Your app's description is a place to talk about your app, not ours! Even if we
really like your service, you're not allowed to say "Zapier" in your app's
description.

Additionally, it's discouraged that you talk about how this integration will `sync`
anything, as the space is supposed to be about your service itself instead of the
Zapier integration in particular.

Lastly, this section should be short and sweet. A brief description (roughly
tweet-sized) is best. Specifically, we're looking for 1 - 3 sentences or at least
40 characters.

✘ an example of an **incorrect** setup:

```
Google Translate enables Zapier users to translate text from one language into
another.
```

✔ an example of a **correct** implementation:

```
Google Translate is a service that translates text from one language into another.
```

---

<a name="M003"></a><a name="M00003"></a>

## M003 - Role Must Be Employee or Contractor

For your integration to go public, you must be employed or hired by the company who
makes the app used in the integration. Go to the Integration Settings page
to select your role.

---

<a name="M004"></a><a name="M00004"></a>

## M004 - Invalid Logo

Your app's logo will be used all over the site in square containers and in various
sizes. To ensure it looks good at all sizes, the logo image must be:

* a square PNG image
* at least 256px by 256px in size
* in RGBA mode so it can have a transparent background

To resize an image or convert an image to PNG, you can use this
[tool](http://www.picresize.com/).

---

<a name="M005"></a><a name="M00005"></a>

## M005 - Admin Team Member Email Domain Matches App Domain

To ensure that this integration is being submitted by the app owner we require that
one of the Admin team members listed on the project have an email address with the same
domain as your app's homepage URL (which must also be present). You can add the homepage
URL at `https://zapier.com/app/developer/app/APP_ID/version/APP_VERSION/settings`. Collaborator team members with the same domain as the homepage do not meet this requirement.

---

<a name="M006"></a><a name="M00006"></a>

## M006 - Homepage URL Must Be Present

Each app must have a homepage URL. You can add the homepage
URL at `https://zapier.com/app/developer/app/APP_ID/version/APP_VERSION/settings`.

---

<a name="M007"></a><a name="M00007"></a>

## M007 - Public Integration Already Exists

We only allow one public integration in our app directory for a given app. If a
public integration with the same title already exists, we probably won't approve
your submission to go public. If you're the owner of the existing public
integration, you may want to create a version and promote that instead of submitting
a new integration.

---

<a name="S001"></a><a name="S00001"></a>

## S001 - 3 Users with a live Zap

To verify user demand, there should be at least 3 users who have a live Zap using
this integration. "Live" means the Zaps are switched on with at least one successful
[Zap run in recent history](https://zapier.com/help/manage/history/view-and-manage-your-zap-history).

You can [invite others to test your integration](https://platform.zapier.com/manage/share-integration)
before publication.

---

<a name="S002"></a><a name="S00002"></a>

## S002 - One Live Zap for Each Trigger/Search/Action

To ensure any show-stopping bugs are worked out, every visible trigger/search/action
of your integration should have a live Zap that demonstrates it works. "Live" means
the Zaps are switched on with at least one successful
[Zap run in recent history](https://zapier.com/help/manage/history/view-and-manage-your-zap-history).

You can create a [new Zapier account](https://zapier.com/help/account/billing-pricing/get-started-with-your-free-zapier-trial)
and [invite it to your integration](https://platform.zapier.com/manage/share-integration)
if you need extra Zaps.

You can also [contact us](https://developer.zapier.com/contact) if you need a trial extension.

---

<a name="S003"></a><a name="S00003"></a>

## S003 - Live Version Count Limit

You can't have more than 5 previous or current production versions with live Zaps. To continue,
migrate users on older versions to a newer version.

---

<a name="T001"></a><a name="T00001"></a>

## T001 - One Successful Zap Run for Each Trigger/Search/Action

There must be at least one successful Zap run for each visible trigger/action/search
in your app.

To ensure you have run a live test of every visible trigger/action/search, create a
Zap for each one, turn it on, and trigger a Zap run while it's on.

This check is performed using the [Zap History](https://zapier.com/app/history) for
accounts belonging to the integration admins, so build your test Zaps in these
accounts.

Learn more about the Zap History [here](https://zapier.com/help/manage/history/view-and-manage-your-zap-history).

---

<a name="T002"></a><a name="T00002"></a>

## T002 - Missing "ID" Field in Live Polling Results

For polling triggers, the deduper uses the `id` field to decide if it's seen an
object before. It can be any sort of string, but it's important that it's unique.
If your object is returned with a differently named `id` field (such as
`contact_id`), write code to rename it.

This check is similiar to `D010`. This check validates the live
polling results in the [Zap History](https://zapier.com/app/history), while `D010`
validates the static samples in your integration definition.

This check is performed using the [Zap History](https://zapier.com/app/history) for
accounts belonging to the integration admins, so build your test Zaps in these
accounts.

✘ an example of an **incorrect** implementation:

```json
{
  "contact_id": 4,
  "contact_name": "David"
}
```

✔ an example of a **correct** implementation:

```json
{
  "id": 4,
  "contact_name": "David"
}
```

---

<a name="T003"></a><a name="T00003"></a>

## T003 - ISO-8601 Date/Time Format in Zap History

To ensure Zapier can correctly parse dates and times, you should always use ISO-8601
format to represent dates or times. Timezone info should also be present if it
contains time.

This check is similiar to `D023`. This check validates the data in the
[Zap History](https://zapier.com/app/history), while `D023` validates
the static samples in your integration definition.

This check is performed using the [Zap History](https://zapier.com/app/history) for
accounts belonging to the integration admins, so build your test Zaps in these
accounts.

✘ examples of an **incorrect** implementation:

```
01 Aug 2019
```

```
01 Aug 2019 06:50:30
```

```
2019-08-01T06:50:30
```

✔ examples of a **correct** implementation:

```
2019-08-01
```

```
2019-08-01T06:50:30-0500
```

```
2019-09-15T09:59:59Z
```

---

<a name="T004"></a><a name="T00004"></a>

## T004 - Static Sample Contains a Subset of Keys from Live Result

Static samples provide Zapier users and partners a way to preview and map fields
for a trigger or action without actually making a request to your API. It's
important that static samples reflect the real results from these calls as seen
in the Zap History. Errors occur when a Zap uses a field from static sample that
is not provided once the Zap is running.

This check requires the static sample you define for each trigger/action/search to
contain a subset of the keys in the latest run in the [Zap History](https://zapier.com/app/history).

This check is performed using the [Zap History](https://zapier.com/app/history)
for accounts belonging to the integration admins, so build your test Zaps in
these accounts.

✘ an example of an **incorrect** implementation:

```
static: {"id": 1, "email": "john@example.com"}
live: {"id": 2, "name": "Alice"}
```

✔ an example of a **correct** implementation:

```
static: {"id": 1, "name": "John"}
live: {"id": 2, "name": "Alice", "email": "alice@example.com"}
```

See [Sample Data](./faq#output) for more details on this.

---

<a name="T005"></a><a name="T00005"></a>

## T005 - Live Trigger Result Respects Output Field Definition

This check takes the latest run from the [Zap History](https://zapier.com/app/history)
and verifies whether the trigger result conforms to the output fields
for the trigger in your integration (if defined). The specific checks are:

* "required" fields must be in the trigger result
* field values in the trigger result match their field type

This check is performed using the [Zap History](https://zapier.com/app/history)
for accounts belonging to the integration admins, so build your test
Zaps in these accounts.

✘ an example of an **incorrect** implementation:

```
live result: {"id": "1"}
output fields: [
    {"key":  "id", "type": "integer"},
    {"key": "email", "type": "string", "required": true}
]
```

✔ an example of a **correct** implementation:

```
live result: {"id": 1, "email": "john@example.com"}
output fields: [
    {"key":  "id", "type": "integer"},
    {"key": "email", "type": "string", "required": true}
]
```

See [Sample Data](./faq#output) for more details on this.

---

<a name="T006"></a><a name="T00006"></a>

## T006 - Polling Sample Contains a Subset of Keys from Live Result

For REST Hook triggers, we require you to provide a Perform List URL
(check `D006`) so that users can retrieve a real data sample in the Zap
editor. This is called a polling sample, and is created when you test
the trigger in the Zap editor before turning it on.

Errors occur when a Zap uses a field from the polling sample that is not
provided by the hook payload sent once the Zap is running.

To ensure this doesn't happen, this check compares the latest item in the
[Zap History](https://zapier.com/app/history) with the selected polling sample in
the corresponding Zap. For it to pass:

- There must be a Zap that is using the trigger.
- The Zap must have at least one Zap run (the most recent run will be used).
- The trigger must have been tested in the Zap editor via the Perform List method
  to retrieve a polling sample.
- The polling sample should have the same data keys, or a subset of keys, compared
  to those available in the Zap run data.

This check is performed using the [Zap History](https://zapier.com/app/history)
for accounts belonging to the integration admins, so build your test Zaps
in these accounts.

✘ an example of an **incorrect** implementation:

```
polling sample: {"id": 1, "email": "john@example.com"}
live: {"id": 2, "name": "Alice"}
```

✔ an example of a **correct** implementation:

```
polling sample: {"id": 1, "name": "John"}
live: {"id": 2, "name": "Alice", "email": "alice@example.com"}
```
See [Sample Data](./faq#output) for more details on this.

---

<a name="U001"></a><a name="U00001"></a>

## U001 - Developer Terms of Service

You must agree to the latest Developer Terms of Service in order to proceed. Go to
[Developer Home](https://zapier.com/app/developer) to agree.

---

<a name="Z001"></a><a name="Z00001"></a>

## Z001 - Polling Sample Respects Output Field Definition

For REST Hook triggers, we require you to provide a Perform List URL
(check `D006`) so that users can pull a live sample in the Zap editor.
This is called a polling sample.

This check takes the latest polling sample from a Zap with this trigger
and verifies that the sample conforms to the output fields for the
trigger in your integration (if defined). The specific checks are:

* "required" fields must be in the polling sample
* field values in the trigger result must match their field type

This check is performed using the Zaps in accounts belonging to the
integration admins, so build your test Zaps in these accounts.

✘ an example of an **incorrect** implementation:

```
polling sample: {"id": "1"}
output fields: [
    {"key":  "id", "type": "integer"},
    {"key": "email", "type": "string", "required": true}
]
```

✔ an example of a **correct** implementation:

```
polling sample: {"id": 1, "email": "john@example.com"}
output fields: [
    {"key":  "id", "type": "integer"},
    {"key": "email", "type": "string", "required": true}
]
```

{% endraw %}
