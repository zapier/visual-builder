---
title: Embed pre-fill Zaps with Partner API
order: 6
layout: post-toc
redirect_from:
---

# Embed pre-fill Zaps with Partner API

Prefills allow you to define the input fields on behalf of the user, thus simplying the experience of setting up their Zap.

## Prerequisites

- You will need to know the required input fields per trigger or action step. You can find the fields as defined in your Zapier integration.

## Create Zap with pre-filled fields

Use the `create_url` (available in a [Zap template object](https://platform.zapier.com/embed/partner-api)) in order to create the Zap. 

Next, add parameters to the `create_url` so that the user's Zap is prefilled with the provided custom values.

### Example with single app

You can prefill the name of a Trello card (field: `name`) in the second step of the Zap template:

> `https://api.zapier.com/v1/embed/trello/create/113?steps[1][params][name]=hello`

- `template=113`
- `steps[1][params][name]=hello`

Here's what it would look like in the editor:

![Zap Editor showing "hello" pre-filled into the name field of a new Zap titled Create Card in Trello](https://cdn.zappy.app/5db273249f668a1520e1632cf331a141.png)

You can prefill multiple values for the user. In this example `name` and `desc` are prefilled

> `https://api.zapier.com/v1/embed/trello/create/113?steps[1][params][name]=yoyoyo&steps[1][params][desc]=yeehaw`

- `template=113`
- `steps[1][params][name]=yoyoyo`
- `steps[1][params][desc]=yeehaw`

![Zap Editor showing "yoyoyo" pre-filled into the name field, and "yeehaw" pre-filled into the description field of a new Zap titled Create Card in Trello](https://cdn.zappy.app/35882f8b86dade9e41c13cdbd0baf03c.png)

You can provide a label for prefill dropdowns as we won't fetch all of the pages of choices until the user opens the dropdown:

> `https://api.zapier.com/v1/embed/trello/create/113?steps[1][params][board]=1234&steps[1][meta][parammap][board]=Test`

- `template=113`
- `steps[1][params][board]=1234`
- `steps[1][meta][parammap][board]=Test`

![Zap Editor showing "Test" pre-filled into the board field of a new Zap titled Create Card in Trello](https://cdn.zappy.app/fd9fd4872773018bfd15dfebea0795a4.png)

### Example with multiple apps

Similarly, you can prefill apps, events, and input field values in the Zap Editor with the following URL schema:

Base URL: `https://api.zapier.com/v1/embed/{your_app}/create` - you can find `{your_app}` by using the [Prefill Generator](https://platform.zapier.com/embed/prefill-zaps#using-the-pre-filled-zap-generator)

#### URL parameters (with example values)

- Trigger app (required): `steps[0][app]=MailchimpCLIAPI@latest` 
- Trigger event: `steps[0][action]=new_member`
- Trigger field prefills: `steps[0][params][list_id]=123`
- Action app: `steps[1][app]=GoogleAdsCLIAPI@latest`
- Action event: `steps[1][action]=add_to_customer_list_v2`
- Action field prefills: `steps[1][params][list_id]=234`

#### Requirements

- A trigger app is required. The `steps` index for a trigger is always `0`.
- Use `app_latest` values from the [`/apps` endpoint](https://platform.zapier.com/embed/partner-api#get-v1apps) of the Partner API to define an app. This is case-sensitive, so use exactly the value returned from the API.
- You can define 0 to many subsequent action steps. The `steps` index for actions will be `1` or greater. Please note, only users on a paid Zapier plan have access to multi-step Zaps.
- Events are defined by the `key` of the trigger, action, or search.
- Field prefills are defined by the `key` of the input field. 

#### Examples

Defining a trigger and action app
> `https://api.zapier.com/v1/embed/{your_app}/create?steps[0][app]=MailchimpCLIAPI@latest&steps[1][app]=GoogleAdsCLIAPI@latest`

Defining a trigger and trigger event with no action:
> `https://api.zapier.com/v1/embed/{your_app}/create?steps[0][app]=MailchimpCLIAPI@latest&steps[0][action]=new_member`

Defining a trigger and trigger event with a prefilled value for the "Audience" input field:
> `https://api.zapier.com/v1/embed/{your_app}/create?steps[0][app]=MailchimpCLIAPI@latest&steps[0][action]=new_member&steps[0][params][list_id]=123`

Defining a trigger, trigger event, action, and action event with prefilled values for "Audience" and "Customer List" input fields:
> `https://api.zapier.com/v1/embed/{your_app}/create?steps[0][app]=MailchimpCLIAPI@latest&steps[0][action]=new_member&steps[0][params][list_id]=123&steps[1][app]=GoogleAdsCLIAPI@latest&steps[1][action]=add_to_customer_list_v2&steps[1][params][customer_list_id]=234`

Defining a multi-step Zap with a trigger and two actions:
> `https://api.zapier.com/v1/embed/{your_app}/create?steps[0][app]=MailchimpCLIAPI@latest&steps[1][app]=GoogleAdsCLIAPI@latest&steps[2][app]=FacebookLeadAdsCLIAPI@latest`

## Use the pre-filled Zap generator

The UI-based generator in the Platform UI facilitates constructing pre-filled Zaps. 

**Pre-filled Zaps are simply URLs with field values added as parameters,** which you can use to direct users to the Zap editor with some input fields already filled. Place these URLs inside your product or within an embedded Zap editor to facilitate users creating and publishing Zaps.

Find the pre-filled Zap generator under the _Embed_ and _Pre-filled Zaps_ section of the Platform UI.

![Screenshot of pre-filled Zaps tab](https://cdn.zappy.app/2a4f9c6de6c525cbcdc1b513ec88c519.png)

### Create a pre-filled Zap using the generator

- Select an app and event for both the trigger and action to see the fields you can pre-fill. If no fields appear, the event has no input fields.

![Screenshot of generator trigger step setup](https://cdn.zappy.app/87b9c4951d55298780ff209e217bb750.png)

- Select the fields you want to pre-fill:
  - If you don’t want to pre-fill the field, leave the box unchecked. In the Zap, the field will be empty or set to a default value, if there is one.
  - If there's a static value for a field that applies to every user's Zap (like the title of an email), check the field and provide the value in the text field.
  - If the values are dynamic or you don’t know them yet, replace the placeholders represented in curly brackets (i.e {TRIGGER_LIST_ID}) in the generated URL from Step 2 before using it in your app. This could be something like an account or list ID field. The placeholder serves as a reminder to replace the value at runtime.
  - If the field is greyed out, it requires a complex field value and cannot be pre-filled.

![Screenshot of prefill input field options](https://cdn.zappy.app/9e845182506292214c866f3278861e8d.png)

_Note: fields denoting **(required)** are required for turning the Zap on, not required to be pre-filled._

- Test the Zap! Use the handy test button to make sure the resulting Zap is what you intended. You'll need to connect app accounts on both steps to see the pre-filled fields.
- Copy the code and embed it inside your app to make setting up a Zap easier and faster for users.

The generator only supports creating 2-step Zaps, but you can construct multi-step Zaps by building upon the generated URL and adding `steps` parameters with increased indeces.
 
You also cannot prefill an action field with data returned from the trigger. In this case, use [pre-filled Zaps with Zap Templates](https://platform.zapier.com/embed/zap-editor).
