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

**What error messages a user will see:**

- _“The app did not respond in-time. It may or may not have completed successfully.”_
- _"Problem creating Sample: Our computers ran into a problem"_
- _“We couldn't find any more x. Create a new x in your account and try again.”_

**Best practice:** The Zap editor will only process three new records at a time for sample data, so one way of making sure you can finish in time is by limiting your results to just three records. As this request might look different than a normal request when a Zap is running (especially for a REST Hook trigger), you can leverage the bundle meta parameter `bundle.meta.isLoadingSample`. When that is set to `true`, you can know the user is in the Zap editor testing and can respond with a limited payload. More on `bundle.meta` properties [here](https://zapier.github.io/zapier-platform/cli#logs).

## Custom fields request

**Constraint:** If your trigger, action, or search supports retrieving custom fields from your API, you must be aware of both the 30 second and 1,000 field limits. You should also consider how a user will find and map data to a specific custom field if you provide a large number of custom fields.

**What errors a user will see:**

- Slow rendering of the step that includes your action
- Custom fields might not display
- The user will not see an error message, but not all output fields will be available for mapping in later steps

**Best practice:** We’ll offer how one integration works around both of these issues. [Hubspot](https://zapier.com/apps/hubspot/integrations) offers a CRM product, and users often have thousands of custom fields for Company records. In their **_Create Company_** action, they’ve taken this innovative approach. Instead of presenting an overwhelming number of custom fields, they present a set of default fields that all companies have, then allow the user to select the other fields they might need from an **_Additional Properties to Retrieve_** dropdown menu field. Those fields chosen are then subsequently retrieved by the Zap editor for mapping. This helps in both making sure the request can be accomplished within the time limit, and also making sure the user can easily find the custom fields important to their specific workflow.

![](https://cdn.zappy.app/4ac409c47f194303c54adff79fcd693f.png)

## Zap startup (polling triggers)

**Constraint:** When a user clicks the “On” button of a Zap, Zapier does some additional initialization that must be accomplished in 30 seconds. First, it tests the user’s authentication to your service. Then it uses your default perform method to build a deduplication table of records so that the Zap will not run for existing records. More on that process is [here](https://platform.zapier.com/legacy/dedupe).

**What errors a user will see:**

- Users will receive an email with an error message about not being able to enable their Zap

**Best practice:** There is also a `bundle.meta` property that you can take advantage of here, `bundle.meta.isPopulatingDedupe`. When this is set to `true`, you can know the Zap is being enabled and create a distinct request. One option you might want to consider is loading more records into the Zap’s deduplication table than you usually request in your `perform`. This is especially relevant for an API that might return an inadvertent older record in your request. As the deduplication process only uses the id property of each record, you can also limit the data returned here to retrieve more records in the 30 second limit.

**Example:** The [Salesforce](https://zapier.com/apps/salesforce/integrations) integration has an **_Updated Field on Record_** trigger. It can fire on older records that a user might not consider appropriate for their running Zap. To help mitigate this, the integration downloads up to 104,000 records to the deduplication table during Zap startup.

# Zap step execution

Once a Zap is enabled, then a different set of constraints and best practices come into play. This is true of the Zapier run-time, but also usually true of your integration and its API requests. We’ll touch on both.

## Timeouts (triggers)

**Constraint:** Once a user's Zap is running, each time the Zap is run, the trigger step must finish processing in 30 seconds. Polling triggers run based on a user's Zapier plan, REST Hook Triggers run on an inbound POST to their subscription URL.

**What errors a user will see:**

- User will receive an email with an error message about the trigger error

**Best practice:** For polling, reducing the number of records you retrieve can help. If you have multiple requests per record, another option is to use the Zapier platform dehydration service to lazily complete the full record. These additio

## Timeouts (actions)

**Constraint:** Sometimes an API request can’t be finished within 30 seconds - the rendering of a file conversion is a good example of this.

**What errors a user will see:**

- An error in the Zap history of their Zap due to the request timing out

**Best practice:** To help with this kind of problem, the Zapier platform provides a webhook-based callback service. This allows your action to be performed asynchronously, and when finished, POST to the callback URL. The Zap will be put in waiting mode until this POST. More on utilizing this method [here](https://github.com/zapier/zapier-platform/tree/master/packages/cli#zgeneratecallbackurl).

**What a user will see:**

- Zap will have Waiting/Delayed status in Zap history until the POST is received.

## Reducing requests to your API

**Constraint:** Each time a Zap runs and your integration is invoked can mean multiple requests to your API endpoints, depending on what your trigger/action seeks to accomplish. This can mean hundreds of requests/hour based on a Zapier customer plan, or thousands based on a Zap with an active RESThook Trigger.

**Best practice:** One way to reduce that API load is via the dehydration feature mentioned earlier. A pointer is created for any subsequent requests that might need to happen, and these will only be made if the Zap needs a hydrated property in a later step.

This is especially true for polling triggers that might require an additional request to create a full record. By putting these secondary requests behind a dehydration pointer, Zapier will only make this request once, although it might see these same records again and again based on the Zap’s polling cycle.

More on dehydration [here](https://github.com/zapier/zapier-platform/tree/master/packages/cli#dehydration).

## Reducing file requests

**Constraint:** Each time a Zap step requests a file from your API, it will be accessed and downloaded.

**Best practice:** Much like data dehydration, you can implement a file request using [dehydration](https://github.com/zapier/zapier-platform/tree/master/packages/cli#file-dehydration), so again the file will only be accessed and downloaded when a later Zap step asks for it.

To make this even more efficient, you can [stash the file](https://github.com/zapier/zapier-platform/tree/master/packages/cli#stashing-files) at Zapier. Rather than provide the file to the requesting step, Zapier will stash the file (under a dehydrated URL), so that only one request will ever be made for the file from your API.

# Throttling

There are a number of throttles that a Zapier user could encounter when using your integration, including those set by your API.

## Throttling (your API)

**Constraint:** Your API has request limits

**What errors a user will see:**

- If a trigger, user will receive an email with an error message about the trigger error
- If an action, user will see an error in Zap history

**Best practice:** You can add a specific 429 `Retry-After` header to your response, or add a timed delay in your error response. Instead of a user’s Zap erroring and halting, the request will be retried at the specified time. More on the retry [here](https://github.com/zapier/zapier-platform/tree/master/packages/cli#handling-throttled-requests).

## Webhook throttles (Zapier)

**Constraint:** Zapier’s current limits are [here](https://zapier.com/help/troubleshoot/behavior/rate-limits-and-throttling-in-zapier#step-4). We will issue a 429 response when your integration exceeds these throttle limits.

**What errors a user will see:**

- If a trigger, user will receive an email with an error message about the trigger error
- If an action, user will see error in Zap history

**Best practice:** You should support a retry/back-off schedule to make sure the data is eventually received.

## Polling trigger throttle (Zapier)

**Constraint:** There is a default limit of 100 returned items/poll.

**What errors a user will see:**

- The user will receive an email about the held Zap runs, as well as a banner with the same information in their Zap history.

**Best practice:** If your trigger will be returning > 100 new records consistently, we’d encourage you to look at these two options:
Converting your trigger to be RESThook based. Webhook limits are much expanded (up to 10,000 requests in a 5 minute period).
Add support for Transfer. This is a new service that supports paging so users can select and send up to 25,000 records: https://platform.zapier.com/docs/transfer

# Important Zapier constraints

| Time Limits                                                 |            |
| ----------------------------------------------------------- | ---------- |
| Zap Editor test step: request(s) + scripting                | 30 seconds |
| Polling trigger: request(s) + scripting                     | 30 seconds |
| Create/search action: requests(s) + scripting + scripting   | 30 seconds |
| REST Hook trigger: payload processing scripting + scripting | 30 seconds |

| Size limits         |                      |
| ------------------- | -------------------- |
| Deduplication table | 105,000 rows per Zap |
| Custom fields       | 1000                 |
| Webhook payload     | 10 MB                |
| Response payload    | 6 MB                 |
| Downloaded files    | ~120 MB              |

| Throttles         |                             |
| ----------------- | --------------------------- |
| Polling trigger   | Default: 100 new items/poll |
| REST Hook trigger | 10000 webhooks/5 minutes    |
|                   | 30 webhooks/second          |

More on throttles [here](https://zapier.com/help/troubleshoot/behavior/rate-limits-and-throttling-in-zapier#step-3).

Integration IP Address assignment: [AWS-East](https://zapier.com/help/troubleshoot/behavior/cant-access-or-use-zapier-with-other-apps)
