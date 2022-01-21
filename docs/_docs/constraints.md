---
title: Zapier Operating Constraints
order: 16
layout: post-toc
redirect_from: /platform_wide/
---

# Zapier operating constraints and your integration

Zapier offers a relatively unique run-time environment for your integration and its requests to your API. The environment is stateless and restricts both execution time and payload size to offer normalized reliability and running time. There are three distinct contexts of this run-time that your integration will need to run within.

- Zap step setup using the Zap editor
- Zap startup
- Zap step execution when a Zap runs

This document exposes various operating constraints of these run-time modes, errors users and your integration could run into, as well as best practices. This information is targeted towards users of our CLI development environment, but many of the strategies can be used in code mode in our Platform UI.

Many errors can be viewed in your integration's log monitoring in the [Platform UI](https://platform.zapier.com/docs/testing#monitoring), or if using the [CLI](https://platform.zapier.com/cli_docs/docs#handling-throttled-requests#logs), using `zapier logs`.

# Zap step setup using the Zap editor

There are three areas where a user will interact with your integration in the Zap Editor:

- Testing
- Configuration with custom fields
- Zap Startup

## Testing

All steps added to a Zap have a test step function to help the user verify their configuration by providing sample response data from your integration. Triggers are somewhat distinct, as their test step can provide multiple sample records a user can choose from.

## Timeouts (triggers)

**Constraint:** When a user clicks **Test Trigger** in the Zap editor the output of your `perform` (polling) or `performList` (REST Hook) must be returned within 30 seconds.

**What error messages a user could see if constraint hit:**

- _“The app did not respond in-time. It may or may not have completed successfully.”_
- _"Problem creating Sample: Our computers ran into a problem"_
- _“We couldn't find any more x. Create a new x in your account and try again.”_

**Best practice:** The Zap editor will only process three new records at a time for sample data, so one way of making sure you can finish in time is by limiting your results to just three records. As this request might look different than a normal request when a Zap is running (especially for a REST Hook trigger), you can leverage the bundle meta parameter `bundle.meta.isLoadingSample`. When that is set to `true`, you can know the user is in the Zap editor testing and can respond with a limited payload. More on `bundle.meta` properties [here](https://platform.zapier.com/cli_docs/docs#bundlemeta).

## Payload size (triggers)

**Constraint:** When a user clicks **Test Trigger** in the Zap editor the output of both your request and the `perform` (polling) or `performList` (REST Hook) method must be less than 6MB.

**What error messages a user could see if constraint hit:**

- _“Scripting payload too large ('n' bytes but max is 6291456bytes).”_ - 'n' being be the number of bytes of your payload

**Best practice:** The Zap editor will only process three new records at a time for sample data, so one way of making sure your minimize your payload size is by limiting your results to just three records. As this request might look different than a normal request when a Zap is running (especially for a REST Hook trigger), you can leverage the bundle meta parameter `bundle.meta.isLoadingSample`. When that is set to `true`, you can know the user is in the Zap editor testing and can respond with a limited payload. More on `bundle.meta` properties [here](https://platform.zapier.com/cli_docs/docs#bundlemeta).

## Timeouts (actions/searches)

**Constraint:** When a user clicks **Test and Review** or **Retest and Review** in the Zap editor the output of your `perform` must be returned within 30 seconds.

**What error messages a user could see if constraint hit:**

- _“The app did not respond in-time. It may or may not have completed successfully.”_

**Best practice:**
Options will depend on whether the timeout issue is your API endpoint or the `perform` method processing the response payload. One `perform` technique we have seen help is the reduction of `z.console.log` calls, especially in looping code.

## Payload size (actions/searches)

**Constraint:** When a user clicks **Test and Review** or **Retest and Review** in the Zap editor the output of both your request and the `perform` method must be less than 6MB.

**What error messages a user could see if constraint hit:**

- _“Scripting payload too large ('n' bytes but max is 6291456bytes).”_ - 'n' being be the number of bytes of your payload

**Best practice:** If your API endpoints supports this, one option is to provide input filter fields in the action/search so a user can decide what record data they want to return. If that is not available, you might look at having multiple endpoints for this record data. Your integration could then provide multiple action/searches for the user so they can get a full record.

## Step configuration with custom fields

**Constraint:** If your trigger, action, or search supports retrieving custom fields from your API, you must be aware of both a 30 second and 1,000 field limit. You should also consider how a user will find and map data to a specific custom field if you provide a large number of custom fields.

**What errors a user could see if constraints hit:**

- _“Scripting payload too large ('n' bytes but max is 6291456bytes).”_ - 'n' being be the number of bytes of your payload
  _“The app did not respond in-time. It may or may not have completed successfully.”_
- Slow rendering of the step that includes your action
- Custom fields might not display
- Not all output fields will be available for mapping in later steps

**Best practice:** We’ll offer how one integration works around both of these issues. [Hubspot](https://zapier.com/apps/hubspot/integrations) offers a CRM product, and users often have thousands of custom fields for Company records. In their **_Create Company_** action, they’ve taken this innovative approach. Instead of presenting an overwhelming number of custom fields, they present a set of default fields that all companies have, then allow the user to select the other fields they might need from an **_Additional Properties to Retrieve_** dropdown menu field. Those fields chosen are then subsequently retrieved by the Zap editor for later mapping in subsequent steps. This helps in both making sure the request can be accomplished within the time limit, and also making sure the user can easily find the custom fields important to their specific workflow.

![](https://cdn.zappy.app/4ac409c47f194303c54adff79fcd693f.png)

# Zap startup

## Timeouts and payload size (polling triggers)

**Constraint:** When a user clicks the “On” button of a Zap, Zapier does some additional initialization that must be accomplished in 30 seconds. First, it tests the user’s authentication to your service. Then it uses your default perform method to build a deduplication table of records so that the Zap will not run for existing records. More on that process is [here](https://platform.zapier.com/legacy/dedupe). The payload returned from this request must also be less than 6 MB.

**What errors a user will see if constraint hit:**

- Users will receive an email with an error message that includes the text _"could not be switched on"_.

**Best practice:** There is also a `bundle.meta` property that you can take advantage of here, `bundle.meta.isPopulatingDedupe`. When this is set to `true`, you can know the Zap is being enabled and create a distinct request. As the deduplication process only uses the id property of each record, one option you might want to consider in this request is filtering the fields you return to reduce record size. This can have two distinct benefits, albeit in somewhat opposite directions. For those requests that can exceed timeout or size limits, you can make sure your filtered request is successful. If your filtered request has a lot of headroom (both time and size), you could instead use this to load more records into the Zap’s deduplication table than you usually request in your `perform`. This is especially relevant for an API that might return an inadvertent older record in a normal request.

**Example:** The [Salesforce](https://zapier.com/apps/salesforce/integrations) integration has an **_Updated Field on Record_** trigger. It can fire on older records that a user might not consider appropriate for their running Zap. To help mitigate this, the integration uses a distinct filtered request to download up to 104,000 records to the deduplication table during Zap startup.

# Zap step execution

Once a Zap is enabled, then a different set of constraints and best practices come into play. This is true of the Zapier run-time, but also usually true of your integration and its API requests. We’ll touch on both.

## Timeouts (triggers)

**Constraint:** Each time a Zap executes the trigger's `perform` (polling) method must finish processing in 30 seconds. Polling triggers run on an interval based on a user's Zapier plan, REST Hook triggers run on an inbound POST to their subscription URL.

**What errors a user will see if constraint hit:**

- User will receive an email with an error message, usually with _"Trigger Partner Failure"_ in the message text. An example of the email sent to when the trigger errors due to a timeout:

![](https://cdn.zappy.app/17cc8fb9313f8b0920a7ccd6dd95e9b0.png)

**Best practice:**

- For polling triggers, reducing the number of records per poll (much like the sample example earlier)
- For both types of triggers, optimizing `perform` scripting you have for manipulating the payload
- Using [console logging](https://platform.zapier.com/cli_docs/docs#console-logging) can help you determine where the issue might lie. One thing to look out for here, too much console logging can also cause timeouts due to round trip HTTP calls for each log message.
- If you have multiple requests per record that are causing timeouts, another option is to use the Zapier platform dehydration service, as explained [here](https://platform.zapier.com/cli_docs/docs#dehydration). Instead of making the request directly, a dehydration pointer is created, and this pointer will only be resolved if the Zap needs a hydrated property in a later step.
- Dehydration provides one other advantage - if there is an error in trying to hydrate the request, the error will be exposed in Zap History and the Zap can be replayed from there.

## Payload size (polling triggers)

**Constraint:** Each time a Zap executes, the trigger's response payload must be less than 6MB.

**What error messages a user could see if constraint hit:**

- User will receive an email with an error message, usually with _"Trigger Partner Failure"_ in the message text.

**Best practice:**

- If your API endpoints supports this, one option is to provide input filter fields in the trigger so a user can decide what record data they want to return.
- If that is not available, you might look at having multiple API endpoints for this record data. Your integration could then provide a trigger for notification of a new/updated record that includes standard record keys. Then for the other endpoints, use the Zapier platform dehydration service, as explained [here](https://platform.zapier.com/cli_docs/docs#dehydration). Instead of making one large request, a dehydration pointer is created for each smaller request, and this pointer will only be resolved if the Zap needs a hydrated property in a later step.
- Dehydration provides one other advantage - if there is an error in trying to hydrate the request, the error will be exposed in Zap History and the Zap can be replayed from there.

## Payload size (REST Hook triggers)

**Constraint:** A POST to to a trigger's REST Hook subscription URL must be less than 10 MB.

**What error messages a user could see if constraint hit:**

- User will receive an email with an error message, usually with _"Trigger Partner Failure"_ in the message text.

**Best practice:**

- If your REST Hook subscription endpoint supports this, one option is to provide input filter fields in the trigger so a user can decide what record data they want to return.
- If that is not available, you might look at supporting a notification style REST Hook that includes minimal keys. Then for the rest of the record data, use the Zapier platform dehydration service, as explained [here](https://platform.zapier.com/cli_docs/docs#dehydration). A dehydration pointer is created for each subsequent request, and this pointer will only be resolved if the Zap needs a hydrated property in a later step.
- Dehydration provides one other advantage. If there is an error in trying to hydrate the request, the error will be exposed in Zap History and the Zap can be replayed from there.

## Timeouts (actions)

**Constraint:** Sometimes an API request will never be finished within 30 seconds - the rendering of a file conversion is a good example of this.

**What errors a user will see if constraint hit:**

- An error in the Zap history of their Zap due to the request timing out

**Best practice:** To help with this kind of problem, the Zapier platform provides a webhook-based callback service. This allows your action to be performed asynchronously, and when finished, POST to the callback URL. The Zap will be put in waiting mode until this POST. More on utilizing this method [here](https://platform.zapier.com/cli_docs/docs#zgeneratecallbackurl).

**What a user will see:**

- Zap will have Waiting/Delayed status in Zap history until the POST is received.

## Payload size (actions/searches)

**Constraint:** When a user clicks **Test and Review** or **Retest and Review** in the Zap editor your response payload must be less than 6MB.

**What error messages a user could see if constraint hit:**

- _“Scripting payload too large ('n' bytes but max is 6291456bytes).”_

**Best practice:** If your API endpoints supports this, one option is to provide input filter fields in the action/search so a user can decide what record data they want to return. If that is not available, you might look at having multiple endpoints for this record data. Your integration could then provide multiple action/searches for the user so they can get a full record.

## Reducing requests to your API

**Constraint:** Each time a Zap runs and your integration is invoked can mean multiple requests to your API endpoints, depending on what your trigger/action seeks to accomplish. This can mean hundreds of requests/hour based on a Zapier customer plan, or thousands based on a Zap with an active REST Hook Trigger.

**Best practice:** One way to reduce that API load is via the Zapier platform dehydration feature mentioned earlier. By putting these secondary requests behind a dehydration pointer, Zapier will only make this request once, although it might see these same records again and again based on the Zap’s polling cycle.

More on dehydration again [here](https://platform.zapier.com/cli_docs/docs#dehydration).

## Reducing file requests to your API

**Constraint:** Each time a Zap step requests a file from your API, it will be accessed and downloaded.

**Best practice:** Much like data dehydration, you can implement a file request using [dehydration](https://platform.zapier.com/cli_docs/docs#zgeneratecallbackurl#file-dehydration), so again the file will only be accessed and downloaded when a later Zap step asks for it.

To make this even more efficient, you can [stash the file](https://platform.zapier.com/cli_docs/docs#stashing-files) at Zapier. Rather than provide the file to the requesting step, Zapier will stash the file (under a dehydrated URL), so that only one request will ever be made for the file from your API.

# Throttling

There are a number of throttles that a Zapier user could encounter when using your integration, including those set by your API.

## Throttling (your API)

**Constraint:** Your API has request limits

**What errors a user will see if constraint hit:**

- If a trigger, user will receive an email with an error message about the trigger error
- If an action, user will see an error in Zap history

**Best practice:** You can add a specific 429 `Retry-After` header to your response, or add a timed delay in your error response. Instead of a user’s Zap erroring and halting, the request will be retried at the specified time. More on the retry [here](https://platform.zapier.com/cli_docs/docs#handling-throttled-requests). The user will see this message in Zap History instead of an error while the limit is still in place:
![](https://cdn.zappy.app/0933736266259b11771a0eba0aff23ce.png)

## Webhook throttles (Zapier)

**Constraint:** Zapier’s current webhook limits are [here](https://zapier.com/help/troubleshoot/behavior/rate-limits-and-throttling-in-zapier#step-4). We will issue a 429 response when your integration exceeds these throttle limits.

**What errors a user will see:**

- If a trigger, user will receive an email with an error message about the trigger error
- If an action, user will see error in Zap history

**Best practice:** You should support a retry/back-off schedule to make sure the data is eventually received.

## Polling trigger throttle (Zapier)

**Constraint:** There is a default limit of 100 returned items/poll.

**What errors a user will see if constraint hit:**

- The user will receive an email about held Zap runs, as well as a banner with the same information in their Zap history.

**Best practice:** If your trigger will be returning > 100 new records consistently, we’d encourage you to look at these two options:

- Converting your trigger to be REST Hook based. Webhook limits are much expanded (up to 10,000 requests in a 5 minute period).
- Add support for Transfer. This is a new Zapier service that supports paging so users can create a Zap tp select and batch transfer up to 25,000 records at one time. More [here](https://platform.zapier.com/docs/transfer).

# Important Zapier constraints summary

| Time Limits                                                |            |
| ---------------------------------------------------------- | ---------- |
| Zap Editor test step: request(s) + scripting               | 30 seconds |
| Polling trigger: request(s) + scripting                    | 30 seconds |
| REST Hook trigger: ingest and payload processing scripting | 30 seconds |
| Create/search action: requests(s) + scripting              | 30 seconds |

| Size limits           |                      |
| --------------------- | -------------------- |
| Deduplication table   | 105,000 rows per Zap |
| Custom fields         | 1000                 |
| Webhook payload       | 10 MB                |
| HTTP response payload | 6 MB                 |
| Downloaded files      | ~120 MB              |

| Throttles                                                                                                           |                             |
| ------------------------------------------------------------------------------------------------------------------- | --------------------------- |
| Polling trigger                                                                                                     | Default: 100 new items/poll |
| REST Hook trigger                                                                                                   | 10000 webhooks/5 minutes    |
|                                                                                                                     | 30 webhooks/second          |
| More on throttles [here](https://zapier.com/help/troubleshoot/behavior/rate-limits-and-throttling-in-zapier#step-3) |                             |

| TCP/IP                  |                                                                                                     |
| ----------------------- | --------------------------------------------------------------------------------------------------- |
| Integration assigned IP | [AWS-East](https://zapier.com/help/troubleshoot/behavior/cant-access-or-use-zapier-with-other-apps) |
