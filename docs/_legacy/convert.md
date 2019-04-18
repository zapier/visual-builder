---
title: Convert to Zapier Platform CLI
order: 2
layout: post-toc
redirect_from: /legacy/
---

# How to Convert a Legacy Web Builder Integration to Zapier Platform UI or CLI

The original Zapier Platform included a Web Builder to build Zapier integrations in your browser. In the years since then, Zapier has moved on to our newer Platform v3 which includes both a CLI to build integrations in your local coding environment, and a UI with a visual builder to build new integrations in your browser.

If you have an existing Zapier integration built with our now-legacy Web Builder, here's how to convert it to the newest version of the Zapier Platform and maintain it using Zapier Platform CLI.

## Why should I convert my Zapier app to the CLI?

The Zapier CLI was built to address the feedback we heard from many developers about ways to make it easier to build and manage a successful Zapier application over time.  Some of these improvements:

* The Zapier CLI is code-oriented, allowing your developers to work in their own development environments where they are the most productive, using tools they are familiar with, to most quickly produce high quality code.
* Code can be managed in your own repository, and teams of developers can easily collaborate on the same app without having to share Zapier login credentials.
* With the collaborate feature multiple developers can push changes to your app without having to share login credentials.
* Developers can create and run automated tests from their own environment with every change making it much easier to keep bugs from creeping into your code.
* Zapier CLI is standard JavaScript, and allows you to include your own NPM modules to extend the functionality of your app.
* Managing new versions of your app and testers is much more powerful with the CLI.  In Web Builder to make a change to your app you'd need to create a clone of it and when you were ready, you'd replace the running instance of your app with the clone.  In the CLI you'll simply create a new *version* of your app.  Once you promote a version of your app to production, you can control when to migrate existing users to it.  You'll even be able to migrate percentages of your users to the new version and migrate them back to the original version if you discover a problem.
* In 2018 new platform features will start being introduced only for the CLI platform.



## What do I need?

Some familiarity with Javascript. If you did custom scripting in your Web Builder app you've got what it takes!  If you need a refresher on JavaScript, we recommend reading [this guide](https://developer.mozilla.org/en-US/docs/Web/JavaScript/A_re-introduction_to_JavaScript).  A big difference in code from Web Builder to CLI is that the CLI uses asynchronous requests when it calls your API, so if you're new to [promises](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Using_promises) it's a great idea to get a bit more familiar with them, as well as some other ES6 basics.

**Required Software:**

Any recent version of Node.js.  An easy option to get set up with Node.js is to visit https://nodejs.org/en/download/ and download the official installer for your OS. If you're installing with a [package manager](https://nodejs.org/en/download/package-manager/) it's even easier.

## How do I use it?

**Step 1) First, install the latest version of the CLI.**

Make sure you've installed the latest by running in a terminal window:

`npm i -g zapier-platform-cli`

Learn more about getting set up at https://zapier.github.io/zapier-platform-cli/#getting-started.

**Step 2) Run `zapier login`**

From your terminal command line run

`zapier login`

When prompted use the email address and password that you use to login to zapier.com.

This will configure authentication between your dev environment and the Zapier platform.  This command will set up a `.zapierrc` file in your home directory.

**Step 3) Locate the app id of the Web Builder app you'll be converting**

You can find your app id by going to the web UI and selecting your Web Builder app.  Once selected you can find your app id in the URL.

![](https://cdn.zapier.com/storage/photos/80842fa0250bd4d1782ed0c44acd7fcb.png)

**Step 4) Run the convert command**

From the terminal run

{% highlight text %}
{% raw %}
zapier convert 1234 your-new-cli-app-dir
{% endraw %}
{% endhighlight %}

where “1234” is the web builder app id you located in step 2, and “your-new-cli-app-dir” is the local directory that the generated code will be placed.

**What did we just do here**?

The zapier convert command grabbed your Web Builder app definition and custom scripting file and used that to generate a version of your app in your local dev environment.

At this point it's just code in your local environment.  **Your Web Builder app is unaffected by running convert**. In addition, the CLI platform is unaware of this new, generated app until you run zapier push.  (We'll do that in step 5!)

When you open up your new project folder you'll see a collection of new files and directories similar to:

{% highlight text %}
{% raw %}
your-app
├── creates
    └── issue.js
├── test
    ├── creates
    ├── issue.js
    ├── triggers
    ├── issue.js
    └── repo.js
├── triggers
    └── issue.js `
├── .env
├── .gitignore
├── .zapierapprc
├── authentication.js
├── index.js
└── package.json
{% endraw %}
{% endhighlight %}

Some key files and directories to note:

* `package.json` is a standard npm file. There's nothing here you need to pay attention to right now, just know this file will be used later to upgrade to a new version of the Zapier CLI and to create new versions of your app.
* `index.js` is the entry point and definition file for you app
* The `creates` directory will contain a file for each of your create actions. Similarly you'll find a directory for each trigger and search action.  
* The .`zapierapprc` file will be created for you in step 5 below.  It's where you'll find this app's id once it's been registered with the Zapier platform.
* The test directory contains stubs to test each of your actions and triggers, locally on your machine.  With the Zapier CLI you can run `zapier test` before pushing changes to the server to catch errors quickly.
* The `.env` file is where you can define local env variables to be used when you run tests locally.  
* If you added custom scripting code to your Web Builder app, then a `scripting.js` file will be included here, where all of that code will be.  You'll see function calls to that code that use our `legacy-scripting-runner` from your actions and triggers.


**Step 5) Run npm install**

In the terminal cd into your new project directory

`cd your-new-cli-app-dir`

Now run the following to install the libraries you'll need to run your app

`npm install`


**Step 6) Run the validate command**

cd into the directory of your new CLI app and run

`zapier validate`

This will check the structure of the app that was generated and make sure there aren't any identifiable problems.  Check out “Common issues and how to fix them” below if this command reveals errors or warnings.

**Step 7) Run the push command**

Running

`zapier push`

will register your app with the Zapier platform and upload your code.  Once you run this command you'll be able to see your app on your dashboard at https://zapier.com/developer/builder.   

**Step 8) Set needed env variables**

Your app likely has some “environment variables” set up in order to function.  For example if your app uses OAuth, the CLIENT_ID, the CLIENT_SECRET, the AUTHORIZATION_URL, the REFRESH_TOKEN_URL, and the ACCESS_TOKEN_URL will need to be configured through environment variables.  In Web Builder these particular values were set in the UI behind the “Manage Authentication Settings” button, and these sensitive values were not brought over when your app was converted.

Look for places in your CLI code where environment variables are used.  Any reference to `process.env.VARIABLE_NAME` is one that you'll need to define.

To set env variables you'll use the zapier env command:  

`zapier env 1.0.0 VARIABLE_NAME foo`

For details on how to use the env command check out https://zapier.github.io/zapier-platform-cli/cli.html#env or run

`zapier help env`

Environment variables are a cool new feature in CLI that easily allow you to have different versions of your app that point to staging and production environments, for example.

**Step 9) Create test Zaps**

Once your new CLI app is pushing without errors and you've configured your environment variables, it's time to test it out!  You've been developing and testing Zapier apps with the Web Builder by creating test Zaps and making sure everything works the way it's supposed to.  Zaps created with your CLI app should work just the same from the user's perspective.  You've probably got a suite of test Zaps you use to test your Web Builder app.  You might just copy those in the editor, and go in and replace your Web Builder app with the new CLI version you just pushed.  Hint: you might need to search for it in the app selection UI.

One difference between Web Builder and the CLI is the way you'll get logging and debugging into.  In Web Builder you'd view debug information from the Web UI.  In CLI you'll look at your logs from the command line with the following command:

`zapier logs`

Run `zapier help logs` for information on the various options available.  You can filter to see http logs, or the console logs - debug statements you added to your code with  `z.console.log` statements.  You can limit the number of rows returned, get detailed info with `--debug`.  You can even look an one of your users logs if you know their email address.  

**Step 10) Check out the tests**

Creating test Zaps and making sure that the user experience matches what we wanted for our users is essential.  But what we'd like is an automated way to test our code every time we make a change to catch as many errors as we can before we ever even push our code.  Good news!  This is a feature of the CLI platform and your converted app includes some scaffolds of automated tests to give you a head start building out your automated test suite.  

Zapier CLI testing is based on the popular mocha framework (https://mochajs.org/).  If you have a look in the /test directory you'll find a test files for each of your triggers, actions, and searches.  The following command will run each test and indicate if there was a problem.

`zapier test`

The convert command created a test file for each of your triggers, actions, and searches, which only covers the basic test scenarios. You'll need to go in and add the logic to the test code to ensure that each one actually indicates that the operation is doing what it's supposed to.

## Migrating your production users to the new CLI version

When you're happy with the new CLI version of your app and you're ready to start migrating your existing production users over to it, contact us at [partners@zapier.com](mailto:partners@zapier.com).  

## Differences between a converted app and one you would write “the CLI way”

If you haven't added custom scripting to your Web Builder app, then the CLI project that gets generated will be largely consistent with they way that you would have written it from scratch in the CLI.  If you've introduced WB scripting to your app you'll see:

* A file called scripting.js in your project directory that contains all the code you wrote
* A library called legacy-scripting-runner that is introduced into your project modules that handles executing the code in scripting.js.
* For operations that you've customized with scripting, you'll see some code in those triggers/actions/searches that configures and calls the legacy script runner.  If you wrote this code for the CLI, you'd write it directly in the perform method and skip all the references to legacy scripting runner

{% highlight javascript %}
{% raw %}
const getList = (z, bundle) => {
  const scripting = require('../scripting');
  const legacyScriptingRunner = require('zapier-platform-legacy-scripting-runner')(scripting);

  bundle._legacyUrl = 'https://www.example.com/api/v3/things';
  bundle._legacyUrl = replaceVars(bundle._legacyUrl, bundle);

  const responsePromise = z.request({
    url: bundle._legacyUrl
  });
  return responsePromise.then(response => {
    // Do a _post_poll() from scripting
    const postPollEvent = {
      name: 'trigger.post',
      key: 'activity',
      response
    };
    return legacyScriptingRunner.runEvent(postPollEvent, z, bundle);
  });
};
{% endraw %}
{% endhighlight %}

Rewriting to be more “native CLI” like, it would become something like:

{% highlight javascript %}
{% raw %}
const getList = (z, bundle) => {
  const responsePromise = z.request({
      method: 'GET',
      url: `https://www.example.com/api/v3/things`
  });
  return responsePromise.then(response => {
    // Your custom "post_poll"-like logic would go here
    return JSON.parse(response.content);
  });
};
{% endraw %}
{% endhighlight %}

## Common issues and how to fix them

* Parameters (`inputData`) don't seem to pass to the server correctly when running `zapier test`. The common errors for this are HTTP 400 or 404 errors. The converter tool can't know what parameters to pass to the server to do a good test. The only thing it can do is to fetch all the required fields and the fields with a default value and put them into a test case. You'll need to edit those in the test code.
* Seeing HTTP 401 error when running `zapier test`. Make sure you've put your credentials into the `.env` file. There's a known bug where the file could use the wrong environment variable names, e.g., the file uses `APIKEY` while it's supposed to be `API_KEY`.  You'll need to fix that.
* Seeing “TypeError: Cannot read property 'operation' of undefined” when running `zapier test`:  There is a known bug where the converted test code and the operation (trigger/search/create) code uses different key styles (camelCase vs. snake_case). To fix, manually correct the key in the test code or in the operation code.
* Seeing “... is not any of &lt;/BasicPollingOperationSchema&gt;,&lt;/BasicHookOperationSchema&gt;” when running `zapier validate`: We recently started requiring samples for all the triggers/searches/creates. If your Web Builder app has samples, they'll be copied to the converted CLI app automatically. But if your Web Builder app doesn't have samples, you need to add them to your CLI app. A fake sample like `{id: 1}` is enough to make it pass, but if your users will see this example in the Zap Editor our review team requires that it accurately represents the data that the operation returns.

## Web Builder features unsupported by the converter

* `z.dehydrate` and `z.dehydrateFile` are unavailable.
* `z.cookie_jar` is unavailable (uncommon).
* `$` is *mostly unavailable*, except for `$.param()` and `$.parseXML()` (other functionality is uncommon and too big to add).
* `bundle.zap` won't be filled out in most cases (CLI doesn't receive this information except for `performSubscribe `and `performUnsubscribe` in Hooks).
* Hooks are not supported by the converter (yet). Those will be converted to polling triggers.
