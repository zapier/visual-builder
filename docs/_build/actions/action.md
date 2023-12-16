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

Zapier actions create or update new data into apps through API calls that pass data from user customized [input fields](https://platform.zapier.com/build/add-fields). 

![Zapier Action Visual Builder](https://cdn.zappy.app/57f28534d180f2a642ebe0be2e236c32.png)

Zaps can have one or more actions.

There are two types of actions to select.

## 1. Create actions

Most Zapier integrations should at a minimum include create actions to let users add items to their app automatically. Common actions by app category [here](https://platform.zapier.com/quickstart/integration-design-examples) should be used for inspiration when building your app.

_Create_ actions in Zaps can create new items in an app or update existing items. The output returned should be an object containing individual fields that will be parsed for mapping into subsequent Zap steps.

## 2. Search actions

_Search_ actions find existing items in an app and can optionally be paired with _create_ actions to add a new item if the search does not return a result.

Search actions let users do more with the data they’ve already added to your app; such as avoiding adding duplicate items or look up info about an item, for example weather, conversion, and contact lookup, to use in a subsequent step. 

The output returned by a _search_ should be a JSON-formatted array sorted with the best match first. Only the first item will be returned. For no match found, a `200` with an empty array must be returned. 

Zapier strongly recommends against action steps that delete or remove data. To prevent data loss, action steps should only add or update data. If you are considering adding a delete action to your app, consider alternative actions for items such as deactivating, unsubscribing, or canceling, instead of deleting items completely.