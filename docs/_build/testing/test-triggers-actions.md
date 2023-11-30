---
title: Test triggers or actions
order: 2
layout: post-toc
redirect_from: 
---

# Test triggers or actions

Once authentication is tested, trigger and action steps are easy to test inside Zapier visual builder. Set up the trigger or action settings and API calls, then as the last step the familiar _Test Your API Response_ box appears. It will show any accounts you added to your integration previously during the authentication testing.

![Test new Trigger or Action in Zapier](https://cdn.zappy.app/b8bd7bcad203fd0473c25a64dd2203c6.png)

## Prerequisites

- Completed authentication configuration with your app's authentication scheme
- Set of valid user credentials for your app - recommended to use a new account specifically for testing so you don't clutter your core app account with testing data. 
- A successful authentication test

## Steps

1. Within _API Configuration_ for each trigger or action, access the _Test your API Request_ section
2. Fill in details for each of the input fields in the _Configure Test Data_ form. Add data that will successfully work in this API call, similar to what you would use in a live Zap.
3. Enter individual values in each field to add single objects. If you include commas in the field data, Zapier will turn that field into an array sent to your API. Select _Raw_ to preview the JSON formatted data.
4. Select _Test Your Request_ to run the trigger or action step, verify it ran successfully and show the JSON results which you can explore as in the Authentication testing.
5. If an error is returned, check the following:

    - Authentication: Did your app's authentication work correctly in the authentication step? You can only test an integration once you've connected an app account to Zapier.
    - Test Data: Did your test data include the details your app expects, such as actual dates in date fields or complete email addresses in email address fields?
    - Input Field Keys: Did you use the same field keys in your input field as your API expects? Double-check that in the Input Designer, and change if needed.
    - API Call Customization: Does your API expect something different than the standard API call details Zapier sets by default? You may need to use Code Mode if the options you need aren't available.

6. When testing a [REST Hook trigger](https://platform.zapier.com/build/hook-trigger), you will instead have to create and test a Zap in the Zap Editor as follows:

    - Test the trigger to confirm that the Perform List works and provides live data from the app.
    - Turn on the Zap to confirm that the subscription is successful.
    - Perform the trigger event in the app to confirm that the webhook is sent to the Zap's webhook URL and triggers the Zap.
    - Compare the data returned from the Perform (can be seen in the [Zap history](https://help.zapier.com/hc/en-us/articles/8496291148685-View-and-manage-your-Zap-history)) with the data returned from the Perform List and confirm that they are both in the same format and have the same information in them.
    - Turn off the Zap to confirm that the unsubscription is successful. A successful unsubscription should delete the Zap's webhook URL from your app.

It is recommended that you check the logs in the [Monitoring](https://platform.zapier.com/build/test-monitoring) component for feedback from your Zap testing.