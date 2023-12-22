---
title: Hydration/dehydration limits
order: 9
layout: post-toc
redirect_from: 
---

# Hydration/dehydration limits

[File dehydration](https://github.com/zapier/zapier-platform/blob/main/packages/cli/README.md#dehydration) is an extremely useful tool to remain within time and size constraints for Zapier triggers and actions. However, it does have its own limits.

## Constraint

There is a hard limit of 150MB on the size of dehydrated files. Depending on the complexity of the app, issues can also occur for files over ~100MB.

## Errors user will see if constraint is hit

- In their Zap history, the user will see an error like `Runtime exited with error: signal: killed`.

## Best practice

If your integration regularly loads large files, provide checks on file size and don't perform hydration for files that are larger than ~100MB. Include messaging for users letting them know of the limit on file size in the trigger/action description or in a `Copy` field above the file input field.