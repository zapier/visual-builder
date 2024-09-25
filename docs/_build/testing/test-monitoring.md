---
title: Test and monitor your integration in your Zapier account
order: 4
layout: post-toc
redirect_from: /build/test-integration#monitoring
---

# Test and monitor your integration in your Zapier account

Testing inside the Platform UI is crucial during the building process. To ensure users can benefit from your integration's features, it is equally crucial to test your integration within the Zap editor. This is the best way to notice details that might have been overlooked while building your integration. 

![Test new integration inside Zapier](https://cdn.zappy.app/4f69910e7b7d5fb9325d0e36579bca5a.png)

## Prerequisites

- Completed build of your Zapier integration
- A [Zapier account](https://zapier.com/sign-up)
- If you haven’t used Zapier before, you'll want to learn the basics in our [Zapier Getting Started Guide](https://zapier.com/learn/zapier-quick-start-guide/).
- Set of valid user credentials for your app - recommended to use a new account specifically for testing so you don't clutter your core app account with testing data. 

## Steps

1. Create a Zap in the [Zap editor](https://zapier.com/app/editor/), selecting your app in the _Choose App_ selector. 

2. Your integration will show the name and logo set in _Integration Settings_, along with the integration's current version number and a _By Invite_ tag. If your integration is a new version of an existing _Public_ integration, look for the _Latest_ tag, the latest version number and the _By Invite_ tag to differentiate from existing, public integrations.

3. Check each of the following as you setup Zaps:
- **Authentication**: Does your app account successfully connect? Zapier will show any testing accounts you already added, but try adding a new account here for a complete test. To remove connected accounts, you can delete connections from [Apps/Custom integrations](https://cdn.zappy.app/c97ff65c5857c3ebfeb302ffa8454867.png). 
- **Connection Label**: Does the Zap editor show the [expected connection label](https://cdn.zappy.app/693c0b1c08dabf06ea515995eab636aa.png) on the new account, with the info you set when building your integration?
- **Trigger and Action List**: Do you see every trigger and action included in your integration? Is each trigger and action's name and description accurate and grammatically correct?
- **Fields**: Do triggers and actions show the input fields you expect? Are their names and labels accurate and grammatically correct? Do any links or formatting in descriptions work correctly? Do drop-down fields or those with multiple selectors work correctly?
- **Output**: When you run a Zap trigger or action's test, does the step return the fields and data you expect in the correct format? Do triggers show the most recently added item from your app, and do searches return appropriate results?
- **Input**: Open your app, and check each item that Zapier actions added or updated for the correct format and expected appearance in your app. 
- **Automation**: Turn on Zaps with each of your integration's triggers and actions. Do they run correctly when the data they watch for is added or updated in your app? You can check your [Zap History](https://zapier.com/app/history) to make sure Zaps ran as expected for triggering events. Do your integration's actions successfully add and update items when those Zaps are triggered? 

## Monitoring

Use the _Monitoring_ page in the Platform UI to ensure that test Zaps and the expected requests are running without errors. Every request made to your API by your Zapier integration is shown. 

Adjust the Chart Filter for the correct timeframe, then click on any data point in the chart to see the any error messages and logs which should help you troubleshoot further. You can also filter by log type and by user email. 

![Monitoring Zapier integration](https://cdn.zappy.app/8e7113b876e9dd37b71722fee763cf3e.png)

To manually print a log statement you can see in Monitoring, use `z.console.log` in Code Mode:

`z.console.log('Here are the input fields', bundle.inputData);`

## User testing

Have internal team members and/or beta users test your integration. If you are going to submit your app for _Publishing_ in the Zapier App Directory, you'll need at least 3 users with live Zaps. Each additional tester helps ensure that your app doesn't ship with usability problems or bugs.

Internal team members can be invited from _[Manage Team](https://platform.zapier.com/manage/invite-team-member)_ as admins or collaborators. 

Beta users external to your organization can be invited from _[Sharing](https://platform.zapier.com/manage/share-integration)_

The _Insights_ section in the Platform UI provides usage statistics by trigger and action. 