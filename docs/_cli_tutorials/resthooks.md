---
title: How to Use REST Hooks in Zapier CLI
order: 2
layout: post-toc
redirect_from: /cli-tutorials/
---

# How to Use REST Hooks in Zapier CLI

## What are REST Hooks?

REST Hooks are an alternative to polling. We subscribe to your server using a unique URL on a per Zap basis and you send a payload of data back to the unique URL to trigger that particular Zap. This will allow your customers' Zaps to trigger instantly and will also reduce the load on your servers as we will not be constantly querying for data every 5 or 15 minutes.

You can read more about how REST hooks work in general at [https://resthooks.org](https://resthooks.org/). **These are not the same as static webhooks**. With static webhooks, your customer needs to copy and paste a specific URL to connect your app and their Zap together, whereas with REST hooks this is all handled automatically for them between Zapier and your app.

## Getting Started With REST Hooks

What you need to get started with REST Hooks:

* A way to store the unique URLs we send you. A database is one such solution.
* A way to send payloads in JSON format to the URLs you stored earlier, when a specific event happens that you want to trigger the associated Zap on.
* One or more endpoint(s) to receive subscribe and unsubscribe payloads (these can be the same endpoint(s) or separate ones)

An overview of the process:

* When the Zap is turned on, we will call the `subscribeHook` function with a payload of data that includes the URL we expect you to send data to in order to trigger the Zap. You **must** store this URL and use it whenever you want to trigger this Zap.
* When the Zap is turned off, we will call the `unsubscribeHook` function asking you to delete the URL you previously stored for this Zap.

## Step 1: Write the `subscribeHook` Function

The first function to implement is the `subscribeHook` function which provides the URL you will use to trigger the Zap. This takes the following parameters:

* `url` should be `bundle.targetUrl` which is an URL we will automatically generate for each Zap.
* Any other data you want to send, e.g. data from input fields such as dropdowns, etc.

It would look something like this:

```
const subscribeHook = (z, bundle) => {
  const data = {
    url: bundle.targetUrl,
    another_param: "my data",
    something_else: true
    // etc
  };

  const options = {
    url: 'your endpoint url',
    method: 'POST',
    body: JSON.stringify(data)
  };

  // make the request and parse the response - this does not include any error handling.
  return z.request(options)
    .then(response => z.JSON.parse(response.content));
}
```

which is then called in the `performSubscribe` method on the module for the Trigger, like so:

```
module.exports = {
  // Other data about the Trigger, e.g. key, name, etc. omitted
  performSubscribe: performSubscribe
};
```

This function will then run every time the Zap is turned on.

## Step 2: Write the `unsubscribeHook` Function

The next function to implement is the `unsubscribeHook` function which will be called when a Zap is turned off. This will notify your servers so you can delete the URL you've been storing and stop sending payloads to it. This takes the following parameters:

* `bundle.subscribeData.id` is required — this is the ID of the hook in question. You could assign it to a `hookID` variable or similar.

It would look something like this:

```
const unsubscribeHook = (z, bundle) => {
  // bundle.subscribeData contains the parsed response from the subscribeHook function.
  const hookId = bundle.subscribeData.id

  const options = {
    url: `your endpoint url/${hookId}`,
    method: 'DELETE'
  }

  return z.request(options)
    .then(response => z.JSON.parse(response.content));
};
```

which is then called in the `performUnsubscribe` method on the module for the Trigger, like so:

```
module.exports = {
  // Other data about the Trigger
  performUnsubscribe: unsubscribeHook
};
```

## Step 3: Write the `perform` Function

The next function to write is the `perform` function which sends the payload of data received from your server to the Zap. This is what actually triggers the Zap. Typically, you would simply return the cleaned request in an array. It is extremely important that the request is returned in an array—this is a requirement outlined [here](https://github.com/zapier/zapier-platform/blob/master/packages/cli/README.md#return-types).

```
const parsePayload = (z, bundle) => {
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
  // Other data about the Trigger
  perform: parsePayload
};
```

## Step 4: Write the `performList` Function

The final function to write is the `performList` function which is only used when testing the Trigger. This allows your users to bring in samples to use to set up the rest of their Zap. This is required for public apps to ensure the best UX experience for your users. Situations where a user has to go and generate their own webhook event generally result in confusion and a bad UX experience.

You need to make a request to an endpoint that returns data that the user can use. It **must** be live data from their account and it **must** be formatted exactly how the webhook payload will be formatted, otherwise mapped fields using this data in the Action step of a Zap will break when it is turned on.

```
const getFallbackSample = (z, bundle) => {
  // For the test poll, you should get some real data, to aid the setup process.
  const options = {
    url: 'your API endpoint here',
    params: {
      style: bundle.inputData.style
    }
  };

  return z.request(options)
    .then(response => JSON.parse(response.content));
};
```

followed by:

```
module.exports = {
  // Other data about the Trigger
  performList: getFallbackSample
};
```

## BasicHookOperationSchema

### `subscribeHook`

This should be a function that sends a payload of data to an endpoint you control. You need to grab the `targetUrl` parameter and store it securely somewhere as you will need this URL to send data back and trigger the Zap. You can see an example of this [here](https://github.com/zapier/zapier-platform-example-app-rest-hooks/blob/master/triggers/recipe.js#L1-L22).

### `unsubscribeHook`

This should be a function that calls an endpoint you control with a payload of data, including the `targetUrl` parameter. You need to deactivate or delete the URL from your storage completely as the Zap associated will no longer trigger when requests are made to it. You can see an example of this [here](https://github.com/zapier/zapier-platform-example-app-rest-hooks/blob/master/triggers/recipe.js#L24-L39).

### `perform`

This should be a function that processes the inbound webhook request. No `HTTP` request has to made here. As seen in our example app [here](https://github.com/zapier/zapier-platform-example-app-rest-hooks/blob/master/triggers/recipe.js#L41-L54), this can simply take the data from `bundle``.``cleanedRequest` and build a new object that is returned within an array. It's important to return this object within an array as specified [here](https://github.com/zapier/zapier-platform/blob/master/packages/cli/README.md#return-types).

### `performList`

Testing the trigger of a REST hook app will only call `performList`, not `perform`. `performList` ideally should make a `HTTP` request to an endpoint that can return data the user can use to set up the Zap. As exampled [here](https://github.com/zapier/zapier-platform-example-app-rest-hooks/blob/master/triggers/recipe.js#L56-L67). This is required for public apps to ensure the best UX for the end-user. Situations where a user is “waiting” for a hook to return sample data generally result in confusion and a bad UX.
