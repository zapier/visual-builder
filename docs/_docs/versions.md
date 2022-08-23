---
title: Versions
order: 16
layout: post-toc
redirect_from: /docs/
---

# Manage Versions of Your Zapier Integration

Your Zapier integration should be ready to use when first launched—minimal, perhaps, but with the basics covered. The app authentication will let users connect to your API, and the triggers and actions should get data to and from your API.

Over time, though, things will change. Users will request new triggers and actions, or want to send and receive more data with your existing ones. You’ll add new features to your app and want to add them to your Zapier integration, too. And eventually, your API may change, and your Zapier integration’s authentication or API calls may need to be changed as well.

That’s where versions come in. Zapier lets you create multiple versions of your integration to test and build new features without interrupting existing users. You can then release the new version to some users, ensure everything is working, and eventually migrate all of your users to the new version. After that, you can deprecate and remove the old version.

This guide will cover the steps for _Cloning_, _Promoting_, _Migrating_, and _Deprecating_ integration versions in more detail. Put briefly, the process of creating a new version of your integration takes three steps in either the Developer Platform [Visual Builder](https://developer.zapier.com/) or [Zapier Command Line Interface](https://platform.zapier.com/cli_tutorials/getting-started) (CLI).

In the Visual Builder:

1. In the sidebar on the left, navigate to **Manage**, then **Versions**
2. Select the gear icon next to the version you’d like to update, then select **Clone**
3. Select a new version number, then **Clone** and **Edit** to create the new version and begin editing it

Using the Zapier CLI:

1. Increment the version number in your app’s `package.json` file
2. Make the necessary updates to the rest of the app’s resources
3. Run `zapier push` to build and upload the new version to Zapier

This guide is intended to cover version management in the Visual Builder. If you're using the CLI, we recommend reading the [CLI version tutorial](https://platform.zapier.com/cli_tutorials/versions).

## Which Version Can Users Access?

A Zapier integration can be either _Private_, _Beta_, or _Public_. Private integrations require an [invitation](https://platform.zapier.com/docs/testing#how-to-invite-others-to-test-new-integrations) for users to access it. Public and Beta integrations can be seen by Zapier users on [the public Apps page](https://zapier.com/apps). Each integration can have many versions, but only one version can be public at a time, while the rest remain private. 

Newly published integrations will feature a _Beta_ tag when first published. While your integration is in Beta, we’ll monitor how it’s performing. When your integration reaches 50 users, our team will get in touch to invite you to start the [official partner program](https://zapier.com/platform/partner-program) launch process.

To review your integration’s versions, open it in the Visual Builder and navigate to Manage then Versions. This page shows a list of all versions of the integration, along with status and the number of users of each.

![The Versions page in the Zapier Developer Platform](https://cdn.zappy.app/220a5f0055ab88b41ec83bfa953db20b.png)

> **Note:** In the Zapier CLI, you can also run `zapier versions` to see the information in your terminal.

For Public apps, which are searchable in the Zap Editor/App Directory, a user that selects your integration in the Zap Editor will be using the current Public version by default. Optionally, you can use the Sharing page to send users an invitation to a specific private version, which will allow them to select it in the Zap Editor. This is also how all users of Private integrations are added.

## Making Changes

To make edits to a version of your integration in the Developer Platform Visual Builder, select it in the Version dropdown menu in the top right, or select **Edit** from the options menu on the Versions page.

![Highlighting the Version dropdown menu, and Edit option on the Versions page](https://cdn.zappy.app/bea20fbdee6ee96c6af4cf39261481a2.png)

That will update the _Authentication_, _Triggers_, _Actions_, and _Advanced_ sections to reflect the latest changes to that version. You can then make changes in those sections as needed, and saving those changes will automatically apply them to the version (and by extension, any Zaps using it). 

While using the Zapier CLI, you can change which version you are editing by updating the version number in your `package.json` file. When you run `zapier push` your code will overwrite the specified version. While optional, we also recommend using some form of versioning software, such as GitHub or GitLab, to keep track of previous versions of your code.

## Why can’t I edit a particular version?

To make sure that existing Zaps can continue to work consistently, the Zapier Developer Platform only allows you to edit versions that are Private and have fewer than 5 users. Versions that are Public or have more than 5 users will show a warning message prompting you to Clone the version instead.

!['You can't edit this version'](https://cdn.zappy.app/8b5cbf5a37ce60ba89eb555c0429eca6.png)

## Cloning

_Cloning_ is a process in the Zapier Developer Platform Visual Builder that allows you to create a new version of your integration, based on a previous one. 

> **Note:** While the term “cloning” doesn’t appear in the Zapier CLI, this is equivalent to updating the version number in `package.json` and running `zapier push` to create a new version. 

To clone a version of your integration, navigate to **Manage** then **Versions** in the Developer Platform, and select the **gear icon** next to the version you’d like to duplicate. 

![Selecting the 'Clone' option](https://cdn.zappy.app/6b8b23a4943bfe11c8dd4abd29bf8994.png)

That will open a window that prompts you to select a number for the new version, to help represent the kinds of changes you plan on making.

![The 'Clone Version' window, showing the options for a new version number](https://cdn.zappy.app/7cd3bf761bb35529c33d5bd5c9c376db.png)

Zapier uses semantic versioning numbers, which gives you three options to choose from:

* **Patch** (e.g. 1.0.0 to 1.0.1) can be used for changes that are still compatible with the previous version, such as fixing a bug or updating help text.
* **Minor** (e.g. 1.0.0 to 1.1.0) is recommended for changes that add new functionality without changing what’s already there, such as creating a new trigger or action.
* **Major** (e.g. 1.0.0 to 2.0.0) is used when making changes that are likely to break existing Zaps, such as removing triggers or actions, changing authentication methods, or starting over from scratch.

Select the version that feels correct based on your plans, then click **Clone** to create the new version and start editing it.

## Promoting a version

After your integration has entered the _Beta_ or _Public_ status, one of its versions also becomes _Public_, meaning users see and use it by default. The process of changing which version is Public is called _Promotion_, and can be done from either the CLI or the Versions page. 

In the CLI, running `zapier promote [version]` will make the specified version number the new Public version. [Read more about that here](https://platform.zapier.com/cli_docs/docs#promoting-an-app-version).

In the Visual Builder, head to **Manage** then **Versions**, and select the **gear icon** next to the version you’d like to make public. In the menu that appears, select **Promote**.

![Selecting 'Promote' on the Versions page](https://cdn.zappy.app/dd4fccc5acb2beb2194ca448871c0d4d.png)

If you’re working with an integration that’s currently private, the _Promote_ option won’t appear. Instead, make sure users you’d like to test or move to the new integration version are invited to that version, and encourage them to try it out.

### What happens when a version is promoted?

* Zap templates are updated to use the new Public version of your app
* Any new triggers or actions will appear on your integration’s public app page
* When a user selects your integration in a new Zap, they’ll use the promoted version by default

## Migrating users

Once you’ve added all the changes needed to your integration, you can start rolling it out to users to update their existing Zaps and let users make new Zaps with your new integration features.

If you made a new version with only minor, non-breaking changes, you can migrate existing users and Zaps to your new integration version. On the **Versions** page, select the **Migrate** option on your new integration version.

![Selecting the 'Migrate' option on the Versions page](https://cdn.zappy.app/ee93e158cfe97f48a2cdc7b8881df405.png)

That will reveal a screen that will allow you to move users between two versions. Select the _From_ and _To_ versions, then select **Migrate** to begin moving users to the selected version.

![After selecting 'Migrate', the Migration window allows you to select 'From' and 'To' versions](https://cdn.zappy.app/5d8d487544914ddaa1c72037b331aad1.png)

When migrating users, you are also migrating their Zaps. This means that any active Zaps using the _From_ version will begin using the _To_ version as soon as the migration is complete. This makes it a great solution for Patch and Minor updates, but _not_ a recommended option for Major updates. For Major updates, review our section on Deprecation instead.

In some cases, it may be more useful to migrate only a portion of the current users, to ensure that the minor change did not accidentally introduce any unforeseen issues. You can do that using the **Percentage** option in the Migration window, or select **Email** to migrate only one user at a time.

![Using the Percentage slider to migrate only 55% of users](https://cdn.zappy.app/5b3a6a1a49fbed8e22a4b423f72d35d0.png)

You can then repeat the Migration process later on, and migrate the rest of the users once you are comfortable with how the new version is running in production.

> **Note:** It is also possible to migrate a portion of users with the CLI using the `zapier migrate` command. [Read more about that here](https://platform.zapier.com/cli_docs/docs#deploying-an-app-version). 

### What is a “breaking change”?

Before performing a migration, it is important to consider all Zaps which are currently running on previous versions of your integration. The configuration of these Zaps will not be modified during the migration, so they will need to be capable of functioning correctly on both the old and new versions.

Because of that, a “breaking change” can be defined as any modification to the integration which renders existing Zaps incompatible with the new version. Examples include:

* Removing an input or output field on a trigger/action
* Changing the Authentication scheme
* Making a previously optional input field “required”
* Deleting a trigger/action

## Deprecating versions

_Deprecation_ is an optional process that allows you to set a date from which a non-Public version of your integration will no longer be supported. This is usually recommended after promoting a major update which cannot support automatic migration of users due to breaking changes. It allows Zapier to notify all of that version's users that a new version is available, and that action is required on their part to update their Zaps manually.

To deprecate a Private version, select the **gear icon** next to the version number on the Versions page, then select **Deprecate**.

![The window that opens when selecting 'Deprecate'](https://cdn.zappy.app/7e62435659f494a9143aa1602640ef97.png)

> **Note:** You can also set a deprecation date using the CLI, with the `zapier deprecate` command. [More about that here](https://platform.zapier.com/cli_docs/docs#promoting-an-app-version).

When a deprecation date is set, Zapier sends a notification to that version’s users, to let them know about the need to upgrade to the latest Public version. Users can then manually update their Zaps, and ensure that the new version fits their workflows.

After the deprecation date has passed, the version will still be available in the Versions page for future reference. You can even invite users to it with the options in the Sharing page, like you would with a Private version.

### Should I deprecate or delete?

You may have noticed that it’s also possible to _Delete_ versions from the Versions page. That option will fully remove the version from the Developer Platform, meaning that neither you nor users will be able to access it from that time — so use it with caution! 

In most cases, either deprecation or leaving a private version untouched are recommended, and deletion should only be used when absolutely necessary.

## Can I start over?

In some cases, it may make sense to rebuild your integration from scratch. For example, if your company has introduced a new product, or if the API that was originally used with the integration is now considered “Legacy”. There’s also a chance that it’s just been a while since you’ve used Zapier, and you wish to refresh your knowledge of the Developer Platform.

Because our mutual users see your Zapier integration as an extension of your brand, we do not allow creating separate integrations in these cases. Even if the new integration is clearly labelled as “New App!” or “App V2”, having two separate versions of your brand available often causes confusion amongst users, so we have this restriction in place to prevent them selecting the wrong version by mistake.

Instead, we recommend cloning the latest version of your integration, and picking the **Major** version number change. The triggers, actions, and even authentication of the new version can be changed entirely, so that the update looks and feels like a brand new app, but maintains the brand consistency for our end users.

It is also possible to change which development environment your integration is built in, to help make the experience of building the new version easier for your team:

If your integration was built with our [Visual Builder](https://developer.zapier.com), you can export and convert it to the Zapier CLI using [the steps provided here](https://platform.zapier.com/docs/export). The CLI gives full control over your integration’s code, and is a great fit for teams of developers who are used to sharing code via tools like GitHub or GitLab.

Alternatively, if your integration was built with the Zapier CLI, and your team would prefer to use our Visual Builder moving forward, please [contact our Support team](https://developer.zapier.com/contact) to let us know. In some cases, we can create a new version of your integration that can be edited on the Visual Builder, while allowing the existing CLI integration to continue running.