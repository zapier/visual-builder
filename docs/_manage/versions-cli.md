---
title: Manage integration versions in Platform CLI
order: 7
layout: post-toc
redirect_from: /manage/
---

# Manage integration versions in Platform CLI

Your Zapier integration should be quite nice when first launched—minimal, perhaps, but with the basics covered. The app authentication will let users connect to your API, and the triggers and actions should get data to and from your API.

Over time, though, things will change. Users will request new triggers and actions, or want to send and receive more data with your existing ones. You’ll add new features to your app and want to add them to your Zapier integration, too. And eventually, your API may change, and your Zapier integration’s authentication or API calls may need to be changed as well.

That’s where versions come in. Zapier lets you create multiple versions of your integration to test and build new features without interrupting existing users. You can then release the new version to some users, ensure everything is working, and eventually migrate all of your users to the new version. After that, you can deprecate and remove the old version.

## Manage Integration Versions in Zapier

An App Version is related to a specific App but is an “immutable” implementation of your app. This makes it easy to run multiple versions for multiple users concurrently. The App Version is pulled from the version within the `package.json`. To create a new App Version, update the version number in that file. By default, **every App Version is private** but you can `zapier promote` it to production for use by over 1 million Zapier users.

**Examples**

```
# push your app version to Zapier
zapier push

# list your versions
zapier versions
```

One way to improve your workflow is to possibly link your Zapier app versions to you git workflow. Here are guides on how to manage your releases within [GitHub](https://docs.github.com/en/repositories/releasing-projects-on-github/managing-releases-in-a-repository) or [GitLab](https://docs.gitlab.com/ee/user/project/releases/). This will help if you ever need to rollback and/or keep track of and sync all of the versions you have on Zapier with your own repository.

## Edit a Version of Your Integration

You can add, edit, and test features in your new integration version just as you did in the original version. All you need to do is switch between your integration versions to add changes to the new version, not the original.

To create a new version of your integration within your CLI app, all you need to do is go to the `package.json` file within your project. Once you’re in there, simply change the version number, that’s it! Once that is changed, you are free to _push_ that new version, so Zapier can see it.

You can also test any version of your integration from Zapier’s standard Zap editor. Search for your app name when adding a Zap step, and Zapier will show multiple entries on your account with the version number beside each. Select the newest one to test your new changes.

**Additions Vs Enhancements**

The two main ways to edit your integration will either be adding new features or changing existing Triggers/Actions/Searches to have new functionality or bug fixes. There are a couple of things you want to keep in mind when doing either.

**Additions**

When adding new Triggers/Actions/Searches, feel free to add all of the ones you would like. However, I would encourage you to keep in mind the workflows or use-cases you are attempting to enable. The best integrations have a curated list of Triggers/Actions/Searches rather than every endpoint that exists in your API. One way to see what kinds of features users are asking for is to utilize our “Issues” section on your app, within the UI. Our support team will open up new bugs and or feature requests based on user feedback.

**Enhancements**

Outside of adding new features, you can modify or update existing functionality to improve the experience for your users. Zapier’s Zaps are configured based on the JSON representation of what comes back from your API, so if you ever remove any fields being returned or modify that structure, this is considered a breaking change. If you modify a new version of your app that does have a breaking change on a Trigger/Action/Search, you will not be able to migrate users to that new version.

There are two strategies for this. You can “hide” the existing Trigger/Action/Search that users are using, and then create a new version with the enhancements for those new users. This would enable you to bring your users between versions as this is helpful when you only are improving something relatively small. However, when there is a larger change where you would like to deprecate the older Trigger/Action/Search if you are retiring that endpoint or upgrading the whole API for example, you will want to leave users on the old version and not migrate them between versions. The reason for this, is you can use our built-in [deprecation tool](#deprecate-an-older-version-of-your-integration) to alert users that they will need to manually migrate their Zaps to the latest version by a specific date.

## Testing Your Integration

One advantage building your integration within the CLI environment, you can write your own unit tests!
See our complete [Testing Guide here](../cli_docs/docs#testing).

## Migrate Users to Your New Integration Version

Once you’ve added all the changes needed to your integration, you can start rolling it out to users to update their existing Zaps and let users make new Zaps with your new integration features.

If you made a patch version with only minor, non-breaking changes, you can migrate existing users and Zaps to your new integration version. For a complete guide to the `migrate` command, look [here](../cli_docs/cli#migrate).

Typically, Zapier recommends moving a small percentage of your users—perhaps 10 or 20%—to the new integration version to make sure everything is working as expected. Once everything looks good, you can migrate the remainder of your users to the new version.

Major versions of integrations—especially if authentication or API calls were changed and other breaking changes were added—will require users to re-create their Zaps with the new version of your integration. In that case, you won’t be able to migrate existing users. Instead, you’ll need to promote the new version and deprecate the old one so new users and Zaps will be made with the new integration.

**Examples**

```
# migrate 100% of your users between version 1.0.0 over to 1.0.1
zapier migrate 1.0.0 1.0.1

# migrate 15% of your users between version 1.0.1 over to 2.0.0
zapier migrate 1.0.1 2.0.0 15

# migrate the specific user user@example.com between version 2.0.0 to 2.0.1
zapier migrate 2.0.0 2.0.1 --user=user@example.com
```

## Promote a New Version of Your Integration

You can also Promote your new integration version to make it the default version that Zapier shows to users when creating new Zaps. For a complete guide to the `promote` command, look [here](../cli_docs/cli#promote).

If this isn’t the first time you’ve promoted your app - you might have users on older versions. You can `zapier migrate` to either move users over (which can be dangerous if you have breaking changes). Or, you can `zapier deprecate` to give users some time to move over themselves.

**Examples**

```
# promote your app version to all Zapier users
zapier promote 1.0.1

# OPTIONAL - migrate your users between one app version to another
zapier migrate 1.0.0 1.0.1

# OR - mark the old version as deprecated
zapier deprecate 1.0.0 2020-06-01
```

## Deprecate an Older Version of Your Integration

If you introduce breaking changes to your integration and want existing users to switch to the new version, you can deprecate the old version.

Deprecation is only recommended if the older integration version will eventually stop working, such as if the related API will be removed. Zapier is normally a “set it and forget it” experience for users, so use this feature carefully.

When you deprecate an integration version:

* The Zaps that use it will continue to run until the deprecation date. On the deprecation date, they will be paused.
* Zapier will send users with active Zaps a notification that they need to update their Zaps.
* When adding a new Zap step, Zapier will no longer show the deprecated version of your integration as an option.

Zap steps using this integration version will include a Deprecated tag in the Zapier editor, to help prompt users to re-build the Zap with the new integration.

To deprecate a version, you will use the deprecate command. For a complete guide to the `deprecate` command, look [here](https://platform.zapier.com/reference/cli-docs#deprecate).

**Example**

```
# deprecates version 1.2.3 on October 1st, 2021
zapier deprecate 1.2.3 2021-10-01
```

Zapier then shows a yellow exclamation mark beside that version in your integration’s versions menu, showing the date it will be deprecated when you hover over it. You can also track your user count as it goes down, switching from the old integration version to the new.

## Delete Older Versions of Your Integration

Once you’ve deprecated an integration version and it has no existing users, you can delete that version to clean up your Zapier integration. This is mostly for clearing out old test apps you used personally.

To deprecate a version, you will use the `delete:version` command. For a complete guide to the `delete:version` command, look [here](https://platform.zapier.com/reference/cli-docs#deleteversion). The command will fail if there are any users. You probably want `deprecate` instead.

**Example**

```
# deletes version 1.0.0
zapier delete:version 1.0.0
```
