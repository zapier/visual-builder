---
title: Build your first public integration on Zapier
order: 1
layout: post-toc
redirect_from: /partners/lifecycle-planning
---

# Build your first public integration on Zapier

This guide gives an overview of the process to publishing a public integration. 

## Benefits to building a public integration

- Building a public integration on the Zapier Platform is free.
- There are no fees for publishing an integration.
- Users of your integration are responsible for their own Zapier plans and billing.
- Partners do not incur fees as a result of the usage of their integration.
- You'll get support from [Zapier's Partner Program](https://platform.zapier.com/publish/partner-program) once your app has been successfully reviewed.

To get a picture of how your integration will show up on Zapier's website, you can browse the[ app directory](https://zapier.com/apps). It's a great idea to explore similar apps to see what triggers and actions they provide for building Zapier workflows, called Zaps.

## **1. Before you start**

Consider workflows your app will support, and what types of activities your users want to automate. Learn[ how Zapier works](https://platform.zapier.com/quickstart/how-zapier-works) and set up a few Zaps to get a sense of the user experience.

To design useful triggers and actions for your integration, consider how your users might need data from your app to run other parts of their business. Some of the most popular use cases for Zapier integrations include:

- Sending follow-up emails or messages
- Copying data from a bill or invoice into another system
- Updating contact records in multiple databases
- Creating or updating records in a project management tool

Learn more about how to [design an integration](https://platform.zapier.com/quickstart/integration-design-examples).

## **2. Build your integration**

Building a Zapier integration means identifying the right APIs for your triggers and actions, and designing an intuitive experience for your users to select and map the data they need.

There are two ways to build an integrations on Zapier’s Platform:

- The Platform UI lets you create a Zapier integration in your browser without code using API endpoint URLs. You can also set any custom options your API may need, including custom URL params, HTTP headers, and request body items, using code mode.
- Zapier Platform CLI lets you build a Zapier integration in your local development environment, collaborate with version control and CI tools, and push new versions of your integration from the command line.

Both of these tools run on the same Zapier platform, so choose the one that fits your workflow the best.

Learn more about the difference between building with the[ Platform UI and the CLI](https://platform.zapier.com/quickstart/zapier-platform).

## **3. Test your integration**

While you’re building your integration, you can test your API requests within the Integration Builder. For developers building on Zapier Platform CLI, you can write unit tests that run locally, in a CI tool like[ Travis](https://travis-ci.com/).

To get a sense of the user experience, it’s recommended to test your integration within the Zap editor.[ Create a new Zap](https://zapier.com/help/create/basics/create-zaps) that uses your integration’s triggers or actions to ensure they all work as expected. After you’re done building, invite users to try your integration before making it available to a wider audience.

Learn more about testing your integration:

- [Testing using Zapier Platform UI](https://platform.zapier.com/build/test-integration)
- [Testing using Zapier Platform CLI](https://platform.zapier.com/reference/cli_docs#testing)

## **4. Submit your integration for app review**

After you've confirmed your integration is working, you're almost ready to publish your app. To publish your integration, you need to submit your app for review.

Before submitting your integration, review[ Zapier’s integration publishing guidelines](https://platform.zapier.com/publish/integration-publishing-guidelines) to speed up the app review process.

To submit your integration for app review:

1. [Log into the Platform UI](https://zapier.com/app/developer)
2. Select your **integration**.
3. In _Integration Home_, click **Publish.**
4. You’ll need to complete our online form.
5. Click **Submit for Review**.

After you’ve submitted your integration for review, one of our developers will reach out to you in 1 week or less. Zapier will update your:

- App version to **Pending**.
- App status will remain as **Private**.

## **5. Beta phase**

When your integration is approved, Zapier will update your:

- App status to **Public**.
- App version will update to **Beta**.
- Integration will be added to[ Zapier’s app directory](https://zapier.com/apps) with a Beta tag.

Your integration will remain in beta for 90 days.

Whilst in public beta, we recommend completing these tasks to improve your integration:

### **Add help docs to Zapier’s Help Center**

The Zapier team provide frontline support for your integration, and in order to provide the best experience for your users, we also host help documentation about your integration in the[ Zapier Help Center](https://help.zapier.com/hc/en-us). Help our Technical Writing team create accurate documentation by filling out [this form](https://eu.jotform.com/form/202233475923352). We can also include link out to documentation on your site to help customers find the information they are looking for.

Once submitted, it takes roughly 2 weeks to get help docs published in the Help Center.

> **Tip:** As you maintain your integration, you can use the same form to submit updates at any time to the Technical Writing team.

### **Create Zap templates**

As soon as your app is published and in beta you can begin creating and sharing[ Zap Templates](https://platform.zapier.com/publish/zap-templates). Zap Templates are readymade integrations or Zaps with the apps and core fields pre-selected. In a few clicks, they help people discover a use case, connect apps, and turn on the Zap.

Learn more about creating[ Zap templates](https://platform.zapier.com/publish/zap-templates).

### **Embed Zapier in your product or website**

The best way to ensure users are able to discover your Zapier integration is to surface your integration where users are looking at it. By embedding Zapier in your product, you can create end-to-end user experience, helping your customers discover available integrations within your product without having to leave your app.

Learn more about[ embedding Zapier](https://platform.zapier.com/embed/overview).

### **Grow active usage**

During the beta stage of your integration, it's important to actively work on growing the usage of your app. By encouraging more people to use your integration, you'll be able to gather valuable insights and feedback early on, which will help you optimize it further.

Learn more strategy[ tips to improve your integration](https://platform.zapier.com/publish/partner-program-tips).

### **Manage bugs and feature requests**

With the Zapier Issue Manager, you have the ability to conveniently address bugs and new feature requests within your preferred issue-tracking tool. Regularly reviewing and taking action on these items will greatly contribute to enhancing the overall health score of your integration.

Learn more about[ Zapier Issue Manager](https://platform.zapier.com/publish/zapier-issue-manager).

## **6. Public phase**

After 90 days in public beta, your integration will become public:

- Your app status will be updated to public, and the beta tag will be removed.
- You’re added to our[ Partner Program](https://zapier.com/platform/partner-program), where you can earn marketing and support benefits.

Learn more about [maintaining your Zapier integration](https://platform.zapier.com/manage/user-feedback).
