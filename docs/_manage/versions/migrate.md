---
title: Migrate users to a new version
order: 4
layout: post-toc
redirect_from: 
---

# Migrate users to a new version

If this isn’t the first time you’ve promoted your app - you might have users on older versions. If you have made minor, non-breaking changes to improve your integration, you can migrate users to the latest version. When you migrate users to your latest version, it will update all of their Zaps, including Zaps turned on.

## What's the difference between minor and major changes?

Minor changes allow Zaps to continue to work as normal. Minor changes need to be compatible with both the previous and new version. 

When migrating users to a new version, only active Zaps (not [draft](https://help.zapier.com/hc/en-us/articles/8496260938125-Create-drafts-of-your-Zaps )) are migrated. In some cases, after migration, users that have drafts with an older version of the app may edit that draft and publish the draft, thereby publishing a Zap with an older version of the app.

Zapier recommends migrating a small portion of your existing users to the new integration version to make sure everything is working as expected. Monitor the logs in the Monitoring tab, and migrate the remainder of your users to the new version when ready.

Major changes would cause active Zaps to error and potentially turn off. They would require users to manually update the Zap in order to get it working again.  Learn more about [breaking changes to your integration](https://platform.zapier.com/manage/making-changes), best practices and the user impacts. 

Zapier recommends not to attempt to migrate users for major changes. **Migration is not required unless the older version will no longer function.** If necessary, you can [deprecate the version](https://platform.zapier.com/manage/versions-ui#deprecating-versions) to prompt users to [manually update to the latest integration version](https://help.zapier.com/hc/en-us/articles/18755649454989-Update-to-the-latest-app-version-in-Zaps). Please note that deprecating a version is significantly more disruptive to our mutual users than migrating to the latest promoted version, or than leaving users on an older (now) private version when migration is not possible. 

When users are left on an older private version, they will see a [prompt in the Zap editor](https://help.zapier.com/hc/en-us/articles/18755649454989-Update-to-the-latest-app-version-in-Zaps) to encourage them to make the update themselves. 

## Migrate users to new version with Platform UI

In the [Platform UI](https://zapier.com/app/developer):
1. In the _Manage_ section in the left sidebar, click your **Versions**.  
2. On your existing version, click the **three dots icon** <img style="vertical-align: middle;" src="https://cdn.zappy.app/7ff6381b55b013ebfc2bdda0e4662676.png" alt="navMoreHoriz icon" width="24">.
3. Click **Migrate**
4. The *Versioning* sidebar will appear on the right hand side. You'll need to specify:
    - **From Version**. Select which version
    - **To Version**. Select the new version you wish to migrate new users too.
5. In the *Which users(s) to migrate* field, select either: 
    - **Percentage**. This will allow you to migrate users, based on percentage between 5% to 100%. This cautious approach helps ensure that minor updates haven't inadvertently caused any issues. 
        - Select a **percentage**  
        - Click **Migrate**.
    - **Email**. To migrate users one at a time, by email. **Note**: migrating a single user will only migrate Zaps that are private for that user. Zaps that are [shared across the team](https://help.zapier.com/hc/en-us/articles/8496277647629) or [shared app connections](https://help.zapier.com/hc/en-us/articles/8496326497037-Share-app-connections-with-your-team) will not be migrated.
        - In the *Email* field, add the **user's email address** attached to their Zapier account. 
        - Click **Migrate**.
6. The *Versioning sidebar* will update to show *Update status:Estimating*. Once the migration has been completed, the *Versioning sidebar* will disappear.

Once you're confident that the new version works well, you can go ahead and migrate the rest of your users.

## Migrate users to new version with Platform CLI

For Platform CLI users, it's possible to perform full or partial migrations using the [zapier migrate command](https://github.com/zapier/zapier-platform/blob/main/packages/cli/docs/cli.md#migrate). 

**Examples**

```
# migrate 100% of your users between version 1.0.0 over to 1.0.1
zapier migrate 1.0.0 1.0.1

# migrate 15% of your users between version 1.0.1 over to 2.0.0
zapier migrate 1.0.1 2.0.0 15

# migrate the specific user user@example.com between version 2.0.0 to 2.0.1
zapier migrate 2.0.0 2.0.1 --user=user@example.com
```