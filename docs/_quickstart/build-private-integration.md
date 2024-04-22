---
title: Build your first private integration
order: 1
layout: post-toc
redirect_from: 
    - /quickstart/
    - /private_integrations/build-a-private-integration
---

# Build your first private integration on Zapier

This guide will walk you through what steps you need to take to build a [private integration](https://platform.zapier.com/quickstart/private-vs-public-integrations) from start to finish. There are no fees to build an integration with Zapier. 

You can choose to build with either [Zapier Platform UI or Zapier Platform CLI](https://platform.zapier.com/quickstart/ui-vs-cli).

## 1. Prerequisites

* The app you wish to integrate will need to have a [publicly-accessible API](https://zapier.com/learn/apis/)
* Create a [Zapier account](https://zapier.com/sign-up)
* If you haven’t used Zapier before, learn the basics in our [Zapier Getting Started Guide](https://zapier.com/learn/zapier-quick-start-guide/)

## 2. Choose a developer tool

Select [one of the two ways](https://platform.zapier.com/quickstart/ui-vs-cli) to build an integration on Zapier’s Platform.

* The Platform UI lets you create a Zapier integration in your browser without code using API endpoint URLs. You can set any custom options your API may need, including custom URL params, HTTP headers, and request body items.

* Zapier Platform CLI lets you build a Zapier integration in your local development environment, collaborate with version control and CI tools, and push new versions of your integration from the command line.

Both of these tools run on the same Zapier platform, so choose the one that fits your workflow the best. You can try both methods out with the [Platform UI tutorial](https://platform.zapier.com/quickstart/ui-tutorial) and the [Platform CLI tutorial](https://platform.zapier.com/quickstart/cli-tutorial).

## 3. Create a new integration

Create and add details about your integration. Set your Intended audience to select **Private: I’m building an integration for personal use or to explore the Zapier platform**. 

* [Create an integration using Zapier Platform UI](https://developer.zapier.com/app/new)
* [Create an integration using Zapier Platform CLI](https://github.com/zapier/zapier-platform/blob/main/packages/cli/README.md#creating-a-local-app)
  
> **Note**: When building with Zapier Platform CLI, you’ll only need to set your intended audience when you register your app.

## 3. Add an authentication scheme

Configuring authentication allows users to input credentials to authenticate with your API. 

* [Authentication using Zapier Platform UI](https://platform.zapier.com/build/auth)
* [Authentication using Zapier Platform CLI](https://github.com/zapier/zapier-platform/blob/main/packages/cli/README.md#authentication)

  * [Authentication schema](https://github.com/zapier/zapier-platform/blob/main/packages/schema/docs/build/schema.md#authenticationschema)

## 4. Configure triggers

Triggers are how your app’s users can start automated workflows whenever an item is added or updated in your app. Use webhook subscriptions or polling API endpoints to create triggers.

* [Configure a trigger using Zapier Platform UI](https://platform.zapier.com/build/trigger)
* [Configure a trigger using Zapier Platform CLI](https://github.com/zapier/zapier-platform/blob/main/packages/cli/README.md#triggerssearchescreates)

  * [Trigger schema](https://github.com/zapier/zapier-platform/blob/main/packages/schema/docs/build/schema.md#triggerschema)

## 5. Configure actions

Actions allow users to either create, search or update records in your app via your API.

* [Create an action using Zapier Platform UI](https://platform.zapier.com/build/action)
* [Create an action using Zapier Platform CLI](https://github.com/zapier/zapier-platform/blob/main/packages/cli/README.md#triggerssearchescreates)

  * [Search schema](https://github.com/zapier/zapier-platform/blob/main/packages/schema/docs/build/schema.md#searchschema)
  * [Create schema](https://github.com/zapier/zapier-platform/blob/main/packages/schema/docs/build/schema.md#createschema)

## 6. Test your integration

While you’re building your integration, you can test your API requests within the Platform UI. For developers building on Zapier Platform CLI, you can write unit tests that run locally, in a CI tool like [Travis](https://travis-ci.com/).

To get a sense of the user experience, it’s recommended to test your integration within the Zap editor. [Create a new Zap](https://help.zapier.com/hc/en-us/articles/8496309697421) that uses your integration’s triggers or actions to ensure they all work as expected. After you’re done building, invite users to try your integration before making it available to a wider audience.

Learn more about testing your integration:

- [Testing using Zapier Platform UI](https://platform.zapier.com/build/test-integration)
- [Testing using Zapier Platform CLI](https://github.com/zapier/zapier-platform/blob/main/packages/cli/README.md#testing)

## 7. [Optional] Validate your integration

Run automated checks to identify errors and recommendations on how to improve the user experience of your private integration. These checks are required to pass for public integrations, and are recommended for a better user experience for private integrations. 

* [Run automated checks using Zapier Platform UI](https://platform.zapier.com/publish/integration-checks-reference)
* [Run automated checks using Zapier Platform CLI](https://github.com/zapier/zapier-platform/blob/main/packages/cli/docs/cli.md#validate)

## 8. [Optional] Invite team members

You can assign different roles and permissions to team members who you’re collaborating with on your private integration. 

* [Invite team members using Zapier Platform UI](https://platform.zapier.com/manage/add-team)
* [Invite team members using Zapier Platform CLI](https://github.com/zapier/zapier-platform/blob/main/packages/cli/README.md#sharing-an-app-version)

## 9. [Optional] Share your integration

Once you’ve built your integration, you can share it with other Zapier users so they can [create Zaps](https://help.zapier.com/hc/en-us/articles/8496309697421-Create-Zaps) with it.

* [Share your integration](https://platform.zapier.com/manage/sharing)

## 10. Conclusion

Once you’ve built your private integration, continue to make further improvements and manage versions of your integration.

* [Manage integration versions using Zapier Platform UI](https://platform.zapier.com/manage/versions#managing-versions-in-platform-ui)
* [Manage integration versions using Zapier Platform CLI](https://platform.zapier.com/manage/versions#managing-versions-in-platform-cli)


> **Tip**: Learn from the Zapier team and other [Zapier Platform developers in our community forum](https://community.zapier.com/p/developer-zone).