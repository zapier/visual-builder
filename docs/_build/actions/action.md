---
title: Action
order: 1
layout: post-toc
redirect_from: 
    - /quickstart/build-action
    - /docs/actions

---

# Action

Every Zap starts with a single trigger that watches for new or updated data, starting the user's workflow. Action steps then make use of that data.

Zapier actions create or update a single item in your app through API calls that include multiple details from user customized [input fields](https://platform.zapier.com/build/add-fields). 

![Zapier Action Visual Builder](https://cdn.zappy.app/57f28534d180f2a642ebe0be2e236c32.png)

Zaps can have one or more actions.

There are two types of actions to select.

## 1. Create actions

Most Zapier integrations should at a minimum include create actions to let users add items to their app automatically. Common actions by app category [here](https://platform.zapier.com/quickstart/must-have-triggers-and-actions) should be used for inspiration when building your app.

_Create_ actions in Zaps can create new items in an app or update existing items. The output returned should be an object containing individual fields that will be parsed for mapping into subsequent Zap steps.

The [output returned](https://platform.zapier.com/build/response-types) by a _create_ should be an object containing individual fields about the item that was created such as IDs, details about the new item including a link if possible, and any other useful data about the record. Do not return just a `success` message. 

Unsucessful actions should return `4xx` errors. If your API returns a `2xx` error, add custom code to your API call to replace it with a correct error.

Update actions should be separate from create actions.

Actions may create multiple items if needed, using the same data, though you will likely need to customize the API call code to create multiple items at once. Only do this for linked items, such as if an app stores customers and customer addresses separately.  If the multiple items that need to be created are top-level, complex items in your app, they should be separate actions within Zapier. You can then link the two with a drop-down menu in the action to select the paired item, add a search action for users to find the specific item they need, and then let them match the items with the [_Use a Custom Value_ option](https://help.zapier.com/hc/en-us/articles/8496241696141) in Zapier.

## 2. Search actions

_Search_ actions find existing items in an app and can optionally be paired with _create_ actions to [add a new item](https://platform.zapier.com/build/search-or-create) if the search does not return a result.

Search actions let users do more with the data they’ve already added to your app; such as avoiding adding duplicate items or look up info about an item, for example weather, conversion, and contact lookup, to use in a subsequent step. 

Most useful searches return one individual item that will likely be needed in another Zap step.

The [output returned](https://platform.zapier.com/build/response-types) by a _search_ should be a JSON-formatted array sorted with the best match first. Only the first item will be returned. For no match found, a `200` with an empty array must be returned. If your API returns a `404` error for searches without results, add custom code to your API call to replace it with an empty array. 

Zapier strongly recommends against action steps that delete or remove data. To prevent data loss, action steps should only add or update data. If you are considering adding a delete action to your app, consider alternative actions for items such as deactivating, unsubscribing, or canceling, instead of deleting items completely.