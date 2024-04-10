---
title: Update perform method for polling trigger
order: 11
layout: post-toc
redirect_from: /manage/making-changes#updating-a-polling-triggers-perform-method
---

# Update perform method for polling trigger

## Change scenario

It is generally safe to update a polling trigger's [perform method](https://github.com/zapier/zapier-platform/blob/main/packages/schema/docs/build/schema.md#basicpollingoperationschema) (Platform CLI) or [API Configuration](https://platform.zapier.com/build/polling-trigger) (Platform UI), as long as the changes maintain backward compatibility in the returned response data. This means that the output fields and output data structure should remain consistent with previous version’s.

## Impact to users

Updating a polling trigger's perform method or API Configuration might cause deduplication issues and cause old records to trigger a Zap if any of the following changes occur:

- The [primary key](https://platform.zapier.com/build/deduplication) (usually an `id` field) is changed or removed from the API response.
- The perform method's endpoint is modified, resulting in fundamental changes to the primary key value.

For example, if the API or endpoint previously returned dedupe IDs as integers -1,2,3,4 - and is now updated to return alphanumeric values - 1-abc, 2-bcd, 3-cde, 4-def - records that were previously processed will fire again since the new IDs aren't saved in the deduplication table that Zapier references during each poll.

## Best practices

- Ensure the primary key remains unchanged: If the API response changes the primary key, use [custom code](https://platform.zapier.com/build/deduplication#custom-primary-keys) to maintain consistency and prevent deduplication issues.
- Maintain reverse chronological order: the trigger should continue to return data in reverse chronological order to prevent unintended records triggering the Zap.
