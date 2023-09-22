---
title: Platform UI vs Platform CLI
order: 1
layout: post-toc
redirect_from: 
    - /docs/vs
    - /quickstart/zapier-platform
---

# Platform UI vs Platform CLI

There are two different developer tools to build either private or public integrations with on the Zapier Developer Platform: Platform UI or Platform CLI.

## Platform UI

Platform UI is the visual way for users  with API experience to build integrations in a web app editor. It allows for some advanced calls and response parsing when using Code mode; but is predominantly designed for builders more comfortable with a visual form editor than working in code. 

![Zapier Platform UI](https://cdn.zappy.app/a8c009d1109749b44052922f2a6ec9bc.png)

 To get started, check out the following resources:

- [Quick start guide to using Platform UI](https://platform.zapier.com/quickstart/platform-ui-guide)
- [Tutorial using Github's API to build with the Platform UI](https://community.zapier.com/featured-articles-65/zapier-platform-ui-a-complete-guide-on-how-to-integrate-with-github-26298#post108889)

## Platform CLI

Platform CLI is a terminal-based app that allows builders to scaffold new integrations locally, using standard JavaScript in your local development environment and code editor. It allows for custom coding for API calls, middleware, file support and other advanced functionality. It's the preferred tool for engineers comfortable with a standard development workflow and collaborating in a local environment using GIT version control before pushing integration versions to the Zapier server. Platform CLI can be more difficult to use for non-engineers, but will likely be more efficient for an engineering team. 

![Zapier Platform CLI](https://cdn.zapier.com/storage/photos/27d28a5fdd0c878d7558b4abd4f106ec.png)

To get started, check out the following resources:

- [Quick start guide to using Platform CLI](https://platform.zapier.com/reference/cli-docs#quick-setup-guide)
- [Tutorial using Github's API to build with Platform CLI](https://developer.zapier.com/cli-guide/introduction)
- [CLI documentation](https://github.com/zapier/zapier-platform/blob/main/packages/cli/README.md)

##  Comparison between developer tools

You can accomplish the same goals and build equally powerful Zapier integrations with both Platform UI and Platform CLI. The best tool for your integration depends on your work style and integration needs. 

Below you can review what is capable between both developers tools

| Authentication | Platform UI | Platform CLI |
|----------------|----|-----|
| Basic Authentication | ✓ | ✓ |
| Session authentication | ✓  | ✓  |
| API Key | ✓ | ✓ |
| Custom | ✓ | ✓ |
| OAuth v1 |  | ✓ |
| OAuth v2 | ✓ | ✓ |
| Digest | ✓ | ✓ |

| Triggers | Platform UI | Platform CLI |
|----------|----|-----|
| REST Hooks | ✓ | ✓ |
| Polling triggers | ✓  | ✓  |
| Support for static webhooks |  |  |
| Customize request handling with JavaScript | ✓ | ✓ |

| Search Actions | Platform UI | Platform CLI |
|----------------|----|-----|
| Search or create functionality | ✓ | ✓ |
| Customize request handling with JavaScript | ✓  | ✓  |

| Create Actions | Platform UI | Platform CLI |
|----------------|----|-----|
| Customize request handling with JavaScript | ✓  | ✓  |

| Advanced | Platform UI | Platform CLI |
|----------------|----|-----|
| Custom middleware |  | ✓  |
| Resources |  | ✓  |
| File support | | ✓  |
| Hydration | | ✓  |
| Import and use NPM modules  |  | ✓  |
| Organize code with common functions  |   | ✓  |

| Testing and Workflow | Platform UI | Platform CLI |
|--------------------|----|-----|
| GUI with form-based editor | ✓  |   |
| WYSIWYG form preview | ✓  |  |
| Write custom automated test suites |   | ✓  |
| Add team members to project | ✓  | ✓  |
| Manage testers  | ✓  | ✓  |
| Monitor usage  | ✓  | ✓  |
| View logs  | ✓  | ✓  |
| Manage versions  | ✓  | ✓  |
| Use custom source code manager  |  | ✓  |
| Export integration to CLI   | ✓  | -   |
  
If you are still unsure after reviewing our comparsion tables, Zapier advises to build with the Platform UI.

## Switching between developer tools

### Platform UI to Platform CLI

Yes, it is possible to switch your integration from Platform UI to Platform CLI.

You can [export](https://platform.zapier.com/manage/export-integration) an existing Platform UI integration to Platform CLI. Once exported, you can customize your integration in your local development environment. You will still have access to view your integration in the Platform UI.

Before making this change, Zapier recommends to learn about more the user impact when [switching from Platform UI to Platform CLI](https://platform.zapier.com/manage/making-changes#converting-ui-to-cli).

### Platform CLI to Platform UI

It's not possible to export an integration from Platform CLI to Platform UI. 

You would need to create a new integration in the Platform UI, which means existing customers would need to update their Zaps to use your new integration. Learn more about [this process and best practices to minimize user impact](https://platform.zapier.com/manage/making-changes#converting-cli-to-ui).