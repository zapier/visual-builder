---
title: Searches and Creates
order: 12
layout: post-toc
redirect_from: /docs/
---

## Zapier Action Types: Searches and Creates

![Zapier Action Options](https://cdn.zapier.com/storage/photos/d29ad3418c8780c28906716d09ad47b3.png)

Zaps start with a trigger, a Zapier step that watches for new data from an API and starts the Zap workflow. Then it’s up to action steps to make use of that data.

Action steps can find and/or create items in apps. The most common actions—shown at the top of each Zap action step—are _Create_ actions, which as their name implies make new items from the data users enter. Then there are _Search_ actions, which can find data in apps and optionally create new items if the search returns no results.

Creates add new data; Searches find existing data, and fill in gaps if needed.

Most Zapier integrations should at a minimum include create actions to let users add items to their app automatically. Anything people can build in your app could be made automatically with create action.That’s what most Zaps do for people. They add new projects, tasks, contacts, invoices, leads, deals, files, photos, and much more to apps whenever they’re needed. Create actions can also update existing items—something often paired with a Search to locate the item needing updates first.

Search actions, then let users do more with the data they’ve already added to your app. Perhaps they want to avoid adding duplicate items—and prevent errors from your API. Maybe they need to look up info about an item to use in a subsequent step. Or for apps that are built around search—including weather, conversion, and contact lookup apps—search actions might be the integration feature where Zaps find info from this app then use it in subsequent steps.

Search actions can optionally create items if nothing is found for the search. They can’t do this on their own, though—apps first need to have a create action to make the item, and then can pair the search step with a create step, embedding the create inside the search step to find or create items in one step.

Create and Search actions differ not only in their purpose, but also in their API calls. Create actions by default POST data to an API, while Search actions by default GET data from an API like a Trigger. Create actions’ input fields gather data that is sent to the API to create new entries, while Search actions’ input fields gather data used to filter through data and return the closest match. Both can only do one thing at a time: Create actions make one new item, and search actions find the first matching result.

Together, create and search actions give users a powerful way to connect apps, using data they’ve previously saved and adding new entries that can pull from existing data in all of their apps.