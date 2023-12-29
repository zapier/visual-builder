---
title: Add a create action
order: 3
layout: post-toc
redirect_from:
---

# Add a create action

## 1. Add the action settings

* Open the _Actions_ tab in Zapier's Platform UI from the sidebar on the left, and select **Add Action**, selecting your action type. New actions are _create_ type by default, and they add new data or update existing data to your app. 

![Zapier visual builder action settings](https://cdn.zappy.app/c845778e65b58839d1fac151d805bb55.png)

> **Note**: You cannot change an action type once you click _Save and Continue_ on a new action. If you need to change the action type, delete the action and recreate it.

* On the Settings page, specify the following:

-- **Key**: A unique identifier for this action, used to reference the action inside Zapier. Does not need to be the same identifier as used in your API. Not shown to users.

-- **Name**: A human friendly plain text name for this action, typically with a verb such as _Add_ or _Create_ followed by the name of the item this action will create in your app. The title-case name is shown inside the Zap editor and on Zapier's app directory marketing pages.

-- **Noun**: A single noun that describes what this action creates, used by Zapier to auto-generate text in Zaps about your action.

-- **Description**: A plain text sentence that describes what the action does and when it should be used. Shown inside the Zap editor and on Zapier's app directory marketing pages. Starts with the phrase "Creates a new". 

-- **Visibility Options**: An option to select when this action will be shown. _Shown_ is chosen by default. Choose `Hidden` if this action should not be shown to users. `Hidden` is usually selected if you build a _create_ action solely to [pair with a search action](https://platform.zapier.com/build/search-create-action) but do not want it used on its own.

* Click on the _Save and Continue_ button. 

## 2. Complete the Input Designer

On the _Input Designer_ page, add user [input fields](https://platform.zapier.com/build/add-fields) for this action. All action steps _must_ include an input form for Zapier to gather the data needed to create or find items in your app. Add at least one input field to your action.

Before building your action's input form, list each piece of data your app needs to create a new item. For example, if building an action to send an email, fields for the email address, subject, and email body would be needed. Your action will likely have several required fields, along with others that are optional, such as for tags or other details.

Add action fields for each piece of data your app needs to create or find this item in your app. Add the fields in the order they're listed in your app, with _required_ fields first, for the best user experience. 

## 3. Set up the API Configuration

The final page of building your action tells Zapier how to send the data to your API.

A `POST` call populates for _create_ actions by default, sending a single item to the provided API endpoint. Zapier then expects a response with an object containing a single item, to be evaluated by [isPlainObject](https://lodash.com/docs#isPlainObject) and parsed into individual fields for use in subsequent Zap steps.

Select the correct API call if your app expects something other than the default, then paste the URL for your API call in the box under _API Endpoint_. Zapier will include each of your input form fields in the _Request Body_ automatically.

If your API call expects input data in the core URL, reference any input field's key with the following text, replacing `key` with your field key:

{% raw %}`{{bundle.inputData.key}}`{% endraw %}

The defaults on all other settings work for most basic API calls. If you need to configure more options, click _Show Options_ to add URL Params, HTTP Headers, set your action to omit empty parameters, or customize the request body. Alternately, switch to [Code Mode](https://platform.zapier.com/build/code-mode) to write custom JavaScript code for your action.

![Zapier action API configuration](https://cdn.zappy.app/1b33f697838f7a4e160d4aa8ef3c6d93.png)

## 4. Test your API request

Configure test data to [test the _create_ action](https://platform.zapier.com/build/test-triggers-actions). Note that testing a POST or PUT request will create or update the item in your app. 

## 5. Define your output

Define sample data and output fields following [the guide](https://platform.zapier.com/build/sample-data).
