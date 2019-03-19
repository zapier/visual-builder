---
title: Known Issues & Top Tips
order: 19
layout: post-toc
redirect_from: /docs/
---

# Known Issues & Top Tips

## Known Issues

The visual builder is a brand new addition and as such we're bound to have a few wrinkles to iron out.  Here's a couple we know about and are working on.  If you find issues not listed here be sure to let us know at contact@zapier.com.  If you have questions please join us and other Zapier Platform developers on Slack [here](https://zapier-platform-slack.herokuapp.com/).

- **Concurrent development bug**  If two developers are working on an integration at the same time and both save edits at the same time, one will get an error and their work won't be saved.  
- **JSON payloads only** When you POST or PUT data we send your data as JSON.  If your API expects `application/x-www-form-urlencoded` or `multipart/form-data` encoded body content we'll have a fix out soon that will let you switch to Code Mode and use Javascript to encode your data.
- **RestHook Testing**  Today you may need to switch to Code Mode in order to use the embedded test tool to test your requests. See [FAQ](https://platform.zapier.com/docs/faq#how-do-i-define-rest-hooks-and-use-the-embedded-tester-with-them)
- **Ignorable Async/Await Syntax Warnings**  The Zapier Platform supoorts async/await Javascript syntax, but when in code mode you'll see syntax warnings.  You can ignore these and save/test your code.  
- **Incomplete validation rules for input fields** When adding input fields, particularly when working with dictionary types, line items, and drop downs, take care when selecting options like "allow multiples", etc.  For now you might have a look at the [schema](https://zapier.github.io/zapier-platform-schema/build/schema.html#fieldschema) for Fields to see what's allowed, while we work to implement better guard rails for field creation.


## Top Tips

- Save your work often!
- When you are defining an API request, you will have two ways of configuring it - the tool provides a "Form Mode" and "Code Mode".  Form mode allows you to define a request, setting headers and params, with tab completion to map variables. (_Bonus tip, type \{\{ to see tab completion suggestions._)  Code mode allows you to provide a Javascript function to customize the request and response.  These two modes are mutually exclusive, and the contents are independent.  The visual builder will only run and save what is presently displayed on the screen and ignore the other.  [FAQ](https://platform.zapier.com/docs/faq#how-does-code-mode-work)
- When configuring a dynamic dropdown in the Input Designer we show you a preview of what that dropdown will look like over on the right side of the page.  If you click on it, it won't actually load data and will show an error.  This is ok - it doesn't mean there's a problem with your dropdown.  It's just that the preview isn't connected to a live account.  To see your dynamic dropdown with real data loaded, create a Zap in the Zap Editor.
- In the embedded test component there is a form that allows you to enter test data for any input field that would normally be provided by the Zap when it's running.  The form, or "Pretty" view only accepts scalar values (strings, integers, booleans, etc).  If your action takes, say, a line item or dictionary type, use the "Raw" view to add that JSON directly into the mock data object that will be passed to your request while testing.
- If you are adding _dynamic fields_, create and configure a Zap to test your code.  Use the Monitoring component (available from the left hand navigation) to see what's going on with your request under the hood.
- If you are adding _dynamic fields_ you'll want to use Code Mode when configuring the API request and use something like `...bundle.inputData` to reference all of the fields that were created dynamically at runtime.
- Be sure to review the other [FAQs](https://platform.zapier.com/docs/faq) for other helpful tips!