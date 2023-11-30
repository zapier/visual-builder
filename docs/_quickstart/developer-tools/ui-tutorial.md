---
title: Platform UI tutorial
order: 2
layout: post-toc
redirect_from: 
    - /quickstart/platform-ui-guide
    - /quickstart/what-you-need
    - /quickstart/create-integration
    - /docs/start
    - /build/add
---

# Platform UI tutorial

This tutorial walks you through the process of building an integration on Zapier with authentication, a trigger and an action using the Platform UI. 

## Prerequisites

- You'll need a [Zapier account](https://zapier.com/sign-up).
- If you haven’t used Zapier before, you'll want to learn the basics in our [Zapier Getting Started Guide](https://zapier.com/learn/zapier-quick-start-guide/).
- Familiarity with [APIs](https://zapier.com/resources/guides/apis)
- Select an API with public documentation, whether your own app's API or an app you're familiar with as a user.

## 1. Start an integration

To add an integration:

- Go to [https://developer.zapier.com/](https://developer.zapier.com/).
- Log into your Zapier account. 
- Click **Start a Zapier Integration**.
- Next, you will be ask to provide information about your integration:
  - **Name**: Add the name of your integration. 
  - **Description**: Add a description the app in 140 characters or less.
  - **Homepage URL**: Add the homepage URL of your app. The domain will be used as the email domain to allow team members to [join your integration as a collaborator](https://platform.zapier.com/manage/invite-team-member).
  - **Logo**: Upload a square, transparent PNG image of your app logo. The image must be at least 256x256px in size, and doesn't include the app name. Learn more in [branding guidelines](https://platform.zapier.com/publish/integration-brand-design-guidelines).
  - **Intended Audience**: From the dropdown menu, select if you are building a [public or private integration](https://platform.zapier.com/quickstart/private-vs-public-integrations).
  - **Role**: Select your relationship with the app you're integrating with Zapier from the dropdown menu.
  - **Category**: Select how you would categorize your app from the dropdown menu. 
- Once you have completed adding details your integration, click **Create**. 
 

## 2. Add authentication

[Authentication](https://platform.zapier.com/build/auth) defines how Zapier’s platform authenticates with the app's API you're connecting to, collecting and storing user data to allow access to their accounts. Zapier supports the following authentication schemes:
- [API key](https://platform.zapier.com/build/apikeyauth)
- [Basic authentication with username and password](https://platform.zapier.com/build/basicauth)
- [Digest](https://platform.zapier.com/build/digestauth)
- [OAuth v2](https://platform.zapier.com/build/oauth)
- [Session](https://platform.zapier.com/build/sessionauth)

Refer to the API documentation for the app you're building with to choose the correct authentication scheme for your API. Add the authentication fields for the input form your users will see when connecting their app account to Zapier. 

Move through each configuration step of your chosen authentication scheme, adding the relevant endpoint to be used as the authorization URL to exchange the credentials supplied by the user for authentication. Depending on your API's authentication method, you may also need to configure Zapier-provided application credentials in your app's developer settings. 


## 3. Add a trigger

[Triggers](https://platform.zapier.com/build/trigger) allow users to start Zapier workflows when something is added or updated in the app. 

Add settings for how your trigger displays to users, any optional input fields, and connect the app's API in the API Configuration tab. 

If the API you're building with supports REST Hooks, you can configure your trigger to create a unique subscription from every Zap to your app that will run in near real-time and send events to Zapier as they occur in your app. 

Alternatively, configure a polling trigger that automatically polls the URL you've provided for new data every 1 to 15 minutes, depending on the user’s Zapier plan. An appropriate polling endpoint will return results in reverse chronological order to make sure new or updated items can be found on the first page of the results. Polling an endpoint most commonly uses a GET request. 

The default _Form Mode_ allows you to add API endpoint URLs, choose the API call type, and include any authentication details and input form data with the API call. 

The optional toggle into [_Code Mode_](https://platform.zapier.com/build/code-mode) converts everything entered in the API request form to JavaScript code and is an advanced feature beyond the scope of this tutorial. 

## 4. Add an action

[Actions](https://platform.zapier.com/build/action) allow users to create, search, or update records in your app through your API. In general, delete actions are not recommended for integrations. 

Add settings for how your action displays to users, and at least one input field and connect the app's API in the API Configuration tab. 

Refer to the API documentation for your app to choose a frequently used record with an available endpoint and add a create action that will add an record in your app when tested. Creating a new record most commonly uses a POST request.   

## 5. Test your integration

When building an integration, it's important to test the functionality of your authentication, triggers, and actions in the Platform UI and also in the [Zap editor](https://zapier.com/editor/). In the Zap editor, you'll see how users of your integration will create Zaps using your triggers, and actions.

Learn more about [testing your integration](https://platform.zapier.com/build/test-integration).

## 6. (Optional) Validate your integration

[Run automated checks](https://platform.zapier.com/publish/integration-checks-reference) to identify errors and recommendations on how to improve the user experience of your integration.

These checks are only required to pass if you are building a public integration, but they are also useful to identify suggestions for future updates to any integration. 

## 7. (Optional) Invite team members

Integrations are not owned by individuals, but rather by teams. You can invite team members to collaborate with in the Platform UI as either an admin or a collaborator. 

Learn more about [adding team members](https://platform.zapier.com/manage/invite-team-member) to your integration. 

## 8. (Optional) Share your integration

Once you have at least one trigger or action, you'll want to share your integration with some users. Early feedback helps make sure you're building functionality that will be used.

You can [share your integration with users](https://platform.zapier.com/manage/share-integration) by a public link or by email. 

Note: [Public integrations](https://platform.zapier.com/quickstart/private-vs-public-integrations) can be accessed by any Zapier user and doesn't require users to be specially invited. 

## 9. Modify your integration

If you need to make any changes to your integrations, you can do so by creating [a new version](https://platform.zapier.com/manage/versions-ui). Versions helps to track and manage changes to your integration over time.

Public integrations or private integrations with more than 5 users **must have** a new version to make any edits. It is still recommended to make changes for private integrations with fewer than 5 users in a new version as well and [consider Zapier's best practices](https://platform.zapier.com/manage/making-changes) when doing so. 

## Learn more

- Recommended features for your integration [by app category](https://platform.zapier.com/build/recommended-integration-features). 
- [Step-by-step tutorial](https://community.zapier.com/featured-articles-65/zapier-platform-ui-a-complete-guide-on-how-to-integrate-with-github-26298#post108889) that uses the GitHub API. 
- About [different types of support](https://platform.zapier.com/quickstart/support) available to help you build your integration.