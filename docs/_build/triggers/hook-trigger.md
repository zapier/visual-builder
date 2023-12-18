---
title: Add a REST Hook trigger
order: 3
layout: post-toc
redirect_from: /build/resthooks

---

# Add a REST Hook trigger 

Set up your REST Hook trigger in the Platform UI with the Settings, Input Designer and API Configuration tabs. 

## Prerequisites

- Your app supports REST Hooks - webhook subscriptions that can be manipulated through a REST API.
- An endpoint/s to set up and remove the hook subscription exists for Zapier to send Subscribe and Unsubscribe API requests to with a unique subscription URL, the`bundle.targetUrl`, for each active Zap.
- A separate endpoint exists that returns a list of sample items that would be expected to trigger the user's Zap. This is optional for apps remaining private and ***required*** for public apps.
- If your webhook subscriptions expire, make sure the subscribe endpoint returns an `expiration_date` property containing an ISO8601 date. The platform will automatically attempt to resubscribe after the expiration date.

## 1. Add the trigger settings

- Open the _Triggers_ tab in Zapier's Platform UI and select **Add Trigger**.
- On the Settings page, specify the following:

-- **Key**: A unique identifier for this trigger to be referenced inside Zapier. This is not shown to users. This cannot be edited once saved.

-- **Label**: A human-friendly name for this trigger, typically with an adjective such as _New or Updated_ followed by the name of the item that the trigger watches for inside  your app. The label is shown inside the Zap editor and on Zapier’s app directory marketing pages.

-- **Noun**: A single noun that describes what this trigger watches for, used by Zapier to auto-generate text in Zaps about your trigger.

-- **Description**: A plain text sentence that describes what the trigger does and when it should be used. Shown inside the Zap editor and on Zapier’s app directory marketing pages.

-- **Visibility in Editor**:  An option to select when this trigger will be shown. _Shown_ is chosen by default. Choose `Hidden` if this trigger should not be shown to users.`Hidden` is usually selected when the trigger is not ready to be used in the integration, or for polling triggers that power [dynamic dropdown](https://platform.zapier.com/build/add-fields#dynamic-dropdown) fields.

-- **Directions** is used for static webhooks only to describe how and where to copy-paste the static webhook URL for the trigger within your app. **Directions** will not show to users in other cases. Static webhooks are not permitted in public integrations. 

- Click on the **Save and continue** button.

## 2. Complete the Input Designer
 
On the Input Designer page, add user [input fields](https://platform.zapier.com/build/add-fields) needed by your API to watch for the triggering item.

Trigger input fields allow users to enter filters, tags, and other details to filter through new or updated data at the endpoint.

If no input data is needed for this trigger's endpoint, continue. 

## 3. Set up the API Configuration

On the API Configuration page, select **REST Hook** as the trigger type, and complete each section.

![](https://cdn.zappy.app/0368aeae12e11ec59688d10a7ef69d8c.png)

REST Hook triggers are marked as _Instant_ [in the Zap editor](https://cdn.zappy.app/f510859bf90c0e341bc94997a75f9626.png).

### Subscribe
This request, usually a POST, is performed when a user activates a Zap that starts with this REST Hook trigger. This is how a Zap makes a subscription request to your API to be notified (via webhook) of all trigger events with the given parameters going forward.

Click on the _Show Options_ dropdown to add data to the Request Body or HTTP Headers that are needed by your API for a successful subscription. Note that you’ll need to make sure the keys here match what your API expects. 

Zapier includes a `targetUrl` when making this request. You need to store the targetUrl, usually in a database, and you'd typically associate it with an id. Return that id in the response back to Zapier to be used later in the Unsubscribe.

Your app's event system would determine which stored subscriptions should be invoked when an event occurs in your app, posting to the corresponding stored `targetUrl`.

The webhook URL can be accessed via  {% raw %}`{{bundle.targetUrl}}`{% endraw %}.

For example, for Gitlab's API `url` is used as the key for the {% raw %}`{{bundle.targetUrl}}`{% endraw %} value that contains the webhook URL to send data to.

![](https://cdn.zappy.app/8b7941e3092850bd7edf331cb78b5659.png)

If you need to customize the subscription request, select _Switch to Code Mode_ and [write custom JavaScript code](https://platform.zapier.com/build/code-mode) to handle the API call and the response parsing as needed. 

It is recommended that a successful Subscribe response return a 201 status code. The data returned with the response should include any data needed to later the Unsubscribe request. This data will be stored in `bundle.subscribeData`.

### Unsubscribe
This request, usually a DELETE, is how Zapier notifies your API when it is no longer listening for trigger events, when the Zap is deactivated or deleted. If your API continues posting notification payloads to the Zap after it has unsubscribed, you can expect to see a 410 response from Zapier.

Click on the _Show Options_ dropdown to add data to the Request Body or HTTP Headers that is needed by your API for a successful unsubscription. Note that you’ll need to make sure the keys here match what your API expects. When Zapier sends the request to your API to unsubscribe the webhook, it can reference any data that was returned from your API during the Subscribe request and was stored in `bundle.subscribeData`.

![](https://cdn.zappy.app/44615176b56966a90101067d719b09ad.png) 

A REST Hook trigger missing a Subscribe or Unsubscribe endpoint, is presented to users as a [Static Webhook](https://cdn.zappy.app/3b35908a6a0c232087b5da807cf9d6fb.png). Static hooks are [not supported in public integrations](https://platform.zapier.com/publish/integration-checks-reference#d017---static-hook-is-discouraged), but they could be used if the integration intends to remain private.

### Perform List
This request, usually a GET, is used to collect sample data in the Zap editor, typically prior to a Zap's activation. This will be used to fetch sample data when users are testing the trigger and mapping fields to their Zap's subsequent steps. Though optional, not defining a Perform List is a sub-optimal experience for users and is [required for public apps](https://platform.zapier.com/quickstart/private-vs-public-integrations). 

Most commonly this is a GET request to an endpoint of your API which will provide a response with the exact same schema as the data delivered via webhook when a trigger event happens.

Response data returned must be an array, even if the array contains only one object. It must have the exact same schema as the data delivered via webhook when a trigger event happens otherwise fields mapped from this sample in subsequent steps of a Zap will break when it runs live.

### Perform
The Perform function is called each time your app delivers a notification payload to Zapier. Use custom code to parse the webhook payload and modify it as required before returning it to the Zap as trigger data.

The data returned by the perform must be an array. By default, Zapier includes `return [bundle.cleanedRequest]` to return the data from the webhook as an array. If the data needs to be transformed, or includes multiple objects, you can add custom code to parse the response data in `bundle.cleanedRequest` within the Perform into an array of objects.

If your webhook already provides an array, you can remove the wrapping array and simply `return bundle.cleanedRequest`.

If, for architectural reasons, your webhook will receive some data that shouldn't trigger the Zap, include code for the Perform function to return an empty array in those cases, so the Zap won't run.

For data sent to Zapier via REST Hook, most requests will be successful and return a 200 status code with some request-tracking data. This indicates that Zapier has accepted the data, but it is still possible for errors to occur within the Zap if the structure of the provided data is unexpected.

### Best practices when sending data to a Rest Hook trigger:

- Be mindful of Zapier's [rate limits](https://zapier.com/help/troubleshoot/behavior/rate-limits-and-throttling-in-zapier#step-4).
- If your app receives a 410 response, that webhook subscription is no longer active, and you should stop sending data to it.
- If your app receives repeated 4xx or 5xx failures from Zapier outside those error types, this can be handled at your discretion. You may choose to try again later, or to stop sending data and deactivate the hook.
- To signal that your app has deactivated the hook for any reason, you can optionally send a _reverse unsubscribe_ call to Zapier. This can allow users to manage their subscriptions from inside your app, or permit you to clean up after a user deletes their account or revokes credentials. The request should be of the form `DELETE <target_url>`, where `target_url` is the unique target URL that was provided when the subscription was created. This will pause the Zap within Zapier.

Once you've configured all the endpoints, click _Save API Request & Continue_

## 4. Test your API request

To test the REST Hook trigger, [build a Zap in the editor](https://platform.zapier.com/build/test-triggers-actions).

## 5. Define your output

Define sample data and output fields following [the guide](https://platform.zapier.com/build/sample-data).
