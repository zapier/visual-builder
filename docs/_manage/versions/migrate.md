---
title: Migrate users to a new version
order: 4
layout: post-toc
redirect_from: 
---

# Migrate users to a new version

If you have minor changes to improve your integration, you can migrate users to the latest version. When you migrate users to your latest version, it will update all of their Zaps, including Zaps turned on.

## What's the difference between minor and major changes?

Minor changes would would not prevent their Zaps, including Zaps turned on, continuing to work as normal. Minor changes need to be compatible with both the previous and new version.

Major changes would cause active Zaps to error and potentially turn off. They would require users to update the Zap in order to get it working again.  Learn more about [breaking changes to your integration](https://platform.zapier.com/manage/versions-ui#what-is-a-breaking-change) and the impact it can have on users. 

Zapier recommends not to migrate users for major changes. Instead  [deprecate the version](https://platform.zapier.com/manage/versions-ui#deprecating-versions) and allow users to [update to the latest integration version](https://help.zapier.com/hc/en-us/articles/18755649454989-Update-to-the-latest-app-version-in-Zaps).

## Migrate users to new version

### Platform UI

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
    - **Email**. To email users one at a time. **Note**: migrating a single user will only migrate Zaps that are private for that user. Zaps that are [shared across the team](https://help.zapier.com/hc/en-us/articles/8496277647629) or [shared app connections](https://help.zapier.com/hc/en-us/articles/8496326497037-Share-app-connections-with-your-team) will not be migrated.
        - If the *Email* field, add the **user's email address** attached to their Zapier account. 
        - Click **Migrate**.
6. The *Versioning sidebar* will update to show *Update status:Estimating*. Once the migration has been completed, the *Versioning sidebar* will disappear.

Once you're confident that the new version works well, you can go ahead and migrate the rest of your users.

### Platform CLI

For Platform CLI users, it's possible to perform full or partial migrations using the [zapier migrate command](https://platform.zapier.com/manage/versions-cli#migrate-users-to-your-new-integration-version). 