---
title: Add a Trigger
order: 7
layout: post-toc
redirect_from: /quick-start/
---

# Build Your Integration

## Poll for New Data With a Trigger

![Zapier Trigger Demo Animation](https://cdn.zappy.app/ce3ad77e27df60694a6b9af4f1283c25.gif)

_In the Zap Editor, users can set triggers to watch for the precise data they want_

Zapier triggers get new data from your API, parse individual data fields, and let users include that data in subsequent Zap action steps. Triggers can run every time something new is added to an API endpoint or pushed to Zapier via a Webhook, or they can use filters to watch for specific items.

To add a trigger to your integration, Zapier Visual Builder will first have you add details in a form. You will then build an input form to request data from users if your trigger needs filtering—or you can skip that if you want Zapier to run your trigger every time something new is added to your app. Finally, set your API settings with a `GET` HTTP method or REST Hook to let Zapier receive data from your API.

Let's have our example GitHub integration poll for new GitHub issues in a specified repo, and trigger Zaps if it finds new issues in that repo. We’ll use a `GET` HTTP method, which is called a polling trigger. Zapier will call this every few minutes for each Zap and check for new data.

## 1. Configure Trigger Settings

![Zapier Visual Builder trigger settings](https://cdn.zappy.app/1acb400e936c56c2c021d3bc38af5790.png)

_Each trigger starts with adding details to a form._

Add a new Trigger, then add Trigger settings. Each trigger includes a:

- **Key** used internally to reference the trigger
- **Name** that users see for the trigger
- **Noun** to describe what object this trigger provides
- **Description** to explain the trigger to users

Add those details to your GitHub new issue trigger, then save and continue.

## 2. Design an Input Field Form

![Zapier Visual Builder trigger input designer](https://cdn.zappy.app/a3e8a454ede58f6f69abc88edc277256.png)

_Need to gather data from users for your trigger? Add input form fields to your integration to do so._

We want to use the List repository issues endpoint [detailed here](https://docs.github.com/en/rest/issues/issues?apiVersion=2022-11-28#list-repository-issues) so we’ll need input fields for this trigger as the endpoint is `/repos/{owner}/{repo}/issues`

Add a _Repo Input Field_ in the _Input Designer_ tab first, where users can add the repository they want to watch for issues. Enter a label, key, and help text for the repo field—and set it as required.

To make this example integration simple, use a `string` field type where the user can type the repo name into Zapier instead (then for a challenge later, you could try making a dynamic trigger that has Zapier fetch the user's repositories and show them in a dropdown list).

> Learn more about Input Field forms and dynamic dropdowns in our detailed [input designer docs](https://platform.zapier.com/docs/input-designer).

Your GitHub integration needs an additional input field: an _Owner_ field for users to enter the username of the owner of that repository.

![Zapier Visual Builder trigger input Designer dropdown](https://cdn.zappy.app/003a44b3652726572d3ff5d31a137c88.png)

_You can also build a dropdown menu with dynamic or static options_

Since _State_ is an available parameter for this endpoint, let’s add that too as it will be useful to be able to choose which type of issues should trigger the Zap. Repeat the steps to add the _Owner_ field then the _State_ field. For the _State_ field, add a default value of _open_ and check the _Dropdown_ box and the _Static_ option. Enter the following in the code box to build your menu, then save your field:

`["open","closed","all"]`

![Zapier Visual Builder trigger input designer a state field](https://cdn.zappy.app/1446ddb567eef0941310f2ac77a05e97.png)

## 3. Configure Your API

![Zapier Visual Builder trigger API configuration](https://cdn.zappy.app/07662723850787806694485fa09440d4.png)

_Add the URL where Zapier can request data from your app, Zapier will configure some fields automatically_

Now, add the GitHub API call. Select the _API Configuration_ tab in Zapier Visual Builder, choose the _Polling_ option, then enter GitHub’s issue API endpoint in the field:

{% raw %}`https://api.github.com/repos/{{bundle.inputData.owner}}/{{bundle.inputData.owner}}/issues`{% endraw %}

Zapier dynamically replaces the {% raw %}`{{bundle.inputData.fieldname}}`{% endraw %} fields with the text users enter into the respective fields when setting up the trigger. Here, we have Zapier sending the request to GitHub's `/repos/{owner}/{repo}/issues` endpoint.

Zapier automatically includes every inputField in the URL Params section - we’ll only keep _State_ as the other fields are included in the URL, so you can remove _Repo_ and _Owner_ from URL Params.

The authentication details are automatically included in the HTTP headers section of the `GET` request. 
There is also the option to switch to Code Mode to see the specifics of the request being made, or work in code if that is your preference. 

## 4. Test Your Trigger

![Zapier Visual Builder test trigger](https://cdn.zappy.app/5b80de656d9003107c8b12ff753558fc.png)

_The test step ensures your trigger works as expected_

Now test your trigger. Click the *Test your API Request* step to see the GitHub account you added in the Authentication step ready to use (if not, connect your account first here). Underneath, the _Configure Test Data_ section includes form fields to test your trigger. Enter a real GitHub repository name, the username of the owner of that repository, and optionally a state, then click *Test Your Request*.

![Zapier Visual Builder example response](https://cdn.zappy.app/5ab721f6e4b5de01e90080c95dffd24f.png)

_See the data that your API call returns to Zapier_

Zapier will find a recent issue from your repo with the matching state and show the raw JSON output in the _Response_ tab. You can see the field names GitHub sends with this API request, along with example data from your GitHub account.

## 5. Add Sample Data

![Zapier Sample Data](https://cdn.zappy.app/6d4f18f174ec438afd6de91fea14ddb9.png)

_Zapier Triggers should always include sample data_

Finally, you need to define sample data so Zapier will always have some example data to use when users set up Zaps, even if they don't test their trigger first.

In the _Sample Data_ field, add fields and example data for those fields with JSON formatting. Only include the most commonly used fields for your integration; for a new GitHub issue, for example, you could use the following code:

	{
	  "body": "This issue is causing problems",
	  "html_url": "https://github.com/",
	  "title": "New Issue"
	}

Alternatively, you can use the _Use Response from Test Data_ button, but only if your test is expected to contain the same field keys as any user would see.

Then click _Generate Output Field Definitions_ to turn your sample data into output fields, and add a friendly, easy-to-read title to each field.

![Zapier Output Fields](https://cdn.zappy.app/b6f4759016281ee787d2a63faf5f2536.png) 

Save your completed trigger, and you can now use your new Zapier GitHub integration to watch for new issues in a Zap.
