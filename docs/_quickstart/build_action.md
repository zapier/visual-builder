---
title: Add an Action
order: 8
layout: post-toc
redirect_from: /quick-start/
---

# Build Your Integration

## Add New Data With an Action

![Zapier Action Demo Animation](https://cdn.zappy.app/7160a6ce9b11c9427cceb1b7241016cc.gif)

_The input form in Zapier actions lets users map fields from trigger and previous action steps to your app_

Zapier actions push new data or update existing data into your API from input fields that users set in their Zaps. Zapier includes *search* actions to find data in an app, and *create* actions to add new items via API calls.

Adding an action to your Zapier integration works much like building a trigger. Only here with *create* actions, Zapier will `POST` or `PUT` the data users enter in the input fields to your API—and *every* action needs an input form to gather data and send to your app.

Let’s add an _Action_ to our example GitHub integration so Zapier can send data to GitHub. This tells the Zapier Platform how to create the Zap Editor form where users can configure their Zaps and map data to and from the API, then tells it how to make calls to the API endpoint.

## 1. Configure Action Settings

![Zapier Visual Builder action settings](https://cdn.zappy.app/10d48377c1b0020384db1d1029ba8fc6.png)

_Each action starts with adding details to a form._

Enter your new action settings, as with your trigger. Select a _Create_ action since this action will create new issues; then include a key, name, noun, and description for an issue. The type of action cannot be changed once created, so you will need to decide whether the [response type you expect to use](https://platform.zapier.com/docs/faq#what-response-type-does-zapier-expect) for your action would be better served by a _Search_ or a _Create_. 

## 2. Design an Action Input Field Form

![Zapier Visual Builder action input fields](https://cdn.zappy.app/7f56cceae7d3d47a2c10bd040dc03a86.png)

_Add a new field for every piece of data users need to send to your app for this action_

Then add the input fields from the _Input Designer_ tab. Select from _Input Field_ that let users enter static text, _Dynamic Fields_ that pull in data from triggers, and _Line Item Groups_ to include line item data.

![Zapier Visual Builder action input designer](https://cdn.zappy.app/3acb59af771b5999b8d3c57472769192.png)

_Each field type includes its own settings—and you can preview the finished input form on the right_

For our example GitHub integration, we need 4 input fields: `owner` to add the repository's owner, `title` to list your issue title, `repo` to add the repository's name, and `body` to add details about the issue. Add the first three as you did in the Trigger setup, with the default `string` field type and the `owner`, `title`, or `repo` keys respectively. Then, for the issue details, select a _Text_ field type so users can enter longer text and use the `body` key.

> Learn more about Input forms in our detailed [input designer docs](https://platform.zapier.com/docs/input-designer).

## 3. Configure Your API

![Zapier Visual Builder action API](https://cdn.zappy.app/6b0317389c1a08003db207cfcd732dd3.png)

_Add the URL where Zapier will send data to your app_

Now, select the _API Configuration_ tab in Zapier Visual Builder to tell Zapier how to send the data to the API. Select the `POST` API call, then enter GitHub’s issue API endpoint with the {% raw %}`{{bundle.inputData.fields}}`{% endraw %} fields as with the trigger:

{% raw %}`https://api.github.com/repos/{{bundle.inputData.owner}}/{{bundle.inputData.repo}}/issues`{% endraw %}

Zapier will automatically include the `owner` and `repo` from the input fields in your API request body. Click the *Show Options* button to see the mapped fields and customize/remove them if needed—Zapier includes all the input fields by default - keep the issue `title` and `body` that this [GitHub endpoint](https://docs.github.com/en/rest/issues/issues?apiVersion=2022-11-28#create-an-issue) expects in the request body, and use the `owner` and `repo` fields in the URL path.

## 4. Test Your Action

![Zapier Visual Builder action test](https://cdn.zappy.app/73cbb372bd51bc99d526c2f156de4b42.png)

_Test your action by sending data to it as users will in their Zaps_

Then test the API request. As with the trigger, add sample data  in the *Configure Test Data* form, using a real GitHub repo along with example text and body for your issue. Click *Test Your Result*, and Zapier will try creating an issue with your test data.

## 5. Define Your Action Output Fields

![Zapier Visual Builder output fields](https://cdn.zappy.app/2bff8f873b1d2333c2dc580a18005a15.png)

_Add example data and user friendly names to your app's most popular fields, especially those that users set in the input form for this action_

Finally define sample data and output fields, as in the trigger setup, including example JSON data with the most popular fields, and reader-friendly names so users can easily identify which fields to map in subsequent actions. If a label is not specified, the JSON field name on the left will be used. 

![Zapier Visual Builder output field labels](https://cdn.zappy.app/198b5862b9311e71cdfb1e3fa1d344ab.png)

Save your action, and you now have a complete Zapier integration with authentication, a trigger, and an action!

## Your Action in Zap Editor

![Action Step Zap Editor 1](https://cdn.zappy.app/84c5b5ee42862728f2d443e14e7d90c1.png)

![Action Step Zap Editor 2](https://cdn.zappy.app/f2dee890e67998edde96894c6e2f8a10.png)

![Action Step Zap Editor 3](https://cdn.zappy.app/acd2a7263a190700312b71de30ea088f.png)

![Action Step Zap Editor 4](https://cdn.zappy.app/1821f9ce96a9f224d7e353a21643e2cd.png)

Your GitHub Action's fields let you type in text or map data from previous steps in your Zap so Zapier can copy it into the app. Users clicking into a field can select data from previous steps to use in that field. Then, when the Zap runs, Zapier copies the data that triggered the Zap run and/or any previous steps, and uses it to make the new item in your app—a new GitHub issue in this case.
