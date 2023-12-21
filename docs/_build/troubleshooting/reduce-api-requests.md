---
title: Reduce requests to your API
order: 7
layout: post-toc
redirect_from: 
    - /build/operating-constraints#reducing-requests-to-your-api
    - /build/operating-constraints#reducing-file-requests-to-your-api
---

# Reduce requests to your API

## Trigger/action runs in a Zap

### Constraint

Each time a Zap runs and your integration is invoked, it can mean multiple requests to your API endpoints, depending on what your trigger/action seeks to accomplish. This can mean hundreds of requests/hour for your polling triggers based on a [Zapier customer's plan](https://zapier.com/pricing), or thousands based on a Zap with an active REST Hook Trigger from another app and an action in your app.

For triggers/actions that include files in the output, each time a Zap step requests a file from your API, it will be accessed and downloaded from the relevant endpoint.

### Best practice

One way to reduce that API load is via the Zapier platform [dehydration feature](https://github.com/zapier/zapier-platform/blob/main/packages/cli/README.md#dehydration). By putting any secondary requests behind a dehydration pointer, Zapier will only make this request once, although it might see the same records again and again based on the Zap’s polling cycle. 

For file outputs, implementing dehydration means the file will only be accessed and downloaded when a later Zap step asks for it.

To make this even more efficient, you can [stash the file](https://github.com/zapier/zapier-platform/blob/main/packages/cli/README.md#stashing-files) at Zapier. Rather than provide the file to the requesting step, Zapier will stash the file (under a dehydrated URL), so that only one request will ever be made for the file from your API.