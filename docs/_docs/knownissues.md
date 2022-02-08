---
title: Known Issues & Top Tips
order: 21
layout: post-toc
redirect_from: /docs/
---

# Top Tips

- When you are defining an API request, you will have two ways of configuring it - the tool provides a "Form Mode" and "Code Mode". Form mode allows you to define a request, setting headers and params, with tab completion to map variables. (_Bonus tip, type \{\{ to see tab completion suggestions._) Code mode allows you to provide a Javascript function to customize the request and response. These two modes are mutually exclusive, and the contents are independent. The visual builder will only run and save what is presently displayed on the screen and ignore the other. [FAQ](https://platform.zapier.com/docs/faq#how-does-code-mode-work)
- In the embedded test component there is a form that allows you to enter test data for any input field that would normally be provided by the Zap when it's running. The form, or "Pretty" view only accepts scalar values (strings, integers, booleans, etc). If your action takes, say, a line item or dictionary type, use the "Raw" view to add that JSON directly into the mock data object that will be passed to your request while testing.
- If you are adding _dynamic fields_, create and configure a Zap to test your code. Use the Monitoring component (available from the left hand navigation) to see what's going on with your request under the hood.
- If you are adding _dynamic fields_ you'll want to use Code Mode when configuring the API request and use something like `...bundle.inputData` to reference all of the fields that were created dynamically at runtime.
- Be sure to review the other [FAQs](https://platform.zapier.com/docs/faq) for other helpful tips!
