---
title: Zapier Glossary
order: 1
layout: post
redirect_from: /docs/glossary
---

## Zapier Glossary

- **Zapier**: An integration platform that connects over {{ site.partner_count }} web apps and APIs together into [multi-step, automated, customizable workflows](https://platform.zapier.com/quickstart/how-zapier-works). When an event happens in one app, Zapier can tell another app to perform (or do) a particular action.
- **Zap**: An [automated Zapier workflow](https://help.zapier.com/hc/en-us/articles/8496309697421) that connects your app to others that have built integrations. Each Zap consists of a trigger and one or more actions. When you turn your Zap on, it will run the action steps every time the trigger event occurs.
- **Trigger**: The app integration event that [starts a Zap when new or updated data is added](https://platform.zapier.com/build/trigger) to your app, either by Zapier polling a specific API endpoint to check for new data or via a notification REST webhook from your app that pushes new data to Zapier.
- **Action**: The app integration step that [finds, creates, or updates data](https://platform.zapier.com/build/action) in your app using a GET, PUT or POST request to your API using data provided when a Zap is triggered by an event in another app.
- **Create action**: The app integration step that creates or updates a single item in your app through an API call. 
- **Search action**: The app integration step that finds existing data in your app, optionally with a create action to add an item if the search does not return a result.
- **Task**: An action that a Zap successfully completes will count towards [task usage](https://help.zapier.com/hc/en-us/articles/8496196837261). The number of tasks a user has depends on their [Zapier pricing plan](https://zapier.com/pricing). 
- **Zap editor**: The [user interface](https://zapier.com/editor) where end users build their Zaps, adding triggers and actions built by app integration developers. 
- **Zap history**: An end user's [log of all the Zaps](https://help.zapier.com/hc/en-us/articles/8496291148685#h_01HD2KKYMTS7ASSEPXRMT57H63) that have run live, showing the data going in and out of each step, any error messages and task usage.  
- **Filter**: A built-in Zapier function that users can add to their Zap to [restrict it to run](https://help.zapier.com/hc/en-us/articles/8496276332557) only when certain conditional values contain specific data.
- **Paths**: A built-in Zapier function that users can add to their Zap to combine Filters and Actions to perform different actions based on different conditions. [Paths use conditional, if/then logic](https://help.zapier.com/hc/en-us/articles/8496288555917): if A happens in your trigger app, then perform this action, if B happens, then perform this other action. 
- **Formatter**: A built-in Zapier function users can add to their Zap to [customize and manipulate](https://zapier.com/apps/formatter/help) text, number and date data that is output from triggers and actions. 
- **Delay**: A built-in Zapier function users can add to their Zap to [place it on hold](https://help.zapier.com/hc/en-us/articles/8496288754829-Add-delays-to-Zaps) for a specified amount of time before the remaining actions run, in essence scheduling the action. 
- **Input Fields**: [Individual data fields](https://help.zapier.com/hc/en-us/articles/8496259603341-Different-field-types-in-Zaps) are received from trigger and action steps in a Zap, and mapped into subsequent steps' by a user to send that data as inputs to those steps' destination API. 
- **Beta**: If your app is published in the Zapier App Directory, it will [remain in Beta](https://platform.zapier.com/publish/public-integration#5-beta-phase) for 90 days to indicate its newer status to end users. 
