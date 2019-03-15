---
title: How Does Zapier Work?
order: 1
layout: post-toc
redirect_from: /docs/
---

## How Does Zapier Work?

All new Zapier integrations are built using Zapier Platform v3, the latest version of our development platform. You can build an integration using Zapier's Platform CLI, a command line interface to build integrations in JavaScript code from your local development environment. Or, you could build integrations using Zapier Platform UI, an online visual builder to create integrations in a form layout.

Both interfaces use the same Zapier Platform and function the same internally. In general, Zapier integrations include definitions of API calls for triggers that watch for new and updated data, searches that request specific data, and create actions that send new data to an API. Zapier bundles your app definition along with any input data received from users in life Zaps, prepares API requests, includes authentication details, and makes the API call. Zapier then parses the API response for individual fields and deduplicates the results from Trigger and Search steps that expect an array of results.

Zapier will then take action depending on the step. For triggers, if the item is new, Zapier then runs the remaining Zap steps. For searches, if an item exists, Zapier will perform resource hydration, parse its details and run subsequent steps in the Zap; if it does not exist, Zapier may stop the Zap or run a create action to add that item, depending on user selection in the Zap setup. For actions, Zapier will return the results after creating the item, and either run subsequent steps in the Zap if the Zap includes additional steps, or stop the Zap and log this run of the Zap as successful.

Here's a diagram example of how this works with a trigger step; search and create steps work similarly with their differing final steps as outlined above:

![Zapier Platform Diagram](https://cdn.zapier.com/storage/photos/54fe2e91170f3337ed8648ec29e97aaf.png)

Trigger steps's internal workflow differs if triggered with a rest hook as well.

See [Zapier's Platform CLI documentation](https://zapier.github.io/zapier-platform-cli/#getting-started) for more detail on how Zapier integrations work.

***

# How Zapier Legacy Web Builder Works

> **Note**: The following only applies to integrations built with Zapier's legacy web builder.

For integrations built with Zapier's [Platform v2]({{base_url}}versions/#version-2-2015-07-31)'s legacy web builder, the following diagrams show how Zapier trigger and action calls work.

## Triggers

To reduce visual noise, assume `KEY` or `TK` is the key you define for your trigger.

### Polling

The methods mentioned here can be seen in more detail in the [Available Methods for Polling doc](https://zapier.com/developer/documentation/v2/available-methods/#polling).

<img src="https://cdn.zapier.com/storage/photos/952e19287daf24693988e64e547d5051.png" alt="Diagram of how Polling Triggers work" style="border: none">

### REST Hooks

> The methods mentioned here can be seen in more detail in the [Available Methods for REST Hooks doc](https://zapier.com/developer/documentation/v2/available-methods/#static-and-rest-hooks).

> NOTE: This diagram excludes the [subscription process](https://zapier.com/developer/documentation/v2/rest-hooks/#step-1-subscribe-smallema-call-from-zapier-to-your-appemsmall) as that will just happen once the Zap’s turned on.

1. Your API makes an HTTP request to Zapier
2. `TK_catch_hook` is called
3. Zapier parses the received data and triggers on it

<img src="https://cdn.zapier.com/storage/photos/d88a35691254c08215cdb3c7e1ba1ca4.png" alt="Diagram of how REST Hook Triggers work" style="border: none">

### Notification REST Hooks

> The methods mentioned here can be seen in more detail in the [Available Methods for Notification REST Hooks doc](https://zapier.com/developer/documentation/v2/available-methods/#notification-rest-hooks).

> NOTE: This diagram excludes the [subscription process](https://zapier.com/developer/documentation/v2/notification-rest-hooks/#step-1-subscribe-smallema-call-from-zapier-to-your-appemsmall) as that will just happen once the Zap’s turned on.

1. Your API makes an HTTP request to Zapier (with the URL for the "GET Resource" call)
2. Zapier builds an HTTP request for the "GET Resource" call
3. `TK_pre_hook` is called
4. Zapier makes the HTTP Request for the "GET Resource" call
5. Your API receives a request and sends back a response
6. `TK_post_hook` is called
7. Zapier parses the received data and triggers on it

<img src="https://cdn.zapier.com/storage/photos/918e49e175c7e6e27d2c85f0f6487ce2.png" alt="Diagram of how Notification REST Hook Triggers work" style="border: none">

## Actions

To reduce visual noise, assume `AK` is your `ACTION_KEY` (what you define as your action’s key) and `SK` is your `SEARCH_KEY` (what you define as your search’s key).

### Writes

> The methods mentioned here can be seen in more detail in the [Available Methods for Actions doc](https://zapier.com/developer/documentation/v2/available-methods/#action-methods).

1. Zapier builds an HTTP Request
2. If `AK_write` exists, it's called (and will override steps 3 through 6)
3. `AK_pre_write` is called
4. Zapier makes the HTTP Request
5. Your API receives a request and sends back a response
6. `AK_post_write` is called
7. Zapier parses the received data, and makes it available for subsequent steps in the Zap

<img src="https://cdn.zapier.com/storage/photos/226846474b0341c4f910a509897abe75.png" alt="Diagram of how Actions work" style="border: none">

> NOTE: If you have the Custom Action Fields URL defined, there are a couple of additional calls to `AK_pre_custom_action_fields` and `AK_post_custom_action_fields` after 2 and before 3.

> NOTE 2: If this write runs as part of a `search_or_write`, there are a couple of additional calls to `SK_read_resource` OR `SK_pre_read_resource` and `SK_post_read_resource` after 6 and before 7, to make sure the output there is the same as the search.

### Searches

> The methods mentioned here can be seen in more detail in the [Available Methods for Searches doc](https://zapier.com/developer/documentation/v2/available-methods/#search-methods).

1. Zapier builds an HTTP Request
2. If `SK_search` exists, it's called (and will override steps 3 through 6)
3. `SK_pre_search` is called
4. Zapier makes the HTTP Request
5. Your API receives a request and sends back a response
6. `SK_post_search` is called
7. If a [Resource URL]({{base_url}}reference/#resource-url) is not set, Zapier skips to step 13
8. If `SK_read_resource` exists, it’s called (and will override steps 8 through 12)
9. Zapier builds an HTTP Request for the “GET Resource” call
10. `SK_pre_read_resource` is called
11. Zapier makes the HTTP Request for the "GET Resource" call
12. Your API receives a request and sends back a response
13. `SK_post_read_resource` is called
14. Zapier parses the received data, and makes it available for subsequent steps in the Zap

<img src="https://cdn.zapier.com/storage/photos/c1b25709ce79c0037a8c2c45b3e952fd.png" alt="Diagram of how Searches work" style="border: none">

> NOTE: If you have the Custom Search Fields URL defined, there are a couple of additional calls to `SK_pre_custom_search_fields` and `SK_post_custom_search_fields` after 2 and before 3