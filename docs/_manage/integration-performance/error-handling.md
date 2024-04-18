---
title: Improve error response handling
order: 3
layout: post-toc
redirect_from: 
    - /manage/making-changes#custom-error-handling-in-the-ui
    - /docs/versions-best-practices#custom-error-handling
    - /manage/analyze-integration-performance#errors
---

# Improve error response handling

Errors from your API cause pain for users at two vital points:

- During the Zap setup process, stopping them from enabling and activating their Zaps
- During the Zap’s runtime, once it has been turned on, preventing the Zap from completing all actions successfully

Zap runs that encounter an error response status code when making a request to your API throw an exception and receive the “Stopped / Errored” status. This will [display an error message to the user](https://help.zapier.com/hc/en-us/articles/20505304170637-Review-Zap-run-statuses) in their Zap History and they will be notified via email based on their [notification settings](https://help.zapier.com/hc/en-us/articles/8496289225229-Manage-notifications-when-errors-occur-in-Zaps). 

Even if the `message` included in the response details an error, users should **never receive** a success/200 response if there was an error in the request as this will not show up as an error in the Zap history. 

If [95% of a Zap’s runs in the last 7 days are assigned the “Stopped / Errored” status](https://help.zapier.com/hc/en-us/articles/8496037690637-Troubleshoot-errors-in-Zapier#500-series-error-codes-0-3), the Zap will be automatically turned off. The Zap will not run again until the user manually enables it, so only return an error if the scenario is truly an error that needs to be fixed.

Monitor spikes in errors from the the _Monitoring_ page in the Platform UI as leading indicators of problems users are facing within your integration.

The more descriptive and thorough [error handling](https://github.com/zapier/zapier-platform/blob/main/packages/cli/README.md#error-handling) your API and integration have in place, the easier it will be for users to resolve their own issues and for Zapier’s support team to assist with debugging.

If you don’t have control to make changes to the API itself, utilize custom error handling to improve your error messages:

- Elaborate on briefly worded errors with user-friendly messaging.
- When writing user-facing error messages however, keep the message below 250 characters total as Zapier truncates errors from integrations at 250 characters when displaying them to users.
- Update “not_authenticated” to “Your API Key is invalid. Please reconnect your account.”
- Surface specific information to users regarding the field and why it’s producing an error. This empowers users to fix Zap issues independently.
- Instead of “Provided data is invalid”, return “Contact name is invalid”.
- Improve “Contact name is invalid” with “Contact name exceeds character limit.”
- Format the error to include a second, optional argument code machines can use to identify the type of error, and last, optional argument of a HTTP status code.
`throw new z.errors.Error('Contact name exceeds character limit.', 'InvalidData', 400);`

Your app integration can use custom code to improve the user experience in Zapier by returning a user-friendly message and optional error and status code. Typically, this will be prettifying 4xx responses or APIs that return errors as 200s with a payload that describes the error. The code and status is used by Zapier to provide relevant troubleshooting to the user when communicating the error.

## Prerequisites

- Documentation for the API you're working with that includes the response status codes per endpoint
- Familiarity with [general error handling in Zapier](https://github.com/zapier/zapier-platform/blob/main/packages/cli/README.md#general-errors). 

## 1. Custom errors in Platform CLI

Switching to the [Platform CLI](https://platform.zapier.com/manage/export-integration), allows you to [make use of HTTP middleware](https://github.com/zapier/zapier-platform/blob/main/packages/cli/README.md#using-http-middleware) to implement any [custom error response handling](https://github.com/zapier/zapier-platform/blob/main/packages/cli/README.md#error-response-handling). 

This will allow you to write a single script that applies across the entire integration to detect a specific error from the API, and show the relevant message to the user within Zapier. 

## 2. Custom errors in Platform UI

When you build and maintain your app in the UI, custom error handling can still be implemented. The main difference is that you’ll need to add it to each individual element of the integration (triggers, actions, searches, authentication) that could encounter the error.

In the UI, `skipThrowForStatus` is set from the [Advanced tab](https://platform.zapier.com/build/errors). This allows for custom error handling for status codes above 400. Note that 401 status codes will throw a `RefreshAuthError` [regardless](https://github.com/zapier/zapier-platform/blob/main/packages/cli/README.md#user-content-error-response-handling).

![advanced settings](https://cdn.zappy.app/8cafa443c6e5844d6881f2690e4f34c5.png)

Once set, you can add [error handling](https://github.com/zapier/zapier-platform/blob/main/packages/cli/README.md#general-errors) when in Code Mode within the API Configuration for each trigger/action/search.

```js
return z.request(options).then((response) => {
  if (response.status === 404) {
    throw new z.errors.Error(
      "An error was returned. Help!",
      "InvalidData",
      404
    );
  }
  return response.json;
});
```

![code screenshot](https://cdn.zappy.app/9553266cb5a5ab7804d3f9ac1a9eed60.png)