---
title: Change trigger from polling to REST Hook
order: 10
layout: post-toc
redirect_from: /manage/making-changes#trigger-type-changes-polling-vs-rest-hook
---

# Change trigger from polling to REST Hook

## Change scenario

Your app needs to change how it notifies Zapier of new records - changing the type of trigger - from Zapier polling an app endpoint for new items to instead a REST Hook subscription where the app notifies Zapier of new records; or vice versa.

## Impact to users

This is a breaking change. Edits to an existing trigger’s type will cause your users’ Zaps to stop working and they would need to create new Zaps with the new trigger type, and manually re-create their actions. Using the [Duplicate feature](https://help.zapier.com/hc/en-us/articles/15408145778829-Duplicate-your-Zap) would help, but each Zap would need to be mapped individually with the new trigger.

## Best practices

- Copy the trigger configuration into a new trigger and give it a new **key** (such as appending `_v2` on the end), change the type for this new trigger, and **hide** the previous trigger. This way existing Zaps continue to work with the previous (and now hidden) trigger definition, and new Zaps will use the new trigger definition.
- This is the recommended path forward whether using the Platform UI or the Platform CLI, with the only difference being using the _Visibility: Hidden_ toggle in the UI and setting the `hidden` key as `true` [in the CLI](https://github.com/zapier/zapier-platform/blob/main/packages/schema/docs/build/schema.md#basicdisplayschema).