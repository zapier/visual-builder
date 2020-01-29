---
title: Export Project to CLI
order: 21
layout: post-toc
redirect_from: /docs/
---

# Export Your Project to the Zapier CLI

The Zapier CLI (Command Line Interface) is a toolset you install and run on your local development environment. It allows you to build, test, and manage your Zapier integration through JavaScript code and terminal commands.

<a id="why"></a>

## Why switch to the CLI?

We created the visual builder to be the easiest way for everyone to get started building their Zapier integration. The CLI is, on the other hand, the most powerful tool for professional developers and teams. Some of the advantages:

- Access to all [features](/docs/vs) of the Zapier Platform
- Ability to better optimize your code. Move shared logic into modules. Leverage middleware to centralize request & response processing.
- Easier team collaboration. You'll be able to check all the code for your Zapier integration into your team's source control repo.
- Set up automated regression tests, to catch errors each time you push a change.
- More!

<a id="how"></a>

## How to export your integration

_Step 1: Install and configure the Zapier CLI on your development environment._

Follow the steps in the setup section in our [quickstart guide](https://zapier.com/developer/start/introduction)

_Step 2: Run the `convert` command to create a CLI version of your project locally_

Create a new directory for your Zapier project and from the command line `cd` into it. Then run:

`zapier convert {your integration id} . --version={integration version you want to convert}`

Your integration ID can be found in the browser location bar:

![](https://zappy.zapier.com/4452B664-3C68-4762-A85A-4AF75DAB0E62.png)

Similarly, your version can be found there, and elsewhere throughout the UI:

![](https://zappy.zapier.com/ECE260EE-8B9D-46B7-B6AD-6BEA5078EEDF.png)

Using this example to create our project in the current directory our command would be:

`zapier convert 10318 . --version=1.0.1`

_Step 3: Explore your new CLI project and get familiar with the tool_

Check out the resources available in the [CLI section](/cli_docs/docs) of the docs to learn all about the Zapier CLI.

If you need a refresher on JavaScript, it's well worth the time to check out some of the many great resources available [online](https://javascript.info/). The Zapier Platform uses promises pretty heavily, so this is a good JavaScript topic to get familiar with.

_Step 4: Deploy_

When you ran convert and created your new local CLI project, it was automatically associated with your Zapier integration (using the `.zapierapprc` file).

A couple of important things to know before deploying:

- When you push the CLI project to the server it will create a _new version_ of your integration. If you haven't gotten familiar with how versions work you might take a moment and learn about those [here](/../versions).
- Take a look at the version number in your `package.json` file. When you created your project with the `convert` tool we automatically incremented the version you converted. You can change this to a different version number depending on your needs, but make sure a version with that number doesn't already exist in your integration. Run `zapier versions` from your project directory to see what's already been created.
- You will not be able to edit your new CLI-built version from the UI. You can still use the options under the "Manage" section. Your earlier versions, created within the UI, are still there and can still be edited and used. If you decide that the CLI tool is not for you, you can go back and continue where you left off in the UI.

When you're ready to deploy your CLI version run:

`zapier push`

When that completes you'll be able to see the new version in the UI in the Versions section, and will be able to make Zaps with your new CLI-built version!
