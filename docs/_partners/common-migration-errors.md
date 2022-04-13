---
title: Common Errors When Migrating Users
order: 11
layout: post-toc
redirect_from: /partners/
---
<a id="deploy-errors"></a>

## Common Errors When Migrating Users and Zaps Between Versions

There are certain changes to an integration the platform considers breaking changes, meaning migrating users and their Zaps to the new version will break existing, live Zaps and cause them to be turned off. 

Zapier's platform runs basic automated checks to prevent situations that may break Zaps before migrating users. But the checks can't cover everything, so please be extra aware of possible breaking changes when updating your integrations. No checks exist for version promotions, as having existing incompatible versions in parallel is acceptable.

Here are some commonly encountered errors and breaking changes to watch out for, with suggested solutions:

> **Note:** You can also always choose not to migrate users, and follow our [deprecation process](https://platform.zapier.com/cli_tutorials/versions#deprecate-an-older-version-of-your-integration).

### You cannot remove or update keys for existing Triggers, Actions, and Searches.

You will see a similar error to the one below from our automated checks:
`vX.X is missing the following keys: {<list of missing keys>}. Hide them instead of removing them.`

The Triggers, Actions, and Searches are identified by their **key**, so if you remove it, or change its **key**, this message appears.

There are two solutions:

- If you need to remove a Trigger/Action/Search, change its visibility to **hidden** instead.
- If you've renamed the **key** for a Trigger/Action/Search, you'll need to switch it back to the previous **key**.

### You cannot change the authentication type

You will see a similar error to the one below from our automated checks:
`You cannot migrate users between auth types (from "{}" to "{}").`

Changing an integration's authentication type (such as Basic Auth, API Key, or OAuth) to a different one is a pretty big change, because existing connected accounts will stop working for their Zaps if you migrate users. In this case, we suggest not migrating users and following the [deprecation process](https://platform.zapier.com/cli_tutorials/versions#deprecate-an-older-version-of-your-integration).

### You cannot add a required field without a previously matching required field (by key).

If you're adding a new **required** input field or making a previously optional input field now required, it's possible Zaps without a value for the newly required field exist and thus, may break. There is no automated check for this.

**If this is a field in a Trigger, Action, or Search, there are two solutions:**

- Leave the field as "optional", and use custom code in your API call to set a value if users leave it blank in their Zaps.
- Copy the Trigger/Action/Search and give it a new **key** (such as appending `_v2` to the end), add your required field to the **new** Trigger/Action/Search, and **hide** the previous Trigger/Action/Search. That way, existing Zaps will continue to work with the previous (and now hidden) Trigger/Action/Search definition, and new Zaps will be forced to provide a value for the required field.

**If this is a field in your authentication:**

This is a pretty big change, because it means all of the accounts already setup won't work with the integration.

There are two solutions:

- Leave the field as "optional", and use custom code in your API call to set a value if left blank.
- [contact us](mailto:partners@zapier.com), and we'll try to help find the best approach.

### You cannot change an existing Trigger's type (Polling vs REST Hooks).

A change in an existing trigger's type will cause your user's Zaps to stop working. There is no automated check for this.

Here's a solution:

- Copy the Trigger and give it a new **key** (such as appending `_v2` on the end), change the type for this new Trigger, and **hide** the previous Trigger. This way existing Zaps continue to work with the previous (and now hidden) Trigger definition, and new Zaps will use the new Trigger definition.
