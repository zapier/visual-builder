---
title: Code mode
order: 15
layout: post-toc
redirect_from: /build/
---

# Code mode

## How does Code mode work?

![Zapier visual builder code mode](https://cdn.zappy.app/17f0890ad5856b53d61e32b26fbb1070.png)
_Each API call pane in Zapier visual builder includes a code mode toggle_

The Zapier visual builder includes a form to add API endpoint URLs and choose the API call type, then automatically includes any authentication details and input form data with the API call. You can also set any custom options your API may need, including custom URL params, HTTP headers, and request body items. Zapier then parses JSON-encoded responses into individual output fields to use in subsequent Zap steps.

This is the best way to set up most API calls and options in Zapier integration authentication, triggers, and actions.

If your API calls need more customization, however, or your API response is in a non-JSON format, you will need to write custom JavaScript code to handle your API call and/or response parsing. The Zapier visual builder includes a _Switch to Code Mode_ toggle on every API request, similar to the one pictured above, that switches that specific API call to code mode.

> **Remember:** Code mode is a toggle. Code mode and Form mode are saved separately; changes to one do not affect the other. The settings in the currently visible editor are the ones Zapier uses in your integration.

The first time you switch to code mode, Zapier copies everything entered in the API request form, including any custom options added, and converts them to JavaScript code. It then changes the UI to code mode, where you can add code for your API call.

In code mode, you can write JavaScript code, using Zapier's default code as a base or writing custom code. Use the `z.object` for Zapier specific features, including `z.console` to write to the console log, `z.JSON` to parse JSON, `z.errors` to take action on errors, and more. Check [Zapier's CLI Z Object docs](https://github.com/zapier/zapier-platform/blob/main/packages/cli/README.md#z-object) for details.

Additionally, use Zapier bundles to access auth data, data from user input forms, request data, and more. Learn more in our [Zapier bundle docs](https://platform.zapier.com/docs/advanced#bundle).

> **Note**: If you were familiar with our legacy Web Builder environment, we used to include several 3rd party libraries, like lodash, and made them available on the z object. Those libraries are not included in the new version of the UI tool. If you need access to additional modules you can easily move your project to the [Zapier CLI](https://github.com/zapier/zapier-platform/blob/main/packages/cli/README.md) and take advantage of npm to bring in any additional libraries you need.

> Note that, in Code mode you can import from Node's standard library with `z.require`, for example, `z.require('querystring')` or `z.require('crypto')`. We strongly recommend you keep it simple when coding in the UI tool. The CLI is much better suited to building and testing complex code. And be sure you know what you're doing - we can't guarantee that everything you might use from the standard library will be supported in our platform's runtime.

There is a time limit of 30 seconds for each trigger and action, so keep your custom code as light and quick as feasible. If code takes longer than 30 seconds to run, it will time out, and users' Zaps will not be successful.

Do note that changes are not saved automatically. Once you have added the code you want, click _Save & Continue_ to add the changes to your integration.

![Zapier code mode switch to form mode](https://cdn.zappy.app/1fa2f12c1c41a49f3d7aeff4d2706f7c.png)
_Switch back to form mode to use the form mode settings instead of your custom code_

Once you switch to code mode, Zapier uses your custom code for that API call, and does not use the data you previously entered in the form.

If you wish to switch back to the form mode, click the _Switch to Form Mode_ button to see the form options as they were when you first switched to code mode. Zapier will save the code you entered, but will not convert it back to the form mode or use the custom code in your live integration.

You may switch back to code mode again—though this time, Zapier will show the last saved version of your code, and will not copy any changes from your API call form to the code.

Here are some resources that will be helpful when using the Code Mode: 
- [HTTP Request Options](https://github.com/zapier/zapier-platform/blob/master/packages/cli/README.md#http-request-options)
- [HTTP Response Object](https://github.com/zapier/zapier-platform/blob/master/packages/cli/README.md#http-response-object)
- [HTTP Requests](https://github.com/zapier/zapier-platform/blob/master/packages/cli/README.md#manual-http-requests)
- [Dynamic Dropdowns](https://github.com/zapier/zapier-platform/blob/master/packages/cli/README.md#dynamic-dropdowns)
- [Return Types for Triggers, actions and searches](https://github.com/zapier/zapier-platform/blob/master/packages/cli/README.md#return-types)
- [The Bundle Object](https://github.com/zapier/zapier-platform/blob/master/packages/cli/README.md#bundle-object)
- [Accessing Environment Variables](https://github.com/zapier/zapier-platform/blob/master/packages/cli/README.md#accessing-environment-variables)
- [When to use placeholders or curlies vs template literals](https://github.com/zapier/zapier-platform/blob/master/packages/cli/README.md#when-to-use-placeholders-or-curlies)
- [Error Handling](https://github.com/zapier/zapier-platform/blob/master/packages/cli/README.md#error-handling)
- [Error Response Handling](https://github.com/zapier/zapier-platform/blob/master/packages/cli/README.md#error-response-handling)
- Schema Docs: [11.3.0](https://github.com/zapier/zapier-platform/blob/zapier-platform-schema@11.3.3/packages/schema/docs/build/schema.md), [10.2.0](https://github.com/zapier/zapier-platform/blob/zapier-platform-schema@10.2.0/packages/schema/docs/build/schema.md), [9.7.3](https://github.com/zapier/zapier-platform/blob/zapier-platform-schema@9.7.3/packages/schema/docs/build/schema.md)

## Is my Zapier integration using the Form or Code mode settings?

Zapier uses the currently visible option when running each part of your integration. If the form mode is visible for an API call in an integration's authentication, trigger, or action settings, that Zapier integration is using the data from form mode. If the code mode is visible for an API call, Zapier is using the code instead to turn that part of the integration.

To check which mode and settings Zapier is using for each API call, open that part of your Zapier integration and visually check to see if the form or code mode is visible.

<a id="cli"></a>

For this request, wrap the response with an array instead of the default `return results`, to have Zapier return an array of issues.

![](https://cdn.zappy.app/3bec13fa502f47ff1e5f9bfded052b4d.png)

> Remember: "Code Mode" is a toggle; if you switch back to Form mode your code will be ignored! [Learn more](#code).

Now, retest the request and it should run successfully.

![](https://cdn.zappy.app/af56c7fed5183aed462d2e7efbf78f8c.png)

<a id="censored"></a>



