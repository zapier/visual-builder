---
title: Deprecate or delete a version
order: 5
layout: post-toc
redirect_from: 
---

# Deprecate or delete a version

Deprecation is an optional process that allows you to set a date from which a non-public version of your integration will no longer be updated. This is only applicable after promoting a major update that cannot support automatic migration of users due to breaking changes. When the older version will no longer function, it will be deprecated.

## What happens after setting a version to deprecate

### 1. Email notification

After setting the date, an initial email will be sent to users, informing them that they need to manually update their Zaps to continue using the new version. Zapier recommend supplementing these automated messages by also notifying your general user base through in-app announcements or email marketing campaigns. For privacy reasons, Zapier cannot provide you with an email list of users of your integration.

### 2. Deprecation date reached

  - Zaps that haven't been updated will be automatically paused.
  - A second email, titled “X Zaps paused over deprecated apps,” will be sent out to those users. Customizing this email is not possible.
  - The deprecated version will be labelled as “Deprecated” in the Zap editor, with a prompt for users to update to the latest version.

### 3. Post-deprecation

After the deprecation date, the version will still be visible in the Versions page for your future reference. Although you can technically still invite users to the deprecated version, it's not recommended.

## Deprecate a version: Platform UI

To deprecate an integration version:

1. Log into the [Platform UI](https://zapier.com/app/developer).
2. Select your **integration**. 
3. In the _Manage_ section in the left sidebar, click **Version**. 
4. Click the **three dot** icon in line with the integration version you want to deprecate.
5. Click **Deprecate**.
6. In the dialog box, add the **Deprecate Date**. You can set a deprecation date anytime between 2 weeks and 1 year from the current date.
7. Click **Deprecate**. 
8. Click **Close**

Once you've completed your deprecation of your version, Zapier recommends to [promote your new version] to users.

## Deprecate a version: Platform CLI

To deprecate an integration version use the command zapier deprecate. Learn more about [Platform CLI commands](https://github.com/zapier/zapier-platform/blob/main/packages/cli/README.md#user-content-deploying-an-app-version).

## Deleting deprecated versions

You have the option to delete versions entirely, but exercise this option with extreme caution. Deleting a version makes it permanently inaccessible, both to you and to your users.

In most scenarios, it’s advisable either to deprecate the version or leave it as a private version. Deletion should be a last resort, used only when you are certain that the version will never be needed again.