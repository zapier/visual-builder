---
title: Zapier Operating Constraints
order: 1
layout: post-toc
redirect_from: /platform_wide/
---

# Zapier operating constraints and your integration overview

Zapier offers a relatively unique run-time environment for your integration and its requests to your API. The environment is stateless and restricts both execution time and payload size to offer normalized reliability and running time. There are two distinct contexts of this run-time that your integration will need to run within:

Zap step setup using the Zap editor
Zap step execution when a Zap runs

This document exposes various operating constraints of these run-time modes, errors users and your integration could run into, as well as best practices. This information is targeted towards users of our CLI development environment, but many of the strategies can be used in code mode in our Platform UI.

Integration log monitoring can be viewed in the Platform UI - https://platform.zapier.com/docs/testing#monitoring, or if using the CLI, using zapier logs: https://zapier.github.io/zapier-platform/cli#logs

## Zap step setup using the Zap editor

There are three areas where the user will interact with your integration when they add a trigger, action, or search step in their Zap.

**Test step (all triggers):**
Constraint: When a user clicks Test Trigger in the Zap editor the output of your perform (polling) or performList (RESThook) must be returned within 30 seconds.

What a User will see:
“The app did not respond in-time. It may or may not have completed successfully.”
"Problem creating Sample: Our computers ran into a problem"
“We couldn't find any more x. Create a new x in your account and try again.”

Best practice: The Zap editor will only process three new records at a time for sample data, so one way of making sure you can finish in time is by limiting your results to just three records. As this request might look different than a normal request when a Zap is running (especially for a RESThook trigger), you can leverage the bundle meta parameter bundle.meta.isLoadingSample. When that is set to true, you can know the user is in the Zap Editor testing and can respond with a limited payload. More on bundle meta properties here:

https://github.com/zapier/zapier-platform/tree/master/packages/cli#bundlemeta

{% include prev-next.html %}
