---
title: Automated App Development Checks
order: 18
layout: post-toc
redirect_from: /docs/
---

# Automated App Development Checks

In accordance with our [app development guide](https://platform.zapier.com/partners/planning-guide), we run your app through a set of automated checks to ensure it's giving our users the best possible experience. Violations come in two flavors:

- **Errors** will block deployment of your app until they're fixed. These include missing data (that renders an app invalid), style concerns, or security issues
- **Warnings** won't block deployment, but are good things to consider. We've done our best to make these only show up when appropriate, but they may be safe to ignore if your app doesn't use the feature described.

When the checks are run, we'll give a brief blurb summarizing the issue (with an issue `id`) along with a link to this page. This will act as a full reference explaining each error and giving examples for each.

---

<a name="ZDE001"></a>

## ZDE001 - Invalid Markdown Link

A valid markdown link consists of a pair of square brackets with the link text paired with a pair of parens that have the link itself. See the [markdown cheatsheet](https://daringfireball.net/projects/markdown/syntax#link) for more info.

If you want to show a full link without actually linking to it, use backticks. This makes it clear to the user that they don't need to click the link, it's just used as an example. Any link used in plain text needs to either be a proper link or in backticks.

&#10008; examples of an **incorrect** implementation:

```text
See [Google(https://google.com)
```

```
See https://google.com
```

&#10004; examples of a **correct** implementation:

```text
See [Google](https://google.com)
```

```text
See `https://google.com`
```

If you see this error, you should look through both the description for the trigger/search/action and the help text for any fields that might have bad links.

---

<a name="ZDE002"></a>

## ZDE002 - Has Redundant Help Text

Help text is optional and meant to provide non-obvious information or links for the user. If the label and help text are too similar, they are considered redundant.

&#10008; an example of an **incorrect** implementation:

```json
{
  "label": "Subdomain",
  "help_text": "your subdomain"
}
```

&#10004; an example of a **correct** implementation:

```json
{
  "label": "Subdomain",
  "help_text": "Where you (and your users) can access your forms. eg: https://<SUBDOMAIN>.typeform.com"
}
```

---

<a name="ZDE003"></a>

## ZDE003 - OAuth URL Must Be HTTPS

When dealing with credentials, it's important to communicate using the `https` protocol to ensure sensitive information isn't leaked to malicious parties. More information can be found [here](https://developers.google.com/web/fundamentals/security/encrypt-in-transit/why-https).

&#10008; an example of an **incorrect** implementation:

```text
http://slack.com/oauth/authorize
```

&#10004; an example of a **correct** implementation:

```text
https://slack.com/oauth/authorize
```

---

<a name="ZDE004"></a>

## ZDE004 - Invalid Description

Your app's description is a place to talk about your app, not ours! The description should start with `App Name is a` and go on to talk about the purpose of your service. Even if we really like your service, per our [App Development guide](https://platform.zapier.com/partners/planning-guide#app-description-copy) you're not allowed to say `Zapier` in your app's description.

Additionally, it's discouraged that you talk about how this integration will `sync` anything, as the space is supposed to be about your service itself instead of the Zapier integration in particular.

Lastly, this section should be short and sweet. A brief description (roughly tweet-sized) is best.

&#10008; an example of an **incorrect** setup:

```text
Google Translate enables Zapier users to translate text from one language into another.
```

&#10004; an example of a **correct** implementation:

```text
Google Translate is a service that translates text from one language into another.
```

---

<a name="ZDE005"></a>

## ZDE005 - Needs a Titlecased Label

In order to have a consistent style across Trigger and Action labels, it is required they be presented in title case. If you fail this check, a passing version of your label will be shown.

&#10008; an example of an **incorrect** implementation:

```text
new contact
```

&#10004; an example of a **correct** implementation:

```text
New Contact
```

We use the `titlecase` library ([Github](https://github.com/ppannuto/python-titlecase)) to enforce this. If you're not sure how to titlecase something correctly, use [this repl](https://repl.it/@xavdid/titlecase-test) like so:

![](https://zappy.zapier.com/DFFBA05A-440B-44B1-8D19-90AE51FADCA1.gif)

Try it: [https://repl.it/@xavdid/titlecase-test](https://repl.it/@xavdid/titlecase-test)

---

<a name="ZDE006"></a>

## ZDE006 - Consists Only of a Single Static Webhook

[Static Webhooks](https://zapier.com/developer/documentation/v2/static-webhooks/), while convenient to build, leave a lot to be desired from our side. For this reason, Zapier doesn't allow apps that are a single static hook. To fix this, add more Triggers and Actions.

---

<a name="ZDE007"></a>

## ZDE007 - Hook Trigger Needs a Polling URL

When users are setting up a hook-based (aka instant) Trigger, it's important to have a polling fallback. For example, imagine a Zap that triggers on a new slack message. Without a polling url, the test won't complete without the user sending an actual message in a Slack channel, which is disruptive. Instead, the test fetches a (real) recent message and uses it as the test result. After that, the polling url is only used for tests.

It's very important that the structure of an object from a webhook and from a poll are identical. Typically, this means modifying a poll result so that it looks like a hook. If a poll has fields that a hook doesn't, the user may map them to a later step and when the zap is run for real, the value will be blank.

Let's walk through an example. Say we have a `New Contact` REST hook trigger. When a new contact is created, Zapier gets a webhook that looks like this:

```json
{
  "id": 1,
  "firstName": "Bruce",
  "lastName": "Wayne",
  "job": "Batman"
}
```

The accompanying polling url would look something like `https://site.com/contacts/list` and return:

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

Typically you could return the first object from the `results` array as part of a poll (and hydrate the `friends`), but since the hook has no friend information, you should always remove it. A good way to do this is a `processContact` function that you map all results (of either type) through that reduces each object to the lowest common denominator.

---

---

<a name="ZDE008"></a>

## ZDE008 - A Trigger Must Be Designated as a Test Call

To test stored credentials, a Trigger is chosen as the "Test Trigger". This can be an existing trigger or a hidden one used specifically for this purpose. The important factor is that it's a call that requires no configuration and will work for all users, regardless of product level or account type.

&#10008; an example of an **incorrect** implementation:

```text
https://slack.com/api/channels.info?channel_id=C12345
```

&#10004; an example of a **correct** implementation:

```text
https://slack.com/api/auth.test
```

### Resolution

For **v2** apps, you denote a test trigger. There's more information [here](https://zapier.com/developer/documentation/v2/test-triggers/).

For **CLI** apps, you add a test url or function to your authentication, details [here](https://github.com/zapier/zapier-platform-cli#authentication).

---

---

<a name="ZDE009"></a>

## ZDE009 - Is Missing "ID" Field in Sample Data

For polling Triggers, the deduper uses the `id` field to decide if it's seen an object before. It can be any sort of string, but it's important that it's unique. If your object is returned with a differently named `id` field (such as `contact_id`, use a `_post_poll` function (web builder) or `.map` (CLI) to rename it. Hooks are not deduped, so they're not required to have an `id`.

An example of such a function might be:

```javascript
var results = z.JSON.parse(bundle.request.data).results // array of contact objects

return results.map(function(contact) {
  contact.id = contact.contact_id
  delete contact.contact_id
  return contact
})
```

&#10008; an example of an **incorrect** implementation:

```json
{
  "contact_id": 4,
  "contact_name": "David"
}
```

&#10004; an example of a **correct** implementation:

```json
{
  "id": 4,
  "contact_name": "David"
}
```

---

<a name="ZDE010"></a>

## ZDE010 - Requires at Least One Search Field

When making a search step, it's important to have a field to search on! Common examples for searching for a user are by name, email, and username. See [here](https://zapier.com/developer/documentation/v2/reference/#search-fields) for more information.

---

<a name="ZDE011"></a>

## ZDE011 - Logo Image Is Not Square

Your app's logo is used all over the site in square containers. To ensure it's never warped or distorted, it must be square.

&#10008; an example of an **incorrect** implementation:

```text
300px by 400px
```

&#10004; an example of a **correct** implementation:

```text
300px by 300px
```

---

<a name="ZDE012"></a>

## ZDE012 - Logo Image Must Be Larger Than 256px

Your app's logo is used all over the site in various sizes. To ensure it looks good at all sizes, it must be at least 256px by 256px. To resize an image, you can use [this](http://www.picresize.com/) tool

&#10008; an example of an **incorrect** setup:

```text
192px by 192px
```

&#10004; an example of a **correct** implementation:

```text
300px by 300px
```

---

<a name="ZDE013"></a>

## ZDE013 - Logo Image Must Be a PNG

To ensure your logo looks good across devices and at all sizes, it must be a PNG file. To convert an existing image to PNG, you can use [this](http://www.picresize.com/) tool.

&#10008; an example of an **incorrect** setup:

```text
mylogo.jpg
```

&#10004; an example of a **correct** implementation:

```text
mylogo.png
```

---

<a name="ZDE014"></a>

## ZDE014 - Unable to Process Image

For whatever reason, your image was unable to be processed. Try a different file or contact [support](https://zapier.com/app/contact-us) for more information.

---

<a name="ZDE015"></a>

## ZDE015 - Connects to [Trigger|Search|Action] NAME, Which Doesn't Exist

Zapier provides a few constructs for connecting multiple steps in a Zap (such as [dynamic dropdowns](https://zapier.com/developer/documentation/v2/dynamic-dropdowns/) and [search connectors](https://zapier.com/developer/documentation/v2/reference/#search-connector)). If these are used, it's important that the target step exists and is of the correct type.

---

<a name="ZDE016"></a>

## ZDE016 - Asks for API Key in Action Instead of in Auth

Some apps incorrectly have `api_key` or similar as an an action field in an action instead of centrally used in auth. This is worse because action fields typically aren't treated with the same level of security as auth fields are (eg: scrubbed from logs) and aren't action specific. Additionally, the ability to test the validity of auth doesn't exist for action fields, so anything auth related should be put into an auth field instead.

---

<a name="ZDE017"></a>

## ZDE017 - Has a Search Connector, but no Dynamic Dropdown

By design, to get the `Add a Search Step` button, an action needs both a search connector and a (valid) dynamic dropdown. If you can't provide a valid dropdown, you can instead point to a dummy trigger that always returns an empty array.

&#10008; an example of an **incorrect** setup:

```json
{
  "key": "update_thing",
  "search": "thing.id"
}
```

&#10004; an example of a **correct** implementation:

```json
{
  "key": "update_thing",
  "search": "thing.id",
  "dynamic": "things.id.name"
}
```

---

<a name="ZDE018"></a>

## ZDE018 - Has been moved

See [ZDE004](https://zapier.com/developer/documentation/v2/app-checks-reference/#ZDE004) instead.

---

<a name="ZDE019"></a>

## ZDE019 - Important Polling Triggers Should Always Have Sample Data

When users are setting up a Trigger, they need sample data to be returned in order to have fields available to map the Action. If testing the trigger returns no live results, we use Sample Data as a fallback.

It's very important that the structure of an object from the actual trigger and in the sample data are identical. [Learn how to properly set up Trigger sample results](https://zapier.com/developer/documentation/v2/trigger-sample-results/).

---

<a name="ZDE020"></a>

## ZDE020 - Search Requires a URL

When making a search step, it's important to have a URL to send a search request too. This URL is needed to fetch a search request or search resource to present to the user.

---

<a name="ZDE021"></a>

## ZDE021 - URL for Triggers|Searches|Actions should be HTTPS

For privacy, consistency, and security purposes, we require all your authentication and app URLs to be on HTTPS, the 'S' at the end of HTTPS stands for 'Secure'. This means all communications between the browser and website are encrypted.

---

<a name="ZDE022"></a>

## ZDE022 - You must select a category for your App

So we can correctly categorize your App on Zapier, please choose the category that fits best.

You can specify a category for your app by clicking the "Edit Title, Image or Description" button on your App's Development/Build tab. You'll see the category option after you update the Intended audience dropdown to "Public".

---

<a name="ZDW001"></a>

## ZDW001 - Needs a Noun

We use templates to communicate with the user what sorts of objects they're dealing with. It helps when we're able to correctly identify them, so it's nice to provide a noun. That way, we can say `Select a name for your new Contact` instead of `Select a name for your new Object`.

&#10008; an example of an **incorrect** setup:

```text
{
    "label": "New Contact"
}
```

&#10004; an example of a **correct** implementation:

```text
{
    "label": "New Contact",
    "noun": "Contact"
}
```

---

<a name="ZDW002"></a>

## ZDW002 - Has Help Text With X Characters (Which Is over the Limit of Y)

Help text is meant to be a short blurb that gives the user clear instructions about configuring the step. If there's more detailed information you need to pass on, link to a help doc instead.

&#10008; an example of an **incorrect** implementation:

```text
{
    "label": "Name",
    "help_text": "A contact's name is that which is (usually) given to them by their parent(s). It can come in many forms, some of which are abbreviated. There's also the matter of the surname, which is not chosen directly by the parents."
}
```

&#10004; an example of a **correct** implementation:

```text
{
    "label": "Name",
    "help_text": "The contact's full name, separated by a space."
}
```

---

<a name="ZDW003"></a>

## ZDW003 - Consider Using Z.JSON.Parse() Instead of JSON.Parse()

In scripting, we provide a number of helpful methods on the globally available `z` object. Our version of `JSON.parse()` has error handling and logging included out of the box, so we recommend you use it. For more information, see the [scripting docs](https://zapier.com/developer/documentation/v2/scripting/#parsing-json-zjsonparse).

&#10008; an example of an **incorrect** implementation:

```javascript
var result = JSON.parse(bundle.response.content)
```

&#10004; an example of a **correct** implementation:

```javascript
var result = z.JSON.parse(bundle.response.content)
```

---

<a name="ZDW004"></a>

## ZDW004 - There Should Be No More Than X Important Triggers|Searches|Actions in an App

In order to highlight your most popular steps and give the user a clear recommendation of what to use Zapier for, we encourage a limited number of "important" steps. These are shown first in the UI and aren't behind a "show more" click.

These can be adjusted in the settings for each individual step, either via checkbox (V2 Platform) or via the `important` property (CLI)

---

<a name="ZDW005"></a>

## ZDW005 - Contains a REST Hook Trigger, but The "(Un)Subscribe URL" Is Missing

For convenience, there's a central `subscribe_url` for REST hooks. It's not required, but is helpful! See [these docs](https://zapier.com/developer/documentation/v2/rest-hooks/) for more information.

---

<a name="ZDW006"></a>

## ZDW006 - URLs Should Be HTTPS

When handling customer data (which all Zapier functions do), it's **strongly** encouraged that all communication take securely. Using SSL is a big part of that, so ensure your urls have `https` as their protocol. This goes for subscribe/unsubscribe urls, as well as all triggers and actions. Really any url you see.

If you need help setting up an SSL certificate for your API, we suggest [Let's Encrypt](https://letsencrypt.org/).

&#10008; an example of an **incorrect** setup:

```text
http://site.com/messages/subscribe
```

&#10004; an example of a **correct** implementation:

```text
https://site.com/messages/subscribe
```

---

<a name="ZDW007"></a>

## ZDW007 - Is Using a Static Webhook

As static webhooks are a little more complicated to set up correct, we discourage their use. We no longer support adding new static webhook triggers to a public app, please use an alternative trigger type.

---

<a name="ZDW008"></a>

## ZDW008 - "PARAM" Is Included in the Url but Not Marked as Required

URLs can have variables in them (such as {% raw %}`https://{{subdomain}}.typeform.com`{% endraw %}). If those variables are optional and not supplied by the user, the url will be invalid and the step will never work.

If you want add optional parameters to the url, do this by modifying the `bundle.request.params` object via scripting. For example, for a trigger with key `task`, define a method `task_pre_poll`. See the [documentation](/developer/documentation/v2/scripting/#key_pre_poll) and [examples](https://zapier.com/developer/documentation/v2/scripting/#trigger-pre-poll-examples) for more details.

---

<a name="ZDW009"></a>

## ZDW009 - Consider Using a Direct Link to API Key Location

It's often not obvious where a user can find their API key for a service. If you use a pasted API key as an authentication method, it's strongly encouraged that you link the user to the page (or relevant help doc) that has their key.

&#10008; an example of an **incorrect** implementation:

```text
API key is found on the "Integrations" page in settings
```

&#10004; an example of a **correct** implementation:

```text
Go to the [API Details](https://my.site.com/manage/api-details)
screen from your Website Dashboard to find your API Key.
```

---

<a name="ZDW010"></a>

## ZDW010 - Should Have a Connection Label Set

[Connection Labels](../appdevguide-auth/#connection-label) helps customers understand and remember which account they connected for a given Connected Account. These should be short and something easily identifiable.

For both [CLI](https://github.com/zapier/zapier-platform-cli#basic) and [Web Builder](https://zapier.com/developer/documentation/v2/app-dev-guide/#connection-label), the connection label is a string. You can use any data returned by your test function.

For instance, if a successful run of the auth test returns the following json:

```json
{
  "name": "Malcom Reynolds",
  "email": "youcanttaketheskyfromme@serenity.com",
  "job": "Captain"
}
```

Your auth label could be the following:

{% raw %}

```text
"{{name}} - {{email}}"
```

{% endraw %}

The most important part of the label is that it uniquely identifies the auth it's labeling.

&#10008; an example of an **incorrect** Connection Label:

```text
"Slack"
```

&#10004; an example of a **correct** Connection Label:

{% raw %}

```text
"{{user}} @ {{team}}"
```

{% endraw %}

Assuming the Test Trigger returns an object with a `user` and a `team` property.

To **fix** this, see examples at the following links:

- CLI: https://github.com/zapier/zapier-platform-cli#basic
- Web Builder: https://zapier.com/developer/documentation/v2/app-dev-guide/#connection-label

---

<a name="ZDW011"></a>

## ZDW011 - Search Should Have a Resource URL

[Resource URL](https://zapier.com/developer/documentation/v2/searches/#resource-url) is used to fetch the full details of a Search result or (in the case of a Search or Action when no results are found) Create result. This is helpful because most searches only return a subset of a result's fields. It also ensures that regardless of it having found or created, the same data is returned.

---

<a name="ZDW012"></a>

## ZDW012 - ID fields should have dynamic dropdowns

We've found that instead of instructing users to paste an item `id` into Zapier, providing them with a [dynamic dropdown](https://zapier.com/developer/documentation/v2/trigger-fields/#dynamic-dropdown) greatly increases the likelihood of the user setting up Zaps correctly. Users will still be able to map custom fields, but this gets them started on the right foot.

Read more about implementing dynamic dropdowns below:

- CLI: https://github.com/zapier/zapier-platform-cli#dynamic-dropdowns
- Web Builder: https://zapier.com/developer/documentation/v2/dynamic-dropdowns/

---

<a name="ZDW013"></a>

## ZDW013 - There Should Be At Least X Important Triggers|Searches|Actions in an App

In order to highlight your most popular steps and give the user a clear recommendation of what to use Zapier for, we encourage the use of "important" steps. Important steps are shown first in the UI, while non-important steps are shown after a "show more" click.

These can be adjusted in the settings for each individual step, either via checkbox (V2 Platform) or via the `important` property (CLI)

---

<a name="ZDE500"></a>

## ZDE500 - Upgrading the platform version on a public app is not allowed right now.

Please reach out to [partners@zapier.com](mailto:partners@zapier.com) to get your new version of your app deployed. Unfortuntely, partners are not able to deploy a new platform version public app at this time.

---

<a name="ZDE501"></a>

## ZDE501 - You cannot add this required field without a previously matching field

Adding a new required field within an existing trigger/action/search or authentication may break all existing Zaps. There are a few ways to handle this:

1. If the new required field is within a trigger/action/search, you can hide the old/existing trigger/action/search and create a new one with the required field added. All exisitng Zaps will continue to function with the older/hidden item, but new Zaps will use the new trigger/action/search with the required field.
2. Define the new field without using the ""required"" flag, and then use scripting for the trigger/action/search to specify a default value, before sending requests to your API endpoint.

---

<a name="ZDE502"></a>

## ZDE502 - You cannot change the auth type

Changing the auth type of your app will break all existing user's Zaps. Please visit this doc for the available options: https://zapier.com/developer/documentation/v2/migrating-your-zapier-integration/

---

<a name="ZDE503"></a>

## ZDE503 - Do not remove this trigger!

You cannot remove triggers that have live Zaps. You'll need to hide the trigger instead so it is no longer available to use in new Zaps.

To mark a trigger as hidden - add <code>hidden: true</code> parameter to the trigger's display definition.

```text
{
  key: 'my_tigger',
  noun: 'My Trigger'
  display: {
    label: 'My Old Trigger!',
    description: 'Triggers when it trigger',
    hidden: true
  }
}
```

---

<a name="ZDE504"></a>

## ZDE504 - You cannot change an existing trigger's data source

Changing the data source of a trigger breaks live Zaps. Instead, you'll want to hide this trigger and create a new trigger with the updated data source. All existing Zaps will continue to function as is, but new Zaps will use the new trigger with the updated data source.

---

<a name="ZDE505"></a>

## ZDE505 - Do not remove this action!

You cannot remove action that have live Zaps. You'll need to hide the action instead so it is no longer available to use in new Zaps.

---

<a name="ZDE506"></a>

## ZDE506 - Do not remove this search!

You cannot remove search that have live Zaps. You'll need to hide the search instead so it is no longer available to use in new Zaps.

---

<a name="ZDW500"></a>

## ZDW500 - The new (OAuth) does not match the old one.

The Client ID, Client Secret, Authorization URL, or Access Token URL has changed. Validate that the current version is correct.
