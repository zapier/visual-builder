---
title: Add an Action
order: 8
layout: post-toc
redirect_from: /quick-start/
---

# Build Your Integration

## Add New Data With an Action

![Zapier Action Demo Animation](https://cdn.zappy.app/7160a6ce9b11c9427cceb1b7241016cc.gif)

_The input form in Zapier actions let users map fields from trigger and previous action steps to your app_

Zapier actions push or put new data into your API from input fields that users set in their Zaps. Zapier includes *search* actions to find data in an app, and *create* actions to add new items via API calls.

Adding an action to your Zapier integration works much like building a trigger. Only here with *create* actions, Zapier will `POST` or `PUT` the data users enter in the input fields to your API—and *every* action needs an input form to gather data and send to your app.

Let’s add an _Action_ to our example GitHub integration so Zapier can send data to GitHub. This tells the Zapier platform how to create the Zap Editor form where users can configure their Zaps and map data to and from the API, then tells it how to make calls to the API endpoint.

## 1. Configure Action Settings

![Zapier Visual Builder action settings](https://cdn.zappy.app/35d98d82cc88d3dc5451f07f14143e34.png)

_Each action starts with adding details to a form._

Enter your new action settings, as with your trigger. Select a _Create_ action since this action will create new issues, then include a key, name, noun, and description for an issue. The type of action cannot be changed once created, so decide whether the [response type you expect to use](https://platform.zapier.com/docs/faq#what-response-type-does-zapier-expect) for your action better meets a _Search_ or _Create_. 

## 2. Design an Action Input Field Form

![Zapier Visual Builder action input fields](https://cdn.zappy.app/2726149681f334bf2f8822a1ed7a0c14.png)

_Add a new field for every piece of data users need to send to your app for this action_

Then add the input fields from the _Input Designer_ tab. Select from _Input Field_ that let users enter static text, _Dynamic Fields_ that pull in data from triggers, and _Line Item Groups_ to include line item data.

![Zapier Visual Builder action input designer](https://cdn.zappy.app/3ebd6387ae198e7c9d30e758809fa81c.png)

_Each field type includes its own settings—and you can preview the finished input form on the right_

For our example GitHub integration, we need 4 input fields: `owner` to add the repository's owner, `title` to list your issue title, `repo` to add the repository's name, and `body` to add details about the issue. Add the first three as you did in the Trigger setup, with the default `string` field type and the `owner`, `title`, or `repo` keys respectively. Then, for the issue details, select a _Text_ field type so users can enter longer text and use the `body` key.

> Learn more about Input forms in our detailed [input designer docs](https://platform.zapier.com/docs/input-designer).

## 3. Configure Your API

![Zapier Visual Builder input API](https://cdn.zappy.app/b797baa659d703d3d029b82619e08edd.png)

_Add the URL where Zapier will send data to your app_

Now, select the _API Configuration_ tab in Zapier Visual Builder to tell Zapier how to send the data to the API. Select the `POST` API call, then enter GitHub’s issue API endpoint with the {% raw %}`{{bundle.inputData.fields}}`{% endraw %} fields as with the trigger:

{% raw %}`https://api.github.com/repos/{{bundle.inputData.owner}}/{{bundle.inputData.repo}}/issues`{% endraw %}

Zapier will automatically include the `owner` and `repo` from the input fields in your API request body. Click the *Show Options* button to see the mapped fields and customize/remove them if needed—Zapier includes all the input fields by default - keep the issue `title` and `body` that this [GitHub endpoint](https://docs.github.com/en/rest/issues/issues?apiVersion=2022-11-28#create-an-issue) expects in the request body, and use the `owner` and `repo` fields in the URL path.

## 4. Test Your Action

![Zapier Visual Builder input test](https://cdn.zappy.app/b678a3d2400780a31091c28d31d0e3cf.png)

_Test your action by sending data to it as users will in their Zaps_

Then test the API request. As with the trigger, add sample data  in the *Configure Test Data* form, using a real GitHub repo along with example text and body for your issue. Click *Test Your Result*, and Zapier will try creating an issue with your test data.

## 5. Define Your Action Output Fields

![Zapier Visual Builder output fields](https://cdn.zappy.app/6056088fe66e6fd0264f9c7db0f089f5.png)

_Add example data and user friendly names to your app's most popular fields, especially those that users set in the input form for this action_

Finally define sample data and output fields, as in the trigger setup, including example JSON data with the most popular fields, and reader-friendly names so users can easily identify which fields to map in subsequent actions. If a label is not specified, the JSON field name on the left will be used. 

![Zapier Visual Builder output field labels](https://cdn.zappy.app/ce33633bc7d987f701d1ae838d8ad70f.png)

Save your action, and you now have a complete Zapier integration with authentication, a trigger, and an action!

## Your Action in Action

![Mapping Fields in Zapier](https://cdn.zappy.app/6bd1765cafb09592dbfe73f306840437.gif)

Your GitHub Action's fields let you type in text or map data from previous steps in your Zap so Zapier can copy it into the app. Users clicking into a field can select data from previous steps to use in that field. Then, when the Zap runs, Zapier copies the data that triggered the Zap run and/or any previous steps, and uses it to make the new item in your app—a new GitHub issue in this case.
