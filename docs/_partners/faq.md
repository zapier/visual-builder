---
title: Zapier Integration Tips and FAQs
order: 5
layout: post-toc
redirect_from: /docs/
---

# Zapier Integration Partner Tips and FAQs

Before you develop your Zapier integration, it’s important to become familiar with the criteria Zapier uses to review all new app integrations. 

The following tips are based on the most common issues we encounter and will help you to breeze through the app review phase.

## Get Familiar with Zapier

If you haven't used Zapier before, [sign up](https://zapier.com/sign-up/) for a free account and try a few popular integrations before building your integration. This will help you understand how Zapier works, how your users will set up Zaps, and how your integration can best fit into Zap workflows.

## Focus on Key Use Cases

Your initial Triggers, Actions, and Searches should focus on the main things users do with your app. Check similar apps in [Zapier's App Directory](https://zapier.com/apps/) to get some ideas on which items to include in your integration. Don't include too many triggers or actions at first, as new apps with more than 5 Triggers, Actions, or Searchers may not be able to go public (unless each each Trigger, Action, and Search has a lot of test users already). 

## Test Early With Real Users

Hopefully, you have a bunch of keen users waiting to get their hands on your integration. Send them your app’s invite link to give them early access. Zapier requires at least 10 unique, active users of your integration to submit it for review. That help give us confidence that your integration is useful and working well for a bunch of users. 

## Check Your App Integration Style

Users should already be familiar with the terminology used in your Zapier integration—it should be consistent with what is used in your app's own UI. It should also be consistent with the style used in other popular Zapier integrations.

We strive to give users a consistent experience throughout Zapier. Be sure to follow [Zapier's standards for app branding](https://platform.zapier.com/partners/planning-guide#how-to-brand-your-zapier-integration) to make your app fit into the Zapier ecosystem well.

## Make Connecting New Accounts Easy

Connecting to Zapier must be easy for the user. OAuth v2 is the preferred authentication scheme; otherwise, make sure users can easily retrieve or generate an API Key or other credentials themselves without needing support assistance. Also, the Test Trigger should provide actionable error messages to help users successfully connect their account.

## Provide a Valid Test Account

The App Review Team will go through each Trigger, Action, or Search in your integration to verify that it’s working in a similar way the interactions should work within your app. In order to do this, set up a valid test account and share the credentials with our team (ideally with contact@zapier.com as the account email address). Make sure the account includes all the features needed to test out each Zap step, with any special configurations set. If features require an environment that is hard to replicate or require specific hardware, provide a demo video or documentation to the Zapier team.

## Ensure Your Integration is Complete and Platform Consistent

You should submit your integration for review only when it is complete and ready to be published. Make sure to thoroughly test your integration for edge cases and fix all bugs before submitting. Please don’t treat the App Review as a software testing service for your platform, and make sure both the platform and integration work consistently without errors. We will not allow incomplete or error-ridden app integrations to become public.

## Avoid Repeated Submissions

Submitting several app integrations that are essentially the same ties up the App Review process and risks the rejection of your integrations. Please be thoughtful and consider combining your apps into one where it makes sense. Also, please do not spam the App Review team with multiple versions of the same integration while going through that review process.

## Avoid Misleading or Malicious Functionality

Your app must perform as advertised and should not give users the impression the app is something it is not. If your app appears to promise certain features and functionalities, it needs to deliver. Do not create a Zapier integration that can be used to spam, phish, or send unsolicited messages to users.

If you attempt to cheat the system (for example, by trying to trick the review process, steal user data, or fake real users) your apps will be removed from Zapier and you could be expelled from submitting any apps in the future.

### Further Reading

For more information, check [Zapier's guide to building a Zapier integration](https://platform.zapier.com/partners/planning-guide) for the core guidelines to follow when building and branding your Zapier integration.


***

## Contact Zapier

Can't find the answer you need here or in Zapier's [integration planning guide](https://platform.zapier.com/partners/planning-guide)? Feel free to get in touch with our team:

### Join Zapier Platform Slack

Zapier's Platform team has a [community Slack channel](https://join.slack.com/t/zapier-platform/shared_invite/enQtNTg1MjM5NjMzNTI3LWVhZjk3NjFlNWFiMTBmMDExMzI5NDZiZmFiOTJjYmI3NmY2MzEwZDUxNzQ3MTliMTM5N2M3NGM2MmQ2Y2VkODE) dedicated to helping developers with new and existing app integrations. We're a worldwide team, so there's usually someone around to answer your questions. We'd love to hear your experience building on Zapier.

### Email Zapier's Platform Team

For questions about building Zapier integrations, email [partners@zapier.com](mailto:partners@zapier.com), where our Platform team can help resolve issues you encounter while building Zapier integrations, and our Partnerships team can help launch your Zapier integration.

If you have issues with your Zaps and core Zapier account, reach out to [contact@zapier.com](mailto:contact@zapier.com). Our support team has access to the most recent logs and other details that will help them work on your issue.

### Find a Zapier Integration Partner

We're excited to help you with your Zapier app, but we can't build it for you. If you'd like someone to take over the technical reins, check our [a list of third-party Zapier developers and consultants](https://zapier.com/help/integration-developers-partners/) to find someone to help develop a Zapier integration for your app.

