---
title: Trigger
order: 1
layout: post-toc
redirect_from: 
    - /quickstart/build-trigger
    - /docs/triggers
    - /build/trigger
    - /build/triggers
---

# Trigger

Every Zap has a single trigger. Triggers are how your app's users can start automated workflows whenever an item is added or updated in your app. New or updated contacts, database records, blog posts, subscribers, form entries and project tasks, are examples of items that can be used to trigger a Zap. 

![Zapier Trigger Visual Builder](https://cdn.zappy.app/024547d6df8622335ca65456c6d0a11c.png)

Triggers only watch for new data and typically send no or little data to your app. They are often quicker to set up than Zapier [actions](https://platform.zapier.com/build/action). 

Design triggers around how users interact with your app, not based on which API endpoints are available.

The are two types of triggers.

## 1. Polling trigger 

This trigger type periodically checks the provided API endpoint for new or updated data. 

The update time or frequency of polling occurs per active Zap every 1 to 15 minutes, depending on the user's [Zapier plan level](https://zapier.com/app/pricing).

The API endpoint must list new or updated items in an array sorted in reverse chronological order. These are typically the most common API endpoints to read data from a platform. For new item triggers, the endpoint should list newly created items first; while for updated item triggers, recency of update is preferred.  If your API lists items in a different order by default, but allows for sorting, include an order or sorting field in your API call to ensure newest records are returned on the [first page of results.](https://platform.zapier.com/build/dedupe)

Include details in your trigger description to let users know which type of updates will run the trigger.

Zapier automatically deduplicates incoming polling trigger data, so that Zaps do not run multiple times on the same data. Known as deduplication, this is [explained to users as a concept](https://zapier.com/help/create/basics/data-deduplication-in-zaps). Ensure your polling triggers behave as users expect by following [deduplication guidelines](https://platform.zapier.com/build/dedupe) for new item and updated item triggers. 

## 2. REST Hook trigger

This trigger requires your app to support REST Hooks - webhook subscriptions that can be manipulated through a REST API. It runs in near realtime with your app pushing data to Zapier, running Zaps as soon as new data comes into your app instead of waiting for Zapier to fetch new data from your API on a polling frequency.

This method of triggering also prevents numerous - and sometimes unnecessary - requests from being made to your API's endpoints in polling requests. 

A webhook subscription is created between Zapier and your app, and whenever the trigger event occurs in your app, a webhook is sent by your app to the unique webhook URL provided by Zapier for each active Zap started with that trigger. Zapier does not support Identity Confirmation.