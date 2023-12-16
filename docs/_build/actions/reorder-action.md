---
title: Reorder or remove action
order: 4
layout: post-toc
redirect_from:
---

# Reorder or remove action

## Reordering actions

Whenever a user selects your app's integration in a Zapier action step, they'll see every _create_ and _search_ action in your integration. Zapier shows _create_ actions first, followed by _search_ actions. Within the Create and Search sections, actions are listed in alphabetical order and this order cannot be changed.

![Actions inside Zapier](https://cdn.zappy.app/5d3c2e8f9f6cf0f6daadd3ee97fa5e80.png)

If you don't want an action to be shown, you can change the action's visibility at any time. 

To change an actions's visibility:
1. Log into the [Platform UI](https://zapier.com/app/developer).
2. Select your **integration**. 
3. In the _Build_ section on the left sidebar, click **Actions**. 
4. Click on the action whose visibility you wish to change.
5. Scroll to the bottom of the page to the **Visibility in Editor** and select `Hidden` if you want to keep users from being able to select the action
6. Users with that action selected in their existing Zaps would continue to be able to use it, but if they edit the Zap and select a different action, they will not be able to select the `Hidden` action again. 

## Removing actions

You may want to remove an action your app no longer supports. Deleted actions cannot be restored.

If you remove an action from a live Zapier integration, this will break existing Zaps. As such, before removing an action, always [create a new major version](https://platform.zapier.com/manage/versions) of your integration, hide the action in the new version, to allow users to [manually switch to a new action](https://platform.zapier.com/manage/change-keys) without breaking their Zaps. Monitor integration usage by action from the Dashboard to only remove actions with no usage. 

To remove an action: 
1. Log into the [Platform UI](https://zapier.com/app/developer).
2. Select your **integration**. 
3. In the _Build_ section on the left sidebar, click **Actions**. 
4. Click on the ellipses for the action you wish to remove, and click **Delete**.
5. On the confirmation prompt, click **Delete**

![Remove Zapier action](https://cdn.zappy.app/809321da0cd78edef6f464eb1f803855.png)