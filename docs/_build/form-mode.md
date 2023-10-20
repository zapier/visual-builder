---
title: Use form mode to setup your API calls
order: 1
layout: post-toc
redirect_from: 
---

# Use form mode to setup your API calls

In the Platform UI, when building your authentication, triggers and actions, the default setting under _API Configuration_ is to create each component of your integration using Form Mode. 


## Capabilities

With Form Mode you can:

- Add the API endpoint for the request to be made 
- Choose the API request type 
- Set any custom URL parameters, HTTP headers and the request body under _Show Options_.

By default, the configured authentication is included as HTTP Headers, which you can modify if needed. 

![form mode screenshot](https://cdn.zappy.app/e380a04c42f0332d57df4fd0d1532590.png)

By default, any Input fields are included as URL Params. To instead include them within the API endpoint, use format `{{bundle.inputData.fieldkey}}` where `fieldkey` is the key of the input field. 

![input fields](https://cdn.zappy.app/fdc8807e9b6d41427d937d1362f20fbd.png)

When the request runs, Zapier parses JSON-encoded responses into individual output fields to use in subsequent Zap steps.

Form Mode is the simplest way to set up most API calls and options in your Platform UI integration's authentication, triggers, and actions.

## Refine the API call further

If your API calls need more customization than Form Mode offers or your API response is in a non-JSON format, you will need to write custom JavaScript code to handle your API call and/or response parsing. To do so, use [Code Mode](https://platform.zapier.com/build/code-mode).

The first time you switch to Code Mode, Zapier copies everything entered in Form Mode, including any custom options added, and converts that to JavaScript code. It then changes the UI to include a code block, where you can add code for your API call.

Zapier uses the currently visible option when running each part of your integration. To check which mode and settings Zapier is using for each API call, open that part of your Zapier integration and visually check to see if the Form or Code Mode is visible.

To switch back to the Form Mode, click the _Switch to Form Mode_ button to see the form options as they were when you _first switched_. Zapier will save the code you entered, but will not convert it back to the Form Mode nor use the custom code in your API Request.

If you then switch back to Code Mode again — you will see the last saved version of your code, and no changes you made in Form Mode will be refelcted in that code.