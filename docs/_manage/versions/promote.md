---
title: Promote a version
order: 3
layout: post-toc
redirect_from: 
---
# Promote a version

After your integration has entered the beta or public status, you can set a new default version for public use. This process is called promoting a version.

## Promote a version with Platform UI 

1. Log into the [Platform UI](https://zapier.com/app/developer).
2. Select your **integration**. 
3. In the *Manage* section in the left sidebar, click your **Versions**.  
4. On your version you want to promote, click the **three dots icon** <img style="vertical-align: middle;" src="https://cdn.zappy.app/7ff6381b55b013ebfc2bdda0e4662676.png" alt="navMoreHoriz icon" width="24">.
5. To make the chosen version the public and default version, click **Promote**.


![Platform UI Versions tab, showing where to find the three dots icon](https://cdn.zappy.app/2ee11c82946187818a9622c4b4bf65bc.png)

> **Note**: If you have a private integration, you will not see the *Promote* option. Instead, you can [share your new version](https://platform.zapier.com/manage/share-integration) with users.

## Promote a version with Platform CLI

In the Platform CLI, you can run `zapier promote [version]` to make the specified version number the new public and default version. Learn more about [promoting a version using the Platform CLI ](https://platform.zapier.com/reference/cli-docs#promoting-an-app-version).


## What happens after you promote a version?

After successfully promoting a version:

- **Zap templates update**: If there are no breaking changes, all Zap templates will be updated to use the new public version.
- **New triggers and actions**: Any newly added triggers or actions will be displayed on your integration's public app page.
- **User experience**: Users who select your integration for a new Zap will interact with the promoted version by default.

By following these steps, you can seamlessly promote a new version of your integration, ensuring that your users have access to the latest features and improvements.