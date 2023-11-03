---
title: Versions
order: 1
layout: post-toc
redirect_from: 
    - /docs/versions
    - /manage/versions-ui
---


# Versions

Versions in Developer Platform allow developers to create multiple iterations of their integration to experiment with and implement new features without affecting existing users. Each integration can have many versions, but only one version can have a public status at a one time.

Versions allow you to have:

- **Seamless user experience**: This allows existing users with uninterrupted service, while new features are being tested and deployed.
- **Incremental upgrades**: You can facilitate phased roll outs of new features, allowing for thorough testing and feedback collection before full deployment.
- **Version management**: It provide a structred approach to deprecate older versions post the migration of users to updated versions.

## Managing versions in Platform UI

To manage your versions:

1. Log into the [Platform UI](https://zapier.com/app/developer).
2. Select your **integration**. 
3. In the _Manage_ section in the left sidebar, click your **Versions**.  

This page shows a list of all versions of the integration, along with status, number of active users and active Zaps on each. For public integrations will also show the changelogs input when a new version is promoted. 

![The Versions page in the Zapier Developer Platform](https://cdn.zappy.app/b443129368e61bdaa86c6f5a741fbe8a.png)

Learn more on:
- [Clone an version]()
- [Migrate users to a new version]()
- [Promote an version]()
- [Deprecate or delete an version]()

## Managing versions in Platform CLI 

Integrations created with the Platform CLI cannot be edited and manage versions in the Platform UI, however you can view versions in the Platform UI. You can also run the [`zapier versions`](https://github.com/zapier/zapier-platform/blob/master/packages/cli/docs/cli.md#versions) command to see the same information in your local terminal.

## Who can view your versions?

For public integrations, which are searchable in the Zap editor or in the app directory, a user who selects your integration in the Zap Editor will be using the current public version by default. 

For both [private and public integrations](https://platform.zapier.com/quickstart/private-vs-public-integrations), only team members added to the integration, or users with whom you have shared private versions with specifically, will see those versions as well.

## Editing versions

To make sure that existing Zaps can continue to work consistently, the Developer Platform only allows you to edit versions that have a private status and have fewer than 5 users. Versions that are public or have more than 5 users will show a warning message prompting you to clone the version instead.

!['You can't edit this version'](https://cdn.zappy.app/8b5cbf5a37ce60ba89eb555c0429eca6.png) 

When making integration updates in newer versions, consider the potential impact on user migration and existing Zaps. Ensuring your API and app integration on Zapier remains backwards compatible is crucial to [avoid disruption to users](https://platform.zapier.com/manage/making-changes).