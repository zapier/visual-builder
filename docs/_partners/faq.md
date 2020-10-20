---
title: Zapier Integration Tips and FAQs
order: 6
layout: post-toc
redirect_from: /partners/
---

# Zapier Integration Partner Tips and FAQs

Before you develop your Zapier integration, it’s important to become familiar with the criteria Zapier uses to review all new app integrations.

The following tips are based on the most common issues we encounter and will help you to breeze through the app review phase.

## Get Familiar with Zapier

If you haven't used Zapier before, [sign up](https://zapier.com/sign-up/) for a free account and try a few popular integrations before building your integration. This will help you understand how Zapier works, how your users will set up Zaps, and how your integration can best fit into Zap workflows.

## Focus on Key Use Cases

Your initial Triggers, Actions, and Searches should focus on the main things users do with your app. Check similar apps in [Zapier's App Directory](https://zapier.com/apps/) to get some ideas on which items to include in your integration. Don't include too many triggers or actions at first, as new apps with more than 5 Triggers, Actions, or Searchers may not be able to go public (unless each each Trigger, Action, and Search has a lot of test users already).

## Test Early With Real Users

Hopefully, you have a bunch of keen users waiting to get their hands on your integration. That help give us confidence that your integration is useful and working well for a bunch of users.

## Check Your App Integration Style

Users should already be familiar with the terminology used in your Zapier integration—it should be consistent with what is used in your app's own UI. It should also be consistent with the style used in other popular Zapier integrations.

We strive to give users a consistent experience throughout Zapier. Be sure to follow [Zapier's standards for app branding](https://platform.zapier.com/partners/planning-guide#how-to-brand-your-zapier-integration) to make your app fit into the Zapier ecosystem well.

## Make Connecting New Accounts Easy

Connecting to Zapier must be easy for the user. OAuth v2 is the preferred authentication scheme; otherwise, make sure users can easily retrieve or generate an API Key or other credentials themselves without needing support assistance. Also, the Test Trigger should provide actionable error messages to help users successfully connect their account.

## Provide a Valid Test Account

The App Review Team will go through each Trigger, Action, or Search in your integration to verify that it’s working in a similar way the interactions should work within your app. In order to do this, set up a valid test account and share the credentials with our team (ideally with contact@zapier.com as the account email address). Make sure the account includes all the features needed to test out each Zap step, with any special configurations set. If features require an environment that is hard to replicate or require specific hardware, provide a demo video or documentation to the Zapier team.

## Ensure Your Integration is Complete and Platform Consistent

You should submit your integration for review only when it is complete and ready to be published. Make sure to thoroughly test your integration for edge cases and fix all bugs before submitting. Please don’t treat the App Review as a software testing service for your platform, and make sure both the platform and integration work consistently without errors. We will not allow incomplete or error-ridden app integrations to become public.

## Avoid Repeated Submissions

Submitting several app integrations that are essentially the same ties up the App Review process and risks the rejection of your integrations. Please be thoughtful and consider combining your apps into one where it makes sense. Also, please do not spam the App Review team with multiple versions of the same integration while going through that review process.

## Avoid Misleading or Malicious Functionality

Your app must perform as advertised and should not give users the impression the app is something it is not. If your app appears to promise certain features and functionalities, it needs to deliver. Do not create a Zapier integration that can be used to spam, phish, or send unsolicited messages to users.

If you attempt to cheat the system (for example, by trying to trick the review process, steal user data, or fake real users) your apps will be removed from Zapier and you could be expelled from submitting any apps in the future.

### Further Reading

For more information, check [Zapier's guide to building a Zapier integration](https://platform.zapier.com/partners/planning-guide) for the core guidelines to follow when building and branding your Zapier integration.

---

<a id="deploy-errors"></a>

## Common Errors When Deploying a Zapier Integration

If your app is usable by other people (Invite-Only, Pending, or Public), a series of checks will occur when you deploy/replace the app with a new version. This is to avoid situations that may cause existing Live Zaps to stop working, or will put Paused Zaps into a corrupted state which causes them to fail when turned on.

Here are some of the commonly encountered issues, and their solutions:

### You cannot add this required field without a previously matching field (by key).

This means that you're adding a new **required** field, and it's possible that the existing Zaps don't have a value for that field (and thus, the Zaps may break).

**If this is a field in a Trigger, Action, or Search, there are three solutions:**

- Leave the field as "optional", and use custom code in your API call to set a value if the user left blank in their Zap.
- If the Zaps are your own (or a co-worker's), and the quantity is "very small", try deleting the Zaps that are using this Trigger/Action/Search, then wait for the stats to re-cache (they're cached every midnight UTC), then retry the deployment.
- Copy the Trigger/Action/Search and give it a new **key** (like appending `_v2` on the end), add your required field to the **new** Trigger/Action/Search, and **hide** the previous Trigger/Action/Search. That way existing Zaps will continue to work with the previous (and now hidden) Trigger/Action/Search definition, and new Zaps will be forced to provide a value for the required field.

**If this is a field in your Authentication:**

This is a pretty big change, because it means that all of the accounts that your users have already setup won't work with the app.

There are two solutions:

- Leave the field as "optional", and use custom code in your API call to set a value if left blank.
- Please [contact us](mailto:partners@zapier.com) and we'll try to find the best approach.

### Do not remove this trigger/action/search! Be sure its key matches a trigger/action/search in the new app if you did not remove it.

The Triggers, Actions, and Searches are identified by their **key**, so if you remove it, or change its **key**, this message appears.

There are two solutions:

- If you need to remove a Trigger/Action/Search, change its visibility to **hidden** instead.
- If you've renamed the **key** for a Trigger/Action/Search, you'll need to switch it back to the previous **key**.

### You cannot change an existing trigger's data source (Polling, REST Hooks, etc).

A change like this will cause your user's Zaps to stop working.

There are two solutions:

- If the Zaps are your own (or a co-worker's), and the quantity is "very small", try deleting the Zaps that are using this Trigger, then wait for the stats to re-cache (may take an hour), then retry the deployment.
- Copy the Trigger and give it a new **key** (like appending `_v2` on the end), change the data source of this new Trigger, and **hide** the previous Trigger. That way existing Zaps will continue to work with the previous (and now hidden) Trigger definition, and new Zaps will use the new Trigger definition.

### You cannot change the auth type

The existing app uses an authentication type (like Basic Auth, API Key, or OAuth), and your new app uses a different authentication type. This is a pretty big change, because all of the accounts that your users have connected up will stop working for their Zaps.

The typical solution is to take your new app and put it into "Invite Only" status, or submit it for "Publishing", and then [contact us](mailto:partners@zapier.com) and ask us to "hide" the previous app. You can [learn more about the process of getting the new app deployed here.](https://zapier.com/developer/documentation/v2/migrating-your-zapier-integration/)

### Deduplication comparison for triggers errored

If your app contains triggers that use "polling", our system performs a test to ensure that the new version of your app returns the same set of information as the existing/current app.

The way that is determined is that our system will randomly select a set of Zaps (that are turned "on") and are using your app's polling trigger. Our system runs the "polling cycle" using the current app, and the new app, and then compares the set of `ID` fields returned by both. If they don't match (or an error occurs when testing the newer trigger), then the deployment is halted, and an e-mail is sent to the owner of the app.

Some common issues that may cause this:

- If you change the "limit" or "page size" of the data returned. For example, if your trigger was previously receiving 100 records, and the new version receives 1000 records, that will cause the test to fail. If you need to make this kind of change, we will need to "pause" all of the Zaps using the trigger(s), perform the deploy, and then "resume" all of those Zaps (so that they'll "see" the "new" set of IDs/objects, and will use that as the baseline for future polling).
- If you change any filtering logic in your API call -- IE: adding a default `?status=open` query string parameter. The issue is that if the old trigger didn't have that, and the new trigger does, the Zapier system may see new results returned and cannot distinguish if it really is an intended trigger by the user, or a side effect of a slightly different API call.
- API Rate limits. If your endpoint has a limit on the quantity of calls that may be performed within a small span of time (like "one API call per second"), the polling test will succeed when testing the existing/current trigger, but will hit that limit when testing the new trigger.
- Reading data "deletes" it. If your endpoint provides information so that it can only be "read once" (like an activity log), this will cause the test to fail, because the polling cycle with the newer trigger will receive an empty set of data. Polling triggers cannot be used for this kind of purpose.

---

## Contact Zapier

Can't find the answer you need here or in Zapier's [integration planning guide](https://platform.zapier.com/partners/planning-guide)? Feel free to get in touch with our team:

### Join Zapier Develoer Community

Zapier's Platform team has a [community](https://community.zapier.com/developer-discussion-13) dedicated to helping developers with new and existing app integrations. We're a worldwide team, so there's usually someone around to answer your questions. We'd love to hear your experience building on Zapier.

### Email Zapier's Platform Team

For questions about building Zapier integrations, email [partners@zapier.com](mailto:partners@zapier.com), where our Platform team can help resolve issues you encounter while building Zapier integrations, and our Partnerships team can help launch your Zapier integration.

If you have issues with your Zaps and core Zapier account, reach out to [contact@zapier.com](mailto:contact@zapier.com). Our support team has access to the most recent logs and other details that will help them work on your issue.

### Find a Zapier Integration Partner

We're excited to help you with your Zapier app, but we can't build it for you. If you'd like someone to take over the technical reins, check our [a list of third-party Zapier developers and consultants](/partners/trusted-developers) to find someone to help develop a Zapier integration for your app.
