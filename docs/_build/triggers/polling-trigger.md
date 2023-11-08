---
title: Add a polling trigger
order: 2
layout: post-toc
redirect_from: 
---

# Add a polling trigger 

Set up your polling trigger in the Platform UI with the Settings, Input Designer and API Configuration tabs. 

## Prerequisites
- Understanding of the [concept of deduplication](https://platform.zapier.com/build/dedupe) and familiarity with how it is [explained to users](https://zapier.com/help/create/basics/data-deduplication-in-zaps)

## 1. Add the trigger settings

- Open the _Triggers_ tab in Zapier's Platform UI and select **Add Trigger**.
- On the Settings page, specify the following:

-- **Key**: A unique identifier for this trigger to be referenced inside Zapier. This is not shown to users. This cannot be edited once saved.
-- **Label**: A human-friendly name for this trigger, typically with an adjective such as _New or Updated_ followed by the name of the item that the trigger watches for inside  your app. The label is shown inside the Zap editor and on Zapier’s app directory marketing pages.
-- **Noun**: A single noun that describes what this trigger watches for, used by Zapier to auto-generate text in Zaps about your trigger.
-- **Description**: A plain text sentence that describes what the trigger does and when it should be used. Shown inside the Zap editor and on Zapier’s app directory marketing pages.
-- **Visibility in Editor**:  An option to select when this trigger will be shown. _Shown_ is chosen by default. Choose `Hidden` if this trigger should not be shown to users. `Hidden` is usually selected when the trigger is not ready to be used in the integration, or for polling triggers that power [dynamic dropdown](https://platform.zapier.com/build/add-fields#dynamic-dropdown) fields.
-- **Directions** is used for [static webhooks](https://platform.zapier.com/publish/integration-checks-reference#d017---static-hook-is-discouraged) only to describe how and where to copy-paste the static webhook URL for the trigger within your app. **Directions** will not show to users in other cases. Static webhooks are not permitted in public integrations. 

- Click on the **Save and continue** button.

## 2. Complete the Input Designer
 
On the Input Designer page, add user [input fields](https://platform.zapier.com/build/add-fields) needed by your API to watch for the triggering item.

Trigger input fields allow users to enter filters, tags, and other details to filter through new or updated data at the endpoint.

If no input data is needed for this trigger's endpoint, continue. 

## 3. Set up the API Configuration

Platform UI selects a _Polling_ trigger type by default.

![Zapier Polling Trigger Settings](https://cdn.zappy.app/0f08230cffa8a3a568d4847e35e42d0c.png)

Enter your API URL in the _API Endpoint_ field. If your API URL requires specific data in the URL path, enter the following text in the URL where your API expects that data, replacing `key` with the input field key containing the relevant input field you created in the previous step:

{% raw %}`{{bundle.inputData.key}}`{% endraw %}

Otherwise, Zapier will automatically include any input field data with the API call as URL parameters (for GET requests), or in the request body as JSON (for POST requests).

If your API requires any additional data to return the new or updated items in the [expected response type](https://platform.zapier.com/build/response-types) of an array sorted in reverse chronological order, add it using the _Show Options_ button to expose more detailed request configuration. Alternatively select _Switch to Code Mode_ to [further customize the API call](https://platform.zapier.com/build/code-mode) in JavaScript code. 

Only if you plan to use this trigger to power dynamic dropdown menus in other Zap steps (such as to find users, projects, folders, and other app data often used to create new items), and if your API call can paginate data, select _Support Paging_ (see [more details on dropdowns](https://platform.zapier.com/build/add-fields#dynamic-dropdown) below).

Once you've added your trigger settings, click _Save API Request & Continue_.

## 4. Test your API Request

Configure test data to [test the polling trigger](https://platform.zapier.com/build/test-triggers-actions).

## 5. Define your Output

Define sample data and output fields following [the guide](https://platform.zapier.com/build/sample-data).