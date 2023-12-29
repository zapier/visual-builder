---
title: Zapier integration structure
order: 2
layout: post-toc
redirect_from: 
    - /quickstart/project-structure
    - /quickstart/zapier-integration-structure
    - /manage/analyze-integration-performance#how-to-view-insights
---

# Zapier integration structure

[Zapier's Developer Platform](https://developer.zapier.com/) includes everything needed to build and manage a new Zapier integration. When you access your integration project by name, you'll see the left sidebar outlines the core project structure. 

### Dashboard

_Dashboard_ tab is used to monitor and analyze your integration's growth, usage, and embed metrics. You **must** be an [admin or collaborator](https://platform.zapier.com/manage/add-team) to view an integration’s dashboard.

![Screenshot of Dashboard tab in Developer Platform](https://cdn.zappy.app/d7a53ee12f8fb94a44edbc0f8e3195ea.png)

### Build

_Build_ tab defines your integration:

  - _Version Overview_ shows the outline of the version selected in the [dropdown](https://cdn.zappy.app/ca49500dc40cd1986693223661ab22b2.png)
  - _Authentication_ sets how users authenticate with your API; using basic, API key, digest, session, or OAuth v2 authentication.
  - _Triggers_ control how Zapier gets data from your API into a Zap, with `GET` HTTP calls or REST Hooks.
  - _Actions_ control how Zapier sends data to your API, including:
    - _Create Actions_  to send new data from a Zap to your API, with `POST` or `PUT` HTTP calls to create or update items.
    - _Search Actions_  to perform lookups through your API using `GET` calls.
  - _Advanced_ manages environment variables to store secret values your integration needs to communicate with your API, such as API keys or client IDs and secrets, or manage switching between staging and production environments in a version.

When planning your integration build, think through your integration and what features from your app your users might find the most valuable. Review [integration design examples](https://platform.zapier.com/build/recommended-integration-features) by app category for inspiration. 

Walk through building an integration with the [UI tutorial](https://platform.zapier.com/quickstart/ui-tutorial) or the [CLI tutorial](https://platform.zapier.com/quickstart/cli-tutorial). 

### Manage

_Manage_ tab is where you access tools to maintain your integration:

  - _Versions_ gives an [overview of each version's status](https://platform.zapier.com/manage/versions), user activity and for published apps; the changelog included in a promotion
  - _Sharing_ is where you [give users access](https://platform.zapier.com/manage/sharing) to private versions via an invite link to all versions or an email invite to a specific version
  - _Manage Team_ is used to [add team members](https://platform.zapier.com/manage/add-team) to manage your integration
  - _Monitoring_ gives access to [logs for requests](https://platform.zapier.com/build/test-monitoring#steps) made to your API by your Zapier integration  
  - _History_ shows the 50 most recent audit logs for changes to your integration
  - _Bugs & Feature Requests_ are reported by users for published apps and should be used to communicate on these issues with Zapier Developer Support

### Embed

_Embed_ tab shows for [public integrations](https://platform.zapier.com/quickstart/private-vs-public-integrations) only and describes a [variety of ways](https://platform.zapier.com/embed/full-zapier-experience) to surface your Zapier integration directly within your own product. It allows your users to search for apps that connect with yours, see popular workflows used with your app, and (most importantly) enables them to sign up for Zapier, build Zaps and edit them, too — without leaving your product.