---
title: Intro
order: 1
layout: post-toc
redirect_from: /quick-start/
---

# Welcome to Zapier Platform UI

[Zapier](https://zapier.com/){:target="_blank"} is an app automation platform where over 2 million people connect apps into customized workflows—what we call Zaps. A Zapier integration can connect your app's API to the Zapier platform and let it integrate with {{ site.partner_count }} other popular apps to watch for new or updated data, find existing data, or create and update data.

![Example Zap](https://cdn.zappy.app/eeff50e2737492689f688c379c1db65a.gif)

_Building an example Google Forms to GitHub Zap in Zapier's editor._

For example, say you want to turn bugs submitted in a Google Form into GitHub issues. A Zap like the one above could watch your Google Form for new entries, then use the form data to make a new GitHub issue. Fill out the form anytime to add a new issue.

A Zapier integration for your app lets your users build workflows like that and more with your app. Check out a demo [here](https://zapier.com/demo). 

Each Zap created starts with a trigger (something that happens in one app) and then one or more actions (something else that happens in another app). These triggers and actions take input, communicate with an API, and return output. 

The first step is always the trigger, which watches for new or updated data every few minutes (with polling triggers) or waits until your API tells us to do something (with subscription triggers), and starts the Zap. Subsequent steps—or actions—then use that data to find or add items to an app, with search actions to find data with GET calls or create actions to add new or update existing items with POST or PUT calls.

![Zapier Fields](https://cdn.zappy.app/494bbd089cb1c74b65c8da7ea42b27a0.gif)

_Each step of a Zap returns data that can be used in subsequent steps_

Zapier integrations define authentication, triggers, searches, and actions so users can connect any part of your app’s API to other applications. When you build an integration for your API, you:

1. Define how your app authenticates users
2. Choose the parts of your API that make the most sense to use as Zap steps, including triggers and actions
3. Highlight what data output from your app that users will most often use in other Zap steps.

That curated set of API features will let your app users build powerful workflows using your app. Using Zapier's Platform UI, you can build an integration with your API using the Visual Builder and input form fields that help you know exactly what to include.

Each step in a Zap returns data. Triggers return individual details from the new or updated items in an array, such as the data from each column in a new spreadsheet row or each bit of contact info for a new lead. Searches return the same data array for items they locate from the search. Create actions return a data object about the item Zapier created.

When you add an action step to a Zap, you can map the data from any previous step to find or create new items in that action. That's how Zapier is used to build workflows between two or more apps. 

![Zapier Platform UI](https://cdn.zappy.app/7be3b0b8ebb66691d7e60547c76b6128.png)

To enable those workflows for your app's API, you need to build a Zapier integration. The easiest way to do that is with [Zapier Platform UI](https://developer.zapier.com/){:target="_blank"}, a new tool to build complete Zapier integrations online in minutes. Add your app's authentication scheme, turn your API calls into triggers, search or create actions, and build forms where users can input the data your app needs—then release your new integration to let users connect it to {{ site.partner_count }} apps with Zapier.

If you haven't used Zapier before, sign up for a free [Zapier](https://zapier.com/){:target="_blank"} account and check our [Zapier Getting Started guide](https://zapier.com/learn/zapier-quick-start-guide/ ){:target="_blank"} to learn the basics about using Zapier.

Then follow this guide to learn how to create an example GitHub integration in 15 minutes or less with Zapier Platform UI. Explore Zapier's core features, learn how to add OAuth v2 authentication, triggers, and actions to an integration, and build a working integration. You'll then be ready to use Zapier Visual Builder to make an integration for your app.

Let's get started.
