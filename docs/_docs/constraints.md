---
title: Zapier Operating Constraints
order: 17
layout: post-toc
redirect_from: /platform_wide/
---

# Zapier operating constraints and your integration

Zapier offers a relatively unique run-time environment for your integration and its requests to your API. The environment is stateless and restricts both execution time and payload size to offer normalized reliability and running time. There are three distinct contexts of this run-time that your integration will need to run within.

- Zap step setup using the Zap editor
- Zap startup
- Zap step execution when a Zap runs

This document exposes various operating constraints of these run-time modes, errors users and your integration could run into, and best practices. This information is targeted towards users of our CLI development environment, but many of the strategies can be used in [Code Mode](./faq#codemode) in our Platform UI.

Many errors can be viewed in your integration's log monitoring in the [Platform UI](https://platform.zapier.com/docs/testing#monitoring), or if using the [CLI](https://platform.zapier.com/cli_docs/docs#handling-throttled-requests#logs), using `zapier logs`.

# Zap step setup using the Zap editor

There are three areas where a user will interact with your integration in the Zap Editor:

- Testing
- Configuration with custom fields
- Zap Startup

## Testing

When users add steps to their Zaps using your integration, they have the opportunity to test the step to help them verify their configuration, which uses sample response data from your integration. Trigger test steps can provide multiple sample records a user can choose from.

## Timeouts (triggers)

**Constraint:** When a user clicks **Test Trigger** in the Zap editor, the output of your `perform` (polling) or `performList` (REST Hook) must be returned within 30 seconds.

**Error messages a user could see if constraint is hit:**

- _“The app did not respond in-time. It may or may not have completed successfully.”_
- _"Problem creating Sample: Our computers ran into a problem"_
- _“We couldn't find any more x. Create a new x in your account and try again.”_

**Best practice:** The Zap editor will only process three new records at a time for sample data, so one way of speeding up the response is by limiting your results to three records. To determine when the request is for sample data, use the bundle meta parameter `bundle.meta.isLoadingSample`. When that is set to `true`, the user is testing in the Zap editor, and your integration can respond with a limited payload. More on `bundle.meta` properties [here](https://platform.zapier.com/cli_docs/docs#bundlemeta).

## Payload size (triggers)

**Constraint:** When a user clicks **Test Trigger** in the Zap editor, the response payload must be less than 6MB.

**Error messages a user could see if constraint is hit:**

- _“Scripting payload too large ('n' bytes but max is 6291456bytes).”_ - ('n' is the number of bytes in the payload.)

**Best practice:** The Zap editor will only process three new records at a time for sample data, so one way of making sure your payload size is less than the limit is by limiting your results to three records. To determine when the request is for sample data, use the bundle meta parameter `bundle.meta.isLoadingSample`. When that is set to `true`, the user is testing in the Zap editor, and your integration can respond with a limited payload. More on `bundle.meta` properties [here](https://platform.zapier.com/cli_docs/docs#bundlemeta).

## Timeouts (actions/searches)

**Constraint:** When a user clicks **Test and Review** or **Retest and Review** in the Zap editor, the output of your `perform` must be returned within 30 seconds.

**Error messages a user could see if constraint is hit:**

- _“The app did not respond in-time. It may or may not have completed successfully.”_

**Best practice:**
Timeouts can occur on your API endpoint, or within the `perform` method processing the response payload. To speed up the `perform`, check for expensive processing operations, and consider reducing `z.console.log` calls, especially in looping code.

## Payload size (actions/searches)

**Constraint:** When a user clicks **Test and Review** or **Retest and Review** in the Zap editor, the response payload must be less than 6MB.

**Error messages a user could see if constraint is hit:**

- _“Scripting payload too large ('n' bytes but max is 6291456bytes).”_ - ('n' is the number of bytes in the payload.)

**Best practice:** If your API endpoint supports request filtering, one option is to provide input fields in the action/search so a user can decide what record field data they want to return. If that is not available, you might look at having multiple endpoints for this record data. Your integration could then provide multiple action/searches for the user so they can get a full record.

## Step configuration with custom fields

**Constraint:** If your trigger, action, or search supports retrieving custom fields from your API, you are imited to 1000 custom fields.

**Error messages a user could see if constraint is hit:**

- Slow rendering of the step when it is added or edited in the Zap editor
- Custom fields might not display
- Not all output fields will be available for mapping in later steps

**Constraint:** If your trigger, action, or search supports retrieving custom fields from your API, the output of your method must be returned within 30 seconds.

**Error messages a user could see if constraint is hit:**

_“The app did not respond in-time. It may or may not have completed successfully.”_

**Constraint:** If your trigger, action, or search supports retrieving custom fields from your API, the response payload must be less than 6MB.

_“Scripting payload too large ('n' bytes but max is 6291456bytes).”_ - ('n' is the number of bytes in the payload.)

**Best practice:** Here is an example of the way one integration works around all three of these issues. [Hubspot](https://zapier.com/apps/hubspot/integrations) offers a CRM product, and users often have thousands of custom fields for Company records. In their **_Create Company_** action, instead of presenting an overwhelming number of custom fields, they present a set of default fields that all companies have, then allow the user to select the other fields they might need from an **_Additional Properties to Retrieve_** dropdown menu field. The fields chosen are then retrieved by the Zap editor for user editing. This helps in both making sure the request can be accomplished within the time and size limits, and making sure the user can easily find the custom fields important to their specific workflow.

![](https://cdn.zappy.app/4ac409c47f194303c54adff79fcd693f.png)

# Zap startup

## Timeouts and payload size (polling triggers)

**Constraint:** When a user clicks the “On” button of a Zap, Zapier does some additional initialization that must be accomplished in 30 seconds. First, it tests the user’s authentication to your service. Then it uses the trigger's `perform` method to build a deduplication table of records, so that the Zap will not run for existing records. More on that process is [here](./dedupe). The payload returned from this request must also be less than 6 MB.

**Errors a user will see if constraint is hit:**

- Users will receive an email with an error message that includes the text _"could not be switched on"_.

**Best practice:** There is also a `bundle.meta` property that you can take advantage of here, `bundle.meta.isPopulatingDedupe`. When this is set to `true`, the Zap is being enabled, and you can use that to create a distinct request. The deduplication process only uses the id property of each record, so one option to consider for this request is filtering the fields you return to reduce record size.
For those requests that might otherwise exceed timeout or size limits, you can make sure your filtered request is successful. Alternatively, If your filtered request has a lot of headroom in both time and size, you could instead use this to load more records into the Zap’s deduplication table than you usually request in your `perform`. This is especially relevant for an API that might return an inadvertent older record in a later polling request.

**Example:** The [Salesforce](https://zapier.com/apps/salesforce/integrations) integration has an **_Updated Field on Record_** trigger that can trigger on older records that a user might not consider relevant for their running Zap. To help mitigate this, the integration uses a filtered request to download up to 104,000 records to the deduplication table during Zap startup.

# Zap step execution

Once a Zap is enabled, while the time and size constraints remain the same, the needs of the requests are a bit different, so we'll touch on best practices during Zap execution below.

## Timeouts (triggers)

**Constraint:** Each time a Zap executes, the trigger's `perform` (polling) method must finish processing in 30 seconds. Polling triggers run on an interval based on a user's Zapier plan (usually between 1 and 15 minutes). REST Hook triggers run on an inbound POST to their subscription URL.

**Errors a user will see if constraint is hit:**

- User will receive an email with an error message, usually with _"Trigger Partner Failure"_ in the message text. An example of the email sent when the trigger errors due to a timeout:

![](https://cdn.zappy.app/17cc8fb9313f8b0920a7ccd6dd95e9b0.png)

**Best practices:**

- For polling triggers, if your API endpoint supports request filtering around number of records or datetime, using these to reduce the number of records returned
- For both types of triggers, optimize the `perform` scripting for manipulating the payload
- Use [console logging](https://platform.zapier.com/cli_docs/docs#console-logging) efficiently. It can help you determine where the issue might lie, but too much console logging can cause timeouts due to logging overhead.
- If you have multiple requests per record that are causing timeouts, use the Zapier platform dehydration functions, as explained [here](https://platform.zapier.com/cli_docs/docs#dehydration). Instead of making the request immediately, a dehydration pointer is created, and the request will be made if the Zap needs a hydrated property in a later step.

## Payload size (polling triggers)

**Constraint:** Each time a Zap executes, the trigger's response payload must be less than 6MB.

**Errors a user will see if constraint is hit:**

- User will receive an email with an error message, usually with _"Trigger Partner Failure"_ in the message text.

**Best practices:**

- If your API endpoint supports request filtering around number of records or datetime, using these to reduce the number of records returned
- If filtering isn't an option, consider using the simplest available endpoint on your API for the basic record data, and use Zapier platform [dehydration](https://platform.zapier.com/cli_docs/docs#dehydration) to request supplementary data. A dehydration pointer is created for each subsequent request, and this pointer will only be resolved if the Zap needs a hydrated property in a later step.

## Payload size (REST Hook triggers)

**Constraint:** A POST to to a trigger's REST Hook subscription URL must be less than 10 MB.

**Error messages a user could see if constraint is hit:**

- User will receive an email with an error message, usually with _"Trigger Partner Failure"_ in the message text.

**Best practices:**

- If your REST Hook subscription endpoint supports filtering, one option is to provide input fields in the trigger so a user can decide what record data they want to return.
- Consider sending a notification REST Hook that includes minimal record data. You can then use additional API endpoints and Zapier platform [dehydration](https://platform.zapier.com/cli_docs/docs#dehydration) to request the supplementary record data. A dehydration pointer is created for each subsequent request, and this pointer will only be resolved if the Zap needs a hydrated property in a later step.

## Timeouts (actions)

**Constraint:** A Zapier action API request cannot consistently be finished within 30 seconds - for example, file format conversion.

**Errors a user will see if constraint is hit:**

- An error in the Zap history of their Zap due to the request timing out

**Best practice:** Use the webhook-based callback service the Zapier platform provides. This allows your action to be performed asynchronously, and when finished, POST to the callback URL. More on using this method [here](https://platform.zapier.com/cli_docs/docs#zgeneratecallbackurl).

**What a user will see if callback service implemented:**

- Zap will have Waiting/Delayed status in Zap history until the POST is received.

## Payload size (actions/searches)

**Constraint:** An action/search response payload must be less than 6 MB.

**Error messages a user could see if constraint is hit:**

- _“Scripting payload too large ('n' bytes but max is 6291456bytes).”_ - ('n' is the number of bytes in the payload.)

**Best practice:** Consider using the simplest available endpoint on your API for the basic record data, and use Zapier platform [dehydration](https://platform.zapier.com/cli_docs/docs#dehydration) to request supplementary data. A dehydration pointer is created for each subsequent request, and this pointer will only be resolved if the Zap needs a hydrated property in a later step.

## Reducing requests to your API

**Constraint:** Each time a Zap runs and your integration is invoked can mean multiple requests to your API endpoints, depending on what your trigger/action seeks to accomplish. This can mean hundreds of requests/hour based on a Zapier customer plan, or thousands based on a Zap with an active REST Hook Trigger.

**Best practice:** One way to reduce that API load is via the Zapier platform dehydration feature mentioned earlier. By putting these secondary requests behind a dehydration pointer, Zapier will only make this request once, although it might see these same records again and again based on the Zap’s polling cycle. Dehydration provides one other advantage - if there is an error in trying to hydrate the request, the error will be exposed in Zap history and the Zap can be replayed from there.

More on dehydration again [here](https://platform.zapier.com/cli_docs/docs#dehydration).

## Reducing file requests to your API

**Constraint:** Each time a Zap step requests a file from your API, it will be accessed and downloaded.

**Best practice:** Much like data dehydration, you can implement a file request using [dehydration](https://platform.zapier.com/cli_docs/docs#file-dehydration), so the file will only be accessed and downloaded when a later Zap step asks for it.

To make this even more efficient, you can [stash the file](https://platform.zapier.com/cli_docs/docs#stashing-files) at Zapier. Rather than provide the file to the requesting step, Zapier will stash the file (under a dehydrated URL), so that only one request will ever be made for the file from your API.

# Throttling

There are a number of throttles that a Zapier user could encounter when using your integration, including those set by your API.

## Throttling (your API)

**Constraint:** Your API has request limits.

**Errors a user will see if constraint is hit:**

- If a trigger, user will receive an email with an error message about the trigger error
- If an action, user will see an error in Zap history

**Best practice:** Add a specific 429 `Retry-After` header to your response, or specify a timed delay in your error response using a special `ThrottledError`. Instead of a user’s Zap erroring and halting, the request will be retried at the specified time. More on the retry [here](https://platform.zapier.com/cli_docs/docs#handling-throttled-requests). The user will see this message in Zap History instead of an error while the limit is still in place:
![](https://cdn.zappy.app/0933736266259b11771a0eba0aff23ce.png)

## Webhook throttles (Zapier)

**Constraint:** Zapier’s current webhook limits are [here](https://zapier.com/help/troubleshoot/behavior/rate-limits-and-throttling-in-zapier#step-4). We will issue a 429 response when your integration exceeds these throttle limits.

**Errors a user will see if constraint is hit:**

- User will receive an email with an error message about the trigger error

**Best practice:** You should support a retry/back-off schedule to make sure the data is eventually received.

## Polling trigger throttle (Zapier)

**Constraint:** There is a default limit of 100 new items/poll after deduplication. More on that [here](https://zapier.com/help/manage/history/view-and-manage-your-zap-history#holding).

**What errors a user will see if constraint hit:**

- The user will receive an email about held Zap runs, as well as a banner with the same information in their Zap history.

**Best practices:** If your trigger will be returning > 100 new records consistently, we’d encourage you to look at these two options:

- Converting your trigger to be REST Hook based. Webhook limits are much expanded (up to 10,000 requests in a 5 minute period).
- Add support for Transfer. This is a new Zapier service that supports paging so users can create a Zap to select and batch transfer up to 25,000 records at one time. More [here](https://platform.zapier.com/docs/transfer).

# Error messages

When writing user-facing error messages, keep the message below 250 characters total. Zapier truncates errors from integrations at 250 characters when displaying them to users.

As an integration developer, you'll be able to see more detail in your [Monitoring](https://platform.zapier.com/docs/testing#monitoring) page, including the error stacktrace.

# Hydration/Dehydration

[File dehydration](https://platform.zapier.com/cli_docs/docs#file-dehydration) is an extremely useful tool to remain within time and size constraints for Zapier triggers and actions. However, it does have its own limits.

**Constraint**: There is a hard limit of 150MB on the size of dehydrated files. Depending on the complexity of the app, issues can also occur for files over ~100MB.

**What errors a user will see if constraint hit:** In their Zap history, the user will see an error like "Runtime exited with error: signal: killed".

**Best practice**: If your integration regularly loads large files, provide checks on file size and don't perform hydration for files that are larger than ~100MB. Include messaging for users letting them know of the limit.

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
