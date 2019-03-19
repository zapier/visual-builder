---
title: Triggers
order: 10
layout: post-toc
redirect_from: /docs/
---

# Triggers

![Zapier Trigger Visual Builder](https://cdn.zapier.com/storage/photos/2d499138890f7237dffe728fbe9340bc.png)

Every Zap starts with a trigger, powered by either a webhook subscription that watches for new data as it comes in or a polling `GET` API call to check for new data periodically.

Triggers are how your app's users can start automated workflows whenever they add or update something in your app. New emails, messages, blog posts, subscribers, form entries, commits, and much more are the initial data that underpin every Zap.

As triggers only watch for new data and typically need to send no or little data to the app, they're often quicker to setup than Zapier action steps. Zapier can watch for any new or updated item through your API—or optionally, you can include [input fields](https://platform.zapier.com/docs/input-designer) for users to enter filters, tags, and other details to filter through new data and watch for the items they want.

> **Note**: Triggers are displayed in the order they are added to Zapier integrations, so be sure to add your app’s most important triggers first.

## Trigger Types

Zapier only includes one _Trigger_ step, but your app may use triggers in multiple ways. Most Zapier triggers run when new items are added to an app, database, project, or file. Some apps also include update triggers that run whenever an item is updated in the app, which is useful to help users keep data up-to-date across apps using Zapier.

To make a standard trigger, use an API endpoint that lists new items in an array sorted in reverse chronological order. These are typically the most common API endpoints to read data from a platform. If your API lists items in a different order by default but allows for sorting, include an order or sorting field in your API call.

To make an update trigger, use an API endpoint that lists all items, both new and updated, or alternately an endpoint that lists only updated items. Zapier needs a composite `id` field that changes whenever the item is updated (ideally `z.hash('md5', item.id + item.updated_at)`), so subsequent updates aren't be filtered out by Zapier's deduper. Again, this should return an reverse chronological order array. Be sure to include details in your trigger description that lets users know which updates will run this trigger.

# How to Add a New Trigger to a Zapier Integration

## 1. Configure Trigger Settings

![Zapier trigger settings](https://cdn.zapier.com/storage/photos/260a97ab4957746a75987dcb21f8aa1d.png)

Start building your trigger by adding details about what this trigger does. You need to add both internal data to identify your trigger, and user facing text to describe the trigger to users.

Add each of the following to your trigger:

- **Key**: A unique identifier for this trigger to reference it inside Zapier. Does not need to be the same identifier as used in your API. Not shown to users.
- **Name**: A human friendly plain text name for this trigger, typically with a verb such as _New_ or _Updated_ followed by the name of the item this watches for in your app. Shown inside the Zap editor and on Zapier's app directory marketing pages.
- **Noun**: A single noun that describes what this trigger watches for, used by Zapier to auto-generate text in Zaps about your trigger.
- **Description**: A plain text sentence that describes what the trigger does and when it should be used. Shown inside the Zap editor and on Zapier's app directory marketing pages.
- **Visibility Options**: An option to select when this trigger will be shown. _Important_ is chosen by default, and will show this trigger inside Zap trigger steps by default. Choose _None_ if you want this trigger hidden by default, useful for rarely used triggers. Or, choose _Hidden_ if this trigger should not be shown to users.

Once the settings are added, click _Save and Continue_ to add the new trigger and save your settings. You can edit the settings any time later with the exception of the create or search option.

## 2. Build Trigger Input Form (optional)

![Zapier Trigger input form](https://cdn.zapier.com/storage/photos/724d126862b876b7deccb5b798b86997.png)

Most triggers need no user configuration. When something new is added to an app, the API pushes the details to Zapier to start the Zap, with no details needed. If your API supports filtering or requires specific details about the project, folder, or other location details for the data, you may need to add an input form where users can add the necessary details.

In the second tab of the visual builder's trigger settings, add input fields for each data item you need from users for the trigger. Check our [Input Designer Guide](https://platform.zapier.com/docs/input-designer) for complete details on how to create an input form and each of the field types and options available.

Once your form is complete—or if you don't need to include an input form—click the _API Configuration_ settings tab to set how Zapier will get data from your app and test the trigger.

## 3. Enter API Configuration

![Zapier Polling Trigger Settings](https://cdn.zapier.com/storage/photos/af53c9298cb9baf32abb17eb9e51a0dc.png)

The last part of adding a trigger is setting is API configuration.

Zapier uses either a Polling API call to check periodically for new or updated data, or a REST hook with a subscription URL where Zapier can subscribe to receive new or updated data automatically. With both, Zapier expects to receive an array with 0 or more objects that will be passed to Zapier's [deduper](https://zapier.com/developer/documentation/v2/deduplication/)—and it will return any items that haven't been received before, and use them to run the subsequent steps in the user's Zap.

### Polling Trigger

Zapier selects a _Polling_ trigger by default, where Zapier will send a `GET` request to an API endpoint URL to request new data—and in live Zaps, Zapier automatically deduplicates and sorts for the newest data from the API. Live Zaps automatically poll the URL for new data every 5 to 15 minutes, depending on the user's Zapier plan.

To add a polling trigger, select _Polling_ at the top of the settings page, then enter your API URL in the _API Endpoint_ field. If your API URL requires specific data in the URL, enter the following text in the URL where your API expects that data, replacing `key` for the input field key with the relevant data from the input form you created before:

{% raw %}`{{bundle.inputData.key}}`{% endraw %}

Otherwise, Zapier will automatically send any other input field data in the request body with the API call.

If you plan to use this trigger to power dropdown menus in other Zap steps (such as to find users, projects, folders, and other app data often used to create new items), and if your API call can paginate data, check the _Support Paging_ box (see [more details on pagination](#pagination) below).

If your API requires any additional data, you can add them from the _Show Options_ button. Or, if needed, click the _Switch to Code Mode_ to write a custom API call in JavaScript code. The first time you switch to Code Mode, Zapier will translate the settings in the form to code so you can start with the basics already configured. If you switch back to form mode, though, Zapier will not transfer any changes from the code mode to the form.

Once you've added your trigger settings, be sure to click the _Save API Request & Continue_ button to save the settings you've added.

### Rest Hook Trigger

![Zapier Rest Hook Settings](https://cdn.zapier.com/storage/photos/de85ffb1cc01a16b4b0e753dd7c0745c.png)

Alternately, if your app supports [REST Hooks](http://resthooks.org/)—or webhook subscriptions that can be manipulated through a REST API—select _Rest Hook_ for your trigger. This will let your trigger run in near realtime with your app pushing data to Zapier, running Zaps as soon as new data comes into your app instead of waiting for Zapier to fetch new data from your API.

With a REST Hook trigger, you need to add a Subscribe and Unsubscribe URL, along with a Perform List URL where Zapier should check for recent items. Finally, you can customize the code to evaluate the data your app's webhooks pass to Zapier.

As with polling triggers, once you've added your trigger settings, be sure to click the _Save API Request & Continue_ button to save the settings you've added.

![Test Zapier Trigger](https://cdn.zapier.com/storage/photos/120d65ddd8baed9d781c358b66078851.png)

Once you've finished adding your polling or rest hook trigger settings, it's time to make sure everything you've built so far works and fetches the correct data from Zapier. In the _Test Your API Request_ section, you should see the app account you added when testing your authentication. If not, add an app account first.

Then if you added an input form for your Trigger, add data for each of those fields. Be sure to use real data that will work in your app, as Zapier will use it in an API call to your app to fetch live data from your authenticated app account.

Click _Test Your Result_, and if your trigger is set up correctly, you'll see a green checkmark and a _Request Successful_ message in the top right.

![Zapier Trigger Test Results](https://cdn.zapier.com/storage/photos/a43315730778c1cf5251d1e80a465819.png)

Zapier will show the raw, JSON formatted response from your API in the _Response_ tab with every output field your app sends to Zapier. You can see the data Zapier sent to your API in the _Bundle_ tab, or the raw HTTP request in the _HTTP_ tab.

![Zapier Define Output Fields](https://cdn.zapier.com/storage/photos/d9a84ecb06a3f8f9e40fb91ba1a63ea5.png)

As a final step, you need to define the most important output fields to help users easily know what data from your app they should use in subsequent Zap steps. In the _Sample Data_ box, either click the _Use Response from Test Data_ button to import the fields your app sent to Zapier in the previous test, or add your own JSON-formatted fields. Only keep the most important fields, and make sure the data you include with those fields is non-private, non-identifiable testing data that can be shared publicly.

Then click _Generate Output Field Definitions_, and Zapier will build a table of your fields under _Output Fields_. Add a human friendly name for each field and select the field type. Click _Save Output & Finish_ to finish the final part of your trigger.

_[Learn more about how Zapier uses sample data and output fields](http://zapier.github.io/visual-builder/docs/faq#output)_.

You can now make a new Zap using your trigger to test out the trigger live inside Zapier.

## How to Reorder Triggers in a Zapier Integration

![Triggers in Zapier](https://cdn.zapier.com/storage/photos/316fc36427a242269ec9118a06f0347a.png)

When users select your app as the trigger step in a Zap, they'll see the triggers marked as _Important_ by default, with every other integration hidden under the _show less common options_ menu. Zapier displays triggers in the order they were added to your Zapier integration—so the first trigger you added and marked as important will show up at the top of the list.

There is no way to reorder triggers in Zapier visual builder at the moment. It's best to plan your integration before you add triggers, and add the triggers your users will likely use the most first so they'll show at the top of the list. Alternately, you could delete triggers and re-add them in the order you want, if needed.

![Trigger visibility](https://cdn.zapier.com/storage/photos/478830f781668c2f9c6131de63954f1c.png)

You can however change a trigger's importance and thus choose whether it's shown by default or not at any time. Open the trigger in Zapier visual builder, scroll to the bottom of the page to the _Visibility Options_ menu. Select _Important_ to have the trigger show by default, _None_ to have the trigger in the _show less common options_ menu, and _Hidden_ if you want to keep users from being able to use this trigger (often used if the trigger is only used to power dynamic fields).

## How to Remove Triggers From a Zapier Integration

![Delete Trigger from Zapier Integration](https://cdn.zapier.com/storage/photos/188948a918eb589684b1d04c17707a52.png)

If your app no longer supports a trigger, or you wish to fully rebuild one, you can remove it from Zapier anytime. To delete a trigger from an integration, open the Triggers tab in Zapier visual builder, click the gear icon beside the trigger you wish to remove, select _Delete_, and confirm you wish to remove the trigger.

You cannot restore deleted triggers, so make sure you select the correct triggers for deletion.

> **Note**: Only remove triggers from pre-release integrations, or from new versions that will later be rolled out to users. Never remove a trigger from a live, public integration version.

<a id="pagination"></a>
## How to Use Pagination

Zapier triggers by default fetch new or recently updated data to start Zaps, and only need to find the most recently added item. Triggers can also be embedded in Zapier action drop-down menus, though, and there they need to find all possible items to populate the menu.

Instead of a single item, these triggers' API calls for dynamic menus will often find dozens or hundreds of items. Many APIs let you split the results into pages, much like pages of search results or blog entries. The first API call will return the first set of results—often 20 to 100. If you want additional entries, you can make a new API call requesting page 2 and get the next set of results, iterating through the pages until the API has sent every possible option.

![Zapier drop-down](https://cdn.zapier.com/storage/photos/05b63c557de501cb4764f29747b733ec.png)
_Example drop-down menu in the Zap editor, with an option to load more choices via pagination_

To enable pagination, check the _Support Paging_ checkbox in the API settings when building a Zapier trigger. That enables Zapier's `bundle.meta.page` value which tracks which page Zapier has loaded, along with a _Check Ap‌p & reload to bring in new choices_ option in the user-facing Zapier editor's dropdown menus.

![Include pagination value in Zapier API call](https://cdn.zapier.com/storage/photos/0c73268e2e0d62e1bbe7d3d4f552fcda.png)
_In Zapier visual editor, include the bundle.meta.page value to request the correct page of results_

You then need to include that `bundle.meta.page` in your API call to let Zapier dynamically fetch the correct page, as Zapier doesn't include it automatically. First check the _Support Paging_ box. Then click your API endpoint's _Show Options_ button, and add a new URL Param for your API's paging option (or optionally add it to your HTTP Headers if your API expects the paging value there). Use the page request field name from your API on the left, and {% raw %}`{{bundle.meta.page}}`{% endraw %} on the right to have Zapier pull in the correct page value.

![Zapier pagination code mode](https://cdn.zapier.com/storage/photos/36f2051b7fdf684870492a39aab535c8.png)
_Use custom code to _

Zapier's `bundle.meta.page` value uses zero-based numbering. The first time Zapier fetches data from your API, it uses a page value of `0`, followed by `1` the second time, and so on. If your API expects the first API call to request page `1`, with `2` for the second page and so on, you'll need to customize your API call in Zapier's code editor.

The easiest way to do that is to first set your API call in the form mode, then click the _Switch to Code Mode_ toggle. Zapier will convert your form values to code, and if your API works correctly aside from pagination, the defaults in code mode will work. All you need to do is edit your pagination code. If you need non-zero-based numbering, the following code for your pagination header should work (substituting the correct term your API uses for pagination):

`'page': bundle.meta.page + 1,`

![Zapier max entries loaded](https://cdn.zapier.com/storage/photos/4808c60c860e71f82578cedf0e20ce11.png)

To test your paginating trigger, first build a Zapier Action that uses this trigger in a dynamic dropdown. Then make a new Zap in the user-facing Zap editor that uses your action with the dropdown. Click the dropdown, scroll to the end, and click the _Check App & bring in more choices_ button. Repeat until it loads the last options, which will show a result similar to the one above.

![Check headers](https://cdn.zapier.com/storage/photos/8675a69add537f2e7d5ed950724fc15f.png)
_In the Zapier trigger test tool's HTTP logs, you can see the headers and params that Zapier sends to your app_

If you see a _Sorry, no more choices_ option when there should be more options available from your account, go back and check your trigger settings to ensure Zapier is passing the correct details to your app. Test the trigger, and check the HTTP tap for details about the request Zapier sent your app. Zapier should show a `page=0` value (or the correct term for pages in your API) under the Request Params header by default, or a page=1` if you're customizing the page request to start at 1.