---
title: Troubleshoot trigger payload size
order: 3
layout: post-toc
redirect_from: 
    - /build/operating-constraints#payload-size-triggers
    - /build/operating-constraints#payload-size-polling-triggers
    - /build/operating-constraints#payload-size-rest-hook-triggers
    - /build/operating-constraints#timeouts-and-payload-size-polling-triggers
---

# Troubleshoot trigger payload size

## Testing trigger in Zap editor

### Constraint 

When a user clicks **Test Trigger** in the Zap editor, the response payload must be less than 6MB.

### Errors user will see if constraint is hit

- _“Scripting payload too large ('n' bytes but max is 6291456bytes).”_ - ('n' is the number of bytes in the payload.)

### Best practice

The Zap editor will only process three new records at a time for sample data, so one way of making sure your payload size is less than the limit is by limiting your results to three records. 

To determine when the request is for sample data, use the bundle meta parameter `bundle.meta.isLoadingSample`. When that is set to `true`, the user is testing in the Zap editor, and your integration can respond with a limited payload. More on `bundle.meta` properties [here](https://github.com/zapier/zapier-platform/blob/main/packages/cli/README.md#bundlemeta).

## Turning Zap on

### Constraint

When a user toggles a Zap with a polling trigger “On”, Zapier does some additional initialization that must be accomplished in 30 seconds. 

First, it tests the user’s authentication to your service. 

Then it uses the trigger's `perform` method to build a [deduplication table](https://platform.zapier.com/build/deduplication) of records, so that the Zap will not run for existing records. The payload returned from this request must also be less than 6 MB.

### Errors user will see if constraint is hit

- Users will receive an email with an error message that includes the text _"Your Zap could not be turned on"_.

### Best practice

There is a `bundle.meta` property that you can take advantage of here, `bundle.meta.isPopulatingDedupe`. When set to `true`, the Zap is being enabled, and you can use that to create a distinct request. The deduplication process only uses the `id` property of each record, so one option to consider for this request is filtering the fields you return to reduce record size.

More on `bundle.meta` properties [here](https://github.com/zapier/zapier-platform/blob/main/packages/cli/README.md#bundlemeta).

For those requests that might otherwise exceed timeout or size limits, you can make sure your filtered request is successful. Alternatively, if your filtered request has a lot of headroom in both time and size, you could instead use this to load more records into the Zap’s deduplication table than you usually request in your `perform`. This is especially relevant for an API that might return an inadvertent older record in a later polling request.

**Example:** The [Salesforce](https://zapier.com/apps/salesforce/integrations) integration has an **_Updated Field on Record_** trigger that can trigger on older records that a user might not consider relevant for their running Zap. To help mitigate this, the integration uses a filtered request to download up to 104,000 records to the deduplication table during Zap startup.

## Trigger runs in a Zap

### Constraint
 
Each time a Zap executes, the trigger's response payload must be less than 6MB for a polling trigger and less than 10 MB for a REST Hook trigger. 

### Errors user will see if constraint is hit

- User will receive an email with an error message, usually with _"Trigger Partner Failure"_ in the message text.

### Best practice

- For polling triggers, if your API endpoint supports request filtering around number of records or datetime, using these to reduce the number of records returned
- If filtering isn't an option, consider using the simplest available endpoint on your API for the basic record data, and use Zapier platform [dehydration](https://github.com/zapier/zapier-platform/blob/main/packages/cli/README.md#dehydration) to request supplementary data. A dehydration pointer is created for each subsequent request, and this pointer will only be resolved if the Zap needs a hydrated property in a later step.
- For REST Hook triggers, if your REST Hook subscription endpoint supports filtering, one option is to provide input fields in the trigger so a user can decide what record data they want to return.
- Consider sending a notification REST Hook that includes minimal record data. You can then use additional API endpoints and Zapier platform [dehydration](https://github.com/zapier/zapier-platform/blob/main/packages/cli/README.md#dehydration) to request the supplementary record data. A dehydration pointer is created for each subsequent request, and this pointer will only be resolved if the Zap needs a hydrated property in a later step.