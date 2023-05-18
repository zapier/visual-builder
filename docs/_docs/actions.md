---
title: Actions
order: 12
layout: post-toc
redirect_from: /docs/
---

# Actions

![Zapier Action Visual Builder](https://cdn.zappy.app/8b5a6ba27686f0aa783c97949da0dee3.png)

All Zaps start with a trigger that watches for new or updated data. They get the ball rolling. Everything a Zap does with that data, though, is done by actions.

Zapier actions push or put new data into apps through API calls that pass data from user customized [input fields](https://platform.zapier.com/docs/input-designer). 

Action steps in Zaps can create new items in an app or update existing items with a *create* action, or find existing items in an app with *search* actions. Search actions can optionally be paired with create actions to add a new item if the search does not return a result.

Actions should also return output fields detailing what was created (or found), so that data can be used in subsequent steps to build detailed workflows.

Zapier strongly recommends against action steps that delete or remove data. To prevent data loss, action steps should only add or update data. If you are considering adding a delete action to your app, consider alternative actions for items such as deactivating, unsubscribing, or canceling, instead of deleting items completely.

# How to Add a New Action to a Zapier Integration

## 1. Configure Action Settings

![Zapier visual builder action settings](https://cdn.zappy.app/90061640a1c8e2f1f3172033c932bf57.png)

To add a new action step to a Zapier integration, open the _Actions_ page in Zapier visual builder from the sidebar on the left, and select _Add Action_. Start by selecting your action type. New actions are _Create_ type by default, and will add new data to your app. If your action should lookup existing items instead, select _Search_—then jump to the [Search](#search) section below for details on setting up a search action.

Check our [Searches and Creates guide](https://platform.zapier.com/docs/search-create) for more detail on the difference between create and search actions.

> **Note**: You cannot change an action type once you click _Save and Continue_ on a new action. If you need to change the action type, delete the action and recreate it.

Then add the core details to your action, including:

- **Key**: A unique identifier for this action, used to reference the action inside Zapier. Does not need to be the same identifier as used in your API. Not shown to users.
- **Name**: A human friendly plain text name for this action, typically with a verb such as _Add_ or _Create_ followed by the name of the item this action will create in your app. Shown inside the Zap editor and on Zapier's app directory marketing pages.
- **Noun**: A single noun that describes what this action creates, used by Zapier to auto-generate text in Zaps about your action.
- **Description**: A plain text sentence that describes what your action does to help users understand why they should use this action. Shown inside the Zap editor and on Zapier's app directory marketing pages.
- **Visibility Options**: An option to select when this action will be shown. _Shown_ is chosen by default. Choose _Hidden_ if this action should not be shown to users. This is helpful if you build a create action solely to pair with a search action but do not want it used on its own.

Once the action settings are added, click _Save and Continue_ to add the new action and save your settings. You can edit the settings any time later with the exception of the create or search option.

## 2. Build Action Input Form

![Zapier input designer](https://cdn.zappy.app/366cb5a08cef7e31cfc49758cf935478.png)

Then, the _Input Designer_ will open to build the input form field for your action. All action steps _must_ include an input form for Zapier to gather the data needed to create or find items in your app. Add at least one input field to your action before switching to the final _API Configuration_ tab.

Before building your action's input form, list each piece of data your app needs to create a new item. For example, if building an action to send an email, fields for the email address, subject, and email body would be needed. Your action will likely have several required fields, along with others that are optional, such as for tags or other details.

Add action fields for each piece of data your app needs to create or find this item in your app. Add the fields in the order they're listed in your app, if possible, to make the Zapier integration easier for your users to use.

> **Tip**: Check our detailed [Zapier input designer](https://platform.zapier.com/docs/input-designer) guide for details on each option in the input designer, along with each field type you can add to your action's form.

## 3. Enter API Configuration

![Zapier action API configuration](https://cdn.zappy.app/1b33f697838f7a4e160d4aa8ef3c6d93.png)

The last part of building a Zapier action is the most crucial: tell Zapier how to send the data to your API.

Zapier uses a `POST` call for create actions by default, sending a single item to your API endpoint. Zapier then expects a response with an object containing a single item, to be evaluated by [isPlainObject](https://lodash.com/docs#isPlainObject) and parsed into individual fields for use in subsequent Zap steps.

Zapier uses a `GET` call for search actions by default, and sends the data from the input form to your API endpoint. Zapier expects an array response with 0 or more items. If more than 1 item is returned, Zapier shows only the first match, and parses it into individual fields for use in subsequent Zap steps.

For most actions, select the correct API call if your app expects something other than the default, then paste the URL for your API call in the box under _API Endpoint_. Zapier will include each of your input form fields in the _Request Body_ automatically.

If your API call expects input data in the core URL, you can reference any input field's key with the following text, replacing `key` with your field key:

{% raw %}`{{bundle.inputData.key}}`{% endraw %}

The defaults on all other settings work for most basic API calls. If you need to configure more options, though, click _Show options_ to add URL Params, HTTP Headers, set your action to omit empty parameters, or customize the request body. Alternately, switch to [code mode](#code) to write custom JavaScript code for your action.

![Test Zapier API Call](https://cdn.zappy.app/800d5dc90285243ce473c0ca6d2087e0.png)

Once your API call is added, test it inside the Zapier visual builder with testing data. Authenticate with your app if you haven't already, then fill in each input field under the _Configure Test Data_ section with data that will work in your app. Click _Test Your Result_ to have Zapier run the action as it would inside a Zap—and see the results instantly.

If your app returns an error, be sure to check:

- Authentication: Did your app's authentication work correctly in the authentication step? You can only test an integration once you've connected an app account to Zapier.
- Test Data: Did your test data include the details your app expects, such as actual dates in date fields or complete email addresses in email address fields?
- Input Field Keys: Did you use the same field keys in your input field as your API expects? Double-check that in the Input Designer, and change if needed.
- API Call Customization: Does your API expect something different than the standard API call details Zapier sets by default? You may need to use custom coding if the options you need aren't available.

### Define Sample Data and Output Fields

![Zapier Define Output Fields](https://cdn.zappy.app/6c7d6b82dc27d49959d7390682405922.png)

Every time your action step runs, your API will return data to Zapier—ideally detailing the item that was added to your app or found via a search. Each item includes multiple details, including any attribute users would add via the Zap input form, along with other attributes or details that users may not care about as much.

Zapier lets you define the most important fields with friendly field names. Each field you define will show up first in the output field list after the Zap runs, and will be usable in subsequent Zap steps.

First, fill in sample data by clicking the _Use Response from Test Data_ button to import the fields your app sent to Zapier in the previous test, or add your own JSON-formatted fields. This data will also be used as a fallback in the Zap Editor if users skip the test step for the action, so that these fields can still be mapped into other steps. Make sure the data you include with those fields is non-private, non-identifiable testing data that can be shared publicly.

Then click _Generate Output Field Definitions_ and Zapier will list a table of the fields with the keys on the left and the field type on the right. Add a human-friendly name for each field in the center column, especially if users might expect a different name than the API provides, as in the GitHub example above where `body` becomes "Issue Details".  Then select the field type. Lastly, click _Save Output & Finish_ to complete your action.

<a id="code"></a>
## How to Use Custom Code in Zapier Actions

![Zapier visual builder code mode](https://cdn.zappy.app/c8887685a87f49f8bcc1dca815214334.png)

The default API settings form is the best option for most actions. If your action needs customized API calls, scripting to manipulate input field data, or other unique features, you can add custom JavaScript code for your API request.

To use custom code, click the _Switch to Code Mode_ button. Zapier will translate your default API call settings into JavaScript code the first time you switch to code mode for an easy way to start. If you switch back to form mode, though, Zapier will not transfer your code settings back to the form.

<a id="search"></a>
## How to Add a Search Action

![Zapier Search action settings](https://cdn.zappy.app/8aa8bbe51aae1dc502ca46ef0a00396b.png)

Building a search action is much the same as building a create action, only with a couple extra steps. Select *Search* as your action type, then fill in the core action settings as normal.

At the bottom of the settings page, you'll see an option to pair your search with a create action. That lets your action also create an item if the search does not return any results.

If you wish to do so, first add a relevant create action to your Zap. If your action is looking for contacts, say, you would need a *Add New Contact* action to pair with the search, say. You can open your integration's _Actions_ page in a new tab and add a new create action if your integration does not have an appropriate one already.

Then, in your new search action's settings, check the _Pair an existing create action_ box, and select the relevant action from the _Create Action_ menu. Additionally, add a new label that Zapier will show on this step if users choose to have the action create new items as well.

The remainder of your action setup is much like building a Zapier trigger. You will need to add an [Input Form](https://platform.zapier.com/docs/input-designer) to gather data for the search. Most search actions only include a single input field, sometimes along with a drop-down menu to select filter data.

Finally, in the API configuration, add your API endpoint where Zapier will by default pass the search query in a `GET` call, then test the request and define output fields as with other actions.

![Example Search action in Zapier](https://cdn.zappy.app/32ba8f867d02cf60cb6c344a0447b5a5.png)

When users use the search action in a Zap, Zapier will show your core search action settings that you set in the input designer by default. Then, if users check to create an item if nothing is found, Zapier will load the create action's input fields inside the search action so users can fill both out.

## Viewing Actions in a Zapier Integration

![Actions inside Zapier](https://cdn.zappy.app/5d3c2e8f9f6cf0f6daadd3ee97fa5e80.png)

Whenever a user selects your app's integration in a Zapier action step, they'll see every create and search action in your integration. Zapier shows create actions first, followed by search actions. Actions are listed in alphabetical order.

You can change actions' visibility at any time, if you don't want an action to be shown. Open the action in the Zapier visual builder, to the _Settings_ tab, and scroll to the bottom of the page to the _Visibility Options_ section. Select _Hidden_ if you want to keep users from being able to use this action (often used if an action is deprecated but should keep working in users' existing Zaps).

## How to Remove an Existing Action

![Remove Zapier action](https://cdn.zappy.app/809321da0cd78edef6f464eb1f803855.png)

You can remove an action from Zapier visual builder's _Actions_ page. Click _Actions_ in the left sidebar, then click the gear beside any action you wish to remove. Select _Delete_, then confirm to remove the action fully.

If you remove an action from a live Zapier integration, this will break existing Zaps. As such, before removing an action, always [create a new major version](https://platform.zapier.com/docs/versions) of your integration, remove the action from the new version, then follow best practices for migrating users when introducing breaking changes to an integration.
