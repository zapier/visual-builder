---
title: Add a search or create action
order: 5
layout: post-toc
redirect_from: 
    - /docs/search-create
    - /build/search-create-action
---

# Add a search or create action

When adding a _search_ action type, you'll see the option to _Pair an existing search and a create to enable "Find or Create" functionality_ in the _Settings_ page. This embeds the _create_ inside the _search_ step to find or create items in one step of the Zap.

## Add a _create_ action

* Add a relevant _create_ action to your integration. If your _search_ action is looking for contacts, say, you would need a *Add New Contact* action to pair with it. Open your integration's _Actions_ page in a new tab and add a new _create_ action if your integration does not have an appropriate one already.

## Configure the _search_ action

* Back in your new _search_ action's settings, check the _Pair an existing search and a create_ box

* Select the relevant action from the _Create Action_ menu and add a new label that Zapier will show on this step if users choose to have the action create new items as well.

![](https://cdn.zappy.app/41334f793dfce14d21e6c35361179721.png)

* When users use the search action in a Zap, Zapier will show your core _search_ action settings that you set in the _Input Designer_ by default. Then, if users click the checkbox to create an item if nothing is found, Zapier will load the _create_ action's input fields inside the search action so users can fill both out.

![Example Search action in Zapier](https://cdn.zappy.app/32ba8f867d02cf60cb6c344a0447b5a5.png)

* Configure the rest of your search action as normal, including the [Test API Request](https://platform.zapier.com/build/test-triggers-actions) and [Output](https://platform.zapier.com/build/sample-data) sections. 