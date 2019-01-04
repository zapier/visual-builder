---
title: Intro
order: 1
layout: post
redirect_from: /quick-start/
---

## Welcome to Zapier Zapier Visual Builder

[Zapier](https://zapier.com/) is an app automation platform that helps over 2 million people connect apps into customized workflows—what we call Zaps. With a Zapier integration, your API will connect to the Zapier platform and instantly work with 1,300+ other popular apps.

Zaps are powered by triggers, searches, and actions. Triggers watch for new data via polling API calls or webhooks, automatically deduplicating data to run the Zap only when something new is added. Zapier finds something new, it starts the rest of the workflow, with searches that lookup data via API calls or actions that create new items on an API with PUT or POST calls.

![Example Zap](https://cdn.zapier.com/storage/photos/bcad0a485f61f4acccf36cb19a0261ec.gif)

_Building an example Google Forms to GitHub Zap in Zapier's editor._

For example, say you want to turn bugs submitted in a Google Form into GitHub issues. You could make a Zap like the one above that watches your Google Form for new entries, then have Zapier add the form data to your GitHub repository as an issue. Every time the form is filled out after you turn on the Zap, a new issue will be added to GitHub. A Zapier integration for your app would let people build workflows like that and more with your app.

Zaps are built of steps—or functions that take input, communicate with an API, and return output. Users build Zaps from two or more steps from integrations. The first step is always the trigger, that watches for new or updated data every few minutes (with polling triggers) or when your APIs tells us to (with subscription triggers), and starts the Zap. Subsequent steps—or actions—then use that data to find or add items to an app.

![Zapier Fields](https://cdn.zapier.com/storage/photos/e0442350236db38688da231caafdab5f.gif)

_Each step of a Zap returns data that can be used in subsequent steps_

Zapier integrations define authentication, triggers, searches, and actions so users can connect any part of your app’s API to other applications. When you build an integration for your API, you:

1. Define how your app authenticates users
2. Choose the parts of your API that make the most sense to use as Zap steps, including triggers and actions
3. Highlight what data output from your app that users will most often use in other Zap steps.

That curated set of API features will let your app users build powerful workflows using your app. Using Zapier's visual builder, you can build an integration with your API using form fields that help you know exactly what to include.

Each step in a Zap returns data. Triggers return individual details from the new or updated item your Zap watches for, such as the data from each column in a new spreadsheet row or each bit of contact info for a new lead. Searches return the same data for items they locate from the search. Create actions return the data about the item Zapier created. When you add a new action step, you can map the data from any previous step to find or create new items in that action. That's how people use Zapier to build workflows that accomplish anything they want.

![Zapier Visual Builder](https://cdn.zapier.com/storage/photos/2316a669768c5c2ee9f4b1e84c70d1d0.png)

To enable those workflows for your app's API, you need to build a Zapier integration. The easiest way to do that is with [Zapier Visual Builder](https://zapier.com/app/developer/), a new tool to build complete Zapier integrations online in minutes. Add your app's authentication scheme, turn your API calls into triggers, searches, and create actions, and create forms where users can input the data your app needs—then release your new integration to let users connect it to 1,300+ apps with Zapier.

If you haven't used Zapier before, sign up for a free [Zapier](https://zapier.com/) account and check our [Zapier Getting Started guide](https://zapier.com/learn/getting-started-guide/) to learn the basics about using Zapier.

Then, in this Zapier Builder Getting Started guide, you'll learn how to create a new example GitHub integration in 15 minutes or less, using the Zapier visual builder. Explore Zapier's core features, learn how to add basic authentication, triggers, and actions to an integration, and build a working integration. You'll then be ready to use Zapier's visual builder to make an integration for your app.

Let's get started.