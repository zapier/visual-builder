---
title: Zapier Platform UI vs CLI
order: 3
layout: post-toc
redirect_from: /docs/vs
---

# Zapier Platform UI vs CLI

## Zapier Platform UI vs CLI: Which Should I Choose?

Zapier Platform includes two ways to build new integrations: our UI with an online visual builder, and our CLI. Both let you connect your app's API to Zapier to authenticate with user accounts, build triggers and actions, and promote your app on Zapier's app directory.

Zapier Platform UI is the easiest way to build new integrations in a web app. Add your app details, authentication settings, triggers, and actions in an online form, with help text and documentation links to help anytime you get stuck. You can test each part of your integration inside the visual builder, switch to code mode for advanced calls and response parsing, check logs and API response details, and rapidly iterate to build a complete new Zapier integration. It's an easy way for anyone with API experience to build Zapier integrations.

Zapier CLI is the most advanced way to build integrations in your local development environment. Zapier CLI is a terminal-based app that helps you scaffold new integrations then code them in JavaScript using your local development environment and code editor. Once you've coded your app details, authentication, triggers, and actions into the Zapier app package, you can push your Zapier integration to Zapier's server, manage new versions, and invite collaborators all from the command line. It's a powerful way for engineers to build Zapier integrations in their standard development workflow.

### Zapier Platform UI and CLI comparison tables

| Authentication | UI | CLI |
|----------------|----|-----|
| Basic Auth | ✓ | ✓ |
| Session Auth | ✓  | ✓  |
| Custom / "API Key" | ✓ | ✓ |
| OAuth v1 | - | ✓ |
| OAuth v2 | ✓ | ✓ |


| Triggers | UI | CLI |
|----------|----|-----|
| REST Hooks | ✓ | ✓ |
| Polling Triggers | ✓  | ✓  |
| Support for _Static_ Web Hooks | - | - |
| Customize request handling with JavaScript | ✓ | ✓ |


| Search Actions | UI | CLI |
|----------------|----|-----|
| Search or Create functionality | ✓ | ✓ |
| Customize request handling with JavaScript | ✓  | ✓  |



| Create Actions | UI | CLI |
|----------------|----|-----|
| Customize request handling with JavaScript | ✓  | ✓  |


| Advanced | UI | CLI |
|----------------|----|-----|
| Custom middleware | -  | ✓  |
| Resources | -  | ✓  |
| File support | -  | ✓  |
| Hydration | -  | ✓  |
| Import and use NPM modules  | -  | ✓  |
| Organize code with common functions  | -  | ✓  |


| Testing & Workflow | UI | CLI |
|--------------------|----|-----|
| GUI with form-based editor | ✓  | -  |
| WYSIWYG form preview | ✓  | -  |
| Write custom automated test suites | -  | ✓  |
| Add team members to project | ✓*  | ✓  |
| Manage testers  | ✓  | ✓  |
| Monitor usage  | ✓  | ✓  |
| View logs  | ✓  | ✓  |
| Manage versions  | ✓  | ✓  |
| Use custom source code manager  | -  | ✓  |
| Export CLI project  | ✓  | N/A  |


Zapier Platform UI and CLI both include the same core authentication, trigger, action and most testing features. The CLI additionally lets you add advanced features including resources, middleware, files, hydration, and NPM modules, along with options to write custom test suites. The UI gives you an easier way to build integrations with a form-based editor and WYSIWYG preview of your integration in Zapier, with the option to [export projects to the CLI](https://platform.zapier.com/manage/export-integration) if your needs change.

You can accomplish the same goals and build equally powerful Zapier integrations with both Zapier Platform UI and CLI. The best one for your integration depends on your work style and integration needs.

## Zapier Platform UI

![Zapier Platform UI](https://cdn.zappy.app/a8c009d1109749b44052922f2a6ec9bc.png)

**Best for:** Building new integrations quickly in a team with a range of development experience

Zapier Platform UI is the easiest way to build new integrations. With a general understanding of API authentication and calls, you can build a full Zapier integration without any coding. Its visual builder sets many of the defaults for you automatically. All you need to do is add details about your trigger and action steps, build input forms for users to enter data, and set the API call details to send that data to your app.

The visual builder additionally includes a code mode toggle on every API call, where you can write custom JavaScript code for your API call and response data parsing. You can also [export](https://platform.zapier.com/manage/export-integration) an existing Platform UI integration to CLI, which provides an easy way to start new integrations, then customize them in your local development environment, as they both share the same Zapier Platform backend.

Choose Zapier Platform UI for your integration if you're new to Zapier integration development, want an easy way to build a new integration, or have a team with non-engineers working together on the integration who would find the CLI more difficult to use.

_→ Build a [new Zapier Platform UI integration](https://platform.zapier.com/quickstart/platform-ui-guide).

## Zapier Platform CLI (Command Line Interface)

![Zapier CLI](https://cdn.zapier.com/storage/photos/27d28a5fdd0c878d7558b4abd4f106ec.png)

**Best for:** Building customized integrations in an engineering team

Zapier's CLI is the most powerful way to build Zapier integrations, using the same tools your engineering team relies on to build and maintain your app. List your app details in a JSON file, then use standard JavaScript to build your API calls, parse response bundles, and log error messages and details to Zapier. Manage versions of your integrations using GIT version control, if you want. Then push new versions of your integrations to Zapier's server from Terminal.

Zapier CLI lets you build advanced integrations faster than visual builder since every part of your integration is custom built by default. You can use NPM modules as you would in other JavaScript apps, test your integration locally, view detailed HTTP logs, and get started quickly with scaffold and demo apps.

Choose CLI if your API needs custom coding for most API calls or you find writing integrations in code easier than using a web app, and if your integration will maintained by an engineering team. Zapier CLI is more difficult to use for non-engineers, but will likely be more efficient for an engineering team to use than visual builder. And soon, you won't have to choose: You can start with visual builder, then switch to CLI later if you want.

_‌→ Install Zapier Platform CLI with `npm install -g zapier-platform-cli`, check our [CLI Quick Start Guide](https://platform.zapier.com/reference/cli_docs#quick-setup-guide) to build a demo integration, then learn more in [Zapier's CLI documentation](https://zapier.github.io/zapier-platform-cli/)._

## Switching from the UI to the CLI

**It's easy to start your project in the UI and then switch to the CLI later!** If you're having trouble deciding which tool is the best fit for your project, start in the UI and then "export" your project when you find you need the advanced features of the CLI.

See the [section on exporting your project](https://platform.zapier.com/manage/export-integration) to try it out!
