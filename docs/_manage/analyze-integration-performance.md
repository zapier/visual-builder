---
title: Analyze integration performance
order: 4
layout: post-toc
redirect_from: /partners/integration-quality
---

# Analyze integration performance

Integration quality on Zapier boils down to two main pillars: **Health** and **Depth**.

1. **Health** - does the integration allow users to set up Zaps and keep them running reliably?
2. **Depth** - does the integration have all the functionality to allow users to automate what they want through their Zaps?

We’ll examine the main metrics around integration health and explore what they could be telling us about an integration’s quality level:

* **Errors** 
* **Zap activation rate**
* **Embed activation rate**
* **Bugs**
* **Active users retention**

Utilize the various tools and resources available in the developer platform, such as [bugs and feature requests](https://platform.zapier.com/manage/user-feedback), [monitoring](https://platform.zapier.com/build/testing#monitoring), and your integration’s dashboard to monitor and analyze these metrics and your integration’s health. Let’s dig in!

## How to view insights

1. Sign into [Zapier Developer Platform](https://developer.zapier.com/) through your Zapier account to see integrations you can access.
2. Select an integration to view its insights. You **must** be an admin or collaborator to view an integration’s dashboard.
    * If an integration isn’t listed, ask an admin to invite you or try [adding yourself as a collaborator](https://developer.zapier.com/join-integration).
3. Navigate to “Dashboard” in the lefthand sidebar to view growth, usage, and embed insights.

![Screenshot of Dashboard tab in Developer Platform](https://cdn.zappy.app/d7a53ee12f8fb94a44edbc0f8e3195ea.png)

## Errors

Errors can cause pain for users at two vital points:

1. During the Zap setup process, stopping them from enabling and activating their Zaps
2. During the Zap’s runtime, once it has been turned on, preventing the Zap from completing all actions successfully

### Are all errors “bad”?

We don’t want integrations throwing errors unnecessarily, but not all errors are necessarily bad. It’s perfectly acceptable for your integration to throw errors, as long as [they are meaningful](https://platform.zapier.com/publish/integration-review-guidelines#7-error-handling) in stating the problem and ideally the resolution, and [handled correctly](https://platform.zapier.com/reference/cli_docs#error-handling). For example, warnings due to user error or duplications are appropriate to throw and not an issue of the integration itself. So, it’s helpful to identify which errors are actual errors of the integration’s functionality.

### Key Zapier insights

Spikes in errors should be monitored as leading indicators of problems users are facing within your integration. The more descriptive and thorough [error handling](https://platform.zapier.com/reference/cli_docs#error-handling) your API and integration have in place, the easier it will be for users to resolve their own issues and for Zapier’s support team to assist with debugging.

### Best practices

If you don’t have control to make changes to the API itself, utilize custom error handling to improve your error messages:

* Elaborate on terse responses with user-friendly messaging.
    * Update “not_authenticated” to “Your API Key is invalid. Please reconnect your account.”
* Surface specific information to users regarding the field and why it’s producing an error. This empowers users to fix Zap issues independently.
    * Instead of “Provided data is invalid”, return “Contact name is invalid”.
    * Improve “Contact name is invalid” with “Contact name exceeds character limit.”
* Format the error to include a second, optional argument for a code machines can use to identify the type of error, and last, optional argument of a HTTP status code.
    * `throw new z.errors.Error('Contact name exceeds character limit.', 'InvalidData', 400);`


## Zap activation rates

### What is Zap activation rate?

Consider all of the Zaps users try to create with a trigger, action, or search from your integration. Then look at the percentage of those Zaps that actually activated within 24 hours of creation, meaning the Zap ran at least one successful task. _That’s the Zap activation rate._

### Does low activation mean something is broken?

Not necessarily. Maybe the user started to make a Zap, put the kettle on, forgot about what they were doing and didn’t bother ever coming back to finish what they started.

It can also highlight that certain triggers or actions are proving challenging to set up in a Zap or are erroring when run. Perhaps your trigger sample doesn’t return custom fields the user is looking to map in the Zap or the user gets confused by unclear input fields while setting up their action; these are two of many reasons why users abandon Zap setup. 

### Key Zapier insights

Zap activation rates at the individual trigger and action level are a great leading indicator of performance and usability. Don’t forget about the authentication step in your integration too! If users can't authenticate or get their Zaps enabled and activated, they stand little chance of ongoing success.

### Best practices

Give users the best chance to successfully activate their Zaps by making the integration as familiar and easy-to-use as possible:

* Follow our [Integration publishing guidelines](https://platform.zapier.com/publish/integration-publishing-guidelines) which provide detailed user experience best practices for building your integration.
* Create [Zap Templates](https://platform.zapier.com/publish/zap-templates) for popular use cases to simplify the setup process and decrease room for user error.
* Head to the Zap Editor to create and test Zaps using your own integration. This gives you firsthand experience on how users interact with the integration. 
* Keep your platform and Zapier integration parallel to maintain a consistent experience for mutual users.
    * Object and field names referenced in the integration should parallel names in the platform. For example, don’t name your trigger “New Lead” if they are referred to as “Contacts” in your platform. This makes it hard for users to find the functionality they want.
    * Provide all available input fields in the platform in the integration step, including custom fields. 
    * Match the field types in the platform to the integration. For example, if a field is a static dropdown in the platform, implement it as the same type within the integration.


## Embed activation rates

### What is embed activation rate?

How effective are the Zapier embeds in your product at converting user clicks on Zap Templates to Zap activations? Consider all the user clicks on Zap Templates surfaced in your embeds. Then look at the percentage of those Zaps that actually activated within 24 hours of creation, meaning the Zap ran at least one successful task. _That’s the embed activation rate._

In your integration's Dashboard, along with activation rate, see a funnel-view of users who signed up for Zapier, created Zaps, enabled Zaps, and activated Zaps from Zap Templates in your embeds.

![Screenshot of embed insights dashboard](https://cdn.zappy.app/896a5e4d56f2c86ba3909b669abf5d0c.png)

### Does low activation mean something is broken?

Not necessarily. Both your integration and embed(s) could be implemented correctly and in good health, but you could still be seeing low activation rates. Embed insights can help identify where in their journey users are hitting challenges with activating, whether it's the Zapier sign up, Zap setup or enablement stage.

### What we have learned

Embed insights and activation rates are strong indicators of user awareness and integration usability. If the click-to-sign-up ratio is really low, perhaps you haven't set sufficient context and expectations where the embed is placed for users to feel confident when they land on Zapier.com. If the create-to-enabled ratio is low, users could be having trouble with authenticating or field mapping once they're in the Editor creating a Zap from the template.

### Best Practices

* Don't see "Embed insights" in your Dashboard? That means we haven't found any embeds associated with the integration. Check out the "Embed" tab of your integration's Dashboard or our [Partner Solutions](https://zapier.com/l/partner/solutions) to see how you can start embedding.
* We offer a variety of [embed tools](https://platform.zapier.com/embed/overview) as different options work best for different Partners and their platforms. Implement a combination of our partner tools and compare metrics to see which implementations are most successful for your use case.
* Users are more likely to sign-up when they are aware of Zapier and the value we provide by integrating to your app. Give context of Zapier via a brief onboarding flow or link to help docs so users know what to expect.


## Bugs

As users encounter bugs or think of new features they’d like within the integration, some reach out to the Zapier support team. Those requests are logged in Zapier’s issue tracker, which you can see from the Bug & Feature Requests page of the integration’s developer platform. If you prefer syncing and managing issues from your own issue-tracking tools (such as Jira or Trello), you can create Zaps to do so using [Zapier Issue Manager](https://platform.zapier.com/publish/zapier-issue-manager).

Here are a couple things to note about bugs:

1. _When the number of open bugs goes above zero, it doesn’t really matter how many bugs you have._ The important datapoint is how many of your users are affected overall and what percentage of the app’s overall monthly active users that impacts.
2. _Your past history on closing bugs doesn’t influence your current health score._ Running track in college doesn’t mean a darn thing to your doctor thirty years later if you roll in with high cholesterol because of your penchant for McDonalds and KFC. Same with bugs and integration health.

Don’t forget the affected user counts on issues underrepresent the actual totals, as only a small portion of all users facing an issue take the time to contact support. If a significant number of users have made the effort to contact support to say they are affected by a bug in the integration, it should raise flags.

### Key Zapier insights

Open bugs are one of the best indicators of an integration’s health. If users are contacting Zapier’s support team to tell us about problems, we take that as a strong signal something is broken and needs to be fixed.

Regardless of the size of your integration’s user base, keeping the percent of monthly active users affected by open bugs under double figures (and ideally at 0) is recommended for a healthy integration.

### Best practices

* Instead of a “set-it-and-forget-it” mentality, allocate ongoing resources in your team's product roadmap for the maintenance of your Zapier integration to avoid surprise work or gaps in functionality.
* Need help with maintenance? [Match with a Zapier Expert](https://zapier.com/experts/matchmaking) to help you fix one-off bugs or maintain your integration.


## Active users retention

At Zapier, churn means a user used your integration in their Zaps 29 - 56 days ago, but hasn’t run a successful task in one of those Zaps in the past 28 days. This user is considered to have churned from the integration. From the opposite perspective, we can look at active users retention, or the percentage of users who haven’t churned.

### Did users leave Zapier altogether?

Not necessarily. Maybe they switched to using a competing integration or their workflow had a more periodic or seasonal cadence.

But, it could also mean they got so frustrated with the experience of trying to get their Zap working and _keep_ it working successfully, they turned it off, deleted it, and walked away.

### Key Zapier insights

Lowered active user retention rates don’t necessarily mean poor integration health. Some apps lend themselves to use-cases with shorter life-spans than others. That said, spikes in churn rate not related to seasonal variations in usage could be indicators of a problem with something not functioning as expected.

Active user retention is not a leading indicator. In fact, it’s quite a lagging one that may only start indicating a problem up to 28 days after it has been an issue. That doesn’t deem it useless, we just have to know how to make full use of it.

### Best practices

Approaching active user retention with a long-term strategy can help maintain a consistently high level of retention:
 
* [Embed](https://platform.zapier.com/embed/overview) the Zapier experience with copy-and-paste and customizable code within your platform to provide automation value directly to users. Embeds have proven to [reduce churn](https://platform.zapier.com/partner_success_stories/all) on Partners’ platforms. Find live embed examples under the ‘Embed’ tab of the integration’s developer platform.
* [Share use cases](https://platform.zapier.com/publish/partner-faq#tip-4-share-zapier-use-cases-in-your-onboarding) widely during your platform’s onboarding process. Having multiple Zaps using your integration increases stickiness of users not only to the Zapier integration, but also to your platform.
* Update the integration regularly with features as your platform evolves. [Invite stakeholders to your integration](https://platform.zapier.com/manage/invite-team-member) to give them admin or read-only access to insights, metrics, and feedback to prioritize and align improvements. 


## Integration insights definitions

The following includes definitions for each of the metrics provided in the integration dashboard:


| **Metric**                  | Definition                                                                              | Available Filters   |
|-----------------------------|-----------------------------------------------------------------------------------------|---------------------|
| **New users**               | Total number of new users using the integration over a selected period of time.<br><br> A new user = first time a user creates and activates a Zap with this integration. | Last 7 days<br>Last 30 days<br>Last 90 days |
| **Bugs & feature requests** | Total number of open bugs and feature requests for the integrations.                    |              |
| **Daily active users**      | Number of users who had a Zap activated in a day.<br><br> Activated = Zap is on and successfully ran at least one task. | Last 7 days<br>Last 30 days<br>Last 90 days |
| **Monthly active users**    | Total number of users who had a Zap activated in a given month.<br><br> Activated = Zap is on and successfully ran at least one task.                         | By year                  |
| **Active Zaps**             | Total number of active Zaps over a selected period of time.<br><br> Active Zaps = number of Zaps currently on and using the integration.                  | Last 7 days<br>Last 30 days<br>Last 90 days |
| **Daily active Zaps**       | Number of active Zaps in a day.<br><br> Active Zaps = number of Zaps currently on and using the integration. | Last 7 days<br>Last 30 days<br>Last 90 days|
| **Active users retention**  | The percentage of active users retained each month.<br><br> Retention = users who have at least one successful task executed in a given month.                  |                              |
| **Zap activation rate by trigger**       | For a given trigger, the percentage of Zaps using the trigger and the rate of the ones that activated within 24 hours of creation. The higher the rate, the better the trigger is performing.<br><br> Activated = Zap is on and successfully ran at least one task. | Last 7 days<br>Last 30 days<br>Last 90 days|
| **Zap activation rate by action**       | For a given action, the percentage of Zaps using the action and the rate of the ones that activated within 24 hours of creation. The higher the rate, the better the action is performing.<br><br> Activated = Zap is on and successfully ran at least one task. | Last 7 days<br>Last 30 days<br>Last 90 days|
| **Usage by trigger**        | Number of current live Zaps (Zaps turned on), paused Zaps (Zaps turned off), and total Zaps for each trigger.  | By integration version                       |
| **Usage by action**         | Number of current live Zaps (Zaps turned on), paused Zaps (Zaps turned off), and total Zaps for each action.   | By integration version                       |


## Practical applications of integration insights

* Launching a co-marketing campaign or running ads? Track daily and monthly MAU over the launch period to track changes in usage.
* Noticing certain triggers and actions with higher activations? Create additional Zap Templates to expand usage further since you know they are popular functionality.
* Noticing certain triggers and actions with lower activation? Hop into the Zap Editor and test them out yourself. Are there any technical or usability issues you experience? How do other top apps in your category implement similar functionality?


## Embed Insights Definitions

The following includes definitions for each of the embed metrics provided in the Dashboard. All metrics can be filtered by "All Embeds" or individual embeds, and the last 7, 30, and 90 days.

| **Metric**                             | Definition                                                                  |
|----------------------------------------|-----------------------------------------------------------------------------|
| **Total conversion**                   | Percentage of users who clicked on Zap Templates that activated Zaps.       |
| **Users who clicked on Zap Templates** | Percentage and count of users who clicked on Zap Template in an embed.      |
| **Users who signed up to Zapier**      | Percentage and count of users who signed up for a new account on Zapier.    |
| **Users who created Zaps**             | Percentage and count of users who started on Zaps in the editor.            |
| **Users who enabled Zaps**             | Percentage and count of users who created and successfully published Zaps.  |
| **Users who activated Zaps**           | Percentage and count of users who created Zaps that successfully ran tasks. |


## Practical Applications of Embed Insights

* Test different iterations of embeds and compare rates to see which ones resonate most with your users. Do certain sets of Zap Templates garner more clicks and activations than others? Does enabling "App search" on the Full Zapier Experience, so users can see all the apps they can integrate with, increase activations?
* Improve your Zap Templates with short, descriptive titles, and as much prefilled field mapping as possible, so users are immediately aware of the use case and can activate the Zap with the least amount of clicks.
* Provide context with your embed through help docs or an onboarding flow guiding users on how to connect your app with others using Zapier to improve the "Users who signed up for Zapier" rate.