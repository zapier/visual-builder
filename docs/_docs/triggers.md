---
title: Triggers
order: 4
layout: post
redirect_from: /docs/
---

## Triggers

![Zapier Trigger Visual Builder](https://cdn.zapier.com/storage/photos/2d499138890f7237dffe728fbe9340bc.png)

Every Zap starts with a trigger, powered by either a webhook subscription that watches for new data as it comes in or a polling `GET` API call to check for new data periodically.

Triggers are how your app's users can start automated workflows whenever they add or update something in your app. New emails, messages, blog posts, subscribers, form entries, commits, and much more are the initial data that underpin every Zap.

As triggers only watch for new data and typically need to send no or little data to the app, they're often quicker to setup than Zapier action steps. Zapier can watch for any new or updated item through your API—or optionally, you can include [input fields](https://zapier.github.io/visual-builder/docs/input-designer) for users to enter filters, tags, and other details to filter through new data and watch for the items they want.

> **Note**: Triggers are displayed in the order they are added to Zapier integrations, so be sure to add your app’s most important triggers first.

## How to Add a New Trigger to a Zapier Integration

### 1. Configure Trigger Settings

![Zapier trigger settings](https://cdn.zapier.com/storage/photos/260a97ab4957746a75987dcb21f8aa1d.png)

Start building your trigger by adding details about what this trigger does. You need to add both internal data to identify your trigger, and user facing text to describe the trigger to users.

Add each of the following to your trigger:

- **Key**: A unique identifier for this trigger to reference it inside Zapier. Does not need to be the same identifier as used in your API. Not shown to users.
- **Name**: A human friendly plain text name for this trigger, typically with a verb such as _New_ or _Updated_ followed by the name of the item this watches for in your app. Shown inside the Zap editor and on Zapier's app directory marketing pages.
- **Noun**: A single noun that describes what this trigger watches for, used by Zapier to auto-generate text in Zaps about your trigger.
- **Description**: A plain text sentence that describes what the trigger does and when it should be used. Shown inside the Zap editor and on Zapier's app directory marketing pages.
- **Visibility Options**: An option to select when this trigger will be shown. _Important_ is chosen by default, and will show this trigger inside Zap trigger steps by default. Choose _None_ if you want this trigger hidden by default, useful for rarely used triggers. Or, choose _Hidden_ if this trigger should not be shown to users.

Once the settings are added, click _Save and Continue_ to add the new trigger and save your settings. You can edit the settings any time later with the exception of the create or search option.

### 2. Build Trigger Input Form (optional)

![Zapier Trigger input form](https://cdn.zapier.com/storage/photos/724d126862b876b7deccb5b798b86997.png)

Most triggers need no user configuration. When something new is added to an app, the API pushes the details to Zapier to start the Zap, with no details needed. If your API supports filtering or requires specific details about the project, folder, or other location details for the data, you may need to add an input form where users can add the necessary details.

In the second tab of the visual builder's trigger settings, add input fields for each data item you need from users for the trigger. Check our [Input Designer Guide](https://zapier.github.io/visual-builder/docs/input-designer) for complete details on how to create an input form and each of the field types and options available.

Once your form is complete—or if you don't need to include an input form—click the _API Configuration_ settings tab to set how Zapier will get data from your app and test the trigger.

### 3. Enter API Configuration

![Zapier Polling Trigger Settings](https://cdn.zapier.com/storage/photos/af53c9298cb9baf32abb17eb9e51a0dc.png)



![Zapier Rest Hook Settings](https://cdn.zapier.com/storage/photos/de85ffb1cc01a16b4b0e753dd7c0745c.png)

![Test Zapier Trigger](https://cdn.zapier.com/storage/photos/120d65ddd8baed9d781c358b66078851.png)

![Zapier Trigger Test Results](https://cdn.zapier.com/storage/photos/a43315730778c1cf5251d1e80a465819.png)

![Zapier Define Output Fields](https://cdn.zapier.com/storage/photos/d9a84ecb06a3f8f9e40fb91ba1a63ea5.png)

## How to Reorder Triggers in a Zapier Integration

![Triggers in Zapier](https://cdn.zapier.com/storage/photos/316fc36427a242269ec9118a06f0347a.png)

When users select your app as the trigger step in a Zap, they'll see the triggers marked as _Important_ by default, with every other integration hidden under the _show less common options_ menu. Zapier displays triggers in the order they were added to your Zapier integration—so the first trigger you added and marked as important will show up at the top of the list.

There is no way to reorder triggers in Zapier visual builder at the moment. It's best to plan your integration before you add triggers, and add the triggers your users will likely use the most first so they'll show at the top of the list. Alternately, you could delete triggers and re-add them in the order you want, if needed.

![Trigger visibility](https://cdn.zapier.com/storage/photos/478830f781668c2f9c6131de63954f1c.png)

You can however change a trigger's importance and thus choose whether it's shown by default or not at any time. Open the trigger in Zapier visual builder, scroll to the bottom of the page to the _Visibility Options_ menu. Select _Important_ to have the trigger show by default, _None_ to have the trigger in the _show less common options_ menu, and _Hidden_ if you want to keep users from being able to use this trigger (often used if the trigger is only used to power dynamic fields).

## How to Remove Triggers From a Zapier Integration

![Delete Trigger from Zapier Integration](https://cdn.zapier.com/storage/photos/188948a918eb589684b1d04c17707a52.png)

If your app no longer supports a trigger, or you wish to fully rebuild one, you can remove it from Zapier anytime. To delete a trigger from an integration, open the Triggers tab in Zapier visual builder, click the gear icon beside the trigger you wish to remove, select _Delete_, and confirm you wish to remove the trigger.

You cannot restore deleted triggers, so make sure you select the correct triggers for deletion.

> **Note**: Only remove triggers from pre-release integrations, or from new versions that will later be rolled out to users. Never remove a trigger from a live, public integration version.