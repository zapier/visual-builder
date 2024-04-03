---
title: Respond to user feedback and bugs
order: 2
layout: post-toc
redirect_from: 
    - /manage/user-feedback
    - /publish/zapier-issue-manager
    - /partners/zim
    - /manage/analyze-integration-performance#bugs
    - /partners/feature-requests-bugs
---

# Respond to user feedback and bugs

For public integrations, Zapier's Support team logs user requests and reported problems in Zapier's issue tracker, that your team can see from the _Bug & Feature Requests_ page in the Manage section. 

![Issues in Zapier Integration](https://cdn.zappy.app/b986eef73a1558ee3e121cf5d985339a.png)

Problems with your public integration, authentication and API calls will be logged as `bug`, while new functionality users request for your app integration will be logged as `feature request`. You have the ability to filter open `bugs` and `feature requests` to view issues by individual Trigger or Action.

## 1. Monitor issues reported

- Whenever a new issue is added or updated, Zapier will log it in the _Bugs & Feature Requests_ page of your app's Developer Platform page. 

- Issue notifications are automatically sent to all confirmed Administrators and Collaborators on the integration team. If an Administrator or Collaborator is listed as `Invitation Pending`, they will need to accept the invite before they start to receive issue notifications.

- Bug count is not as important as how many of your users are affected overall and what percentage of the app’s overall monthly active users that impacts. Past history on closing bugs doesn’t influence your app's current health score. 

- Affected user counts on issues typically underrepresent the actual totals, as only a small portion of all users facing an issue take the time to contact Zapier Support. 

## 2. Respond to issues in a timely manner

- Reply to the Zapier team about the issue within the _Bugs & Feature Requests_ page to keep communications consistent for both your team and ours. These issues and comments are not visible to affected users; and users will only be notified when an issue is verified as closed/resolved by Zapier Support.

![Reply to Zapier Integration Issue](https://cdn.zappy.app/a5808bdc70214728d0eac9f569f2d2e7.png)

- Lowering your count of issues will help improve your integration’s [health score](https://platform.zapier.com/publish/partner-program#integration-health-score) and increase your tier in the [Partner Program](https://zapier.com/platform/partner-program). The more you maintain a bug-free, quality integration, the more essential your product becomes to your users' workflows. This sets you up to reduce churn, drive account upgrades, and increase customer lifetime value.

- Regardless of the size of your integration’s user base, keeping the percent of monthly active users affected by open bugs under double figures (and ideally at 0) is recommended for a healthy integration.

- Allocate ongoing resources in your team’s product roadmap for the maintenance of your Zapier integration to avoid surprise work or gaps in functionality. Consider a [Zapier Expert](https://zapier.com/experts/matchmaking) to help you fix one-off bugs or maintain your integration.

### Dormant Issues
Any reported issue with no updates from you, Zapier Support, or end users for a year will now be automatically closed. This keeps your workspace current and focused, making it simpler to stay on top of active issues.

## 3. Close resolved issues

- Bugs and feature requests require review and verification from Zapier's Support team before they can be closed. When an issue is closed, email notifications are sent out to all affected users on the issue, notifying them of the update.

- Whenever a new version of your integration is promoted via the UI, you'll be prompted with a changelog form asking you to identify which feature requests or bugs were resolved and to provide a user-facing description of the changes. Issues identified in the changelog will automatically be queued for review by our Support team and closed once resolution is confirmed. Promoting via the CLI doesn't currently support changelogs.

![Changelog Form with Issues](https://cdn.zappy.app/8afba17ecfb25faf6b87597e2cd54387.png)

- You can also request issues to be closed manually by selecting one in the "Bugs & Feature Requests" tab of the developer platform, and leaving a comment to our Support team that the issue has been resolved. Provide info on what version number the fix is on, how to test the updates, and any other helpful callouts.

- Once an issue is reviewed, it will either be closed or responded to with follow-up questions and feedback.

## 4. Consider Zapier Issue Manager

- If you prefer syncing and managing issues from your own issue-tracking tools (such as Jira or Trello), create Zaps using Zapier Issue Manager.

- Zapier Issue Manager is available to all _Beta_ and _Public_ Zapier partners who own and maintain their own integration. To request access, submit the request form below.

<a class="button blue" href="https://airtable.com/shrK5ZOSGEAkDBAXg">Click here to request access to Zapier Issue Manager</a>

- Zapier Issue Manager offers the following for building Zaps:

### Triggers

* New Issue
* Issue Closed
* New Comment
* Affected User Added

### Actions

* Create Comment
* List Issues
* Find Issue
* Generate Report

- Here are some Zap templates to help you get started using Zapier Issue Manager.

<zapier-zap-templates
  theme="light"
  ids="1186967,1186970,1188008,1188017,1188026,1188034,1188054,1188084,1188092,1188102"
  limit="5"
  presentation="row"
  use-this-zap="show"
></zapier-zap-templates>

## 5. Monitor integration insights

- [See all the metrics tracked](https://platform.zapier.com/manage/integration-insights) in this table, or access them for any integration you are an Admin or Collaborator on from the _Dashboard_ tab of the Platform UI. Insights include important data on both the integration's growth and usage, such as monthly active users, retention rates, and Zap usage by triggers and actions.

![Screenshot of Dashboard tab in left sidebar of Developer Platform](https://cdn.zappy.app/d7a53ee12f8fb94a44edbc0f8e3195ea.png)

- Filter growth metrics by the last X number of days to identify trends and changes in user activity in correlation to marketing initiatives, integration changes, and product updates like [embedding Zapier](https://platform.zapier.com/embed/full-zapier-experience). 

- Usage details for each trigger and action will show which functionalities are the most popular and being effectively utilized. 

- Share access to the insights by [inviting collaborators](https://platform.zapier.com/manage/invite-team-member) to the integration without giving them permissions to make changes to it.