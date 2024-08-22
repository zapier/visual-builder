---
title: Zapier operating constraints
order: 1
layout: post-toc
redirect_from: 
---

# Zapier operating constraints

Zapier offers a relatively unique run-time environment for your integration and its requests to your API. The environment is stateless and restricts both execution time and payload size to offer normalized reliability and running time. There are three distinct contexts of this run-time that your integration will need to consider.

- Zap step setup and testing using the Zap editor
- Zap startup - turning a Zap on
- Zap step execution when a Zap runs

The following pages describe the operating constraints of these run-time modes, the errors your integration users could run into, and best practices. Developers in the Platform CLI development environment and those using [Code Mode](https://platform.zapier.com/build/code-mode) in the Platform UI will find these pages most relevant. 

Many errors can be viewed in your integration's log monitoring in the [Platform UI](https://platform.zapier.com/build/test-monitoring), or if using the [Platform CLI](https://github.com/zapier/zapier-platform/blob/main/packages/cli/README.md#handling-throttled-requests), by using `zapier logs` command.

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
| HTTP response payload | 20 MB                 |
| Downloaded files      | ~120 MB              |

| Throttles                                                                                                           |                             |
| ------------------------------------------------------------------------------------------------------------------- | --------------------------- |
| Polling trigger                                                                                                     | Default: 100 new items/poll |
| REST Hook trigger                                                                                                   | 10000 webhooks/5 minutes    |
|                                                                                                                     | 30 webhooks/second          |
| More on throttles [here.](https://help.zapier.com/hc/en-us/articles/8496181445261#h_01H91ED0PQ782E3B34ZRB5DXF7) |                             |

| TCP/IP                  |                                                                                                     |
| ----------------------- | --------------------------------------------------------------------------------------------------- |
| Integration assigned IP | [AWS-East](https://zapier.com/help/troubleshoot/behavior/cant-access-or-use-zapier-with-other-apps) |