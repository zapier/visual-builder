---
title: Visual Builder vs CLI
order: 18
layout: post-toc
redirect_from: /docs/
---

## Zapier Visual Builder vs Zapier CLI: Which Should I Choose?

Zapier includes two ways to build new integrations: our online visual builder, and our Zapier CLI. Both let you connect your app's API to Zapier to authenticate with user accounts, build triggers and actions, and promote your app on Zapier's app directory.

Visual builder is the easiest way to build new integrations in a web app. Add your app details, authentication settings, triggers, and actions in an online form, with help text and documentation links to help anytime you get stuck. You can test each part of your integration inside the visual builder, switch to code mode for advanced calls and response parsing, check logs and API response details, and rapidly iterate to build a complete new Zapier integration. It's an easy way for anyone with API experience to build Zapier integrations.

Zapier CLI is the most advanced way to build integrations in your local development environment. Based on Node.js, Zapier CLI is a terminal-based app that helps you scaffold new integrations. Once you've coded your app details, authentication, triggers, and actions into the Zapier app package, you can push your Zapier integration to Zapier's server, manage new versions, and invite collaborators all from the command line. It's a powerful way for engineers to build Zapier integrations in their standard development workflow.

Visual builder and CLI both let you accomplish the same goals and build equally powerful Zapier integrations. The best one for your integration depends on your work style and integration needs.

## Zapier Visual Builder

![Zapier Visual Builder](https://cdn.zapier.com/storage/photos/26cc01881a504fa51d81dea890fde1e5.png)

**Best for:** Building new integrations quickly in a team with a range of development experience

Zapier's visual builder is the easiest way to build new integrations. With a general understanding of API authentication and calls, you can build a full Zapier integration without any coding. Visual builder sets many of the defaults for you automatically. All you need to do is add details about your trigger and action steps, build input forms for users to enter data, and set the API call details to send that data to your app.

Visual builder additionally includes a code mode toggle on every API call, where you can write custom JavaScript code for your API call and response data parsing. Coming soon, you will also be able to convert a visual builder integration to a Zapier CLI app for an easy way to start new integrations then customize them in your local development environment, if you want.

Choose visual builder for your integration if you're new to Zapier integration development, want an easy way to build a new integration, or have a team with non-engineers working together on the integration who would find the CLI more difficult to use.

*→ Build a [new Zapier Visual Builder integration](https://zapier.com/app/developer/app/new), check our [Visual Builder Quick Start Guide](https://zapier.github.io/visual-builder/quickstart/introduction) to build a sample integration, then get more info in [Zapier's visual builder documentation](https://zapier.github.io/visual-builder/docs/intro).*

## Zapier Command Line Interface (CLI)

![Zapier CLI](https://cdn.zapier.com/storage/photos/27d28a5fdd0c878d7558b4abd4f106ec.png)

**Best for:** Building customized integrations in an engineering team

Zapier's CLI is the most powerful way to build Zapier integrations, using the same tools your engineering team relies on to build and maintain your app. List your app details in a JSON file, then use standard Node.JS JavaScript to build your API calls, parse response bundles, and log error messages and details to Zapier. Manage versions of your integrations using GIT version control, if you want. Then push new versions of your integrations to Zapier's server from Terminal.

Zapier CLI lets you build advanced integrations faster than visual builder since every part of your integration is custom built by default. You can use npm modules as you would in any other Node.JS app, test your integration locally, view detailed HTTP logs, and get started quickly with scaffold and demo apps.

Choose CLI if your API needs custom coding for most API calls or you find writing integrations in code easier than using a web app, and if your integration will maintained by an engineering team. Zapier CLI is more difficult to use for non-engineers, but will likely be more efficient for an engineering team to use than visual builder. And soon, you won't have to choose: You can start with visual builder, then switch to CLI later if you want.

*‌→ Install Zapier CLI with `npm install -g zapier-platform-cli`, check our [CLI Quick Start Guide](https://zapier.com/developer/start/introduction) to build a demo integration, then learn more in [Zapier's CLI documentation](https://zapier.github.io/zapier-platform-cli/).*

## Coming Soon for Visual Builder

Visual Builder is a new way to build Zapier integrations—and we have a lot planned for it. Today, you can build full integrations and ship them from visual builder. Coming soon, visual builder will also let you monitor feature requests for your integration. You will also soon be able to use visual builder to scaffold new integrations, then convert the app to Zapier CLI and continue your integration development there.

If you've built a Zapier in the past with our legacy web builder, this April you'll be able to convert your existing integration to a visual builder integration to maintain your integration in the new editor and add new features.