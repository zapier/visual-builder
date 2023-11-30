---
title: Zap activation rates
order: 7
layout: post-toc
redirect_from: 
    - /manage/analyze-integration-performance#zap-activation-rates
---
# Zap activation rates

Consider all of the Zaps that users try to create with your integration's triggers, actions, or searches. The Zap activation rate is the percentage of those Zaps that actually activated within 24 hours of creation, meaning the Zap ran at least one successful task.

A low activation doesn't necessarily mean something is broken. Maybe the user started to make a Zap, put the kettle on, forgot about what they were doing and didn’t bother ever coming back to finish what they started.

It can also highlight that certain triggers or actions are proving challenging to set up in a Zap or are erroring when run. Perhaps your trigger sample doesn’t return the custom fields the user is looking to map in the Zap or the user gets confused by unclear input fields while setting up their action; these are common reasons a user may abandon setting up their Zap.

## Key Zapier insights

Zap activation rates at the individual trigger and action level are a great leading indicator of performance and usability. Simplifying authentication is a vital first step. If users can't authenticate or get their Zaps enabled and activated, they stand little chance of ongoing success.

## Best practices

Give users the best chance to successfully activate their Zaps by making the integration as familiar and easy-to-use as possible:

- Follow our [Integration publishing requirements](https://platform.zapier.com/publish/integration-publishing-requirements) which provide detailed user experience best practices for building your public integration.
- Create [Zap Templates](https://platform.zapier.com/publish/zap-templates) for popular use cases to simplify the setup process and decrease room for user error.
- Head to the Zap editor to create and test Zaps using your own integration. This gives you firsthand experience on how users interact with the integration. 
- Keep your app and Zapier integration parallel to maintain a consistent experience for mutual users.
- Object and field names referenced in the integration should parallel names in your app. For example, don’t name your trigger _New Lead_ if they are referred to as _Contacts_ in your app. This makes it hard for users to find the functionality they want.
- Provide all available input fields in your app in the integration step, including custom fields. 
- Match the field types in your app to the integration. For example, if a field is a static dropdown in the app, implement it as the same type within the integration.