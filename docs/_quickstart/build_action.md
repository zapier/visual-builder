---
title: Add an Action
order: 8
layout: post-toc
redirect_from: /quick-start/
---

# Build Your Integration

## Add New Data With an Action

![Zapier Action Demo Animation](https://cdn.zapier.com/storage/photos/e216b6e1eaa49626bd18e3ca72b2a513.gif)

_The input form in Zapier actions let users map fields from trigger and previous action steps to your app_

Zapier actions push or put new data into your API from input fields that users set in their Zaps. Zapier includes *search* actions to find data in an app, and *create* actions to add new items via API calls.

Adding an action to your Zapier integration works much like building a trigger. Only here with create actions, Zapier will `POST` or `PUT` the data users enter in the input fields to your API—and *every* trigger needs an input form to gather data and send to your app.

Let’s add an _Action_ to our example GitHub integration so Zapier can send data to GitHub. This tells the Zapier platform how to create the Zap Editor form where users can configure their Zaps and map data to and from the API, then tells it how to make calls to the API endpoint.

## 1. Configure Action Settings

![Zapier visual builder action settings](https://cdn.zapier.com/storage/photos/f4fba922b339ce68376e38b751bc79f1.png)

_Start by entering the core settings for this action_

Enter your new action settings, as with your trigger. Select a _Create_ action since this action will create new issues, then include a key, name, noun, and description for an issue.

## 2. Design an Action Input Field Form

![Zapier Visual Builder action input fields](https://cdn.zapier.com/storage/photos/637ad915851e73847e1bdacdd5fea09d.png)

_Add a new field for every piece of data users need to send to your app for this action_

Then add the input fields from the _Input Designer_ tab. Select from _Input Field_ that let users enter static text, _Dynamic Fields_ that pull in data from triggers, and _Line Item Groups_ to include line item data.

![Zapier Visual Builder action input designer](https://cdn.zapier.com/storage/photos/eb66c144f3f377c564aca2642c43156d.png)

_Each field type includes its own settings—and you can preview the finished input form on the right_

For our example GitHub integration, we need 4 input fields: `repo` to add the repository's name, `username` to add the repository's owner, `title` to list your issue title, and `body` to add details about the issue. Add the first three as you did in the Trigger setup, with the default `string` field type and the `repo`, `username`, or `title` keys respectively. Then, for the issue body, select a _Text_ field type so users can enter longer text and use the `body` key.

> Learn more about Input forms in our detailed [input designer docs](https://platform.zapier.com/docs/input-designer).

## 3. Configure Your API

![Zapier visual builder input API](https://cdn.zapier.com/storage/photos/5148dc2b2d7417e17114617df6a0ad9b.png)

_Add the URL where Zapier will send data to your app_

Now, select the _API Configuration_ tab in Zapier visual builder to tell Zapier how to send the data to the API. Select the `POST` API call, then enter GitHub’s issue API endpoint with the {% raw %}`{{bundle.inputData.fields}}`{% endraw %} fields as with the trigger:

{% raw %}`https://api.github.com/repos/{{bundle.inputData.username}}/{{bundle.inputData.repo}}/issues`{% endraw %}

Zapier will automatically include the username and repo from the input fields in your API request body. Click the *Show Options* button to see the mapped fields and customize them if needed—though Zapier should include the issue title and body by default.

## 4. Test Your Action

![Zapier visual builder input test](https://cdn.zapier.com/storage/photos/e5e053ab3550a339428042d9f9af13bf.png)

_Test your action by sending data to it as users will in their Zaps_

Then test the API request. As with the trigger, add sample data  in the *Configure Test Data* form, using a real GitHub repo along with example text and body for your issue. Click *Test Your Result*, and Zapier will try creating an issue with your test data.

## 5. Define Your Action Output Fields

![Zapier visual builder output fields](https://cdn.zapier.com/storage/photos/ae070045d9e23b162f1b0a0a1507b029.png)

_Add example data and user friendly names to your app's most popular fields, especially those users set in your input form_

Finally define sample data and output fields, as in the trigger setup, including example JSON data with the most popular fields, and reader-friendly names so users can easily identify which fields to map in subsequent actions.

Save your action, and you now have a complete Zapier integration with authentication, a trigger, and an action!

## Your Action in Action

![Mapping Fields in Zapier](https://cdn.zapier.com/storage/photos/e0442350236db38688da231caafdab5f.gif)

Your GitHub Action's fields let you type in text or map data from previous steps in your Zap so Zapier can copy it into the app. Most input fields include a `+` button on the right where users can select data from previous steps to use in that field. Then, when the Zap runs, Zapier copies the new data from the Zap's trigger and previous steps, and uses it to make the new item in your app—a new GitHub issue in this case.