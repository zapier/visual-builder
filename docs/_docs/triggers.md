---
title: Triggers
order: 10
layout: post-toc
redirect_from: /docs/
---

# Triggers

![Zapier Trigger Visual Builder](https://cdn.zappy.app/024547d6df8622335ca65456c6d0a11c.png)

Every Zap starts with one trigger, powered by either a webhook subscription that watches for new data as it comes in, or a polling API call to check for new data periodically.

Triggers are how your app's users can start automated workflows whenever they add or update something in your app. New emails, messages, blog posts, subscribers, form entries, commits, and much more are the initial data that underpin every Zap.

As triggers only watch for new data and typically need to send no or little data to the app, they're often quicker to set up than Zapier [actions](./actions). Zapier can watch for any new or updated item through your API—or optionally, you can include [input fields](https://platform.zapier.com/docs/input-designer) for users to enter filters, tags, and other details to filter through new data and watch for the items they want.

## Trigger Types

Most Zapier triggers run when new items are added to an app, database, project, or file. Some apps also include update triggers that run whenever an item is updated in the app, which is useful to help users keep data up to date across apps using Zapier.

To create a "new item" trigger, use an API endpoint that lists items in an array sorted in reverse chronological order. These are typically the most common API endpoints to read data from a platform. If your API lists items in a different order by default, but allows for sorting, include an order or sorting field in your API call. This is important so that the newest records are returned on the [first page of results.](https://platform.zapier.com/docs/dedupe)

To create an "updated item" trigger, use an API endpoint that lists all items, both new and updated, or an endpoint that lists only updated items. Zapier needs a [composite `id` field](https://platform.zapier.com/docs/dedupe#custom-or-multiple-id-fields) that changes whenever the item is updated (ideally `z.hash('md5', item.id + item.updated_at)`), so subsequent updates aren't be filtered out by Zapier's deduper. Again, this endpoint should return an array of items in reverse chronological order, preferably by recency of update. Be sure to include details in your trigger description that lets users know which updates will run this trigger.

# How to Add a New Trigger to a Zapier Integration

## 1. Configure Trigger Settings

![Zapier trigger settings](https://cdn.zappy.app/2ec8af054d697bc5db5d21112d57ebe6.png)

Start building your trigger by adding details about what this trigger does. You need to add both internal data to identify your trigger, and user facing text to describe the trigger to users.

Add each of the following to your trigger:

- **Key**: A unique identifier for this trigger to reference it inside Zapier. Does not need to be the same identifier as used in your API. Not shown to users.
- **Name**: A human-friendly plain-text name for this trigger, typically with an adjective such as _New_ or _Updated_ followed by the name of the item this watches for in your app. Shown inside the Zap editor and on Zapier's app directory marketing pages.
- **Noun**: A single noun that describes what this trigger watches for, used by Zapier to auto-generate text in Zaps about your trigger.
- **Description**: A plain text sentence that describes what the trigger does and when it should be used. Shown inside the Zap editor and on Zapier's app directory marketing pages.
- **Visibility Options**: An option to select when this trigger will be shown. _Shown_ is chosen by default. Choose _Hidden_ if this trigger should not be shown to users.

Once the settings are added, click _Save and Continue_ to add the new trigger and save your settings. You can edit the settings any time later with the exception of the create or search option.

## 2. Build Trigger Input Form (optional)

![Zapier Trigger input form](https://cdn.zappy.app/ef2150ab448e62c51bb3312bbd12995e.png)

Many triggers need no user configuration. When something new is added to an app, the API pushes the details to Zapier to start the Zap, with no details needed. If your API supports filtering or requires specific details about the project, folder, or other location details for the data, you may need to add an input form where users can add the necessary details.

In the "Input Designer" tab of the visual builder's trigger settings, add input fields for each piece of data you need from users to configure the trigger. Check our [Input Designer Guide](https://platform.zapier.com/docs/input-designer) for complete details on how to create an input form and each of the field types and options available.

Once your form is complete—or if you don't need to include an input form—click the _API Configuration_ settings tab to configure how Zapier will get data from your app and test the trigger.

## 3. Enter API Configuration

![Zapier Polling Trigger Settings](https://cdn.zappy.app/0f08230cffa8a3a568d4847e35e42d0c.png)

The last part of adding a trigger is setting the API configuration.

Zapier uses either a Polling API call to check periodically for new or updated data, or a REST Hook with a subscription URL where Zapier can subscribe to receive new or updated data automatically.

Polling API results are expected to be an array with 0 or more objects that will be passed to Zapier's [deduper](https://platform.zapier.com/docs/dedupe). The deduper will return any items that haven't been received before, and use them to run the subsequent steps in the user's Zap.

### Polling Trigger

Zapier selects a _Polling_ trigger by default, where Zapier will send a request to an API endpoint URL to request new data—and in live Zaps, Zapier automatically deduplicates and sorts for the newest data from the API. Live Zaps automatically poll the URL for new data every 1 to 15 minutes, depending on the user's Zapier plan (see [Plans & Pricing](https://zapier.com/pricing) for more details).

To add a polling trigger, select _Polling_ at the top of the settings page, then enter your API URL in the _API Endpoint_ field. If your API URL requires specific data in the URL path, enter the following text in the URL where your API expects that data, replacing `key` with the input field key containing the relevant data from the input form you created in the previous step:

{% raw %}`{{bundle.inputData.key}}`{% endraw %}

Otherwise, Zapier will automatically include any input field data with the API call as URL parameters (for GET requests), or in the request body as JSON (for POST requests).

If you plan to use this trigger to power dropdown menus in other Zap steps (such as to find users, projects, folders, and other app data often used to create new items), and if your API call can paginate data, check the _Support Paging_ box (see [more details on pagination](#pagination) below).

If your API requires any additional data, you can add it using the _Show Options_ button to expose more detailed request configuration. Or, if needed, click _Switch to Code Mode_ to write a custom API call in JavaScript code. The first time you switch to Code Mode, Zapier will translate the settings in the form to code so you can start with the basics already configured. If you switch back to Form Mode, though, Zapier will not transfer any changes made in Code Mode to the form.

Once you've added your trigger settings, be sure to click the _Save API Request & Continue_ button to save the settings you've added.

### REST Hook Trigger

![Zapier REST Hook Settings](https://cdn.zappy.app/0368aeae12e11ec59688d10a7ef69d8c.png)

Alternately, if your app supports REST Hooks—webhook subscriptions that can be manipulated through a REST API—select _REST Hook_ for your trigger. More detail on REST Hooks is [here](http://resthooks.org/), but please note that the Zapier implementation does not support Identity Confirmation.

This will let your trigger run in near realtime with your app pushing data to Zapier, running Zaps as soon as new data comes into your app instead of waiting for Zapier to fetch new data from your API.

With a REST Hook trigger, you need to add Subscribe and Unsubscribe API requests that Zapier can use to set up and remove the hook subscription. Zapier provides the subscription URL in the Subscribe request as `bundle.targetUrl`.

#### Subscribe

Here's an example Subscribe request using Gitlab's API. Note that you'll need to make sure the parameters here match what your API expects.  In this case `url` is the field name that Gitlab expects to contain the webhook URL to send data to.

![](https://cdn.zappy.app/8b7941e3092850bd7edf331cb78b5659.png)

We recommend that a successful Subscribe response return a 201. The data returned should include any data needed to attempt a later Unsubscribe request. This data will be stored in `bundle.subscribeData`.

#### Unsubscribe

When Zapier sends the request to your API to unsubscribe the webhook, it can reference any data that was returned during the Subscribe request and stored in `bundle.subscribeData`.

![](https://cdn.zappy.app/44615176b56966a90101067d719b09ad.png)

#### Perform List

In addition to the Subscribe and Unsubscribe requests, it's important to add a Perform List request where Zapier can check for recent items. This will be used to fetch data when users are setting up and testing the Zap. If you don't define a Perform List, then the user needs to go into your app and do something to generate a new event while the Zap editor waits for data, which is not an optimal experience.

<a id="perform"></a>
#### Perform

![REST Hook Perform](https://cdn.zappy.app/53a7b57b06b1cd50e33eb5e53584a7c5.png)

Finally, in the Perform, you can customize the code to evaluate the data your app's webhooks pass to Zapier. By default, Zapier includes `return [bundle.cleanedRequest];` to return the request data from the webhook as an array. If your data needs to be transformed, or includes multiple objects, add custom code to parse the response data in `bundle.cleanedRequest` within the Perform and turn it into an array of objects, such as [this example code](https://github.com/zapier/zapier-platform/blob/512f558ffa6dff11a0985c2e43c159d534bb6f36/example-apps/rest-hooks/triggers/recipe.js#L42).

The Perform and Perform List methods should each return an array, even if the array only contains one object. The default Perform code includes an array around the cleaned webhook payload, so if your webhook already provides an array, you can remove the wrapping array and simply `return bundle.cleanedRequest;`.

#### Sending Data to Zapier

The object(s) within the arrays coming from the Perform and Perform List methods should have the same data structure, so that live data will behave as expected based on the test data the user maps. See [Sample Data](./faq#output) in the FAQ for more details on this.

If, for architectural reasons, your webhook will receive some data that shouldn't trigger the Zap, your code can return an empty array in those cases. If the Perform method returns an empty array, the Zap won't run.

For data sent to Zapier via REST Hook, most requests will be successful and return a 200 status code with some request-tracking data. This indicates that Zapier has accepted the data, but it's still possible for errors to occur within the Zap if the structure of the provided data is unexpected.

When sending data:

* Be mindful of Zapier's [rate limits](https://zapier.com/help/troubleshoot/behavior/rate-limits-and-throttling-in-zapier#step-4).
* If your application receives a 410 response, that webhook subscription is no longer active, and you should stop sending data to it.
* If your application receives repeated 4xx or 5xx failures from Zapier outside those error types, this can be handled at your discretion. You may choose to try again later, or to stop sending data and deactivate the hook.

To signal that your app has deactivated the hook for any reason, you can optionally send a "reverse unsubscribe" call to Zapier. This can allow users to manage their subscriptions from inside your app, or permit you to clean up after a user deletes their account or revokes credentials. The request should be of the form `DELETE <target_url>`, where `target_url` is the unique target URL that was provided when the subscription was created. This will pause the Zap within Zapier.

Once you've added your trigger settings, be sure to click the _Save API Request & Continue_ button to save the settings you've added.

## Test Trigger API Calls

![Test Zapier Trigger](https://cdn.zappy.app/653f62b85dd1eeb99789c0485c4fecd5.png)

Once you've finished adding your polling or REST Hook trigger settings, it's time to make sure everything you've built so far works and fetches the correct data from Zapier.

For polling triggers, use the _Test Your API Request_ section. You should see the app account you added when testing your authentication. If not, add an app account first.

Then if you added an input form for your Trigger, add data for each of those fields. Be sure to use real data that will work in your app, as Zapier will use it in an API call to your app to fetch live data from your authenticated app account.

Click _Test Your Result_, and if your trigger is set up correctly, you'll see a green checkmark and a _Request Successful_ message in the top right.

![Zapier Trigger Test Results](https://cdn.zappy.app/a4cd21639ac603017afd8e3daa71f13b.png)

Zapier will show the raw, JSON formatted response from your API in the _Response_ tab with every output field your app sends to Zapier. You can see the data Zapier sent to your API in the _Bundle_ tab, or the raw HTTP request in the _HTTP_ tab.

To test a REST Hook trigger, use the Zap editor to build a real Zap, and try turning it on. Be sure to check the logs in the [Monitoring](./testing#monitoring) component to get feedback from your Zap testing. It's also great idea to verify in your system that the subscription was set up properly.

## Define Sample Data and Output Fields

![Adding Sample Data to Zapier integration](https://cdn.zappy.app/b04dc0eb63cc4cf3cf6c14e3b1578f4c.png)
_Sample Data gives Zapier example data if users don't test the trigger or action. Output Fields give your API data user-friendly names in subsequent Zap steps._

The last step in creating a new Trigger for a Zapier integration is to _Define your Output_. Here, Zapier asks both for Sample Data and Output Fields. Both will help improve the Zapier experience for your users, and Sample Data is especially important for Triggers.

![Sample Data in a Zap Step](https://cdn.zappy.app/437ead89852cbfd339b10c15c085b0ed.png)

Sample Data is the default data Zapier shows users when building a Zap using this trigger. In the Zap Editor, Zapier will ask to test the Zap step after users set it up. With Triggers, Zapier will try to fetch recently added or updated items during the test.

If users are in a hurry, though, they can skip the testing step. Zapier will then show the sample data instead. Or, if the connected account doesn't have any data for this item yet, Zapier will default to showing the sample data instead of showing an error that no items are available.

Note that regardless of how many items are retrieved when testing, the Zap Editor will only show up to three samples during the initial test. If new items are later added, those can be pulled in using "Load More", but older items will not be used.

In the _Sample Data_ box, either click the _Use Response from Test Data_ button to import the fields your app sent to Zapier in the previous test, or add your own JSON-formatted fields. Only keep the most important fields, and make sure the data you include with those fields is non-private, non-identifiable testing data that can be shared publicly.

Then click _Generate Output Field Definitions_, and Zapier will build a table of your fields under _Output Fields_. Add a user-friendly name for each field and select the field type. Click _Save Output & Finish_ to finish the final part of your trigger.

You can now make a new Zap using your trigger to test out the trigger live inside Zapier.

## Viewing Triggers in a Zapier Integration

![Triggers in Zapier](https://cdn.zappy.app/35a3f80c665bcc9afc02b2a55424b805.png)

Triggers are listed in alphabetical order. You cannot customize the order of your integration's trigger list.

![Trigger visibility](https://cdn.zappy.app/402a8dc91f24f70e432d03c6668fbf4e.png)

You can, however, change a trigger's visibility and thus choose whether it's shown or not at any time. Open the trigger in the Zapier visual builder, and scroll to the bottom of the page to the _Visibility Options_ section. Select _Hidden_ if you want to keep users from being able to use this trigger (often used if the trigger is only used to power dynamic fields).

## How to Remove Triggers

![Delete Trigger from Zapier Integration](https://cdn.zappy.app/28f8ae96c9001f21dae66dd6109d5fb3.png)

If your app no longer supports a trigger, or you wish to fully rebuild one, you can remove it from Zapier. To delete a trigger from an integration, open the Triggers tab in Zapier visual builder, click the gear icon beside the trigger you wish to remove, select _Delete_, and confirm you wish to remove the trigger.

You cannot restore deleted triggers, so make sure you select the correct triggers for deletion.

> **Note**: Never remove a trigger from a live, public integration version. Only remove triggers from pre-release integrations, or from new versions that will later be rolled out to users.

<a id="pagination"></a>
## How to Use Pagination

By default, Zapier triggers fetch new or recently updated data to start Zaps, and only need to find the most recently added items. Triggers can also be embedded in Zapier drop-down menus, though, and there they need to find all possible items to populate the menu.

Instead of a single item, these triggers' API calls for dynamic menus will often find dozens or hundreds of items. Many APIs let you split the results into pages, much like pages of search results or blog entries. The first API call will return the first set of results—often 20 to 100. If you want additional entries, you can make a new API call requesting page 2 and get the next set of results, iterating through the pages until the API has sent every possible option.

![Zapier drop-down](https://cdn.zappy.app/f59291e5a74d1977648850f84513e33e.png)
_Example drop-down menu in the Zap editor, with an option to load more choices via pagination_

To enable pagination, check the _Support Paging_ checkbox in the API settings when building a Zapier trigger. That enables Zapier's `bundle.meta.page` value which tracks which page Zapier has loaded, along with a _Load more_ option in the user-facing Zapier editor's dropdown menus.

![Include pagination value in Zapier API call](https://cdn.zappy.app/2492cb37ec953861cceaf243c0625285.png)
_In Zapier visual editor, include the bundle.meta.page value to request the correct page of results_

You then need to include that `bundle.meta.page` in your API call to let Zapier dynamically fetch the correct page, as Zapier doesn't include it automatically. First check the _Support Paging_ box. Then click your API endpoint's _Show Options_ button, and add a new URL Param for your API's paging option (or optionally add it to your HTTP Headers if your API expects the paging value there). Use the page request field name from your API on the left, and {% raw %}`{{bundle.meta.page}}`{% endraw %} on the right to have Zapier pull in the correct page value.

![Zapier pagination code mode](https://cdn.zappy.app/8e7923caa73ff68ea6061d61ad37e451.png)
_Zapier's code mode lets you customize the API calls and bundle response parsing_

Zapier's `bundle.meta.page` value uses zero-based numbering. The first time Zapier fetches data from your API, it uses a page value of `0`, followed by `1` the second time, and so on. If your API expects the first API call to request page `1`, with `2` for the second page and so on, you'll need to customize your API call in Zapier's code editor.

The easiest way to do that is to first set your API call in the form mode, then click the _Switch to Code Mode_ toggle. Zapier will convert your form values to code, and if your API works correctly aside from pagination, the defaults in code mode will work. All you need to do is edit your pagination code. If you need non-zero-based numbering, the following code for your pagination header should work (substituting the correct term your API uses for pagination):

`'page': bundle.meta.page + 1,`

![Zapier Action using paginating Trigger](https://cdn.zappy.app/d7d14e885062e466c4bcbbab8dcfd535.png)

![Zapier max entries loaded](https://cdn.zappy.app/b2d1a5bf597c95f8615ca009ee7d66c6.png)

To test your paginating trigger, first build a Zapier Action that uses this trigger in a dynamic dropdown. Then make a new Zap in the user-facing Zap editor that uses your action with the dropdown. Click the dropdown, scroll to the end, and click the _Load More_ button. Repeat until it loads the last options, which will show a result similar to the one above.

![Check headers](https://cdn.zappy.app/78b76bad2188b7594325c2c6bb85f121.png)
_In the Zapier trigger test tool's HTTP logs, you can see the headers and params that Zapier sends to your app_

If you see a _Sorry, no more choices_ message when there should be more options available from your account, go back and check your trigger settings to ensure Zapier is passing the correct details to your app. Test the trigger, and check the HTTP tab for details about the request Zapier sent your app. Zapier should show a `page=0` value (or the correct term for pages in your API) under the Request Params header by default, or `page=1` if you're customizing the page requests to start at 1.
