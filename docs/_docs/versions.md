---
title: Versions
order: 15
layout: post-toc
redirect_from: /docs/
---

# Manage Versions of Your Zapier Integration

Your Zapier integration should be quite nice when first launched—minimal, perhaps, but with the basics covered. The app authentication will let users connect to your API, and the triggers and actions should get data to and from your API.

Over time, though, things will change. Users will request new triggers and actions, or want to send and receive more data with your existing ones. You’ll add new features to your app and want to add them to your Zapier integration, too. And eventually, your API may change, and your Zapier integration’s authentication or API calls may need to be changed as well.

That’s where versions come in. Zapier lets you create multiple versions of your integration to test and build new features without interrupting existing users. You can then release the new version to some users, ensure everything is working, and eventually migrate all of your users to the new version. After that, you can deprecate and remove the old version.

## Manage Integration Versions in Zapier

![Zapier integration versions](https://cdn.zapier.com/storage/photos/4294ed1a2f6c7e3980cb9ac9c43f8655.png)

Zapier’s Platform UI includes a _Versions_ page in the left sidebar. New integrations provide a starter `1.0.0` version, and you can create other versions as needed.

Click the gear icon beside a version on the _Versions_ page to make changes. You can _Clone_ your integration to make a new version based on the features of an existing version. Once the new version is ready, you can _Promote_ the new version to have new users start using it.

## Decide on How You Want to Work

You and your team can decide what works best for your workflow. You can continue building and developing an integration within the UI, or if your developers prefer to work within a standard [Node.js](https://nodejs.org/en/) app, you can export your app and work within the CLI environment.

When creating a new version of your Zapier integration in the UI, you never need to start over. Instead, to make a new version, start by cloning an existing version. That lets you start with an exact copy of your integration where you can make the changes and additions you need. Learn how to clone your integration [here](#clone-your-integration).

Or if you prefer to export your app for the CLI environment, learn how to do that [here](./export) and skip the cloning portion of this guide.

## Clone Your Integration

![Clone Zapier integration](https://cdn.zapier.com/storage/photos/dca2130ce5dddca928519ad60130d35a.png)

When creating a new version of your Zapier integration, you never need to start over. Instead, to make a new version, start by cloning an existing version. That lets you start with an exact copy of your integration where you can make the changes and additions you need.

To clone a version, click the gear icon in the _Versions_ page, and select _Clone_. In the dialog, select the version to clone from (usually the most recent version, unless you want to roll back recent changes). Then choose what type of version you want to create:

- **Patch**: A `x.x.1` version, typically used to fix bugs and issues in existing integrations
- **Minor**: A `x.1.x` version, typically to add new minor features to existing integrations
- **Major**: A `2.x.x` version to launch a full new version of your integration with new triggers and or actions

Once you clone the integration, click the _Edit_ button to tweak the new version of your integration, or click _Close_ to go back to the _Versions_ page.

## Edit a Version of Your Integration

![Edit Zapier integration version](https://cdn.zapier.com/storage/photos/a506b0a211b75a473fe71a59781eca12.png)

You can add, edit, and test features in your new integration version just as you did in the original version. All you need to do is switch between your integration versions to add changes to the new version, not the original.

To edit a specific integration version, either select it from the upper left of the Platform UI sidebar, or open the _Versions_ page, click the gear icon beside the version you want to edit, and select _Edit_. You can see  what version you’re editing from the version number in the top left of the sidebar anytime.

You can also test any version of your integration from Zapier’s standard Zap editor. Search for your app name when adding a Zap step, and Zapier will show multiple entries on your account with the version number beside each. Select the newest one to test your new changes.

**Additions Vs Enhancements**

The two main ways to edit your integration will either be adding new features or changing existing Triggers/Actions/Searches to have new functionality or bug fixes. There are a couple of things you want to keep in mind when doing either.

**Additions**

When adding new Triggers/Actions/Searches, feel free to add all of the ones you would like. However, I would encourage you to keep in mind the workflows or use-cases you are attempting to enable. The best integrations have a curated list of Triggers/Actions/Searches rather than every endpoint that exists in your API. One way to see what kinds of features users are asking for is to utilize our “Issues” section on your app. Our support team will open up new bugs and or feature requests based on user feedback.

**Enhancements**

Outside of adding new features, you can modify or update existing functionality to improve the experience for your users. Zapier’s Zaps are configured based on the JSON representation of what comes back from your API, so if you ever remove any fields being returned or modify that structure, this is considered a breaking change. If you modify a new version of your app that does have a breaking change on a Trigger/Action/Search, you will not be able to migrate users to that new version.

There are two strategies for this. You can “hide” the existing Trigger/Action/Search that users are using, and then create a new version with the enhancements for those new users. This would enable you to bring your users between versions as this is helpful when you only are improving something relatively small. However, when there is a larger change where you would like to deprecate the older Trigger/Action/Search if you are retiring that endpoint or upgrading the whole API for example, you will want to leave users on the old version and not migrate them between versions. The reason for this, is you can use our built-in [deprecation tool](#deprecate-an-older-version-of-your-integration) to alert users that they will need to manually migrate their Zaps to the latest version by a specific date.

## Migrate Users to Your New Integration Version

![Migrate users to new Zapier integration version](https://cdn.zapier.com/storage/photos/49423feb86f237b5186d7efdcaf2ac53.png)

Once you’ve added all the changes needed to your integration, you can start rolling it out to users to update their existing Zaps and let users make new Zaps with your new integration features.

If you made a patch version with only minor, non-breaking changes, you can migrate existing users and Zaps to your new integration version. Select the _Migrate_ option on your new integration version, then choose which older version of your integration to move users from, and the new version to move them to. Finally, choose what percentage of users to migrate. 

Typically, Zapier recommends moving a small percentage of your users—perhaps 10 or 20%—to the new integration version to make sure everything is working as expected. Once everything looks good, you can migrate the remainder of your users to the new version.

Major versions of integrations—especially if authentication or API calls were changed and other breaking changes were added—will require users to re-create their Zaps with the new version of your integration. In that case, you won’t be able to migrate existing users. Instead, you'll need to promote the new version and deprecate the old one so new users and Zaps will be made with the new integration.

## Promote a New Version of Your Integration

You can also Promote your new integration version to make it the default version that Zapier shows to users when creating new Zaps. Select the _Promote_ button in your version settings to mark an integration as the new default version.

If you're working with an integration that's currently private, the _Promote_ option isn't used. Instead, make sure users you'd like to test or move to the new integration version are [invited](./testing#how-to-invite-others-to-test-new-integrations) to that version, and encourage them to try it out.

## Deprecate an Older Version of Your Integration

![Deprecate Zapier integration version](https://cdn.zapier.com/storage/photos/dd6acdd75278ecd733a5f3945ea641a2.png)

If you introduce breaking changes to your integration and want existing users to switch to the new version, you can deprecate the old version.

Deprecation is only recommended if the older integration version will eventually stop working, such as if the related API will be removed. Zapier is normally a "set it and forget it" experience for users, so use this feature carefully.

When you deprecate an integration version:

* The Zaps that use it will continue to run until the deprecation date. On the deprecation date, they will be paused.
* Zapier will send users with active Zaps a notification that they need to update their Zaps.
* When adding a new Zap step, Zapier will no longer show the deprecated version of your integration as an option.

Zap steps using this integration version will include a `Deprecated` tag in the Zapier editor, to help prompt users to re-build the Zap with the new integration.

To deprecate a version:

* Select _Deprecate_ in the Versions menu.
* Select a date to deprecate the integration version in the calendar drop-down. Choose a date between two weeks and a year from today when Zaps using that version will no longer work. 
* Click the _Deprecate_ button to confirm.

Zapier then shows a yellow exclamation mark beside that version in your integration’s versions menu, showing the date it will be deprecated when you hover over it. You can also track your user count as it goes down, switching from the old integration version to the new.

## Delete Older Versions of Your Integration

![Delete Zapier integration version](https://cdn.zapier.com/storage/photos/86bf4dbabd06b989d7717f95e8479fba.png)

Once you’ve deprecated an integration version and it has no existing users, you can delete that version to clean up your Zapier integration.

Click the _Delete_ button in your version’s gear menu, select _Really?_ when asked to confirm, and Zapier will remove that version of your integration. Since Zapier will only delete deprecated versions with no users, you never have to worry about accidentally removing a version that's in active use.
