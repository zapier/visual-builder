---
title: How to Maintain a Zapier Integration
order: 3
layout: post-toc
redirect_from: /partners/
---

# How to Maintain a Zapier Integration

Things change. Over time, you'll add new tools to your app, improve existing features, fix bugs, and continuously improve it. New features may grow it into a larger category, or make it more focused on a smaller niche. Its description will likely change, as may its logo or even name. The API may even change as your app matures.

Your Zapier integration needs to change, too. The best integrations are improved over time to improve their most popular use cases, remove bugs or confusing descriptions that tripped up users, and keep branding consistent with their core app.

Keep these guidelines in mind as you maintain your Zapier integration:

## How to Update App Branding in Zapier

![Update Zapier integration details](https://cdn.zappy.app/21501f70d3d15a341e6dc7ea90690ee6.png)

You can update your app's name, description, logo, and category anytime in the [Zapier Platform site](https://zapier.com/app/developer). Select your app integration, click the gear icon near its name, then update the app details as needed.

If you built your app using Zapier Platform CLI, you can also update the app name and description from the integration bundle's `package.json` file. You will still need to use the [Zapier Platform site](https://zapier.com/app/developer) to update your app icon and category.

If your app is public, you'll then need to [send us a request](mailto:partners@zapier.com) to publish those changes.

Please make sure to follow [Zapier's branding guidelines](https://platform.zapier.com/partners/planning-guide) whenever updating app branding.

## How to Monitor Feature Requests and Bugs

![Issues in Zapier Integration](https://cdn.zappy.app/b986eef73a1558ee3e121cf5d985339a.png)

As people use your Zapier integration, they may encounter bugs and problems with your integration, or think of new ways they'd like to use your app with Zapier, and send them to the Zapier support team. We log those in Zapier's issue tracker, which you can see from the _Bug & Feature Requests_ page in the Manage section of your integration's sidebar.

Problems and issues with your integration, authentication, API calls, and more will be logged as `bug`, while new things users require from your integration will be logged as `feature request`.

![Reply to Zapier Integration Issue](https://cdn.zappy.app/a5808bdc70214728d0eac9f569f2d2e7.png)

Whenever a new issue is added or updated, Zapier will log it in the _Bugs & Feature Requests_ page of your app's Zapier Developer Platform page. You can reply to the Zapier team about the issue there, or reply to the notification email to add a response to the issue. If you prefer syncing and managing issues from your own issue-tracking tools (such as Jira or Trello), you can create Zaps to do so using Zapier Issue Manager. [Learn more and request access to Zapier Issue Manager here.](https://platform.zapier.com/partners/zim)

Issue notifications are automatically sent to all confirmed Administrators and Collaborators on the integration team. If an Administrator or Collaboroator is listed as `Invitation Pending`, they will need to accept the invite before they start to receive issue notifications.

## How to Monitor Integration Insights

As you launch and maintain your integration, you should monitor and review the insights in the dashboard on a regular cadence. Insights include important data on both the integration's growth and usage, such as monthly active users, retention rates, and Zap usage by triggers and actions. You can [see all the metrics tracked](https://platform.zapier.com/partners/integration-quality#integration-insights-definitions) in this table, or access them for any integration you are an admin or collaborator on from the "Dashboard" tab of the developer platform.

![Screenshot of Dashboard tab in left sidebar of Developer Platform](https://cdn.zappy.app/d7a53ee12f8fb94a44edbc0f8e3195ea.png)

You can filter most growth metrics by the last X number of days to identify trends and changes in user activity in correlation to marketing initiatives, integration changes, and product updates like [embedding Zapier](https://platform.zapier.com/embed/full-zapier-experience). Usage details for each trigger and action will show which functionalities are the most popular and being effectively utilized. You can easily and safely share access to the insights by [inviting collaborators](https://platform.zapier.com/quickstart/invite-team-member#collaborator) to the integration without giving them permissions to make changes to it.

## How to Make a New Version of Your Integration

Sometimes you may want to add something new to your integration. You may need to fix bugs in your integration, or add additional details to resolve user issues. You might want to add additional triggers, actions, or searches to your integration as uses request them. Or, over time, you may need to change your app's authentication and API calls.

The Zapier platform makes it easy to build new versions of your integration when needed. You can create new versions for minor or major changes as needed.

Versions that have been made public, or those with more than 5 users, cannot be edited. In that case, you will need to create a new version to make any changes. This is so that existing users are not surprised by changes to their running workflows.

It's still best to include non-breaking changes in a new integration version, so you can test the changes and roll them out to a smaller subset of your Zapier integration users. Once you've made sure the new version works well, you can roll it out to all of your users.

[Breaking or major changes](https://platform.zapier.com/docs/versions#what-is-a-breaking-change), such as switching to a new API endpoint, changing authentication type, or rewriting an integration, require a new major version of your integration, and users will need to re-create their Zaps with the new version of your integration.

You can test the new version privately, as when you first built your Zapier integration. Once it's ready for wider use, you can promote the new integration version, and deprecate the older version if you want to. Zapier will then mark the integration as having newer versions available, and will show the new version instead of the earlier version when users make new Zaps.

_→ Find how to manage versions in [Zapier Platform UI](https://platform.zapier.com/docs/versions) and [CLI](https://github.com/zapier/zapier-platform/blob/master/packages/cli/README.md#deploying-an-app-version)_.



### We're here to help!

As always, please [contact us](https://developer.zapier.com/contact) if you have any questions!
