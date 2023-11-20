---
title: Reorder or remove triggers
order: 4
layout: post-toc
redirect_from: 
---

# Reorder or remove triggers

## Reordering triggers

Triggers are listed in alphabetical order in the Zap editor and this order cannot be changed. 

You can, however, change a trigger’s visibility to control if it is shown to users or not. 

To change a trigger's visibility:
1. Log into the [Platform UI](https://zapier.com/app/developer).
2. Select your **integration**. 
3. In the _Build_ section on the left sidebar, click **Triggers**. 
4. Click on the trigger whose visibility you wish to change.
5. Scroll to the bottom of the page to the **Visibility in Editor** and select `Hidden` if you want to keep users from being able to select the trigger.
6. Users with that trigger selected in their existing Zaps would continue to be able to use it, but if they edit the Zap and select a different trigger, they will not be able to select the `Hidden` trigger again. 

![](https://cdn.zappy.app/51c3b8911b5384ddf03b9dbfffd40050.png)

## Removing triggers

You may want to remove a trigger that your app no longer supports, or fully rebuild a new one in place of the previous one.

> Note: It is best practice to not remove a trigger that has been used in a live integration version. If a trigger is in use, it is recommended to [hide it rather than deleting it](https://platform.zapier.com/manage/making-changes#updates-to-triggeractionsearch-keys). Only remove unused triggers from staging or development versions. 

To remove a trigger:
1. Log into the [Platform UI](https://zapier.com/app/developer).
2. Select your **integration**. 
3. In the _Build_ section on the left sidebar, click **Triggers**. 
4. Click on the ellipses for the trigger you wish to remove, and click **Delete**.
5. On the confirmation prompt, click **Delete**

![](https://cdn.zappy.app/fc65459abad8ac60504f6085078bb361.png)

Deleted triggers cannot be restored.