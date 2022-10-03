---
title: Assessing and Improving your Integration's Quality
order: 4
layout: post-toc
redirect_from: /partners/
---

# Assessing and Improving your Integration's Quality

Integration quality on Zapier boils down to two main pillars: **Health** and **Depth**.

1. **Health** - does the integration allow users to set up Zaps and keep them running reliably?
2. **Depth** - does the integration have all the functionality to allow users to automate what they want through their Zaps?

We’ll examine the main metrics around integration health and explore what they could be telling us about an integration’s quality level:

* **Errors** 
* **Zap Activation Rate**
* **Bugs**
* **Active User Retention**

Utilize the various tools and resources available in the developer platform, such as [Bugs and Feature Requests](https://platform.zapier.com/partners/feature-requests-bugs#how-to-monitor-feature-requests-and-bugs), [Monitoring](https://platform.zapier.com/docs/testing#monitoring), and your integration’s Dashboard to monitor and analyze these metrics and your integration’s health. Let’s dig in!


## Errors

Errors can cause pain for users at two vital points:

1. During the Zap setup process, stopping them from enabling and activating their Zaps
2. During the Zap’s runtime, once it has been turned on, preventing the Zap from completing all actions successfully

### Are all errors “bad”?

We don’t want integrations throwing errors unnecessarily, but not all errors are necessarily bad. It’s perfectly acceptable for your integration to throw errors, as long as [they are meaningful](https://platform.zapier.com/partners/integration-review-guidelines#7-error-handling) in stating the problem and ideally the resolution, and [handled correctly](https://platform.zapier.com/cli_docs/docs#error-handling). For example, warnings due to user error or duplications are appropriate to throw and not an issue of the integration itself. So, it’s helpful to identify which errors are actual errors of the integration’s functionality.

### What we have learned

Spikes in errors should be monitored as leading indicators of problems users are facing within your integration. The more descriptive and thorough [error handling](https://platform.zapier.com/cli_docs/docs#error-handling) your API and integration have in place, the easier it will be for users to resolve their own issues and for Zapier’s support team to assist with debugging.

### Best Practices

If you don’t have control to make changes to the API itself, utilize custom error handling to improve your error messages:

* Elaborate on terse responses with user-friendly messaging.
    * Update “not_authenticated” to “Your API Key is invalid. Please reconnect your account.”
* Surface specific information to users regarding the field and why it’s producing an error. This empowers users to fix Zap issues independently.
    * Instead of “Provided data is invalid”, return “Contact name is invalid”.
    * Improve “Contact name is invalid” with “Contact name exceeds character limit.”
* Format the error to include a second, optional argument for a code machines can use to identify the type of error, and last, optional argument of a HTTP status code.
    * `throw new z.errors.Error('Contact name exceeds character limit.', 'InvalidData', 400);`


## Zap Activation Rates

### What is Zap Activation Rate?

Consider all of the Zaps users try to create with a trigger, action, or search from your integration. Then look at the percentage of those Zaps that actually activated within 24 hours of creation, meaning the Zap ran at least one successful task. _That’s the Zap Activation Rate._

### Does low activation mean something is broken?

Not necessarily. Maybe the user started to make a Zap, put the kettle on, forgot about what they were doing and didn’t bother ever coming back to finish what they started.

It can also highlight that certain triggers or actions are proving challenging to set up in a Zap or are erroring when run. Perhaps your trigger sample doesn’t return custom fields the user is looking to map in the Zap or the user gets confused by unclear input fields while setting up their action; these are two of many reasons why users abandon Zap setup. 

### What we have learned

Zap Activation Rates at the individual trigger and action level are a great leading indicator of performance and usability. Don’t forget about the authentication step in your integration too! If users can't authenticate or get their Zaps enabled and activated, they stand little chance of ongoing success.

### Best Practices

Give users the best chance to successfully activate their Zaps by making the integration as familiar and easy-to-use as possible:

* Follow our [Integration Review Guidelines](https://platform.zapier.com/partners/integration-review-guidelines) which provide detailed user experience best practices for building your integration.
* Create [Zap Templates](https://platform.zapier.com/partners/zap-templates) for popular use cases to simplify the setup process and decrease room for user error.
* Head to the Zap Editor to create and test Zaps using your own integration. This gives you firsthand experience on how users interact with the integration. 
* Keep your platform and Zapier integration parallel to maintain a consistent experience for mutual users.
    * Object and field names referenced in the integration should parallel names in the platform. For example, don’t name your trigger “New Lead” if they are referred to as “Contacts” in your platform. This makes it hard for users to find the functionality they want.
    * Provide all available input fields in the platform in the integration step, including custom fields. 
    * Match the field types in the platform to the integration. For example, if a field is a static dropdown in the platform, implement it as the same type within the integration.


## Bugs

As users encounter bugs or think of new features they’d like within the integration, some reach out to the Zapier support team. Those requests are logged in Zapier’s issue tracker, which you can see from the Bug & Feature Requests page of the integration’s developer platform. Here are a couple things to note about bugs:

1. _When the number of open bugs goes above zero, it doesn’t really matter how many bugs you have._ The important datapoint is how many of your users are affected overall and what percentage of the app’s overall monthly active users that impacts.
2. _Your past history on closing bugs doesn’t influence your current health score._ Running track in college doesn’t mean a darn thing to your doctor thirty years later if you roll in with high cholesterol because of your penchant for McDonalds and KFC. Same with bugs and integration health.

Don’t forget the affected user counts on issues underrepresent the actual totals, as only a small portion of all users facing an issue take the time to contact support. If a significant number of users have made the effort to contact support to say they are affected by a bug in the integration, it should raise flags.

### What we have learned

Open bugs are one of the best indicators of an integration’s health. If users are contacting Zapier’s support team to tell us about problems, we take that as a strong signal something is broken and needs to be fixed.

Regardless of the size of your integration’s user base, keeping the percent of monthly active users affected by open bugs under double figures (and ideally at 0) is recommended for a healthy integration.

### Best Practices

* Instead of a “set-it-and-forget-it” mentality, allocate ongoing resources in your team's product roadmap for the maintenance of your Zapier integration to avoid surprise work or gaps in functionality.
* Can’t keep up with maintenance? Hire a Zapier expert to help you fix on-off bugs or maintain your integration.


## Active Users Retention

At Zapier, churn means a user used your integration in their Zaps 29 - 56 days ago, but hasn’t run a successful task in one of those Zaps in the past 28 days. This user is considered to have churned from the integration. From the opposite perspective, we can look at active users retention, or the percentage of users who haven’t churned.

### Did they leave Zapier altogether?

Not necessarily. Maybe they switched to using a competing integration or their workflow had a more periodic or seasonal cadence.

But, it could also mean they got so frustrated with the experience of trying to get their Zap working and _keep_ it working successfully, they turned it off, deleted it, and walked away.

### What we have learned

Lowered active user retention rates don’t necessarily mean poor integration health. Some apps lend themselves to use-cases with shorter life-spans than others. That said, spikes in churn rate not related to seasonal variations in usage could be indicators of a problem with something not functioning as expected.

Active user retention is not a leading indicator. In fact, it’s quite a lagging one that may only start indicating a problem up to 28 days after it has been an issue. That doesn’t deem it useless, we just have to know how to make full use of it

### Best Practices

Approaching active user retention with a long-term strategy can help maintain a consistently high level of retention:
 
* [Embed](https://platform.zapier.com/embed/overview) the Zapier experience with copy-and-paste and customizable code within your platform to provide automation value directly to users. Embeds have proven to [reduce churn](https://platform.zapier.com/partner_success_stories/all) on Partners’ platforms. Find live embed examples under the ‘Embed’ tab of the integration’s developer platform.
* [Share use cases](https://platform.zapier.com/partners/partner-faq#tip-3-share-zapier-use-cases-in-your-onboarding) widely during your platform’s onboarding process. Having multiple Zaps using your integration increases stickiness of users not only to the Zapier integration, but also to your platform.
* Update the integration regularly with features as your platform evolves. Invite stakeholders as [Collaborators](https://platform.zapier.com/partners/faq#add-collaborators-to-your-team) to your integration to give them read-only access to insights, metrics, and feedback to prioritize and align improvements. 
