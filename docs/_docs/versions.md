---
title: Versions
order: 15
layout: post-toc
redirect_from: /docs/
---

# Manage Versions of Your Zapier Integration

Your Zapier integration should be quite nice when first launched—minimal, perhaps, but with the basics covered. The app authentication will let users connect to your API, and the triggers and actions should get data to and from your API.

Over time, though, things will change. Users will request new triggers and actions, or want to send and receive more data with your existing ones. You’ll add new features to your app and want to add them to your Zapier integration, too. And eventually, your API may change, and your Zapier integration’s authentication or API calls may need changed as well.

That’s where versions come in. Zapier lets you create multiple versions of your integration to test and build new features without interrupting existing users. You can then release the new version to some users, ensure everything is working, and eventually migrate all of your users to the new version—and remove the old, original integration.

Here’s how.

## Manage Integration Versions in Zapier

![Zapier integratin versions](https://cdn.zapier.com/storage/photos/4294ed1a2f6c7e3980cb9ac9c43f8655.png)

Zapier’s visual builder includes a _Versions_ tab in the left sidebar. New integrations only include the original `1.0.0` version, the same version that Zapier lists in the top left of the visual builder as your app’s current version.

Click either the version number in the top left of your Zapier visual creator sidebar or the gear icon beside your version in the _Versions_ tab to make changes. You can _Clone_ your integration to make a new version based on the features you already added to your integration—then once that version is ready, you can _Promote_ the new version to have new users start using it.

## Clone Your Integration

![Clone Zapier integration](https://cdn.zapier.com/storage/photos/dca2130ce5dddca928519ad60130d35a.png)

Creating a new version of your Zapier integration is easy as you never need to start over. Instead, to make a new version, always start by cloning an existing version. That lets you start with an exact copy of your integration where you can make the changes and additions you need.

To make a Clone, click the version button in the top left of the Zapier visual creator sidebar or the gear icon in the _Versions_ tab, and select _Clone_. In the dialog, select the version to clone from (usually the most recent version, unless you want to roll back recent changes). Then choose what type of version you want to create:

- **Patch**: A `x.x.1` version, typically used to fix bugs and issues in existing integrations
- **Minor**: A `x.1.x` version, typically to add new minor features to existing integrations
- **Major**: A `2.x.x` version to launch a full new version of your integration with new triggers and or actions

Once you clone the integration, you can directly click the _Edit_ button to tweak the new version of your integration, or click _Close_ to go back to your existing, active integration.

## Edit a Version of Your Integration

![Edit Zapier integration version](https://cdn.zapier.com/storage/photos/a506b0a211b75a473fe71a59781eca12.png)

You can add, edit, and test features in your new integration version just as you did in the original version. All you need to do is switch between your integration versions to add changes to the new version, not the original.

To edit a specific integration version, open the _Versions_ tab, click the gear icon beside the version you want to edit, and select _Edit_. You can then see anytime what version you’re editing from the version number in the top left of your Zapier visual editor sidebar.

You can also test any version of your integration from Zapier’s standard Zap editor. Search for your app name when adding a Zap step, and Zapier will show multiple entries on your account with the version number beside each. Select the newest one to test your new changes.

## Migrate Users to Your New Integration Version

![Migrate users to new Zapier integration version](https://cdn.zapier.com/storage/photos/49423feb86f237b5186d7efdcaf2ac53.png)

Once you’ve added all the changes needed to your integration, you can start rolling it out to users to update their existing Zaps and let users make new Zaps with your new integration features.

If you made a patch version with only minor, non-breaking changes, you can migrate existing users and Zaps to your new integration version. Select the _Migrate_ option on your new integration version, then choose which older version of your integration to move users from—and the new version to move them to. Finally, choose what percentage of users to migrate. Typically, Zapier recommends moving a small percentage of your users—perhaps 10 or 20%—to the new integration to make sure everything is working as expected. Once everything seem fine, you can migrate the remainder of your users to the new integration.

Major versions of integrations—especially if authentication or API calls were changed and other breaking changes were added—will require users to re-create their Zaps with the new version of your integration. In that case, you won’t be able to migrate existing users but instead will need to promote the new version and depreciate the old one so new users and Zaps will be made with the new integration.

## Promote a New Version of Your Integration

You can also Promote your new integration version to make it the default version that Zapier shows to users when creating new Zaps. Select the _Promote_ button in your version settings to mark an integration as the new default version.

## Depreciate an Older Version of Your Integration

![Depreciate Zapier integration version](https://cdn.zapier.com/storage/photos/dd6acdd75278ecd733a5f3945ea641a2.png)

If you did introduce breaking changes to your integration and want existing users to switch to the new version, you can depreciate the old version. That will let your older integration and Zaps that use it continue to run—but they will include a `(Legacy)` tag in the Zapier editor to prompt users to re-build the Zap with the new integration. Additionally, when adding a new Zap step, Zapier will no longer recommend the older, depreciated version of your integration.

To depreciate a version, select _Depreciate_ in the Versions menu, then select a date to depreciate the integration in the calendar drop-down. Choose a date between two weeks and a year from today, then click the _Depreciate_ button to confirm.

Zapier will then show a yellow exclamation mark beside that version in your integration’s versions menu, showing the date it will be depreciated if you hover over it. You’ll also be able to see your user count as it goes down, switching from the old integration version to the new.

## Delete Older Versions of Your Integration

![Delete Zapier integration version](https://cdn.zapier.com/storage/photos/86bf4dbabd06b989d7717f95e8479fba.png)

Once you’ve depreciated an integration version and it has no existing users, you can delete that version to clean up your Zapier integration.

Click the _Delete_ button in your version’s gear menu, select _Really?_ when asked to confirm, and Zapier will remove that version of your integration. And since Zapier will only delete depreciated versions with no users, you never have to worry about accidentally removing a version with features you need.