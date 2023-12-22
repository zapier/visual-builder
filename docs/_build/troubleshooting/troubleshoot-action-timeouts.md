---
title: Troubleshoot action timeouts
order: 4
layout: post-toc
redirect_from: 
    - /build/operating-constraints#timeouts-actionssearches
    - /build/operating-constraints#timeouts-actions
---

# Troubleshoot action timeouts

## Testing action in Zap editor

### Constraint 

When a user clicks **Test and Review** or **Retest and Review** in the Zap editor, the output of your `perform` must be returned within 30 seconds.

### Errors user will see if constraint is hit

- _“The app did not respond in-time. It may or may not have completed successfully.”_

### Best practice

Timeouts can occur on your API endpoint, or within the `perform` method processing the response payload. To speed up the `perform`, check for expensive processing operations, and consider reducing `z.console.log` calls, especially in looping code.

## Action runs in a Zap

### Constraint

Each time a Zap step runs, the action/search's `perform` method must finish processing in 30 seconds. If the API request cannot consistently be finished within 30 seconds - for example, file format conversion, an error will show. 

### Errors user will see if constraint is hit

- An error in the Zap history of their Zap due to the request timing out

### Best practice

For longer-running requests, use the webhook-based callback service the Zapier platform provides. This allows your action to be performed asynchronously, and when finished, POST to the callback URL. More on using this method [here](https://github.com/zapier/zapier-platform/blob/main/packages/cli/README.md#zgeneratecallbackurl).

A user will then see the [Waiting/Delayed status](https://help.zapier.com/hc/en-us/articles/20505304170637-Review-Zap-run-statuses) in Zap history for that Zap step, until the POST is received to the callback url, upon which the task will resume. 

