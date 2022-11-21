---
title: Zap Templates
order: 11
layout: post-toc
redirect_from: /partners/
---

# Zap Templates

Zapier empowers apps to do together what they can’t on their own. With a bit of inspiration and creativity, your users can pull dozens of apps together into unique workflows to get more done with your app in far less time.

Zap Templates are ready made integrations or Zaps with the apps and core fields pre-selected, for publicly available Zapier integrations. In a few clicks, they help people discover a use case, connect apps, and turn on the Zap. Zap Templates are the fastest way for your users to automate workflows.

<script type="text/javascript" src="https://zapier.com/apps/embed/widget.js?guided_zaps=192,111,162,1495,883"></script>

They’re also a great way to promote your app, as your Zap Templates are featured in:

- Zapier’s App Directory
- Zapier’s onboarding experience
- In many of Zapier's {{ site.partner_count }} integration partners' apps and sites

Zap Templates can also be featured inside your site and content to help your users start using Zapier integrations. The more Zap Templates you create and the more users they have, the more likely they are to be featured. This helps your Zapier integration gain popularity and rise the ranks of the [Zapier Partner Program](https://zapier.com/platform/partner-program). To learn more about embedding Zap Templates (and other experiences) into your app or website, see our dedicated [Embed](https://platform.zapier.com/embed/overview) section.

You can create Zap Templates for any public Zapier integration. Once your integration is published, you will need to build at least 10 Zap Templates in the [Zap Template Creator](https://zapier.com/zap-templates/create) to join the [Partner Program](https://platform.zapier.com/partners/lifecycle-planning#4-launch-with-the-partner-program) and help people start using your integration.

> Expected time to create a Zap Template: 10 minutes.

![Example Zap Template](https://cdn.zappy.app/0d6ffaf492b547878ef8c06924a714f1.gif)
_An example Zap Template that automatically saves Gmail attachments to Google Drive—a handy way to speed up email file management._

## How to Build a Zap Template

Zap Templates take a few steps to build, similar to any other Zap. You first select the app and trigger you want to start the Zap, then add an action app and map the fields from the trigger app to the action—and optionally add additional steps. Then, add a title and description to help people quickly understand when to use your Zap.

### 1. Add a Trigger Step

![Zap Template select trigger app](https://cdn.zappy.app/64e407ae2b8e5f3ecaf9bedbbacd11d4.png)

Open Zapier’s [Zap Template creator](https://zapier.com/zap-templates/create) at [zapier.com/zap-templates/create](https://zapier.com/zap-templates/create), or click the _Create Zap Template_ button in your [Zap Template dashboard](https://zapier.com/zap-templates/). Select the trigger app, as you would when making a Zap for yourself. Search for the app by name from the dropdown menu.

> **Tip:** The ability to build and publish Zap Templates is only available if your Zapier integration has a [beta tag](https://platform.zapier.com/partners/lifecycle-planning/#beta) or has [officially launched](https://platform.zapier.com/partners/lifecycle-planning#4-launch-your-zapier-integration) and become a part of the Zapier Integration Partner Program.

![Zap Template select trigger](https://cdn.zappy.app/bcf87bac5267b210d520cb97ac0e5612.png)

Choose the app’s trigger from the dropdown that starts your Zap. 

![Zap Template authentication](https://cdn.zappy.app/a1cc719414192c01ed08b085d00bc5ba.png)

For most triggers from apps that require authentication, Zapier loads sample data similar to the data the app would send Zapier when it’s connected with a live account. Click the _Save + Continue_ button to use that in the next steps.

Some triggers require authentication, but don't include sample data. If so, Zapier will note that in a message. You can still use that Zap in a Zap template, though when setting up the Zap's action step(s), you won't be able to pre-map fields for your users.

![Zap Template built-in trigger](https://cdn.zappy.app/84fafa564da379d204b5a8535acfef57.png)

If your trigger includes options—or if you're using a triggers such as Zapier’s _RSS_ or _Schedule_ tool that don’t require authentication—Zapier will then show additional settings for this trigger. Fill in any form fields, select multi-choice options, and click _Continue_ to save them. Or leave the defaults to let users add info to the Zap themselves—in which case, click the _Test This Step_ link in the left sidebar to skip the options.

![Zap Template sample](https://cdn.zappy.app/d90a46d02a04c72341c2534c3c77e353.png)

In the final trigger option, Zapier shows sample data from the app. You can click the down arrow on the sample data to see what details are included and the input fields you can use from this app in the rest of your workflow. Then again click _Continue_ to complete your Zap's trigger.

### 2. Add an Action Step

![Zap Template add action app](https://cdn.zappy.app/ff77e3d0297f9a61bad2b6250472a059.png)

Now add the action step to your Zap. Select the action app from the search menu.

> **Tip:** You can use Zapier integrations that are publicly available or that have applied to be launched publicly.

![Zap Template select action step](https://cdn.zappy.app/667f2e42d0ad4b367f2b86fd1e00398b.png)

Choose the create or search action for your Zap. You may then be prompted to use sample data as before; click _Continue_ to accept.

> **Note**: If you use a search action, you need to also add a second action step to use the data from the trigger and search steps.

As in the trigger step, when setting up most actions, you'll see a screen where your users will authenticate the action app—only in the Zap Template creator, Zapier uses this to pull in sample fields for the app.

![Zap Template form fields](https://cdn.zappy.app/42933f0f6a425d029429dbe918b0a107.png)

Now for the most crucial part of your Zap Template: Map the input fields from the trigger app to the form fields in this action app. The action step’s template shows every field that Zapier can send to the app, with required and optional fields. For the best Zap Templates, you want to fill in as many form fields as possible to help users set up Zaps quickly.

> **Note**: Zap Templates' action fields _never_ show custom fields from apps, including spreadsheet columns, custom CRM fields, and other fields that are added by users, as Zapier's Template creator is not authenticated with an app account and custom fields will vary depending on the user. Your users will always need to add details to custom fields themselves.

For most form fields, you’ll need to add input fields from the trigger to the appropriate form field. Click into the form field and then `Show all options` button to see every input field from the trigger step. Select the input field that fits the action field best. For example, you might select Gmail’s _Attachment_ field to upload the attachment via Google Drive’s _File_ form field, or you might add Stripe’s _Email_ field to Mailchimp’s _Subscriber Email_ form field to add customers to an email list.

> **Tip**: Use [Zapier’s date and time syntax](https://help.zapier.com/hc/en-us/articles/8496275717261) to modify dates and times in action form fields.

Most dropdown menus are used to select folders, projects, and other user-generated data and should be left blank by default. You can, however, select options for dropdowns for boolean yes/no fields if you're certain which option is best for this Zap Template.

![Zap Template required fields](https://cdn.zappy.app/e4222e2c4934485dd27454ef50f17ec0.png)

Zap Template action forms include _required_ and _optional_ fields. When users set up your Zap Template, they will see the required fields by default, and _must_ fill them in before turning on the Zap. Try to map as many required input fields as possible. Then, less-critical fields will often be marked as optional, and are hidden by default when users set up the Zap Template. If you know the best data to map to those fields, add them to make sure your users' Zaps include as much detail as possible.

> **Note**: Do not enter plain text into an action form field unless _every_ user of this Zap Template would want the text included in the action.

![Finish Zap Template Action](https://cdn.zappy.app/6e87adbfde77b00ae144b487c4185c20.png)

Zapier then shows a test screen similar to what users see when setting up the Zap. Since you’re building a Zap Template, Zapier doesn’t create or add anything to your apps—the screen confirms everything should work correctly.

### 3. (Optional) Add Filters or Additional Action Steps

Now you have a choice: You can add another step to your Zap, or finish and save this Zap Template with only two steps.

Most Zap Templates only need two steps, with a Trigger to watch for data from an app and an Action to do something with that data. Sometimes, though, you need more steps for advanced workflows, including:

- **[Additional create actions](https://help.zapier.com/hc/en-us/articles/8496257774221-Set-up-your-Zap-action)** to add additional automations to your workflow
- **[Filters](https://help.zapier.com/hc/en-us/articles/8496276332557)** to watch for specific items from trigger or action step(s)
- **[Search actions](https://help.zapier.com/hc/en-us/articles/8496241402253)** to find specific data from apps, recommended especially to find customers, tickets, projects, and more before creating new items with Zaps

> **Note**: You cannot build Paths in Zap Templates at this time.

To add another search or create action to your Zap, click the _Add a Step_ button after setting up your action above, then repeat step 2 and set up the additional action. To add a _delay_ action, select the _Delay by Zapier_ app when adding a new action.

> **Note**: Code, custom webhook and custom Formatter steps are not allowed in Zap Templates. 

![Add Filter step to Zap Template](https://cdn.zappy.app/23309a53e37648bd8547e0a7ec0c993e.png)

To add a filter, click the `+` button and select _Filter_. You could add it between the trigger and action step to have the Zap only run when specific items come in from the trigger app, or you can add it after the action to watch for particular results (then add subsequent action steps to do more with data if it passes the filter criteria).

![Customize Zapier Filter](https://cdn.zappy.app/db5c3975470b1b2ba7be62b0ceb244ac.png)

Then add details to the filter, if this Zap should always watch for the same data. Select the field the filter should watch, then choose the filter criteria (if the text exists, doesn’t exist, if a number is greater than this value, etc.), and finally type in the text you need Zapier to find. If you need additional conditions in your filter, click the `+ AND` or `+ OR` buttons to add other criteria.

Alternately, leave the filter details blank and let users customize the filter to their needs.

> **Note**: Most Zap Templates don’t need filters, and most filters should be added by users later if required. However, including a filter in a Zap Template can be useful if your Zap Template is only useful with a filter to remove extraneous data.

<a id="shared-zaps-description"></a>

### 4. Add a Title and Description

![Zap Template Description](https://cdn.zappy.app/44e237ef141178a3311bb96a9d8a1633.png)

Now for the final step: add Zap Template’s title and description, then submit your Zap Template for review.

Zap Templates need to showcase a use case and describe it effectively. They provide inspiration for how to automate popular apps and workflows. Your Zap Template's description and title help sell that idea to users.

The title is the first thing people see. Embedded Zaps inside Zapier, your app, blog posts and other content show the Zap's title and app icons. Titles need to fit in well in each environment and sell the use case at a glance.

Descriptions, then, are what users see when they click the Zap Template. They explain the use case and tell how the Zap works. The title grabs interest; the description gets people to invest the minute or three it takes to turn on the Zap.

#### How to write a Zap Template title

![Example Zap Template Title](https://cdn.zapier.com/storage/photos/fc6854d9f356bca06d8879a50ef41036.png)

Zap Template titles clearly and briefly state the apps the Zap connects and the workflow it accomplishes. They include the trigger and action apps and the actions they perform. They use present tense, active voice, and sentence case.

Most Zap Template titles read something like this: `Add new Gmail emails to Google Sheets as rows`. The title mentions what happens in the trigger app followed by what Zapier does in the action app. Some examples of good titles:

- `Create Trello cards for new Wufoo form entries`
- `Get Slack notifications for new Google Drive files in a folder`
- `Subscribe new Gumroad customers to a MailChimp list`
- `Save new liked SoundCloud tracks to Google Drive`

> **Tip**: Use your discretion whether to mention the action or trigger app first. The trigger app works best first in most cases, but sometimes it sounds awkward—if so, go with the action app first.

Follow these rules in your Zap Template Titles:

- **Start with an appropriate verb**. Zap Templates start with an action verb that describes what the Zap does in the action app, such as `Create`, `Add`, `Make`, `Insert`, `Update`, `Subscribe`, or `Get`. Use unique verbs when possible, and use the most appropriate verb for the action Zapier performs with the app. For example:
  - Only use `Send` with messages, including emails and text messages
  - Only use `Post` with social network or chat apps
  - Only use `Log` or `Archive` with spreadsheet, database, or note-taking apps
- **Use sentence case**. Capitalize the first letter in the title and app names when appropriate.
  - **Right:** `Create Trello cards for new Wufoo form entries`
  - **Wrong:** `Create Trello Cards For New Wufoo Form Entries`
- **Use present tense and active voice**. Zaps automatically run for every new item in an app. The title should reflect that with active present tense.
  - **Right:** `Get Slack notifications for new Google Drive files`
  - **Wrong:** `Slack will notify you when a new Google Drive file is saved`
- **Always mention _new_ before trigger apps**. Zaps only run when new items are created in apps, and cannot take action for existing items. Emphasize that by including `new` in your title before the action app name.
- **Make app items plural**. Zaps run on every new item in your trigger app, and will always create the related item in your action app(s). Always make the trigger and action items plural to emphasize that, such as `Google Sheets rows` or `Mailchimp subscribers`.
- **Respect app name styles**. Make sure to use the same capitalization and spelling that the apps in your Zap use in their branding; double-check the app’s site or [Zapier’s integration list](https://zapier.com/apps).
- **Never use `sync` or `automatic` in titles**. All Zaps run automatically, only work on new data, and can’t sync data multiple ways. Avoid these terms in titles; sync is misleading, and automatic is redundant.
- **Don’t use personal pronouns**. Never use `you`, `we`, or `I` in Zap Template titles unless the trigger or action items specifically include those words.

#### How to write a Zap Template description

Zap Template descriptions share more detail about what the Zap does and scenarios in which to use it in two to four sentences. They tell readers what this Zap does for them and how it works.

Start your description with the user's problem or need. Then explain how Zapier meets that need, when the Zap will run, and what the Zap does when it runs. Explain the trigger and action items in plain language that show the workflow's value. Some good examples:

> Find yourself spending too much time adding event attendees to your CRM by hand? Now with the help of Zapier, the tedious work is done for you. This integration will add every new Eventbrite attendee to Zoho CRM as a new contact, saving you time for more important work.

> After someone fills out a form on your site, you'll want to hear about it or send them a follow-up email. This Zapier automation handles both gracefully, sending an email via Gmail to you or the form respondent whenever you get a new Typeform entry. You'll never have to send the same message over and over again.

> Expedient order processing makes for happy customers. Make sure you act on every new delivery with this Zapier automation. It will capture every new order placed on your Shopify store after being set up, creating a delivery task for it on Onfleet so your team can fulfill it without delay.

Keep these guidelines in mind:

- **Use present tense and active voice** as in the Zap title.
- **1 paragraph, 2-4 sentences** is enough for most Zap Template descriptions.
- **Don’t use Zapier-specific terminology** including Zap, Zap Template, trigger, action, or terms that Zapier doesn’t support, such as sync. Instead, use generic words, such as `integration` or `automation`, that are universally understood.
- **Use same terms as the integrations themselves**. If an app calls the results of a form an “entry” don’t call it a “submission,” or if an email app uses "tags," don’t refer to "folders."
- **Include tips at the end**. If your Zap Template requires extra setup for filters or other steps, or if it doesn't cover all use cases users may expect, include a sentence at the end to clarify. Start the tip with `Note:`, and format the entire note in italics with [Markdown](https://zapier.com/blog/beginner-ultimate-guide-markdown/) formatting. For example: `*Note: Add the tag you want to the Zap's [Filter](https://help.zapier.com/hc/en-us/articles/8496276332557) step.*`

> **Note**: Always write unique descriptions for each Zap Template—we will reject Zap Templates that use the same descriptions but only replace app names.

---

Once you've written and added your Zap Template title and description, it's time to save and test your work. Select `Draft` from the _Zap Template Visibility_ menu and click the _Save_ button.

![Test Zap Template](https://cdn.zappy.app/c06a94f004e20748235d5de67efa2960.png)

You should then try using the Zap Template to make sure it works as expected. Open your [Zap Template dashboard](https://zapier.com/zap-templates/), click the gear icon beside the Zap Template you built, and select _Copy Link_. Open that link in a new tab or window, and follow the steps to set up and turn on the Zap—and make sure everything looks and works correctly.

Optionally, you can let your team help test Zap Templates as well. When saving your Zap Template, choose `Shared` instead of draft, then share its link with others on your team so they can try the Zap Template.

<a id="submit-your-zap-templates"></a>

### 5. Submit Zap Template for Review

Finally, when your Zap Template is ready for public release, select the `For review` option on your Zap Template Visibility menu, and click _Save_ again. That submits the Zap Template to our team to review the Zap Template and ensure it works as expected and meets our standards.

> **Note**: Zapier will only approve Zap Templates that include either public integrations or integrations that have applied for public release.

We'll then contact you, typically within a couple of weeks, after reviewing your Zap Template(s). If your Zap Templates pass the tests, we will mark them as public to automatically have them show up on your app's App Directory page, inside select partners' apps and sites, and in Zapier's onboarding experience.

Then make some more Zap Templates. Every Zapier integration must have at least 10 Zap Templates, and the more you make, the easier it will be to start using your Zapier integration. Open the [Zap Template Creator](https://zapier.com/zap-templates/create) again and create any more Zap Templates you want.

## Promote Your Zap Templates

It’s not enough to turn your ideal workflows into Zap Templates. You need to get them in front of everyone who should use your Zaps. Zapier automatically promotes your Zap Templates in our App Directory and in partner apps with embedded Zaps if your Zap Templates include their apps. You can promote them further with a list of your Zap Templates on your site, or include built-in Zap Template embeds inside your app.

### Zapier App Directory

![Zapier App Directory Page](https://cdn.zappy.app/f56ac65d2c36314bae02f21b00f983e4.png)

The easiest way to find Zap Templates is in Zapier’s [App Directory](https://zapier.com/apps/) where we have individual pages for each of the {{ site.partner_count }} apps that integrate with Zapier. Want to find Gmail integrations? Go to [zapier.com/apps/gmail/integrations](https://zapier.com/apps/gmail/integrations/) to see the top apps connected with Gmail on Zapier, followed by a list of popular Gmail Zap Templates and Zapier content about Gmail use cases.

Find your app’s App Directory page at `zapier.com/apps/YourApp/integrations`, replacing `YourApp` with your app’s name.

![Zapier App Directory two-app page](https://cdn.zappy.app/3937aa425d4ac71d0da24efd3a312829.png)

Want to find ways to connect two specific apps? Click one of the top apps on any App Directory page to see our two-app pages, such as the one above for Trello and Gmail. It shows the most popular use cases for those two apps together.

Find your app’s two-app pages at `zapier.com/apps/YourApp/integrations/OtherApp`, substituting `YourApp` with your app’s name and `OtherApp` with the other app connected to your app.

Zapier also shows these top use cases to logged in users, promoting your app’s top Zap Templates to people who have connected Zapier to your app.

## Manage Your Zap Templates

![Zap Template List](https://cdn.zappy.app/83e8b8cece2a25070406f94b3097473d.png)

One Zap Template isn’t enough—you’ll want to make Zap Templates for each of your app’s most popular use cases. Over time, you’ll likely make dozens of Zap Templates. You can manage them—in draft, review, or publicly available—from your [Zap Templates](https://zapier.com/zap-templates/) dashboard alongside Zapier’s developer platform tools.

Filter through your Zap Templates by status on the left sidebar, click a Zap Template to edit it, or select the gear icon on the right of a Zap Template to copy its public link, test it, or delete it.

If you have any Zap Templates in your _Rejected_ list, edit them to fix the issues then re-submit them. You cannot edit public Zap Templates, but if you notice something that you need to change in your existing Zap Templates, please email [partners@zapier.com](mailto:partners@zapier.com) with the link to the Zap Template, and we can set the Zap as _Draft_ again so you can edit and re-submit it with any changes.

Then start again. Whenever you think of something that’s the _perfect_ use case for your Zapier integration, turn it into a Zap Template with the [Zap Template Creator](https://zapier.com/zap-templates/create). As soon as it’s approved, it’ll show up everywhere your Zapier integration is promoted, spreading your use case to the people who will benefit from it most.

### Promoting New Versions of your Integration

When promoting a new version of your integration, all Zap Templates using the integration and having no breaking changes with the existing version will be updated to use the promoted version. The following are considered breaking changes:

* A trigger/action is hidden or deleted.

* A trigger/action key is changed. 

* A trigger/action input field key is changed or removed.

* A trigger/action output field key is changed or removed.

If breaking changes exist between the previous and newly promoted integration versions, Zap Templates will not be automatically updated and will continue to use the previous version.

### Deprecating Versions of your Integration

When deprecating a version of your integration, any Zap Templates using the integration will automatically be marked as _Invalid_ within 24 hours of the deprecation.

While invalid, the Zap Template can still be edited to be fixed, but will not be _Public_ until then. This ensures users won’t use deprecated and broken Zap Templates to make Zaps.
