---
title: Build a private integration
order: 6
layout: post-toc
redirect_from: /quickstart/
---

# Build a private integration

This guide will walk you through what steps you need to take to build a [private integration](https://platform.zapier.com/quickstart/private-vs-public-integrations) from start to finish. We will include information for if you are building with either [Zapier Platform UI or Zapier Platform CLI](https://platform.zapier.com/quickstart/zapier-platform). 

> **Tip**: If you haven’t used Zapier before, learn the basics in our [Zapier Getting Started Guide](https://zapier.com/learn/zapier-quick-start-guide/).

## Prerequisite

* You’ll need a [Zapier account](https://zapier.com/sign-up).

## 1. Choose your developer tool

* [Zapier Platform UI vs CLI: Which should I choose?](https://platform.zapier.com/docs/vs)

> **Note**: If you’re building with Zapier Platform CLI, you’ll need to install [Node.js](https://developer.zapier.com/cli-guide/install-node-js) and [CLI](https://platform.zapier.com/cli_tutorials/getting-started#installing-the-cli).

## 2. Create a new integration

Create and add details about your integration. Set your Intended audience to select **Private: I’m building an integration for personal use or to explore the Zapier platform**. 

* [Create an integration using Zapier Platform UI](https://developer.zapier.com/app/new)
* [Create an integration using Zapier Platform CLI](https://platform.zapier.com/cli_docs/docs#creating-a-local-app)
  * **Note**: If you’re building with Zapier Platform CLI, you’ll set your intended audience when you register your app.

## 3. Create an authentication 

Creating an authentication will tell Zapier what credentials users need to authenticate with your API. 

* [Create an authentication using Zapier Platform UI](https://platform.zapier.com/docs/auth)
* [Create an authentication using Zapier Platform CLI](https://platform.zapier.com/cli_tutorials/getting-started#adding-authentication)
  * [Authentication schema](https://github.com/zapier/zapier-platform/blob/main/packages/cli/README.md#authentication)

## 4. Create triggers

Triggers allow users to find new data as soon as it’s available in your app. Use webhooks or polling endpoints to create triggers.

* [Create a trigger using Zapier Platform UI](https://platform.zapier.com/docs/triggers)
* [Create a trigger using Zapier Platform CLI](https://platform.zapier.com/cli_tutorials/getting-started#adding-a-trigger)
  * [Trigger schema](https://github.com/zapier/zapier-platform/blob/main/packages/schema/docs/build/schema.md#triggerschema)

## 5. Create actions

Actions allow users to either create, search or update records through your API.

* [Create an action using Zapier Platform UI](https://platform.zapier.com/quickstart/build-action)
* [Create an action using Zapier Platform CLI](https://platform.zapier.com/cli_docs/docs#triggerssearchescreates)
  * [Search schema](https://github.com/zapier/zapier-platform/blob/main/packages/schema/docs/build/schema.md#searchschema)
  * [Create schema](https://github.com/zapier/zapier-platform/blob/main/packages/schema/docs/build/schema.md#createschema)

## 6. Test your integration

Test your authentication, triggers, actions, and how your private integration works inside Zapier.

* [Testing using Zapier Platform UI](https://platform.zapier.com/docs/testing)
* [Testing using Zapier Platform CLI](https://platform.zapier.com/cli_docs/docs#testing)

## [Optional] Validate your integration

Run automated checks to identify errors and recommendations on how to improve the user experience of your private integration. 

* [Run automated checks using Zapier Platform UI](https://platform.zapier.com/docs/integration-checks-reference)
* [Run automated checks using Zapier Platform CLI](https://github.com/zapier/zapier-platform/blob/main/packages/cli/docs/cli.md#validate)

## [Optional] Invite team members

You can assign different roles and permissions to team members who you’re collaborating with on your private integration. 

* [Invite team members using Zapier Platform UI](https://platform.zapier.com/manage/invite-team-member)
* [Invite team members using Zapier Platform CLI](https://platform.zapier.com/quickstart/platform-cli-tutorial#invite-team-members-to-help-manage-your-app)

## [Optional] Share your integration

Once you’ve built your integration, you can share it with users who can can [create Zaps](https://help.zapier.com/hc/en-us/articles/8496309697421-Create-Zaps) with it.

* [Share your integration](https://platform.zapier.com/manage/share-integration)

## Conclusion

Once you’ve built your private integration, you can continue to make further improvements and manage versions of your integration.

* [Manage integration versions using Zapier Platform UI](https://platform.zapier.com/manage/versions-ui)
* [Manage integration versions using Zapier Platform CLI](https://platform.zapier.com/manage/versions-cli)


> **Tip**: Learn from the Zapier team and other [Zapier Platform developers in our community forum](https://community.zapier.com/for-developers-61).
