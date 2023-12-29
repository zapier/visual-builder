---
title: Add a search action
order: 3
layout: post-toc
redirect_from:
---

# Add a search action

## 1. Add the action settings

* Open the _Actions_ tab in Zapier's Platform UI from the sidebar on the left, and select **Add Action**, selecting your action type. New actions are _create_ type by default, and add new data or update existing data to your app. 

![Zapier Search action settings](https://cdn.zappy.app/3e47ad8a26c30fb761fdd60390d8705e.png)

> **Note**: You cannot change an action type once you click _Save and Continue_ on a new action. If you need to change the action type, delete the action and recreate it.

* On the Settings page, specify the following:

-- **Key**: A unique identifier for this action, used to reference the action inside Zapier. Does not need to be the same identifier as used in your API. Not shown to users.

-- **Name**: A human friendly plain text name for this action, typically with a verb such as _Find_ or _Search_ followed by the name of the item this action will find in your app. The title-case name is shown inside the Zap editor and on Zapier's app directory marketing pages.

-- **Noun**: A single noun that describes what this action searches, used by Zapier to auto-generate text in Zaps about your action.

-- **Description**: A plain text sentence that describes what the action does and when it should be used. Shown inside the Zap editor and on Zapier's app directory marketing pages. Starts with the phrase "Finds a". 

-- **Visibility Options**: An option to select when this action will be shown. _Shown_ is chosen by default. 

* At the bottom of the settings page, you'll see an option to pair your _search_ with a _create_ action. That lets your [action also create an item](https://platform.zapier.com/build/search-or-create) if the search does not return any results.

* Click on the _Save and Continue_ button. 

## 2. Complete the Input Designer

On the _Input Designer_ page, add user [input fields](https://platform.zapier.com/build/add-fields) for this action. All action steps _must_ include an input form for Zapier to gather the data needed to create or find items in your app. Add at least one input field to your action.

Before building your action's input form, list each piece of data your app needs to find an item. Most search actions only include a single input field, sometimes along with a drop-down menu to select filter data. 

## 3. Set up the API Configuration

In the final _API Configuration_ page, add the API endpoint where Zapier will send the search request to.  

A `GET` call is used for search actions by default, and sends the data from the input form to your API endpoint. 

Zapier expects an array response with 0 or more items. If more than 1 item is returned in the array, Zapier shows only the first match, and parses it into individual fields for use in subsequent Zap steps. 

If you prefer your search to return multiple results, return the set of results as an array of objects ([line items](https://help.zapier.com/hc/en-us/articles/8496277737997)) under a descriptive key. However, using the standard approach is recommended, because not all integrations support line items directly, so users may need to take additional actions to reformat this data for use in their Zaps, depending which app they pair your _search_ with. 

If you'd still like to offer your users a _search_ that returns multiple matches, it is recommended to consider offering both a single item _search_ and multiple item _search_ - for example a `Find Record` that returns a single result and a `Find Record(s)` that could return multiple results. 

For no match found, a `200` with an empty array must be returned to ensure the _search_ step behaves as expected in the Zap editor. A _search_ that returns no results is still considered a successful action step and [should not return an error](https://platform.zapier.com/build/response-types). 

If you need to parse the response from the endpoint into the expected response type, switch to [Code Mode](https://platform.zapier.com/build/code-mode) to write custom JavaScript code for your action.

## 4. Test your API request

Configure test data to [test the _search_ action](https://platform.zapier.com/build/test-triggers-actions). Testing a GET request would be expected to return the item from the endpoint.  

## 5. Define your output

Define sample data and output fields following [the guide](https://platform.zapier.com/build/sample-data).
