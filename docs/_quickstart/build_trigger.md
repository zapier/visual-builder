---
title: Add a Trigger
order: 6
layout: post-toc
redirect_from: /quick-start/
---

# Build Your Integration

## Poll for New Data With a Trigger

![Zapier Trigger Demo Animation](https://cdn.zapier.com/storage/photos/449ad30ba51567045b9d1e9105d9fe90.gif)

_In the Zap editor, users can set triggers to watch for the precise data they want_

Zapier triggers get new data from your API, parse individual data fields, and let users include that data in subsequent Zap action steps. Triggers can run every time something new is added to an API endpoint or pushed to Zapier via a Webhook, or they can use filters to watch for specific items.

To add a trigger to your integration, Zapier visual builder will first have you add details in a form. You will then build an input form to request data from users if your trigger needs filtering—or you can skip that if you want Zapier to run your Trigger every time something new is added to your app. Finally, set your API settings with a `GET` HTTP verb or REST Hook to let Zapier receive data from your API.

Let's have our example GitHub integration poll for new GitHub issues in a specified repo, and triggers Zaps if it finds new issues. We’ll use a `GET` HTTP call, which is called a polling trigger. Zapier will call this every few minutes for each Zap and check for new data.

## 1. Configure Trigger Settings

![Zapier Visual Builder Trigger Settings](https://cdn.zapier.com/storage/photos/2d499138890f7237dffe728fbe9340bc.png)

_Each trigger starts with adding details to a form._

Add a new Trigger, then add Trigger settings. Each trigger includes a:

- **Key** used internally to reference the trigger
- **Name** that users see for the trigger
- **Noun** to describe what object this trigger provides
- **Description** to explain the trigger to users

Add those details to your GitHub new issue trigger, then save and continue.

## 2. Design an Input Field Form

![Zapier Visual Builder input field details](https://cdn.zapier.com/storage/photos/62de2ece0a20ecb837f7dc540194bca2.png)

_Need to gather data from users for your trigger? Add input form fields to your integration to do so._

We want to filter GitHub issues by repository and issue type, which means this trigger needs input fields.

Add a _User Input Field_ in the _Input Designer_ tab first, where users can add the repository they want to watch for issues. Enter a label, key, and help text for the repo field—and set it as required.

To make this example integration simple, use a `string` field type where the user can type the repo name into Zapier instead (then for a challenge later, you could try making a dynamic trigger that has Zapier fetch the users' repositories and show them in a list).

> Learn more about Input forms in our detailed [input designer docs](https://platform.zapier.com/docs/input-designer).

![Zapier Visual Builder dropdown](https://cdn.zapier.com/storage/photos/992bbec7742b65a3b48df6c981e58610.png)

_You can also build a dropdown menu with dynamic or static options_

Your GitHub integration needs two additional input fields: a _Username_ field for users to enter the username of the owner of that repository, and a _Filter_ field to choose which type of issues to trigger the Zap. Repeat the steps to add the username field then the Filter field, and with the Filter check the _Dropdown_ box and the _Static_ option. Enter the following in the code box to build your menu, then save your field:

`["assigned","created","mentioned","subscribed","all"]`

## 3. Configure Your API

![Zapier visual builder API configuration](https://cdn.zapier.com/storage/photos/33cb494cf4aa6ef43df03246d8c9812d.png)

_Add the URL where Zapier can request data from your app, and Zapier will configure the rest automatically_

Now, add the GitHub API call. Select the _API Configuration_ tab in Zapier visual builder, choose the _Polling_ option, then enter GitHub’s issue API endpoint in the field:

{% raw %}`https://api.github.com/repos/{{bundle.inputData.username}}/{{bundle.inputData.repo}}/issues`{% endraw %}

Zapier dynamically replaces the {% raw %}`{{bundle.inputData.fieldname}}`{% endraw %} fields with the text users enter their respective fields. Here, we have Zapier sending the request to GitHub's `/repos/username/repository/issues` endpoint.

Zapier then automatically passes along every other field along with the authentication details in the `GET` call.

## 4. Test Your Trigger

![Zapier visual builder test trigger](https://cdn.zapier.com/storage/photos/ba49443ef2a1222468f1e0f658779762.png)

_The test step ensures your trigger works as expected_

Now test your trigger. Click the *Test your API Request* step to see the GitHub account you added in the Authentication step ready to use (if not, connect your account first here). Underneath, the _Configure Test Data_ section includes form fields to test your trigger. Enter a real GitHub repository name, the username of the owner of that repository, and optionally a filter, then click *Test Your Request*.

![Example Zapier Response](https://cdn.zapier.com/storage/photos/9cf94d89de973edd4b6b3e50971e8375.png)

_See the data that your API call returns to Zapier_

Zapier will find a recent issue from your repo and show the raw JSON output in the _Response_ tab. You can see the field names GitHub sends with this API request, along with example data from your GitHub account.

## 5. Add Sample Data

![Zapier Output Fields](https://cdn.zapier.com/storage/photos/db32cf4e7da4ea55c81bb9f2317473ae.png)

_Zapier Triggers should always include sample data_

Finally, you need to define sample data so Zapier will always have some example data to use when users set up Zaps, even if they don't test their trigger first.

In the _Sample_ field, add fields and example data for those fields with JSON formatting. Only include the most commonly used fields for your integration; for a new GitHub issue, for example, you could use the following code:

	{
	  "body": "This issue is causing problems",
	  "html_url": "https://github.com/",
	  "title": "New Issue"
	}

Then click _Generate Output Field Definitions_ to turn your sample data into output fields, and add a friendly, easy-to-read title to each field.

Save your completed trigger, and you can now use your new Zapier GitHub integration to watch for new issues in a Zap.