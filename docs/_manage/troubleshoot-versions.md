---
title: Troubleshoot migrating users between versions
order: 11
layout: post-toc
redirect_from: /partners/common-migration-errors
---
<a id="deploy-errors"></a>

## Troubleshoot migrating users between versions

There are certain changes to an integration the platform considers breaking changes, meaning migrating users and their Zaps to the new version will break existing, live Zaps and cause them to be turned off. 

Zapier's platform runs basic automated checks to prevent situations that may break Zaps before migrating users. But the checks can't cover everything, so please be extra aware of possible breaking changes when updating your integrations. No checks exist for version promotions, as having existing incompatible versions in parallel is acceptable.

Here are some commonly encountered errors and breaking changes to watch out for, with suggested solutions:

> **Note:** You can also always choose to promote an incompatible version, not migrate users, and either follow our [deprecation process](https://platform.zapier.com/manage/versions-cli#deprecate-an-older-version-of-your-integration) or leave them on the old version.

### You cannot remove or update keys for existing triggers, actions, and searches

You will see a similar error to the one below from our automated checks:
`vX.X is missing the following keys: {<list of missing keys>}. Hide them instead of removing them.`

The triggers, actions, and searches are identified by their **key**, such as `new_contact` or `create_post`, so if you remove it, or change its **key**, this message appears.

There are two solutions:

- If you need to remove a trigger/action/search, change its visibility to **hidden** instead. Use the Visibility Options dropdown in the [UI](https://platform.zapier.com/build/trigger#1-configure-trigger-settings), or the `hidden` key in the [CLI](https://zapier.github.io/zapier-platform-schema/build/schema.html#basicdisplayschema).
- If you've renamed the **key** for a trigger/action/search, you'll need to switch it back to the previous **key**.

### You cannot change the authentication type

You will see a similar error to the one below from our automated checks:
`You cannot migrate users between auth types (from "X" to "Y").`

Changing an integration's authentication type (such as Basic Auth, API Key, or OAuth) to a different one is a pretty big change, because existing connected accounts will stop working for their Zaps if you migrate users. In this case, we suggest not migrating users and following the [deprecation process](https://platform.zapier.com/manage/versions-cli#deprecate-an-older-version-of-your-integration).

### You cannot add a required field without a previously matching required field (by key).

If you're adding a new **required** input field or making a previously optional input field now required, it's possible Zaps without a value for the newly required field exist and thus, may break. There is no automated check for this.

**If this is a field in a trigger, action, or search, there are two solutions:**

- Leave the field as "optional", and use custom code in your API call to set a value if users leave it blank in their Zaps.
- Copy the trigger/action/search and give it a new **key** (such as appending `_v2` to the end), add your required field to the **new** trigger/action/search, and **hide** the previous trigger/action/search. That way, existing Zaps will continue to work with the previous (and now hidden) trigger/action/search definition, and new Zaps will be forced to provide a value for the required field.

**If this is a field in your authentication:**

This is a pretty big change, because it means all of the accounts already setup won't work with the integration.

There are two solutions:

- Leave the field as "optional", and use custom code in your API call to set a value if left blank.
- [Contact us](https://developer.zapier.com/contact), and we'll try to find the best approach.

### You cannot change an existing trigger's type (Polling vs REST Hooks).

A change in an existing trigger's type will cause your user's Zaps to stop working. There is no automated check for this.

Here's a solution:

- Copy the trigger and give it a new **key** (such as appending `_v2` on the end), change the type for this new rrigger, and **hide** the previous trigger. This way existing Zaps continue to work with the previous (and now hidden) rrigger definition, and new Zaps will use the new trigger definition.
