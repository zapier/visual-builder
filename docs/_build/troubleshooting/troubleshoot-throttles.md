---
title: Troubleshoot throttles
order: 8
layout: post-toc
redirect_from: 
    - /build/operating-constraints#throttling-your-api
    - /build/operating-constraints#webhook-throttles-zapier
    - /build/operating-constraints#polling-trigger-throttle-zapier
---

# Troubleshoot throttles 

## Throttling by your API

### Constraint 

Your API has request limits.

### Errors user will see if constraint is hit

- If a trigger, user will receive an email with an error message about the trigger error
- If an action, user will see an error in Zap history

### Best practice

Add a specific `Retry-After` header to your 429 response, or specify a timed delay in your error response using a special `ThrottledError`. Instead of a user’s Zap erroring and halting, the request will be retried at the specified time. 

More on the retry [here](https://github.com/zapier/zapier-platform/blob/main/packages/cli/README.md#handling-throttled-requests). The user will see a [Waiting/Scheduled](https://help.zapier.com/hc/en-us/articles/20505304170637-Review-Zap-run-statuses) message in Zap history instead of an error while the limit is still in place.

![](https://cdn.zappy.app/0933736266259b11771a0eba0aff23ce.png)
 
If implementing a `ThrottledError`, you could consider implementing a jitter for handling 429 errors, that could look something like this to randomize the frequency of the retries as well:

`throw new z.errors.ThrottledError('message here', 60 + Math.floor(Math.random() * 60))`
 
Keep in mind that adding custom error handling with `ThrottledError` would likely require a [new integration version](https://platform.zapier.com/manage/versions), whereas adding to the headers could be implemented on your API's end. 

## Webhook throttles by Zapier

### Constraint

Zapier’s current webhook limits are [here](https://help.zapier.com/hc/en-us/articles/8496181445261#h_01H91ED0PQ56S166BSB7MJNZNT). A 429 response is returned if your integration exceeds these limits in number of webhooks sent to Zapier.

### Errors user will see if constraint is hit

- User will receive an email with an error message about the trigger error

### Best practice

You should support a retry/back-off schedule to make sure the data is eventually received.

## Polling trigger throttles by Zapier

### Constraint

There is a default limit of 100 new items recognized per poll after deduplication. More on that [here](https://help.zapier.com/hc/en-us/articles/8496181445261-Rate-limits-and-throttling-in-Zapier#h_01H91ED0PQ1HK1G1YFTZ9NSPRN).

### Errors user will see if constraint is hit

- The user will receive an email about held Zap runs, as well as a banner with the same information in their Zap history.

### Best practice

If your trigger will be returning > 100 new records consistently, consider converting your trigger to be REST Hook based. Webhook limits are higher (up to 10,000 requests in a 5 minute period).