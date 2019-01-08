---
title: Actions
order: 6
layout: post
redirect_from: /docs/
---

## Actions

![Zapier Action Visual Builder](https://cdn.zapier.com/storage/photos/f4fba922b339ce68376e38b751bc79f1.png)

All Zaps start with a trigger that watches for new or updated data. They get the ball rolling. Everything a Zap does with that data, though, is done by actions.

Zapier actions push or put new data into apps through API calls that pass data from user customized [input fields](https://zapier.github.io/visual-builder/docs/input-designer). 

Action steps in Zaps can create new items in an app or update existing items with a *create* action, or find existing items in an app with *search* actions (which can optionally be paired with create actions to add a new item if the search does not return a result). Every action additionally returns output fields detailing what was created—and that data can be used in subsequent steps to build detailed workflows.

Zapier does not allow action steps to delete or remove data, to prevent data loss. Action steps may only add or update data.

> **Note**: Actions are displayed in the order they are added to Zapier integrations, so be sure to add your app's most important actions first.

## How to Add a New Action to a Zapier Integration

![Zapier visual builder action settings](https://cdn.zapier.com/storage/photos/6774970e27535cea5db5f58bee6fa1b8.png)

To add a new action step to a Zapier integration, open the _Actions_ page in Zapier visual builder from the sidebar on the left, and select _Add Action_. Start by selecting your action type. New actions are _Create_ type by default, and will add new data to your app. If your action should lookup existing items instead, select _Search_—then jump to the [Search](#search) section below for details on setting up a search action.

Check our [Searches and Creates guide](https://zapier.github.io/visual-builder/docs/search-create) for more detail on the difference between create and search actions.

> **Note**: You cannot change an action type once you click _Save and Continue_ on a new action. If you need to change the action type, delete the action and recreate it.

Then add the core details to your action, including:

- **Key**: A unique identifier for this action, used to reference the action inside Zapier. Does not need to be the same identifier as used in your API. Not shown to users.
- **Name**: A human friendly plain text name for this action, typically with a verb such as _Add_ or _Create_ followed by the name of the item this action will create in your app. Shown inside the Zap editor and on Zapier's app directory marketing pages.
- **Noun**: A single noun that describes what this action creates, used by Zapier to auto-generate text in Zaps about your action.
- **Description**: A plain text sentence that describes what your action does to help users understand why they should use this action. Shown inside the Zap editor and on Zapier's app directory marketing pages.
- **Visibility Options**: An option to select when this action will be shown. _Important_ is chosen by default, and will show this action inside Zap action steps by default. Choose _None_ if you want this action hidden by default, useful for rarely used actions. Or, choose _Hidden_ if this action should not be shown to users, helpful if you build a create action solely to pair with a search action but do not want it used otherwise.

Once the action settings are added, click _Save and Continue_ to add the new action and save your settings. You can edit the settings any time later with the exception of the create or search option.

![Zapier input designer](https://cdn.zapier.com/storage/photos/31dfcf36c01b0ee0db946a6a46c3de8c.png)

Then, the _Input Designer_ will open to build the input form field for your action. All action steps _must_ include an input form for Zapier to gather the data needed to create or find items in your app. Add at least one input field to your action before switching to the final _API Configuration_ tab.

Before building your action's input form, list each data item your app needs to create a new item. For example, if building an action to send an email, fields for the email address, subject, and email body would be needed at a minimum. Your action will likely have several required fields, along with others that are optional such as for tags or other additional details.

Add action fields for each item your app needs to create or find this item in your app. Add the fields in the order they're listed in your app, if possible, to make the Zapier integration easier for your users to use.

> **Tip**: Check our detailed [Zapier input designer](https://zapier.github.io/visual-builder/docs/input-designer) guide for details on each option in the input designer, along with each field type you can add to your action's form.



<a id="search"></a>
## How to Add a Search Action

![Zapier Search action settings](https://cdn.zapier.com/storage/photos/04d630c5f8019930d0cad5098ac819b9.png)

Building a search action is much the same as building a create action, only with a couple extra steps. Select *Search* as your action type, then fill in the core action settings as normal.

At the bottom of the settings page, you'll see an option to pair your search with a create action. That lets your action also create an item if the search does not return any results.

If you wish to do so, first add a relevant create action to your Zap. If your action is looking for contacts, say, you would need a *Add New Contact* action to pair with the search, say. You can open your integration's _Actions_ page in a new tab and add a new create action if your integration does not have an appropriate one already.

Then, in your new search action's settings, check the _Pair an existing create action_ box, and select the relevant action from the _Create Action_ menu. Additionally, add a new label that Zapier will show on this step if users choose to have the action create new items as well.

The remainder of your action setup is much like building a Zapier trigger. You will need to add an [Input Form](https://zapier.github.io/visual-builder/docs/input-designer) to gather data for the search. Most search actions only include a single input field, sometimes along with a drop-down menu to select filter data.

Finally, in the API configuration, add your API endpoint where Zapier will by default pass the search query in a `GET` call, then test the request and define output fields as with other actions.

![Example Search action in Zapier](https://cdn.zapier.com/storage/photos/748b1c164b0a310126a1807a706295aa.gif)

When users use the search action in a Zap, Zapier will show your core search action settings that you set in the input designer by default. Then, if users check to create an item if nothing is found, Zapier will load the create action's input fields inside the search action so users can fill both out.

## How to Reorder Actions in a Zapier Integration

![Actions inside Zapier](https://cdn.zapier.com/storage/photos/8dc1f3517e530fd079b9f8107e5e993d.png)

Whenever a user selects your app's integration in a Zapier action step, they'll see every create and search action in your integration. Zapier shows create actions that are marked as _Important_ first, followed by search actions marked as _Important_. If users click the _show less common options_ link, they'll then see the remaining actions that weren't marked as important, if any.

Actions are listed under Create and Search headers in the order they were added to your Zapier integration. You can see their original order in the sidebar of Zapier visual builder, or under the _Actions_ page. At the moment, you cannot rearrange actions in an existing Zapier integration with visual builder. Instead, if you need to reorder actions, you would need to remove and re-add actions in the order you want.

You can, however, change actions' visibility at any time. Edit the action, then in the last option on the _Settings_ page, choose _Important_ to have the action show by default, _None_ to hide it behind the _show less common options_ toggle, or _Hidden_ to make this action not usable inside Zapier.

## How to Remove an Existing Action

![Remove Zapier action](https://cdn.zapier.com/storage/photos/8e220c4270159ca43b7c1e02036f4a04.png)

You can remove an action at any time from Zapier visual builder's _Actions_ page. Click _Actions_ in the left sidebar, then click the gear beside any action you wish to remove. Select _Delete_, then confirm to remove the action fully.

If you remove an action from a live Zapier integration, this will break existing Zaps. As such, before removing an action, always [create a new major version](https://zapier.github.io/visual-builder/docs/versions) of your integration, remove the action from the new version, then migrate users to the new version as when adding any other breaking changes to an integration.