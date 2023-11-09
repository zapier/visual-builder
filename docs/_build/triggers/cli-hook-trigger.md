---
title: Add an instant trigger using REST Hooks in Zapier Platform CLI
order: 7
layout: post-toc
redirect_from: 
  - /cli_tutorials/resthooks
  - /build/resthooks
---

# Add an instant trigger using REST Hooks in Zapier Platform CLI 

REST Hooks are an alternative to polling. The main differences are allowing your customers' Zaps to trigger instantly; and avoiding polling triggers' numerous - and sometimes unnecessary - requests to your API's endpoints to check for new data. 

When building in the [Platform CLI](https://platform.zapier.com/quickstart/ui-vs-cli), use the [example implementation](https://github.com/zapier/zapier-platform/tree/main/example-apps/rest-hooks) for guidance.

With a REST Hook trigger, Zapier subscribes to your server using a unique URL per activated Zap and your app sends a payload of data back to the unique URL to trigger that particular Zap whenever that trigger event occurs in your app.

REST Hooks differ from static webhooks. With static webhooks, your customer needs to manually copy and paste a specific URL per Zap to connect your app and their Zap together, whereas with REST Hooks this is all handled automatically for them between Zapier and your app.

Zapier does not support Identity Confirmation for webhook subscriptions.

## Prerequisites

- Your app supports REST Hooks - webhook subscriptions that can be manipulated through a REST API.
- A way to store the unique URLs we send you, such as a database.
- A way to send payloads in JSON format to each stored URL, when a specific event happens that you want to trigger the associated Zap on.
- One or more endpoint(s) to receive subscribe and unsubscribe payloads (these can be the same endpoint(s) or separate ones)

When a Zap is turned on, the `subscribeHook` function is called with a payload of data that includes the unique URL to send data to in order to trigger the Zap. Store this URL, associating it with an id and use it whenever you want to trigger this Zap. Return that id in the response back to Zapier to be used later in the Unsubscribe.

When the Zap is turned off, the `unsubscribeHook` function is called to notify your app to delete the unique URL previously stored for this Zap.

## 1. Write the `subscribeHook` Function

The first function to implement is the `subscribeHook` function which provides the URL you will use to trigger the Zap. Include the following parameters:

- `url` should be `bundle.targetUrl` which is an URL Zapier automatically generates for each activated Zap.
- Any other data you want to send from any [inputFields](https://github.com/zapier/zapier-platform/blob/main/packages/cli/README.md#input-fields)

```
const subscribeHook = (z, bundle) => {
  const data = {
    url: bundle.targetUrl,
    field: bundle.inputData.field,
    // etc
  };

  const options = {
    url: 'subscription endpoint url',
    method: 'POST',
    body: data
  };

  // make the request and parse the response - this does not include any error handling.
  return z.request(options)
    .then((response) => response.data);
}
```

This function is called in the `performSubscribe` method on the module for the Trigger:

```
module.exports = {
  // Other data about the Trigger, e.g. key, name, etc. omitted
  performSubscribe: subscribeHook
};
```

This function will run every time a Zap is turned on.

## 2. Write the `unsubscribeHook` Function

The next function to implement is the `unsubscribeHook` function which will be called when a Zap is turned off. This notifies your servers to delete the URL you've been storing and stop sending payloads to it. If your API continues posting notification payloads to the Zap after it has unsubscribed, you can expect to see a 410 response from Zapier. 

`bundle.subscribeData.id` is required — this is the ID of the hook in question. You could assign it to a `hookID` variable or similar.

Include the following parameters:

```
const unsubscribeHook = (z, bundle) => {
  // bundle.subscribeData contains the parsed response JSON from the subscribe request.
  const hookId = bundle.subscribeData.id

  const options = {
    url: `unsubscription endpoint url/${hookId}`,
    method: 'DELETE'
  }

  return z.request(options)
    .then((response) => response.data);
};
```

This function is called in the `performUnsubscribe` method on the module for the Trigger: 

```
module.exports = {
  // Other data about the Trigger, e.g. key, name, etc. omitted
  performUnsubscribe: unsubscribeHook
};
```

A REST Hook trigger missing a Subscribe or Unsubscribe function, is presented to users as a [Static Webhook](https://cdn.zappy.app/3b35908a6a0c232087b5da807cf9d6fb.png). Static hooks are [not supported in public integrations](https://platform.zapier.com/publish/integration-checks-reference#d017---static-hook-is-discouraged), but they could be used if the integration intends to remain private.

## 3. Write the `perform` Function

The next function to implement is the `perform` function which is called each time your app delivers a notification payload to Zapier. This is what actually triggers the Zap. Typically, you would simply return the cleaned request in an array. The data returned by the request [must be an array](https://github.com/zapier/zapier-platform/blob/master/packages/cli/README.md#return-types).

```
const parseHookPayload = (z, bundle) => {
  // bundle.cleanedRequest will include the parsed JSON object (if it's not a
  // test poll) and also a .querystring property with the URL's query string.
  const payload = {
    id: bundle.cleanedRequest.id,
    name: bundle.cleanedRequest.name,
    directions: bundle.cleanedRequest.directions,
    style: bundle.cleanedRequest.style,
    authorId: bundle.cleanedRequest.authorId,
    createdAt: bundle.cleanedRequest.createdAt
  };

  return [payload];
};
```

followed by:

```
module.exports = {
  // Other data about the Trigger, e.g. key, name, etc. omitted
  perform: parseHookPayload
};
```

## 4. Write the `performList` Function

The final function to implement is the `performList` function, used when testing the Trigger to collect sample data in the Zap editor. Though optional, not defining a performList is a sub-optimal experience for users and is [required for public apps](https://platform.zapier.com/quickstart/private-vs-public-integrations). 

Most commonly this is a GET request to an endpoint of your API which will provide a response from the user's account with the exact same schema as the data delivered via webhook when a trigger event happens.

Response data returned must be an array, even if the array contains only one object. It must have the exact same schema as the data delivered via webhook when a trigger event happens otherwise fields mapped from this sample in subsequent steps of a Zap will break when it runs live.

```
const getFallbackSample = (z, bundle) => {
  // For the test poll, you should get some real data, to aid the setup process.
  const options = {
    url: 'sample endpoint here',
    method: 'GET',
    params: {
      style: bundle.inputData.style
    }
  };

  return z.request(options)
    .then((response) => response.data);
};
```

followed by:

```
module.exports = {
  // Other data about the Trigger, e.g. key, name, etc. omitted
  performList: getFallbackSample
};
```

## 5. Test your API Request

To test the REST Hook trigger, [build a Zap in the editor](https://platform.zapier.com/build/test-triggers-actions).

## 6. Define sample and outputFields

Define sample data and output fields following [the guide](https://github.com/zapier/zapier-platform/blob/main/packages/cli/README.md#output-fields). You can see an example of this [here](https://github.com/zapier/zapier-platform-example-app-rest-hooks/blob/master/triggers/recipe.js#L102-L122).

## BasicHookOperationSchema

### `subscribeHook`

Function that sends a payload of data to an endpoint you control. You need to grab the `targetUrl` parameter and store it securely as this URL is used to send data from your app to Zapier when the triggering event occurs, and thus trigger the Zap. You can see an example of this [here](https://github.com/zapier/zapier-platform-example-app-rest-hooks/blob/master/triggers/recipe.js#L1-L22).

### `unsubscribeHook`

Function that calls an endpoint you control with a payload of data, including the `targetUrl` parameter. You need to deactivate or delete the URL from your storage completely as the Zap associated will no longer trigger when requests are made to it. If your API continues posting notification payloads to the Zap after it has unsubscribed, you can expect to see a 410 response from Zapier. You can see an example of this [here](https://github.com/zapier/zapier-platform-example-app-rest-hooks/blob/master/triggers/recipe.js#L24-L39).

### `perform`

This should be a function that processes the inbound webhook request. No `HTTP` request has to made here. As seen in the example app [here](https://github.com/zapier/zapier-platform-example-app-rest-hooks/blob/master/triggers/recipe.js#L41-L54), this can simply take the data from `bundle.cleanedRequest` and build a new object that is returned within an array. It's important to return this object within an array as specified [here](https://github.com/zapier/zapier-platform/blob/master/packages/cli/README.md#return-types).

### `performList`

Testing a REST Hook trigger in the Zap editor will only call `performList`, not `perform`. `performList` ideally should make a `HTTP` request to an endpoint that can return sample data to be mapped into subsequent steps of the user's Zap. You can see an example of this [here](https://github.com/zapier/zapier-platform-example-app-rest-hooks/blob/master/triggers/recipe.js#L56-L67). Required for public apps and highly recommended for private apps to avoid user confusion when setting up a Zap. 