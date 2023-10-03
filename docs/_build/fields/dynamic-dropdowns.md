---
title: Use dynamic dropdowns in Zapier Platform CLI
order: 7
layout: post-toc
redirect_from: 
    - /cli_tutorials/dynamic-dropdowns
    - /build/dynamic-dropdowns 
---

# Use dynamic dropdowns in Zapier Platform CLI

API endpoints sometimes require clients to specify a parent object in order to create or access the child resources. For instance, accessing the tasts in a project, or specifying a spreadsheet ID in order to retrieve its worksheets. Since people don’t speak in auto-incremented ID’s, it is necessary that Zapier offer a simple way to select that parent using human readable handles.

Zapier does that with a dropdown that is populated by making a live API call to fetch a list of parent objects. We call these special dropdowns “dynamic dropdowns.”

To define one you include the `dynamic` property on the inputFields object. The value for the property is a dot-separated string concatenation, but the format of the value depends on if the dynamic field is powered by a trigger or by a [resource](https://github.com/zapier/zapier-platform/blob/main/packages/cli/README.md#resources).

If the dynamic dropdown is powered by a trigger, then the value of the `dynamic` property would be `triggerkey.value.label` where:
- `triggerkey` is the key of the trigger that would power the dynamic dropdown. This is required.
- `value` is the value that would be made available in bundle.inputData and that which would actually be sent in the API request. This is also required.
- `label` is the human-friendly value to be shown to the users on the dropdown field in bold. This is optional. If this is not provided, the `value` specified would be shown as the human-friendly value.

If the dynamic dropdown is powered by a resource, the value of the `dynamic` property would be `resourcekeyMethod.value.label` where `resourcekey` is the key of the resource that powers the dynamic dropdown and `Method` is the resource method as specified in the resource code. The combination of the resource key and the method in the value is done with a camel case. For example, if you have a project resource with the key `project` and the method to get a list of the available projects is `list`, then the `dynamic` property value would be `projectList.value.label`.

## Before adding a dynamic dropdown

Before adding a dynamic dropdown, you should have:

- A trigger, create action or search action that has dynamic dropdown field added.
- A trigger or a resource that Zapier would use to make the API call that would get the values to populate the dynamic dropdown field. 

> **Note**: If a trigger is used, and the trigger is not to be made available to the end users, you can hide this trigger from the end users by setting `hidden:true` on the display object of the trigger definition.

## Add dynamic dropdowns

To add a dynamic dropdown in a CLI app:
1. Open the code of the trigger/action/search where the dynamic dropdown field would be used.
2. In the 'InputFields' array of the trigger/action/search definition, add a `dynamic` property to the object of the field that is to be the dynamic dropdown field. This property is what lets Zapier know that the field is a dynamic dropdown field.
3. Specify the value of the `dynamic` property. The format for this value would depend on if the dropdown is powered by a trigger or a resource.
4. Run the `zapier push` command to push this changes to the Zapier integration.

The dynamic dropdown would show up on the user's Zap as a dynamic dropdown menu:

![Example of dynamic dropdown appearing in the Zap editor](https://cdn.zappy.app/e02787cd50af43ab22dc48af457b5a33.png)

You can have multiple dynamic dropdown fields in a trigger, create action, or search action. Also, a dynamic dropdown can depend on the value chosen in another dynamic dropdown when making it's API call. This means you must make sure that the key of the first dynamic dropdown is the same as referenced in the trigger or resource powering the second.