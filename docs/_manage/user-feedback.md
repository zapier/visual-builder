---
title: Respond to user feedback
order: 3
layout: post-toc
redirect_from: /partners/feature-requests-bugs
---

# Respond to user feedback


![Issues in Zapier Integration](https://cdn.zappy.app/b986eef73a1558ee3e121cf5d985339a.png)

As people use your Zapier integration, they may encounter bugs and problems with your integration, or think of new ways they'd like to use your app with Zapier, and send them to the Zapier support team. We log those in Zapier's issue tracker, which you can see from the _Bug & Feature Requests_ page in the Manage section of your integration's sidebar. 

Problems and issues with your integration, authentication, API calls, and more will be logged as `bug`, while new things users require from your integration will be logged as `feature request`. You also have the ability to filter open `bugs` and `feature requests` to view issues by individual Trigger or Action.

![Reply to Zapier Integration Issue](https://cdn.zappy.app/a5808bdc70214728d0eac9f569f2d2e7.png)

Whenever a new issue is added or updated, Zapier will log it in the _Bugs & Feature Requests_ page of your app's Zapier Developer Platform page. You can reply to the Zapier team about the issue there. These issues and comments are not visible to affected users; and users will only be notified when an issue is verified as closed/resolved by the Zapier support team. If you prefer syncing and managing issues from your own issue-tracking tools (such as Jira or Trello), you can create Zaps to do so using [Zapier Issue Manager](https://platform.zapier.com/publish/zapier-issue-manager).

Issue notifications are automatically sent to all confirmed Administrators and Collaborators on the integration team. If an Administrator or Collaborator is listed as `Invitation Pending`, they will need to accept the invite before they start to receive issue notifications.

## How to monitor integration insights

As you launch and maintain your integration, you should monitor and review the insights in the dashboard on a regular cadence. Insights include important data on both the integration's growth and usage, such as monthly active users, retention rates, and Zap usage by triggers and actions. You can [see all the metrics tracked](https://platform.zapier.com/manage/analyze-integration-performance#integration-insights-definitions) in this table, or access them for any integration you are an Admin or Collaborator on from the "Dashboard" tab of the developer platform.

![Screenshot of Dashboard tab in left sidebar of Developer Platform](https://cdn.zappy.app/d7a53ee12f8fb94a44edbc0f8e3195ea.png)

You can filter most growth metrics by the last X number of days to identify trends and changes in user activity in correlation to marketing initiatives, integration changes, and product updates like [embedding Zapier](https://platform.zapier.com/embed/full-zapier-experience). Usage details for each trigger and action will show which functionalities are the most popular and being effectively utilized. You can easily and safely share access to the insights by [inviting collaborators](https://platform.zapier.com/manage/invite-team-memberr) to the integration without giving them permissions to make changes to it.

## How to make a new version of your integration

Sometimes you may want to add something new to your integration. You may need to fix bugs in your integration, or add additional details to resolve user issues. You might want to add additional triggers, actions, or searches to your integration as uses request them. Or, over time, you may need to change your app's authentication and API calls.

The Zapier Platform makes it easy to build new versions of your integration when needed. You can create new versions for minor or major changes as needed.

Versions that have been made public, or those with more than 5 users, cannot be edited. In that case, you will need to create a new version to make any changes. This is so that existing users are not surprised by changes to their running workflows.

It's still best to include non-breaking changes in a new integration version, so you can test the changes and roll them out to a smaller subset of your Zapier integration users. Once you've made sure the new version works well, you can roll it out to all of your users.

[Breaking or major changes](https://platform.zapier.com/manage/versions-ui#what-is-a-breaking-change), such as switching to a new API endpoint, changing authentication type, or rewriting an integration, require a new major version of your integration, and users will need to re-create their Zaps with the new version of your integration.

You can test the new version privately, as when you first built your Zapier integration. Once it's ready for wider use, you can promote the new integration version, and deprecate the older version if you want to. Zapier will then mark the integration as having newer versions available, and will show the new version instead of the earlier version when users make new Zaps.

_→ Find how to manage versions in [Zapier Platform UI](https://platform.zapier.com/manage/versions-ui) and [CLI](https://platform.zapier.com/manage/versions-cli)_.

