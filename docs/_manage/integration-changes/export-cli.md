---
title: Export integration to Platform CLI
order: 13
layout: post-toc
redirect_from: 
    - /docs/export
    - /manage/export-integration
    - /manage/making-changes#converting-ui-to-cli
---

# Export integration to Platform CLI

The Zapier Platform CLI (Command Line Interface) is a toolset you install and run in your local development environment. It allows you to build, test, and manage your Zapier integration through JavaScript code and terminal commands.

Platform UI is the way for users with API experience that are more comfortable with a visual form editor to build integrations on Zapier.

The CLI is, on the other hand, the most powerful tool for professional developers and teams. Some of the advantages:

- Access to all [features](https://platform.zapier.com/quickstart/ui-vs-cli) of the Zapier Platform
- Ability to better optimize your code. Move shared logic into modules. Leverage middleware to centralize request & response processing.
- Easier team collaboration. You'll be able to check all the code for your Zapier integration into your team's source control repo.
- Set up automated regression tests, to catch errors each time you push a change.

To export your existing Platform UI integration to Platform CLI:

## 1. Install and configure the Zapier CLI on your development environment

Follow the steps in the setup section in our [quickstart guide](https://platform.zapier.com/reference/cli-docs#quick-setup-guide)

## 2. Run the `convert` command to create a CLI version of your project locally

Create a new directory for your Zapier project and from the command line `cd` into it. Then run:

`zapier convert {your integration id} . --version={integration version you want to convert}`

Your integration ID can be found in the browser location bar in the Platform UI:

![](https://cdn.zappy.app/c5e0c7f17a5ab52d9661e134394e9cc7.png)

Similarly, your version can be found there, and elsewhere throughout the Platform UI:

![](https://cdn.zappy.app/e31dd202b5e64bbcb13fc8b200518d17.png)

Using this example, to create our project in the current directory our command would be:

`zapier convert 1234 . --version=1.0.0`

## 3. Explore your new CLI project and get familiar with the tool

Check out the resources available in the [CLI section](https://platform.zapier.com/reference/cli-docs) of the docs to learn all about the Zapier CLI.

If you need a refresher on JavaScript, it's well worth the time to check out some of the many great resources available [online](https://javascript.info/). The Zapier Platform uses promises pretty heavily, so this is a good JavaScript topic to get familiar with.

## 4. Deploy

When you ran convert and created your new local CLI project, it was automatically associated with your Zapier integration (using the `.zapierapprc` file).

A couple of important notes before deploying:

- When you push the CLI project to the server it will create a _new version_ of your integration. If you haven't gotten familiar with how versions work you might take a moment and learn about those [here](https://platform.zapier.com/manage/versions).
- Take a look at the version number in your `package.json` file. When you created your project with the `convert` tool we automatically incremented the version you converted. You can change this to a different version number depending on your needs, but make sure a version with that number doesn't already exist in your integration. Run `zapier versions` from your project directory to see what's already been created.
- Integrations converted with the `zapier convert` command will include `convertedByCLIVersion` in the `package.json` for informational purposes.

When you're ready to deploy your CLI version run:

`zapier push`

When that completes you'll be able to see the new version in the Platform UI in the Manage > Versions section, and will be able to make Zaps with your new CLI-built version.

You will not be able to edit your new CLI-built version from the _Build_ section of the Platform UI, the attributes of this version will all [show a lock icon](https://cdn.zappy.app/f048ffc4c905bcbb332e344ce0ce52ba.png). 

You can still use all the other functions of the Platform UI, though, including version management, embed management and your Partner Dashboard. Your earlier versions, created within the Platform UI, are also still available and can still be edited and used. 

If you decide that the Platform CLI is not for you, you can delete your new version from Manage > Versions and continue where you left off in the Platform UI.
