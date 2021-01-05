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

## How to Upgrade Your Zapier Integration

If you have an integration that's usable by other people (either as invite-only or public), there are limitations on the types of changes that you can make in your integration, in order to avoid breaking the Zaps that your users have created on it.
Sometimes, there are occasions when you need to make a "major change" to an integration - either switching things to use a newer version of the endpoints/API (and thus, changing the structure of the data that's used), changing the authentication type (like switching to OAuth v2 tokens), or rewriting a Web-Builder integration using our [CLI Platform](https://zapier.github.io/zapier-platform/cli) .

In these cases, here’s our 4-step approach to upgrading your integration to the V3 UI verson:

### 1. Reach out to our Partnerships Team

Contact us at [partners@zapier.com](mailto:partners@zapier.com) with your intentions **before you start building** the updated integration and we'll help get you started in the right direction. Giving us a heads up will expedite the review process of and help set proper expectations for the replacement integration. We also recommend reading our [blog post](https://zapier.com/engineering/api-auth-migration/) on auth migration best practices and pitfalls, with real-world examples.

### 2. Get Your App Converted

Once all checks are passed, our team will run your app through the conversion process from a Web Builder integration to the upgraded v3 Visual Builder UI counterpart. The latest version of the developer platform offers all new platform tools, overall greater control over your app lifecycle with versioning and deprecation facilities and much more.


### 3. Testing Phase

From here, we’ll ask you to run some thorough tests on the new integration **without** altering any code. These tests will involve making Zaps for each Trigger and Action and confirming they work correctly. The goal here is to weed out any possible issues that may have risen from the conversion process and get them addressed sooner rather than later. Errors we would be looking out for here would be issues with converted app functionality (Auths no longer working, Triggers returning different data, etc). 

If after testing there are still errors or other unintended behaviour found, we’ll fix these issues and ask you to retest again.
Once no errors are found in testing, and the v3 app works as expected, you let us know and we begin migrating.


### 4. Migration

Once no errors are found in testing, and the v3 app works as expected, you let us know and we will begin migrating all your users and their Zaps to the new app version. This is purely a backend process with zero impact to your users, they won’t have to worry about this.

### We're here to help!

As always, please contact us at [partners@zapier.com](mailto:partners@zapier.com) if you have any questions!
