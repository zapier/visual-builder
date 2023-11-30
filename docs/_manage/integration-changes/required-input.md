---
title: Add new required input field
order: 6
layout: post-toc
redirect_from: /manage/making-changes#adding-new-required-fields-in-triggeractionsearch
---

# Add new required input field

## Change scenario

Your app’s API endpoint adds an additional field for filtering records (trigger/search) or an additional property for created records (action).

## Impact to users

Adding a new **required** input field or making a _previously_ optional input field now required, would break existing Zaps without a value for the field. There is no automated check for this when migrating so though it may seem possible, it will be a breaking change for migrated users.

## Best practices

Consider the following options:

- Add new input fields as optional. Use a combination of custom error handling to throw an error if the field is empty and help text to explain the field is required.
- Use [Code Mode](https://platform.zapier.com/build/code-mode) (Platform UI) or code in `Perform` (Platform CLI) to set a default value for the inputField if users have it blank in their existing Zaps. This would only be successful if a universal default could apply to all users (would not work for custom fields for example).
- Create a new trigger/action/search (T/A/S) with the required inputField; and hide the previous T/A/S. That way, existing Zaps will continue to work with the previous (and now hidden) trigger/action/search definition, and new Zaps will be forced to provide a value for the required field.