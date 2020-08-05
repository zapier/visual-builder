---
title: Integration Checks Reference
order: 22
layout: post-toc
redirect_from: /docs/
---

# Integration Checks Reference

We run your integration through a set of automated checks to ensure it's working property and giving our users the best possible experience. To help better address a check in communication, each check is given a unique ID, consisting of a capital letter and three digits, such as `D001`.

You don't need to know the implication of the initial capitial letter. But if you're curious, they are:

Area | Description
--- | ---
<b><u>D</u></b>efinition | Definition of the integration, including auth and trigger/search/action configurations. Some of these checks could block you from saving/pushing if the violation results in a broken trigger/search/action.
<b><u>M</u></b>arketing | Public-facing information, such as the app title, description, and logo. The intent of these rules is to give Zapier users a consistent style among texts and images across all public integrations. They're more likely to block you from going public.
Connected <b><u>A</u></b>ccounts | Connected accounts that are linked to your integration. We verify these to ensure the authentication is working.
<b><u>S</u></b>tats | Usage stats, such as the number of users your integration has. These are more likely to block you from going public.
<b><u>T</u></b>ask History | Data in your task history, produced by live Zaps. These are more likely to block you from going public.
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

Connection Labels help customers understand and remember which account they
connected for a given Connected Account. These should be short and something easily
identifiable.

For both [Platform UI](https://platform.zapier.com/docs/auth#how-to-add-a-connection-label-to-authenticated-accounts)
and [CLI](https://platform.zapier.com/cli_docs/docs#authentication), the connection
label is a string. You can use any data returned by your test function.

For instance, if a successful run of the auth test returns the following json:

```json
{
  "name": "Malcom Reynolds",
  "email": "youcanttaketheskyfromme@serenity.com",
  "job": "Captain"
}
```

Your connection label could be the following:

```
"{{name}} - {{email}}"
```

The most important part of the label is that it uniquely identifies the auth it's
labeling.

✘ an example of an **incorrect** connection label:

```
"Slack"
```

✔ an example of a **correct** connection label:

```
"{{user}} @ {{team}}"
```

---

<a name="D004"></a><a name="D00004"></a>

## D004 - ID Fields Should Have Dynamic Dropdowns

We've found that instead of instructing users to paste an item `id` into Zapier,
providing them with a [dynamic dropdown](https://platform.zapier.com/cli_docs/docs#dynamic-dropdowns)
greatly increases the likelihood of the user setting up Zaps correctly. Users will
still be able to map custom fields, but this gets them started on the right foot.

Read more about implementing dynamic dropdowns below:

- Platform UI: https://platform.zapier.com/docs/input-designer#dropdown
- Platform CLI: https://platform.zapier.com/cli_docs/docs#dynamic-dropdowns

---

<a name="D005"></a><a name="D00005"></a>

## D005 - Dynamic Dropdown Connects to a Non-Existing Trigger

[Dynamic dropdowns](https://platform.zapier.com/cli_docs/docs#dynamic-dropdowns)
allow you to connect an input field to an existing trigger. The dropdown won't work
if the trigger key you specify doesn't exist.

---

<a name="D006"></a><a name="D00006"></a>

## D006 - REST Hook Trigger Needs a Polling URL

When users are setting up a hook-based (aka instant) Trigger, it's important to have
a polling fallback. For example, imagine a Zap that triggers on a new Slack message.
Without a polling URL, the test won't complete without the user sending an actual
message in a Slack channel, which is disruptive. Instead, the test fetches a (real)
recent message and uses it as the test result. After that, the polling URL is only
used for tests.

It's very important that the structure of an object from a webhook and from a poll
are identical. Typically, this means modifying a poll result so that it looks like a
hook. If a poll has fields that a hook doesn't, the user may map them to a later
step and when the zap is run for real, the value will be blank.

Let's walk through an example. Say we have a `New Contact` REST hook trigger. When a
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

Typically you could return the first object from the `results` array as part of a
poll (and hydrate the `friends`), but since the hook has no friend information, you
should always remove it. A good way to do this is a `processContact` function that
you map all results (of either type) through that reduces each object to the lowest
common denominator.

---

<a name="D007"></a><a name="D00007"></a>

## D007 - All URLs Should Be HTTPS

When handling customer data (which all Zapier functions do), it's strongly
encouraged that all communication take securely. Using SSL is a big part of that, so
ensure your URLs have HTTPS as their protocol.

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

This check is similiar to `T002`. But unlike `T002`, this one validates the static
samples in your integration definition instead of the live polling results in the
task history.

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

When a user sets up a trigger, they need sample data to be returned in order to have
fields available to map in the subsequent steps. If testing the trigger returns no
live results, we use static sample data as a fallback.

It's very important that the structure of an object from the actual trigger and in
the sample data are identical. Otherwise, users could map fields that don't exist
in the live results, which results in a broken Zap.

---

<a name="D013"></a><a name="D00013"></a>

## D013 - Connects to a Non-Existing Search

[Search-Powered Fiels](https://platform.zapier.com/cli_docs/docs#search-powered-fields)
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

<a name="D019"></a><a name="D00019"></a>

## D019 - Too Few Important Triggers/Searches/Actions

In order to highlight your most popular steps and give the user a clear
recommendation of what to use Zapier for, we encourage the use of "important" steps.
Important steps are shown first in the UI, while non-important steps are shown after
a "show more" click.

These can be adjusted in the settings for each individual step, either via a
checkbox (Platform UI) or via the `important` property (Platform CLI).

---

<a name="D020"></a><a name="D00020"></a>

## D020 - Too Many Important Triggers/Searches/Actions

In order to highlight your most popular steps and give the user a clear
recommendation of what to use Zapier for, we encourage a limited number of
"important" steps. These are shown first in the UI and aren't behind a "show more"
click.

These can be adjusted in the settings for each individual step, either via a
checkbox (Platform UI) or via the `important` property (Platform CLI).

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

Unlike `T003`, this check validates the fields in static samples instead of task
history.

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

## L002 - Integration Is Pending

This could happen if you're repeatedly submitting an integration that is already
pending for review.

---

<a name="L003"></a><a name="L00003"></a>

## L003 - Version Is Already Production

This could happen if you're promoting a version that is already production.

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
makes the app for the integration to go public. Go to Integration Settings page
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

## M005 - Developer Email Domain Matches App Domain

To ensure that this integration is being submitted by the app owner we require that
one of the developers listed on the project have an email address with the same
domain as your app's homepage URL (which must also be present). You can add the homepage
URL at `https://zapier.com/app/developer/app/APP_ID/version/APP_VERSION/settings`.

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
task in recent history.

---

<a name="S002"></a><a name="S00002"></a>

## S002 - One Live Zap for Each Trigger/Search/Action

To ensure any show-stopping bugs are worked out, every visible trigger/search/action
of your integration should have a live Zap that demonstrates it works.

---

<a name="S003"></a><a name="S00003"></a>

## S003 - Live Version Count Limit

You can't have more than 5 (former and current) production versions with users that
have active Zaps using it. To continue, you should migrate users over to a new
version so you can delete the unwanted versions.

---

<a name="T001"></a><a name="T00001"></a>

## T001 - One Successful Task for Each Trigger/Search/Action

To ensure you have run a live test of every visible trigger/action/search, you'll
need to turn a Zap on and trigger it live for each visible trigger/action/search, so
that there is at least one successful Task for each visible trigger/action/search in
one of the integration admin's [Task History](https://zapier.com/app/history).

Learn more about Tasks [here](https://zapier.com/help/manage/tasks).

---

<a name="T002"></a><a name="T00002"></a>

## T002 - Missing "ID" Field in Live Polling Results

For polling triggers, the deduper uses the `id` field to decide if it's seen an
object before. It can be any sort of string, but it's important that it's unique.
If your object is returned with a differently named `id` field (such as
`contact_id`), write code to rename it.

This check is similiar to `D010`. But unlike `D010`, this one validates the live
polling results in the task history instead of the static samples in your
integration definition.

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

## T003 - ISO-8601 Date/Time Format in Task History

To ensure Zapier can correctly parse dates and times, you should always use ISO-8601
format to represent dates or times. Timezone info should also be present if it
contains time.

Unlike `D023`, this check validates the data in task history instead of static
samples.

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

Static samples provide Zapier users and partners a way to preview and map the fields
without actually making a request to your API. For a better UX, it's important that
static samples truthfully reflect the live results pulled from your API, which users
can see in their Task History.

This check requires the static sample you define for each trigger/action/search to
contain a subset of the keys in the latest Task in your [Task History](https://zapier.com/app/history)
for that trigger/action/search.

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

---

<a name="T005"></a><a name="T00005"></a>

## T005 - Live Trigger Result Respects Output Field Definition

This check takes the latest task from Task History and verifies if the trigger
result conforms to the output fields if you define them for your integration. The
specific checks are:

* "required" fields must be in the trigger result
* field values in the trigger result match their field type

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

---

<a name="T006"></a><a name="T00006"></a>

## T006 - Polling Sample Contains a Subset of Keys from Live Result

For hook triggers, we require you to provide a Perform List URL so that users can
pull a live sample in the Zap editor. This is called a Polling Sample, and is created
when you test the trigger in a Zap before turning it on.

Errors occur when a Zap uses a field from the Polling Sample that ends up not being
provided by the actual hook payload once the Zap is running. To ensure this doesn't
happen, this check compares the latest item in your
[Task History](https://zapier.com/app/history) with the selected Polling Sample in
the corresponding Zap. For it to pass, the selected Polling Sample must contain a
subset of the keys returned in the latest live result in Task History.

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

---

<a name="U001"></a><a name="U00001"></a>

## U001 - Developer Terms of Service

You must agree to the Developer Terms of Service in order to proceed. Go to
[Developer Home](https://zapier.com/app/developer) to agree.

---

<a name="Z001"></a><a name="Z00001"></a>

## Z001 - Polling Sample Respects Output Field Definition

For hook triggers, we require you to provide a Perform List URL so that users can
pull a live sample in the Zap editor. This is called a Polling Sample.

This check takes the latest polling sample from one of the integration admins' Zaps
and verifies if the sample conforms to the output fields if you defined them for
your integration. The specific checks are:

* "required" fields must be in the polling sample
* field values in the trigger result match their field type

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
