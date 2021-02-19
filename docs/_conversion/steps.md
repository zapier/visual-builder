---
title: Step by Step Guide
order: 2
layout: post-toc
redirect_from: /conversion/
---


# Step By Step Guide

**Before you begin:** it’s important that you don’t make any edits to your integration during the conversion process. If you encounter errors during the process, email us at partners@zapier.com and we’ll resolve the issue.

## STEP 1: CONVERT YOUR INTEGRATION

To get started, create a copy of your integration on the new platform. This is a non-destructive operation. It doesn’t change your existing integration or impact your existing users’ Zaps.

Navigate to your integration built on the legacy web builder. At the top of the integration page, you’ll see a banner message with details about the platform update. Click “Get Started” to begin the conversion process.

The tool will identify older copies of your integration to include in the conversion. Copies of your integration will be available as [versions](/docs/versions) of your new integration on the new platform. If any of the copies identified by the tool are separate products, clear the checkbox for those copies. 

_Select Get Started_
![](https://cdn.zappy.app/5d4479163eb1d8448b5a5850b83ad596.png)

_Confirm Copies of Your Integration_
![](https://cdn.zappy.app/0e8430b75ea09f1f2c23091e1fe6ed4a.png)

_Done. Ready to Navigate to the New Tool._
![](https://cdn.zappy.app/0df71bf63b59386c08586a75643cc375.png)

## STEP 2: TEST YOUR NEW INTEGRATION

Now you’ve created a copy of your integration on the new developer platform. The next step is to test your triggers and actions in the Zap editor to make sure everything is working as expected. We’ve provided a checklist to track each trigger and action to test. 

Within the Zap editor, check the task history to confirm there aren’t any errors. If you encounter any issues, email us at partners@zapier.com. Our team will investigate and correct whatever went wrong with your integration conversion.  It’s very important you don’t make changes to the new copy of your integration.

After testing is complete, you’re ready to update your existing users’ Zaps to use the new integration.

### Testing tips

>Ensure that you’re using the _new_ integration to test your triggers and actions. This version is not yet available within Zapier’s public app directory. 

The new platform’s web-based development tool has a feature to create test Zaps. Your new integration’s triggers and actions will be listed on the left sidebar navigation. Select one and you’ll see an option to create a Zap with this trigger or action.

![](https://cdn.zappy.app/098ef458bac63799457ad55e342101d9.png)

Click “Create a Zap” to create a new Zap with this trigger or action in the Zap editor. In this example, we’ll test a trigger from the Bitbucket integration. Add a simple action to verify that data is being passed properly, such as Slack’s send message action. Map your fields to make sure some data is present in your results.

![](https://cdn.zappy.app/018da0dc09fba1f5a9e9fcc46f07a003.png)

When you’re done configuring your Zap, click “Turn on Zap” to test it.

![](https://cdn.zappy.app/711c9ea75998ffabadc130127eeaa10d.png)

Next, force your trigger to execute. In the Bitbucket example, I created a new issue.

You should see your action run. To check the details in your task history, click the clock icon in the right sidebar menu to verify that your trigger/action/search is returning the correct data.

![](https://cdn.zappy.app/f6b9865ed7c6fd95d67b36f986ed9d8c.png)

![](https://cdn.zappy.app/22fca8a22adbe6727154374c51c7b586.png)

### If your integration has hidden triggers or actions

It’s important that you don’t make edits to the new copy of your project during the conversion process. To test hidden triggers and actions in new Zaps, you’ll need to change the visibility of the trigger/action/search. To do this, create a copy of your integration and make the visibility changes to that version only to access those triggers/actions/searches to test them in the Zap editor. When your test is complete, you can delete this copy of your integration.  

To create a temporary test copy of your integration:

In the left sidebar menu, click “Versions.” Next to your new integration, click the gear icon and select “Clone.” In the dialog box that appears, click the “Clone to version” dropdown menu and select “patch.” It doesn’t matter which option you select here, since this version will be deleted after your testing is complete. Then click “Clone.” Click “Close” to exit the dialog box.

![](https://cdn.zappy.app/ef97ecfc1a3f9a9642c6baa4084a3780.png)

Change the visibility of a trigger/action/search so you can make a new test Zap:

To select the test version of your integration, click the “Version” dropdown menu in the upper left, or from the versions section. Then select the new version you just created for this test.

![](https://cdn.zappy.app/9757a3a04626669fe2836229dd7e6b86.png)

In the left sidebar menu, select the hidden trigger or action in your integration. At the bottom of the Settings page click the “Visibility Options” dropdown menu and select “Important (Displayed above the fold in the Zap Editor).” Then click “Save.”

![](https://cdn.zappy.app/11786cd7941cf9eab71dc81d73f244db.png)

### When you’re done testing

If everything works as expected, you’re ready to check this trigger/action/search off the list and repeat this process for the next one. If you see any unexpected results, contact us at partners@zapier.com. 

`<INSERT SCREENSHOT OF SIDEBAR CHECKLIST>`

After you’ve tested all your triggers and actions, you’re ready to update your users’ Zaps with the new integration.

## STEP 3: Update your Users’ Zaps

After you’ve completed testing, update your users' Zaps to use the integration you’ve created on the new platform. We’ll provide the status of the operation, letting you know when it’s complete.  If you have a lot of users this may take several hours to complete.  

After this process is complete, all your users’ Zaps will be using the new version of your integration, and all references to your integration will have been updated across Zapier.
