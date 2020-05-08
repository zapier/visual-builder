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

![Update Zapier integration details](https://cdn.zapier.com/storage/photos/1075ef17df9d18db368adaed7e1d24bc.png)

You can update your app's name, description, logo, and category anytime in the [Zapier Platform site](https://zapier.com/app/developer). Select your app integration, click the gear icon near its name, then update the app details as needed.

If you built your app using Zapier Platform CLI, you can also update the app name and description from the integration bundle's `package.json` file. You will still need to use the [Zapier Platform site](https://zapier.com/app/developer) to update your app icon and category.

If your app is public, you'll then need to [send us a request](mailto:partners@zapier.com) to publish those changes.

Please make sure to follow [Zapier's branding guidelines](https://platform.zapier.com/partners/planning-guide) whenever updating app branding.

## How to Monitor Feature Requests and Bugs

![Issues in Zapier Integration](https://cdn.zapier.com/storage/photos/7e214665d64998a7cc8c3276e5b8f86f.png)

As people use your Zapier integration, they may encounter buggs and problems with your integration, or think of new ways they'd like to use your app with Zapier, and send them to the Zapier support team. We log those in Zapier's issue tracker, which you can see from the _Issues_ tab on your app's Developer Platform settings page.

Problems and issues with your integration, authentication, API calls, and more will be logged as `bug`, while new things users requires from your integration will be logged as `feature request`.

![Reply to Zapier Integration Issue](https://cdn.zapier.com/storage/photos/a793bc2741fd1c82159c01d0a59fe735.png)

Whenever a new issue is added or updated, Zapier will log it in the _Issues_ tab of your app's Zapier Developer Platform settings page. Zapier will also send an email notification about the issue to your integration's original developer.

You can see additional details about the issue, along with the trigger or action it affects and how many users have encountered the issue, in Zapier's issue tracker. You can reply to the Zapier team about the issue there, or can simply reply to the notification email to add a response to the issue.

![Get Zapier Integration Issue Notification Emails](https://cdn.zapier.com/storage/photos/3ac5c7bc98568aac786a7b87fc2695ef.png)

If you want others on your team to receive the issue notifications, or would like to route them to your support or developer team inbox, you can add additional notification email addresses from the bottom of the _Issues_ tab. You may also remove the original developer from the issue after you've added an additional contact.

## How to Make a New Version of Your Integration

Sometimes you may want to add something new to your integration. You may need to fix bugs in your integration, or add additional details to resolve user issues. You might want to add additional triggers, actions, or searches to your integration as uses request them. Or, over time, you may need to change your app's authentication and API calls.

The Zapier platform makes it easy to build new versions of your integration when needed. You can create new versions for minor or major changes as needed.

Non-breaking changes, or changes to an integration that do not effect the way it works, may be added at any time. You may change your app's branding, update the name and description of triggers, actions, and input fields to your integration at any time.
Breaking or major changes, such as switching to a new API endpoint, changing authentication type, or rewriting an integration, require a new version and approval from our team.

Non-breaking changes are still best to build in a new integration version so you can test the features and roll them out to a smaller subset of your Zapier integration users. Once you've made sure the new features work well, you can roll them out to all of your users.

Breaking changes require a new major version of your integration. That requires users to re-create their Zaps with the new version of your integration. You can test the new version privately, as when you first built your Zapier integration. Once it's ready for wider use, you can promote the new integration version and deprecate the older version. Zapier will then mark Zaps using the older integration as _Legacy_, and will show the new version instead of the original integration when users make new Zaps.

_→ Find how to manage versions in [Zapier Platform UI](https://platform.zapier.com/docs/versions) and [CLI](https://zapier.github.io/zapier-platform-cli/#deploying-an-app-version)_

## How to Replace Your Zapier Integration

If you have an integration that's usable by other people (either as invite only or public), you will additionally need to follow our our 4-step approach to replacing your integration with a new one:

### 1. Reach out to our Partnerships Team

Contact us at [partners@zapier.com](mailto:partners@zapier.com) with your intentions **before you start building** the updated integration and we'll help get you started in the right direction. Giving us a heads up will expedite the review process of and help set proper expectations for the replacement integration. We also recommend reading our [blog post](https://zapier.com/engineering/api-auth-migration/) on auth migration best practices and pitfalls, with real-world examples.

### 2. Build the Replacement Integration for a "Hide and Replace"

Your team will build a completely new version of the integration with the same triggers, actions, and searches as your original integration if at all possible. You will need to have 10 test users for the new version of your integration with at least 1 live Zap for each trigger, action, and search, just as with a new integration. Then, you will need to re-submit your integration for approval as with a new integration.

> **Note:** You will need to accumulate enough test users on your new integration before you can request for review. Please expect some time between when you submit for review and when the new integration is made “Public”, as the speed of the review depends on how closely your integration matches our style guide and the responsiveness of your team to our feedback.

When the review process is complete, we'll "hide" the older version of your integration, and deploy the newer version, so it becomes the default version that's used for creating new Zaps.

If the existing API endpoints in the old integration are **still working and available**, they are set as “Pending.” Existing users’ Zaps will continue to work "as is", but no users will be able to create new Zaps with the old version. Any Zaps using the old integration will show a “Legacy” label to prompt users to update their Zaps to use the new one.

If the existing API endpoints will be **deprecated/terminated**, or an **older authentication type is no longer usable**, after we deploy the new version of the integration, existing users’ Zaps will only continue to work as long as the original endpoints are available.

### 3. Migrate Users and Zaps to the new integration

At this time, the users and Zaps on the old integration should be migrated over to the new version. This is **not** done automatically during the "Hide and Replace" step of the replacement.

If the existing API endpoints in the old integration are **still working and available**, the Zapier team will **not** assist you with migrating users and Zaps to the new version. You will need to send out communication to notify your users to update their Zaps on your own.

If the existing API endpoints will be **deprecated/terminated**, or an **older authentication type is no longer usable**, we can assist with migrating over Zaps and users if discussed in advance, so please reach out to [partners@zapier.com](mailto:partners@zapier.com) as early as possible to discuss migration plans and tips on preserving compatibility with the existing integration. Once we've ascertained the new integration is working well, we'll start converting/migrating users and their Zaps from the older integration, and switch them to the newer integration.

This migration process occurs gradually and may take a few weeks or months to complete depending on the quantity of Zaps that are present, and the number of issues that are encountered during the Zap migration. This is to help ensure any edge-cases won't result in a large eruption of data errors if/when a large quantity of Zaps are converted. Our shared goal is to move our mutual users to the new integration as seamlessly as possible.

#### Common Reasons Why Migrations Can't Occur

* The new integration doesn’t have a Trigger, Action, or Search for every respective step being used in a Zap on the old version.
* The new integration requires inputs (trigger or action fields) the old version did not.
* Authentication has changed, and there is no way to programmatically swap in the new authentication for the old authentication.
* The data from the new integration has changed in a way that does not maintain 1:1 parity with the data returned from the old integration, or the format of data returned has changed.

### 4. Migrate existing Zap Templates

We'll also determine whether we can reuse/migrate the [Zap Templates](https://zapier.com/developer/documentation/v2/zap-templates/) for your integration, or need to remove all the Zap Templates if the keys/fields in the data have changed significantly. Templates may not be migrated right away when the ‘Hide and Replace’ occurs, but will be placed in a queue to be migrated in priority order.

### We're here to help!

As always, please contact us at [partners@zapier.com](mailto:partners@zapier.com) if you have any questions!
