---
title: Changes to your API can impact your integration
order: 12
layout: post-toc
redirect_from: /manage/making-changes#making-changes-to-your-api
---

# Changes to your API can impact your integration

## Change scenario

When making changes to your API, consider how these will affect your Zapier integration. API updates can vary from small to significant changes and can have varying effects on your users’ Zaps.

## Impact to users

Though not exhaustive, here are some potential major impacts to users:

- If a new version with breaking changes to authentication is promoted, users with existing Zaps will have to manually reconnect their account on Zapier.
- If a new version with breaking changes to any trigger, action, or search is promoted, users with existing Zaps will have to manually upgrade _each_ Zap using your integration. Keep in mind: power users can have tens to hundreds of Zaps using your integration.
- Changes to a trigger, action, or search’s response data can break or negatively affect the proceeding steps of the Zap.
- Changes to response data in polling triggers can prevent Zaps from triggering on new records or cause them to trigger on old records. This can lead to missed data and undesirable results for your users.

## Best practices

To mitigate the impact of API changes on your Zapier users, consider the following best practices:

- Maintain general backwards compatibility on existing endpoints. This ensures that the existing Zaps continue to work as expected, and your users won't need to modify them due to API changes.
- For polling triggers - changing the number of records returned from the endpoint can significantly impact the functionality of the users' Zaps.
- Implementing pagination on an endpoint can affect how much data is fetched and processed when a Zap polls that endpoint.
- Changing the sort order of response data returned can impact Zap triggers. For polling triggers, ensure that the data is always sorted in reverse chronological order to maintain compatibility.

By adhering to these best practices, you can minimize disruptions to your Zapier users when updating or modifying your API. A well-managed API transition process ensures that your users continue to have a seamless and efficient Zapier integration experience.