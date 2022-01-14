---
title: Zapier Operating Constraints
order: 16
layout: post-toc
redirect_from: /platform_wide/
---

# Zapier operating constraints and your integration

Zapier offers a relatively unique run-time environment for your integration and its requests to your API. The environment is stateless and restricts both execution time and payload size to offer normalized reliability and running time. There are two distinct contexts of this run-time that your integration will need to run within:

- Zap step setup using the Zap editor
- Zap step execution when a Zap runs

This document exposes various operating constraints of these run-time modes, errors users and your integration could run into, as well as best practices. This information is targeted towards users of our CLI development environment, but many of the strategies can be used in code mode in our Platform UI.

Integration log monitoring can be viewed in the [Platform UI](https://platform.zapier.com/docs/testing#monitoring), or if using the [CLI](https://zapier.github.io/zapier-platform/cli#logs), using `zapier logs`.

# Zap step setup using the Zap editor

There are three areas where a user will interact with your integration when they add a trigger, action, or search step in their Zap.

## Test step (all triggers)

**Constraint:** When a user clicks **Test Trigger** in the Zap editor the output of your `perform` (polling) or `performList` (REST Hook) must be returned within 30 seconds.

**What errors a user might see:**

- _“The app did not respond in-time. It may or may not have completed successfully.”_
- _"Problem creating Sample: Our computers ran into a problem"_
- _“We couldn't find any more x. Create a new x in your account and try again.”_

**Best practice:** The Zap editor will only process three new records at a time for sample data, so one way of making sure you can finish in time is by limiting your results to just three records. As this request might look different than a normal request when a Zap is running (especially for a REST Hook trigger), you can leverage the bundle meta parameter `bundle.meta.isLoadingSample`. When that is set to `true`, you can know the user is in the Zap editor testing and can respond with a limited payload. More on `bundle.meta` properties [here](https://zapier.github.io/zapier-platform/cli#logs).

## Custom fields request

**Constraint:** If your trigger, action, or search supports retrieving custom fields from your API, you must be aware of both the 30 second and 1,000 field limits. You should also consider how a user will find and map data to a specific custom field if you provide a large number of custom fields.

**What errors a user might see:**

- Slow rendering of the step that includes your action
- Custom fields might not display
- The user will not see an error message, but not all output fields will be available for mapping in later steps

**Best practice:** We’ll offer how one integration works around both of these issues. [Hubspot](https://zapier.com/apps/hubspot/integrations) offers a CRM product, and users often have thousands of custom fields for Company records. In their **_Create Company_** action, they’ve taken this innovative approach. Instead of presenting an overwhelming number of custom fields, they present a set of default fields that all companies have, then allow the user to select the other fields they might need from an **_Additional Properties to Retrieve_** dropdown menu field. Those fields chosen are then subsequently retrieved by the Zap editor for mapping. This helps in both making sure the request can be accomplished within the time limit, and also making sure the user can easily find the custom fields important to their specific workflow.

![](https://cdn.zappy.app/4ac409c47f194303c54adff79fcd693f.png)

## Zap startup (polling triggers)

**Constraint:** When a user clicks the “On” button of a Zap, Zapier does some additional initialization that must be accomplished in 30 seconds. First, it tests the user’s authentication to your service. Then it uses your default perform method to build a deduplication table of records so that the Zap will not run for existing records. More on that process is [here](https://platform.zapier.com/legacy/dedupe).

**What errors a user might see:**

- Users will receive an email with an error message about not being able to enable their Zap

**Best practice:** There is also a `bundle.meta` property that you can take advantage of here, `bundle.meta.isPopulatingDedupe`. When this is set to `true`, you can know the Zap is being enabled and create a distinct request. One option you might want to consider is loading more records into the Zap’s deduplication table than you usually request in your `perform`. This is especially relevant for an API that might return an inadvertent older record in your request. As the deduplication process only uses the id property of each record, you can also limit the data returned here to retrieve more records in the 30 second limit.

**Example:** The [Salesforce](https://zapier.com/apps/salesforce/integrations) integration has an **_Updated Field on Record_** trigger. It can fire on older records that a user might not consider appropriate for their running Zap. To help mitigate this, the integration downloads up to 104,000 records to the deduplication table during Zap startup.
