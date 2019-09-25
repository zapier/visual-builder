---
title: Integration Checks Reference
order: 22
layout: post-toc
redirect_from: /docs/
---

# Integration Checks Reference

In accordance with our [app development guide](https://platform.zapier.com/partners/planning-guide), we run your app through a set of automated checks to ensure it's giving our users the best possible experience. To help better address a check in communication, each check is given a unique ID, consisting of a capital letter and three digits, such as `D001`.

You don't need to know the implication of the initial capitial letter. But if you're curious, they are:

Area | Description
--- | ---
[**D**]efinition | Definition of the integration, including auth and trigger/search/action configurations. Some of these checks could block you from saving/pushing if the violation results in a broken trigger/search/action.
[**M**]arketing | Public-facing information, such as the app title, description, and logo. The intent of these rules is to give Zapier users a consistent style among texts and images across all public integrations. They're more likely to block you from going public.
Connected [**A**]ccounts | Connected accounts that are linked to your integration. We verify these to ensure the authentication is working.
[**S**]tats | Usage stats, such as the number of users your integration has. These are more likely to block you from going public.
[**U**]ser | Things in the developer's (your) account, such as Terms of Service acceptance.
[**L**]ifecycle | The lifecyle state of your integration or its versions, such as the visibility (private, pending, or public) and the version state (deprecated, non-production, or production).

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
trigger/search/action and the help text for any fields that might have bad links.

---

<a name="D009"></a><a name="D00009"></a>

## D009 - Requires at Least One Search Field

When making a search step, it's important to have a field to search on! Common
examples for searching for a user are by name, email, and username.

---

<a name="D010"></a><a name="D00010"></a>

## D010 - Missing "ID" Field in Sample Data

For polling triggers, the deduper uses the `id` field to decide if it's seen an
object before. It can be any sort of string, but it's important that it's unique.
If your object is returned with a differently named `id` field (such as
`contact_id`), write code to rename it. Hooks are not deduped, so they're not
required to have an `id`.

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

## D012 - Sample Data Is Required

When a user sets up a trigger, they need sample data to be returned in order to have
fields available to map in the subsequent steps. If testing the trigger returns no
live results, we use sample data as a fallback.

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

## D015 - Search-Or-Create Connects to a Non-Existing Search/Action

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

As static webhooks are a little more complicated to set up correctly, we discourage
their use. We no longer support adding new static webhook triggers to a public
integration, please use an alternative trigger type, such as REST Hook or Polling.

---

<a name="D018"></a><a name="D00018"></a>

## D018 - Titlecased Label

In order to have a consistent style across trigger/search/action labels, they're
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

<a name="L001"></a><a name="L00001"></a>

## L001 - Version Is Deprecated

---

<a name="L002"></a><a name="L00002"></a>

## L002 - Integration Is Pending

---

<a name="L003"></a><a name="L00003"></a>

## L003 - Version Is Already Production

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
tweet-sized) is best.

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
sizes. To ensure it looks good at all sizes, it must be a sqaure PNG image, at least
256px by 256px in size. To resize an image or convert an image to PNG, you can use
this [tool](http://www.picresize.com/).

---

<a name="S001"></a><a name="S00001"></a>

## S001 - 10 Live Zaps

To verify user demand, there should be at least 10 live Zaps using your integration.

---

<a name="S002"></a><a name="S00002"></a>

## S002 - One Live Zap for Each Trigger/Search/Action

To ensure any show-stopping bugs are worked out, every trigger/search/action of your
integration should have a live Zap that demonstrates it works.

---

<a name="T001"></a><a name="T00001"></a>

## T001 - One Successful Task for Each Trigger/Search/Action

To ensure you have tested every visible trigger/search/action, there should be at
least one successful task in at least one of the app admin's task
histories for each visible trigger/search/action.

---

<a name="U001"></a><a name="U00001"></a>

## U001 - Developer Terms of Service

You must agree to the Developer Terms of Service in order to proceed. Go to
[Developer Home](https://zapier.com/app/developer) to agree.

{% endraw %}
