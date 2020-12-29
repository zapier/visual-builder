---
title: Testing
order: 13
layout: post-toc
redirect_from: /docs/
---

## Test Your Integration

Zapier includes a number of ways to test your integration before releasing it to users, both inside Zapier's visual builder with tools to test each part of your integration, as well as the Zap builder itself.

Zapier visual builder helps you test your integration's authentication, triggers, and actions while building your integration. Then, be sure to test your integration in Zaps yourself, and invite others to help test your integration as well.

## How to Test Authentication

![Add testing account in Zapier visual builder](https://cdn.zapier.com/storage/photos/5cf2d6babbcb4352e00db0d078d4f14a.png)

Authentication testing in Zapier is crucially important, as this is where you first connect an account from your app to Zapier, which you will then use to test subsequent trigger and action steps as they're built. Once you've added your app's authentication settings and saved them, click _Connect an Account_ in the final Testing step to connect your account to Zapier.

Then, click the _Test Connected Account_ to make the test API call you added to your app authentication. If it's successful, Zapier will show a green check and a _Request Successful_ message on the top right of the dialog.

![Check output from trigger or action in Zapier visual builder](https://cdn.zapier.com/storage/photos/c5dfa2f8ce56471ff1af456a747f6c99.png)

You can then explore the data Zapier sent to and received from your app. The _Response_ tab shows the JSON data response from your API, with each field and its data listed. The _Bundle_ tab shows the data Zapier stores about your authentication. The _HTTP_ tab shows the full request details for each API call Zapier made during the test. And the _Console_ shows any additional data your API calls logged in Zapier if you use custom code for any part of your authentication.

Be sure to check each of them to ensure the expected data came through. Depending on your API, it's possible to have an unsuccessful API call come through as successful if your API returns a message without an HTTP error code. Check the Response to make sure it includes the data expected from this API call, and if anything is incorrect, check the HTTP tab to help diagnose where things went wrong.

While building your integration, it's often best to use a new account specifically for testing so you don't clutter your core app account with testing data. Later on, repeat the steps to connect additional accounts to test your integration with live, active data.

## How to Test Triggers and Actions

![Test new Trigger or Action in Zapier](https://cdn.zapier.com/storage/photos/08abf6c9d3eade40363fdd5cc8743ef2.png)

Once you've tested authentication, trigger and action steps are easy to test inside Zapier visual builder. Set up the trigger or action settings and API calls, then as the last step the familiar _Test Your API Response_ box appears. It will show any accounts you added to your integration previously while during authentication testing.

For all action steps, along with triggers that include [input forms](https://platform.zapier.com/docs/input-designer), first fill in details for each of the fields in the _Configure Test Data_ form. Add data that will successfully work in this API call, similar to what you would use in a live Zap.

Enter individual values in each field to add single objects. If you include commas in the field data, Zapier will turn that field into an array in your API call. Click the _Raw_ button to preview the JSON formatted data from your test data that Zapier will send with the API call.

Then click _Test Your Request_ to run the trigger or action step. Zapier will notify you if it run successfully and show the JSON results which you can explore as in the Authentication testing.

## How to Test New Integrations Inside Zapier

![Test new integration inside Zapier](https://cdn.zapier.com/storage/photos/c288a4e327ca0506da1a93e56c580e6d.png)

Testing inside the visual builder is crucial to building functioning integrations. But to ensure people can easily use your integration, it's equally crucial to test your integration inside Zapier with live Zaps.

To test your integration, make a Zap as normal at [zapier.com/app/editor](https://zapier.com/app/editor/), and choose your app in the _Choose App_ selector. Your integration will show the name and logo set in visual builder, along with the integration's current version number and a _By invite_ tag. If your integration is a new version of an existing integration, look for the latest version number and the _By invite_ tag to differentiate from existing, public integrations.

Then be sure to check each of the following:

- **Authentication**: Does your app account successfully connect? Zapier will show any testing accounts you already added, but try adding a new account here for a complete test.
- **Connection Label**: Does Zapier show a detailed connection label on the new account, with the info you set when building your integration?
- **Trigger and Action List**: Do you see every trigger and action step, respectively, that you added to your integration? Are the ones you marked as _Important_ shown above the fold? Are each trigger and action's name and description accurate and grammatically correct?
- **Fields**: Do triggers and actions show the fields you expect? Are their names and labels accurate and grammatically correct? Do any links or formatting in descriptions work correctly? Do drop-down fields or those with multiple selectors work correctly?
- **Output**: When you run a Zap trigger or action's test, does the step return the fields and data you expect? Are those formatted correctly? Do triggers show the most recently added item from your app, and do searches return appropriate results?
- **Input**: Open your app, and check each item that Zapier actions added or updated. Were they added correctly? Is their data in the correct format?
- **Automation**: Turn on Zaps with each of your integration's triggers. Do they run correctly when the data they watch for is added or updated in your app account? Do your integration's actions successfully add and update items automatically? Check your Zap history and your Zapier visual builder monitoring page to ensure everything is running without errors.

Using your integration inside Zapier's core editor is the best way to notice things that might have been overlooked while building your integration. Pay special attention to the fields included in triggers and actions, and any that might be missing. Additionally, be sure to double-check copy throughout your integration to make your integration easy for users to incorporate in their Zaps.

## How to Invite Others to Test New Integrations

![Zapier integration admins](https://cdn.zapier.com/storage/photos/5db3a5364349cbb17812e02e1eeddf11_2.png)

It's crucial to have as many people test your integration as possible before launching it to the public. Integrations are required to have at least 10 users with live Zaps before they can be released. Each additional tester helps ensure that your app doesn't ship with usability problems or bugs.

While developing your app integration, invite additional admins from your integration's _Admins_ page. These users will have full access to your app's visual builder to edit the app details, authentication, triggers, actions, and versions. This is the best way to add additional developers to your project.

![Zapier integration visibility](https://cdn.zapier.com/storage/photos/c818563358f8566d969e9be09a560220.png)

When your integration is nearly finished and ready for wider testing, you can invite testers from your integration's _Visibility_ page. These testers will be able to use your integration inside the Zapier editor, but cannot change your app's core settings and functionality in visual builder. This is the best way to add non-technical team members, beta testers, and advanced users of your app to your integration, to build up the minimum user count before launching your integration.

![Monitoring Zapier integration](https://cdn.zapier.com/storage/photos/9797530c2c6c7d5ea56dbc3d43e1ffaa.png)

Then, from the _Monitoring_ page, you can see every action taken by your integration users with the Zapier platform. You can filter by user, see auth and trigger/action events, and see whenever errors occur.

Soon you'll additionally be able to see more detailed usage statistics from the _Usage_ tab in visual builder.