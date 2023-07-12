---
title: Platform UI guide
order: 7
layout: post-toc
redirect_from: /quickstart/
---

# Platform UI guide

This guide provides a comprehensive overview of the steps you will need to take to create an integration using the Zapier Platform UI.

## Prerequisite

- You’ll need a [Zapier account](https://zapier.com/sign-up).
- If you haven’t used Zapier before, learn the basics in our [Zapier Getting Started Guide](https://zapier.com/learn/zapier-quick-start-guide/).

## 1. Add an integration

To add an integration:

- Go to [https://developer.zapier.com/](https://developer.zapier.com/).
- Click **Start a Zapier Integration**.

You'll start by creating your integration the the Platform UI, where you'll need to provide information about the name, description, logo, and add information about the integration you're building.

Learn more about [adding an integration](https://platform.zapier.com/build/add) and the difference of building a [private or public integration](https://platform.zapier.com/quickstart/private-vs-public-integrations).


## 2. Add an authentication

The first thing to set up is [authentication](https://platform.zapier.com/build/auth). Your integration defines how Zapier’s platform authenticates with the API and what data needs to be collected from users to allow access to their accounts. Zapier supports most popular authentication schemes, including basic auth with username and password, API key auth, digest, session, and OAuth v2.

Whenever someone uses your integration in a Zap, they’ll first select your app, then will connect their account. That’s where the authentication flow comes in. Zapier shows a popup window where users login and select their account with OAuth2, or where they can enter account details with basic auth.

## 3. Add a trigger

Triggers allow users to find new data as soon as it’s available in your app. Use webhooks or polling endpoints to [create triggers](https://platform.zapier.com/build/trigger).

## 4. Add an action

[Actions](https://platform.zapier.com/build/action) allow users to either create, search or update records through your API.

## 5. Test your integration

Test your authentication, triggers, actions, and how your private integration works inside Zapier.

Learn more about [testing your integration](https://platform.zapier.com/build/test-integration).

## (Optional) Validate your integration

[Run automated checks](https://platform.zapier.com/publish/integration-checks-reference) to identify errors and recommendations on how to improve the user experience of your integration.

## (Optional) Invite team members

You can [add and assign different roles and permissions to team members](https://platform.zapier.com/manage/invite-team-member) who you’re collaborating with on your integration.

## (Optional) Share your integration

Once you’ve built your integration, you can [share it with users](https://platform.zapier.com/manage/share-integration) who can can create Zaps with it.

## Conclusion

Now that you've created your integration, you can continue to make further improvements and [manage versions](https://platform.zapier.com/manage/versions-ui) of your integration.


> **Tip**: Learn more about the [different types of support](https://platform.zapier.com/quickstart/support) available to help you build your integration.