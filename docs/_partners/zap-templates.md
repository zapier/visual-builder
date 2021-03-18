---
title: Zap Templates - Include Zapier in Your App and Website
order: 4
layout: post-toc
redirect_from: /partners/
---

# Zap Templates: Include Zapier in Your App and Website

Zapier empowers apps to do together what they can’t on their own. With a bit of inspiration and creativity, your users can pull dozens of apps together into unique workflows to get more done with your app in far less time.

Zap Templates are readymade integrations or Zaps with the apps and core fields pre-selected, for publicly available Zapier integrations. In a few clicks, they help people discover a use case, connect apps, and turn on the Zap. Zap Templates are the fastest way for your users to automate workflows.

<script type="text/javascript" src="https://zapier.com/apps/embed/widget.js?guided_zaps=192,111,162,1495,883"></script>

They’re also a great way to promote your app, as your Zap Templates are featured in:

- Zapier’s App Directory
- Zapier’s onboarding experience
- In many of Zapier's 1,300+ integration partners' apps and sites

Zap Templates can also be featured inside your site and content to help your users start using Zapier integrations. The more Zap Templates you create and the more users they have, the more likely they are to be featured. This helps your Zapier integration gain popularity and rise the ranks of the [Zapier Partner Program](https://zapier.com/platform/partner-program).

You can create Zap Templates for any public Zapier integration, or for any integration that has applied for publishing. Once you apply for publishing your integration, you will need to build at least 10 Zap Templates in the [Zap Template Creator](https://zapier.com/developer/zap-templates/create) to help people start using your integration.

> Expected time to create a Zap Template: 10 minutes.

![Example Zap Template](https://cdn.zapier.com/storage/photos/c89bedd08435ca8e9dc42b348eca732c.gif)
_An example Zap Template that automatically saves Gmail attachments to Google Drive—a handy way to speed up email file management._

## How to Build a Zap Template

Zap Templates take a few steps to build, similar to any other Zap. You first select the app and trigger you want to start the Zap, then add an action app and map the fields from the trigger app to the action—and optionally add additional steps. Then, add a title and description to help people quickly understand when to use your Zap.

For help as you build, follow the instructions below:

### 1. Add a Trigger Step

![Zap Template select trigger app](https://cdn.zapier.com/storage/photos/800758ee8bf0437e6904dd7842760ac5.png)

Open Zapier’s [Zap Template creator](https://zapier.com/developer/zap-templates/create) at [zapier.com/developer/zap-templates/create](https://zapier.com/developer/zap-templates/create), or click the _Create Zap Template_ button in your [Zap Template dashboard](https://zapier.com/developer/zap-templates/). Select the trigger app, as you would when making a Zap for yourself. Select a popular app from the grid, or search for the app you need from the dropdown menu.

> **Tip:** The ability to build and publish Zap Templates is only available if your Zapier integration has a [beta tag](https://platform.zapier.com/partners/lifecycle-planning/#beta) or has [officially launched](https://platform.zapier.com/partners/lifecycle-planning#4-launch-your-zapier-integration) and become a part of the Zapier Integration Partner Program.

![Zap Template select trigger](https://cdn.zapier.com/storage/photos/ea3a3fb79b79782138180c0ce46e7ba5.png)

Choose the app’s trigger that starts your Zap. Select one of the default options, search for the trigger you want, or click _show less common options_ if you can’t find the trigger you need.

![Zap Template authentication](https://cdn.zapier.com/storage/photos/60167ed1a0c13415ebe471a591e7e62e.png)

For most triggers from apps that require authentication, Zapier loads sample data similar to the data the app would send Zapier when it’s connected with a live account. Click the _Save + Continue_ button to use that in the next steps.

![Zap Template not including sample data](https://cdn.zapier.com/storage/photos/73a293c63f75e05cf68744faec6c5c97.png)

Some triggers require authentication, but don't include sample data. If so, Zapier will note that in a message like the one above. You can still use that Zap in a Zap template, though when setting up the Zap's action step(s), you won't be able to pre-map fields for your users.

![Zap Template built-in trigger](https://cdn.zapier.com/storage/photos/5a8fab320d5e48196d24e57e8173ce00.png)

If your trigger includes options—or if you're using a triggers such as Zapier’s _RSS_ or _Schedule_ tool that don’t require authentication—Zapier will then show additional settings for this trigger. Fill in any form fields, select multi-choice options, and click _Continue_ to save them. Or leave the defaults to let users add info to the Zap themselves—in which case, click the _Test This Step_ link in the left sidebar to skip the options.

In the final trigger option, Zapier shows sample data from the app. You can click the down arrow on the sample data to see what details are included and the input fields you can use from this app in the rest of your workflow. Then again click _Continue_ to complete your Zap's trigger.

### 2. Add an Action Step

![Zap Template add action app](https://cdn.zapier.com/storage/photos/f23d74b8ceb233c51cf0b2c138473cdd.png)

Now add the action step to your Zap. Select the action app, either from the popular apps list or from the search menu.

> **Note:** All public integrations are avaliable here. **Code** steps and **Webhook** steps with prefilled destinations are not allowed.

![Zap Template select action step](https://cdn.zapier.com/storage/photos/8dc73de8622e7fdde9e1da7286b96fd3.png)

Choose the create or search action for your Zap, again using the search menu or _Show less common options_ tools if needed. You may then be prompted to use sample data as before; click _Continue_ to accept.

> **Note**: If you use a search action, you need to also add a second action step to use the data from the trigger and search steps.

As in the trigger step, when setting up most actions, you'll see a screen where your users will authenticate the action app—only in the Zap Template creator, Zapier uses this to pull in sample fields for the app.

![Zap Template form fields](https://cdn.zapier.com/storage/photos/0871b7f9a9665d358465d81856f2432e.png)

Now for the most crucial part of your Zap Template: Map the input fields from the trigger app to the form fields in this action app. The action step’s template shows every field that Zapier can send to the app, with required and optional fields. For the best Zap Templates, you want to fill in as many form fields as possible to help users set up Zaps quickly.

> **Note**: Zap Templates' action fields _never_ show custom fields from apps, including spreadsheet columns, custom CRM fields, and other fields that are added by users, as Zapier's Template creator is not authenticated with an app account and custom fields will vary depending on the user. Your users will always need to add details to custom fields themselves.

For most form fields, you need to add input fields from the trigger to the appropriate form field. Click the `+` button on the right of the field to see every input field from the trigger step. Select the input field that fits the action field best. For example, you might select Gmail’s _Attachment_ field to upload the attachment via Google Drive’s _File_ form field, or you might add Stripe’s _Email_ field to Mailchimp’s _Subscriber Email_ form field to add customers to an email list.

> **Tip**: Use [Zapier’s date and time syntax](https://zapier.com/help/modifying-dates-and-times/) to modify dates and times in action form fields. Adding {{zap_meta_human_now}} to a field will produce the time when the Zap runs.

Most dropdown menus are used to select folders, projects, and other user-generated data and should be left blank by default. You can, however, select options for dropdowns for boolean yes/no fields if you're certain which option is best for this Zap Template.

![Zap Template required fields](https://cdn.zapier.com/storage/photos/da280e25dbcb49ec47133874c0265e73.png)

Zap Template action forms include _required for user_ and _optional for user_ fields. When users set up your Zap Template, they will see the required fields by default, and _must_ fill them in before turning on the Zap. Try to map as many required input fields as possible. Then, less-critical fields will often be marked as optional, and are hidden by default when users set up the Zap Template. If you know the best data to map to those fields, add them to make sure your users' Zaps include as much detail as possible.

> **Note**: Do not enter plain text into an action form field unless _every_ user of this Zap Template would want the text included in the action.

![Finish Zap Template Action](https://cdn.zapier.com/storage/photos/0bf7bddc4ac8cd16d90a4929f2baaaa3.png)

Zapier then shows a test screen similar to what users see when setting up the Zap. Since you’re building a Zap Template, Zapier doesn’t create or add anything to your apps—the screen confirms everything should work correctly.

### 3. (Optional) Add Filters or Additional Action Steps

Now you have a choice: You can add another step to your Zap, or finish and save this Zap Template with only two steps.

Most Zap Templates only need two steps, with a Trigger to watch for data from an app and an Action to do something with that data. Sometimes, though, you need more steps for advanced workflows, including:

- **Additional create actions** to add additional automations to your workflow
- **[Filters](https://zapier.com/help/filter/)** to watch for specific items from trigger or action step(s)
- **[Search actions](https://zapier.com/learn/getting-started-guide/search-actions/)** to find specific data from apps, recommended especially to find customers, tickets, projects, and more before creating new items with Zaps

> **Note**: You cannot build Paths in Zap Templates at this time.

To add another search or create action to your Zap, click the _Add a Step_ button after setting up your action above, then repeat step 2 and set up the additional action. To add a _delay_ action, select the _Delay by Zapier_ app when adding a new action.

![Add Filter step to Zap Template](https://cdn.zapier.com/storage/photos/5a4b65b9cff4bd8bf951a171299794c6.png)

To add a filter, click the `+` button in the left sidebar and select _Filter_. You could add it between the trigger and action step to have the Zap only run when specific items come in from the trigger app, or you can add it after the action to watch for particular results (then add subsequent action steps to do more with data if it passes the filter criteria).

![Customize Zapier Filter](https://cdn.zapier.com/storage/photos/e8e45015feffaae49d57a01a8e1162d6.png)

Then add details to the filter, if this Zap should always watch for the same data. Select the field the filter should watch, then choose the filter criteria (if the text exists, doesn’t exist, if a number is greater than this value, etc.), and finally type in the text you need Zapier to find. If you need additional conditions in your filter, click the `+ AND` or `+ OR` buttons to add other criteria.

Alternately, leave the filter details blank and let users customize the filter to their needs.

> **Note**: Most Zap Templates don’t need filters, and most filters should be added by users later if required. However, including a filter in a Zap Template can be useful if your Zap Template is only useful with a filter to remove extraneous data.

<a id="shared-zaps-description"></a>

### 4. Add a Title and Description

![Zap Template Description](https://cdn.zapier.com/storage/photos/771335061cfa2e631707662981f7e7cb.png)

Now for the final step: add Zap Template’s title and description, then submit your Zap Template for review.

Zap Templates need to showcase a use case and describe it effectively. They provide inspiration for how to automate popular apps and workflows. Your Zap Template's description and title help sell that idea to users.

The title is the first thing people see. Embedded Zaps inside Zapier, your app, and blog posts and other content show the Zap's title and app icons. Titles need to fit in well in each environment and sell the use case at a glance.

Descriptions, then, are what users see when they click the Zap Template. They explain the use case and tell how the Zap works. The title grabs interest; the description gets people to invest the minute or three it takes to turn on the Zap.

#### How to write a Zap Template title

![Example Zap Template Title](https://cdn.zapier.com/storage/photos/fc6854d9f356bca06d8879a50ef41036.png)

Zap Template titles clearly and briefly state the apps the Zap connects and the workflow it accomplishes. They include the trigger and action apps and the actions they perform. They use present tense, active voice, and sentence case.

Most Zap Template titles read something like this: `Add new Gmail emails to Google Sheets as rows`. The title mentions what happens in the trigger app followed by what Zapier does in the action app. Some examples of good titles:

- `Create Trello cards for new Wufoo form entries`
- `Get Slack notifications for new Google Drive files in a folder`
- `Subscribe new Gumroad customers to a MailChimp list`
- `Save new SoundCloud tracks I like to Google Drive`

> **Tip**: Use your discretion whether to mention the action or trigger app first. The trigger app works best first in most cases, but sometimes it sounds awkward—if so, go with the trigger app first.

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
- **Respect app name styles**. Make sure to use the same capitalization and spelling that the apps in your Zap use in their branding; double-check the app’s site or [Zapier’s integration list](https://zapier.com/help/service-documentation/).
- **Never use `sync` or `automatic` in titles**. All Zaps run automatically, only work on new data, and can’t sync data multiple ways. Avoid these terms in titles; sync is misleading, and automatic is redundant.
- **Don’t use personal pronouns**. Never use `you`, `we`, or `I` in Zap Template titles unless the trigger or action items specifically include those words.

#### How to write a Zap Template description

Zap Template descriptions share more detail about what the Zap does and scenarios in which to use it in two to four sentences. They tell readers what this Zap does for them and how it works.

The best descriptions follow a relatively simple pattern:

1. Present a problem statement or job to be done where the integration can help
2. Explain how it works
3. End with the impact on the user's workflow.

Please keep your descriptions unique and varied across the sets of Zaps you create. Please keep to concise, explanatory language that isn't sales or marketing-oriented or unclear. Some good examples below:

> Find yourself spending too much time adding event attendees to your CRM by hand? Now with the help of Zapier, the tedious work is done for you. This integration will add every new Eventbrite attendee to Zoho CRM as a new contact, saving you time for more important work.

> After someone fills out a form on your site, you'll want to hear about it or send them a follow-up email. This Zapier automation handles both gracefully, sending an email via Gmail to you or the form respondent whenever you get a new Typeform entry. You'll never have to send the same message over and over again.

> Expedient order processing makes for happy customers. Make sure you act on every new delivery with this Zapier automation. It will capture every new order placed on your Shopify store after being set up, creating a delivery task for it on Onfleet so your team can fulfill it without delay.

Keep these guidelines in mind:

- **Use present tense and active voice** as in the Zap title.
- **1 paragraph, 2-4 sentences** is enough for most Zap Template descriptions.
- **Don’t use Zapier-specific terminology** including Zap, Zap Template, trigger, action, or terms that Zapier doesn’t support, such as sync. Instead, use generic words, such as `integration` or `automation`, that are universally understood.
- **Use same terms as the integrations themselves**. If an app calls the results of a form an “entry” don’t call it a “submission,” or if an email app uses "tags," don’t refer to "folders."
- **Include tips at the end**. If your Zap Template requires extra setup for filters or other steps, or if it doesn't cover all use cases users may expect, include a sentence at the end to clarify. Start the tip with `Note:`, and format the entire note in italics with [Markdown](https://zapier.com/blog/beginner-ultimate-guide-markdown/) formatting. For example: `*Note: Add the tag you want to the Zap's [Filter](https://zapier.com/learn/getting-started-guide/filters/) step.*`

> **Note**: Always write unique descriptions for each Zap Template—we will reject Zap Templates that use the same descriptions but only replace app names.

---

Once you've written and added your Zap Template title and description, it's time to save and test your work. Select `Draft` from the _Zap Template Visibility_ menu and click the _Save_ button.

![Test Zap Template](https://cdn.zapier.com/storage/photos/87a8cdc2f4d28b3ca8f743d0b332e84c.png)

You should then try using the Zap Template to make sure it works as expected. Open your [Zap Template dashboard](https://zapier.com/developer/zap-templates/), click the gear icon beside the Zap Template you built, and select _Copy Link_. Open that link in a new tab or window, and follow the steps to set up and turn on the Zap—and make sure everything looks and works correctly.

Optionally, you can let your team help test Zap Templates as well. When saving your Zap Template, choose `Shared` instead of draft, then share its link with others on your team so they can try the Zap Template.

<a id="submit-your-zap-templates"></a>

### 5. Submit Zap Template for Review

Finally, when your Zap Template is ready for public release, select the `For review` option on your Zap Template Visibility menu, and click _Save_ again. That submits the Zap Template to our team to review the Zap Template and ensure it works as expected and meets our standards.

> **Note**: Zapier will only approve Zap Templates that include public integrations.

Please allow for up to 14 days for Zap Template reviews. These are processed on a first in, first out basis, and you will rceive automatic emails the day after any of your Zap templates are Published or Rejected. 

If they were Rejected, please see the email you received for rejection reasons - after making the noted edits, please re-submit.

Every Zapier integration must have at least 10 Zap Templates, and the more you make, the easier it will be to start using your Zapier integration. Open the [Zap Template Creator](https://zapier.com/developer/zap-templates/create) again and create any more Zap Templates you want.

Once Zap Templates are published, they will show up on your app's App Directory page, surface anywhere Zap Templates are embedded (like our blog and even inside other Partners' Zapier experience), and in Zapier's product flow.

## Promote Your Zap Templates

It’s not enough to turn your ideal workflows into Zap Templates. You need to get them in front of everyone who should use your Zaps. Zapier automatically promotes your Zap Templates in our App Directory and in partner apps with embedded Zaps if your Zap Templates include their apps. You can promote them further with a list of your Zap Templates on your site, or include built-in Zap Template embeds inside your app.

### Zapier App Directory

![Zapier App Directory Page](https://cdn.zapier.com/storage/photos/b625939587cb8a8c7242f375c714d6aa.png)

The easiest way to find Zap Templates is in Zapier’s [App Directory](https://zapier.com/apps/) where we have individual pages for each of the 3000+ apps that integrate with Zapier. Want to find Gmail integrations? Go to [zapier.com/apps/gmail/integrations](https://zapier.com/apps/gmail/integrations/) to see the top apps connected with Gmail on Zapier, followed by a list of popular Gmail Zap Templates and Zapier content about Gmail use cases.

![Zapier App Directory two-app page](https://cdn.zapier.com/storage/photos/ca6556adda39eeb6f8477a873122d444.png)

Want to find ways to connect two specific apps? Click one of the top apps on any App Directory page to see our two-app pages, such as the one above for Trello and Gmail. It shows the most popular use cases for those two apps together.

Zapier also shows these top use cases to logged in users, promoting your app’s top Zap Templates to people who have connected Zapier to your app.

### Embed Zap Templates in Blog and Content Pages

![Embed Zap Templates](https://cdn.zapier.com/storage/photos/91cd0e758e136539b9c6c6fdc9cd5de7.png)

You can also promote Zap Templates on your site with Zap embeds. The easiest way to make them is with our [Zap Custom Embed Creator](https://zapier.com/partner/embed/). Enter your app’s name, select how many Zaps you want to embed and the color scheme that fits your app or site best, then copy the embed code at the bottom. Zapier will automatically show your app’s most popular Zap Templates in your embed, and whenever someone clicks the _Use this Zap_ button, Zapier will open the Zap Template in a small popover window to keep users on your site while they set up the Zap.

> **Tip**: Learn more about Zap Templates’ benefits in our [Zap Template presentation](https://docs.google.com/presentation/d/e/2PACX-1vQNBCEb0UsK75jnbsn9-1Ki5AnHJyxM8VfAiMHzOnXon2_HzEINt3D5l7a-_HoMDsIzBRjvN2FcWqXJ/pub?start=false&loop=false&delayms=15000).

Want to embed specific individual Zap Templates instead? Copy the Zap ID number from your [Zap Templates Dashboard](https://zapier.com/developer/zap-templates/) by clicking the gear icon beside a Zap and selecting the _Copy ID_ option. Then, include it in place of `1234` in the text below:

`<script type="text/javascript" src="https://zapier.com/apps/embed/widget.js?guided_zaps=1234"></script>`

Want to embed multiple Zap Templates? Include each of their IDs in a comma separated list, such as:

`<script type="text/javascript" src="https://zapier.com/apps/embed/widget.js?guided_zaps=1234,9876,3456"></script>`

<a id="embed-widget-options"></a>
You can additionally use these options to customize your Zap Template embeds:

- `limit=10` to set the number of Zaps to display; use any number you want
- `theme=dark` for a dark-colored embed, instead of the default light background
- `categories=CATEGORYNAME` to show only Zap Templates with apps from a specific category, with `CATEGORYNAME` replaced with the name of a category from [Zapier’s App Directory](https://zapier.com/apps/)
- `categories=-CATEGORYNAME` to _not_ show Zap Templates with apps from a specific category
- `services=-APP,-APP` to exclude specific apps
- `borderColor=%23333` to set the color of the borders to any css value or “none”. Use "%23" in place of "#" for HEX values
- `backgroundColor=green` to set the background of each row to any css value including “transparent”
- `buttonColor=%23000000` to set the background color of the primary button to any css value
- `inheritFont=true` to disable the widget font styling allowing it to inherit from the parent container
- `buttonType=outline` to set the button type. Type `outline` (currently the only option) sets the `buttonColor` as a border around the button with a transparent background
- `title=TITLE` to set a styled header to the widget
- `textColor=red` to set the text color of the widget (template titles)
- `button=BUTTONTEXT` to set the primary button text (default: Use This Zap)
- `width=600` to set a fixed width to the widget. By default, the widget markup is fully responsive with a max width of 100% of its parent’s width.

Include the additional options at the end of the script text with an ampersand, such as:

`<script src="https://zapier.com/apps/embed/widget.js?services=APP&borderColor=green&limit=10&theme=dark"></script>`

### Embed Zap Templates in Your App

![Unbounce Embedded Zaps](https://cdn.zapier.com/storage/photos/ab298d02d423fb9a122b0a75ca7f7512.png)

Want to build Zap Templates into your app? [Zapier’s Partner API](https://zapier.com/developer/documentation/v2/partner-api/) lets you do just that. It can embed a full App Directory into your app to showcase every app that works with your app’s Zapier integration, along with Zap Templates and any active Zaps your users have enabled.

Zapier's embeds maintain Zapier’s design for the most part. With the Partner API, however, you can customize the entire look and feel of Zapier in your app. It’s the perfect way to make your Zapier integrations be first-class features in your app.

Here are some example embedded Zapier experiences with our Partner API, and you can check our [Partner API documentation](https://zapier.com/engineering/partner-api/) for more details:

- **Unbounce** provides a [native-feeling integration experience](https://zapier.com/apps/updates/1228/unbounce-in-app-zapier-integration) where users can set up Zaps, view their active Zaps, and even edit Zaps inside Unbounce (seen above).

![Facebook Embedded Zap Experience](https://cdn.zapier.com/storage/photos/73d073d363d0eae104ccdb159eaba8cd.gif)

- **Facebook** lets you search for and configure Zaps inside their Lead Ad Campaign Manager.

![MeisterTask Embedded Zap](https://cdn.zapier.com/storage/photos/570103e337edbe2b20b62ffba9f5dd7c.gif)

- **MeisterTask** provides an intuitive, styled interface to search for any MeisterTask Zap Template.
- **Trello** leverages the Partner API to let users manage Zaps from their [Trello Dashboard](http://blog.trello.com/zapier-power-up-for-trello).
- **Zoho Connect** lets users set up Zaps [inside the Zoho Connect app](https://cdn.zapier.com/storage/photos/e02db0c000ed037b3385b813b3f1303c.gif).
- **Eventbrite** shows users their most popular Zap templates to make it easy to [export attendees](https://cdn.zapier.com/storage/photos/384ec44fe4856a00a009ee5e53e022f8.png).
- **Typeform** presents popular Zap templates when users set up their forms, something they’ve found to [reduce churn](https://zapier.com/engineering/do-customers-that-integrate-with-zapier-have-lower-churn/).
- **Help Scout** uses Zapier to [extend their integrations directory](https://cdn.zapier.com/storage/photos/bcec803a9b13f20e1a6453f17dee1314.gif) automatically, with Zapier as a fallback if no direct integrations are available.
- **Trainerize** curates the best Zap Templates by [use case](https://cdn.zapier.com/storage/photos/be8d19b9eb8a36ad8231a4f53ef22411.png).

## Manage Your Zap Templates

![Zap Template List](https://cdn.zapier.com/storage/photos/fd0cf812b5abc1f8ca5f0cec8029b428.png)

One Zap Template isn’t enough—you’ll want to make Zap Templates for each of your app’s most popular use cases. Over time, you’ll likely make dozens of Zap Templates. You can manage them—in draft, review, or publicly available—from your [Zap Templates](https://zapier.com/developer/zap-templates/) dashboard alongside Zapier’s developer platform tools.

Filter through your Zap Templates by status on the left sidebar, click a Zap Template to edit it, or select the gear icon on the right of a Zap Template to copy its public link, test it, or delete it.

If you have any Zap Templates in your _Rejected_ list, edit them to fix the issues then re-submit them. You cannot edit public Zap Templates, but if you notice something that you need to change in your existing Zap Templates, please email [partners@zapier.com](mailto:partners@zapier.com) with the link to the Zap Template, and we can set the Zap as _Draft_ again so you can edit and re-submit it with any changes.

Then start again. Whenever you think of something that’s the _perfect_ use case for your Zapier integration, turn it into a Zap Template with the [Zap Template Creator](https://zapier.com/developer/zap-templates/create). As soon as it’s approved, it’ll show up everywhere your Zapier integration is promoted, spreading your use case to the people who will benefit from it most.

## Troubleshoot Zap Template Embeds

### Problems with document.write on load?

Add this parameter with any ID you want: `html_id=`. Then you'll want to have the embeds inside a div with the same ID—this will cause the embeds to load with the div, and not with document.write as they do otherwise. Example:

    <div id=foo>
    <script src="https://zapier.com/apps/embed/widget.js?services=mailchimp&html_id=foo"></script>
    </div>

### Need to load templates asynchronously / non-blocking?

You can load templates asynchronously (without blocking the rest of your page's content) by adding the `async` attribute and `html_id` parameter to the script tag.

> **Note**: For this to work, you must also use the `html_id=` parameter to tell the widget loader where in the DOM you want the templates to appear.

    <div id="foo"></div>
    <script async src="https://zapier.com/apps/embed/widget.js?services=mailchimp&html_id=foo"></script>
    <!-- ...other html that will be loaded before the templates... -->

### Support for React

You can use the widget within React with a class component that dynamically creates a script tag `onComponentDidMount` and sets the script src to the widget.js URL containing the necessary params. Additionally, the URL should contain a `html_id` param set to the id of an empty child element (div) rendered by the component. The script tag should then be inserted into the DOM by either:

- Getting the container element by ID and appending the script
- Using a ref={} in the component for a parent element that will contain the script
- Appending the script to the document body

### Support for Angular

To use the widget within an Angular project, dynamically create and append the embed widget script in a Component's lifecycle hook:

1. Be sure to save a reference to the component's `elementRef.nativeElement` in the constructor.
2. Add a container element with a specific ID in your template used in the next step.
3. In the Component's `ngAfterViewInit()` lifecycle hook, create the script tag dynamically, making sure to **add the `html_id` param set to the DOM ID of the element created in your template.** Then, append the script to the saved reference of the Component's `nativeElement`.

With an empty `<div id="zapierhere"></div>` in your Component's template, your Component code might look like this:

    export class EmbedComponent {
      constructor(el: ElementRef) {
        this.el = el.nativeElement
      }

      ngAfterViewInit() {
        this.zapierScript = document.createElement('script')
        this.zapierScript.type = 'text/javascript'
        this.zapierScript.src =
          'https://zapier.com/apps/embed/widget.js?services=zapier&html_id=zapierhere'
        this.el.appendChild(this.zapierScript)
      }
    }

<small>[See a working example of this code here.](https://codesandbox.io/s/0p54mmr89n)</small>

## Embed Zapier Into Your App With Zapier Partner API

The Zapier Partner API is for partners that wish to have more flexibility and control over a user's experience with Zapier within their product. With the Partner API, you can:

- **Have complete style control** over how you present Zap templates in your product. The Partner API gives you access to the raw Zap Template data so you can give your users access to your Zap template with your product's style, look and feel.
- **Get access to all your Zap templates** and give your users the ability to search to quickly find the one they need.
- **Streamline Zap setup** by pre-filling fields on behalf of your users.
- **Show users the Zaps they have** set up from right within your product keeping them on your site longer and giving them complete confidence in their Zapier integration.

This API is currently for approved partners only. If you'd like to use this API, [request access using this form]({{ site.partner_api_invite_url }}).

Want to better understand what you can achieve with the Partner API? See how other partners have used the API to create a [native Zapier integration for their users](https://zapier.com/developer/documentation/v2/zapier-api/#see-it-in-action-how-unbounce-uses-the-api).

### Authentication

There are two ways to authenticate with the Partner API.

1. Your application's `client_id` which you will receive once you are approved for access to the API
2. A user's access token

Which authentication method you should use depends on which endpoint(s) you are using. Review each endpoint's documentation to understand which parameters are required.

> Note: while we do generate a `client_secret`, the type of grant we use (`implicit`) doesn't need it so it's not something we provide.

#### Access Token

For resources that require a valid access token you can use the [OAuth2 protocol](https://www.digitalocean.com/community/tutorials/an-introduction-to-oauth-2). At the moment, we only permit the [`implicit`](https://tools.ietf.org/html/rfc6749#section-4.2) grant type. Should your use case require a different grant type [send us your request](mailto:partners@zapier.com).

#### Procuring a Token

Construct the following URL, and redirect the user to authorize your application:

> `{% raw %}https://zapier.com/oauth/authorize?client_id={client_id}&redirect_uri={redirect_uri}&scope={scope}{% endraw %}`

```
{% raw %}
  .content th {
    font-weight: bold;
  }
  .content td, .content th {
    padding: 10px;
    border: 1px solid #DADFE2;
    border-right: 0;
    border-bottom: 0;
  }
  .content td:last-child, .content th:last-child {
    border-right: 1px solid #DADFE2;
  }
  .content tr:last-child td {
    border-bottom: 1px solid #DADFE2;
  }
  .content th {
    text-align: center;
    font-weight: 500;
  }
  .content td:nth-child(1), .content td:nth-child(2), .content th:nth-child(1), .content th:nth-child(2) {
    text-align: center;
  }
  .content td:nth-child(1) {
    font-weight: bold;
  }
  .content td:nth-child(1), .content td:nth-child(2) {
    font-family: 'Consolas','Liberation Mono',Courier,monospace;
  }

  .content th:nth-child(1) {
    width: 150px;
  }
{% endraw %}
```

|      Parameter      | Requirement | Explanation                                                                                                                                                                                                         |
| :-----------------: | :---------: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
|    **client_id**    |  Required   | Your application ID.                                                                                                                                                                                                |
|  **redirect_uri**   |  Required   | The URI you provided in the sign-up form. If you need to modify this, you'll need to [send us a request](mailto:partners@zapier.com).                                                                               |
|  **response_type**  |  Required   | Use `token`.                                                                                                                                                                                                        |
|      **scope**      |  Optional   | Space (`%20`) separated variable. See each resource for their required scope, if any.                                                                                                                               |
| **approval_prompt** |  Optional   | One of `auto` or `force`. Use `auto` if the second authorization (before expiration of previous token) should not prompt the user to re-authorize. Use `force` if the user should authorize your application again. |
|      **state**      |  Optional   | A unique string to help your application guard against XSRF.                                                                                                                                                        |

##### Example Prompt

![Example OAuth2 Authorization Prompt](https://cdn.zapier.com/storage/photos/d926ea5ba6ca80c184a45cf3f5e420fb.png)

#### Receiving the Token, or Error

If the user cancels, or approves the authorization the user will be redirected to your `redirect_uri` with the following example urls:

**Approved**

> `http://your.redirect.url/#access_token=iuqhw8egojqenduvybtoken_type=Bearer&expires_in=36000&scope=zap`

**Cancelled**

> `http://your.redirect.url/?error=access_denied`

Your application should use JavaScript to parse the hash parameter and use the token as needed. The **access token will not expire**. If ever invalid, however, provide the user with the authorize flow once more. In the `implicit` grant type, there are no refresh tokens. You can use a hidden iframe with `approval_prompt=auto`, or ask the user to authorize once more, to receive new tokens.

#### Using the token:

Preferred use of the tokens is via an HTTP Authorization Header.

> `{% raw %}curl -H "Authorization: Bearer {token}" "https://api.zapier.com/v1/zaps"{% endraw %}`

### Errors

Zapier uses HTTP response codes to indicate the success or failure of an API request.

| Code    | Status         | Explanation                                                     |
| ------- | -------------- | --------------------------------------------------------------- |
| **200** | OK             | Successful request.                                             |
| **403** | Authentication | Not authorized.                                                 |
| **404** | Not Found      | The resource requested was not found.                           |
| **5xx** | Server Error   | A fatal error occurred while processing the request. Try again. |

All errors will be JSON object with a String array of errors:

```{% raw %}
{
  "errors": ["Malformed request"]
}
{% endraw %}
```

### Resources

#### Zaps

|            URL             | Protected By | Required Scopes |
| :------------------------: | :----------: | :-------------: |
| **api.zapier.com/v1/zaps** | Access Token |      `zap`      |

#### Notes

1. The zaps returned are narrowed/filtered by your Zapier app. For example, if you are Trello you'll only be returned a user's Zap that contain Trello in one of the steps of the Zap.

2. If your app is built with the [Zapier CLI](https://github.com/zapier/zapier-platform-cli) the Zaps returned are for **any** version of your app.

#### Arguments

Available parameters to the Zaps resource:

| parameter                                    | requirement | notes                                                                                                                                      |
| -------------------------------------------- | ----------- | ------------------------------------------------------------------------------------------------------------------------------------------ |
| `{% raw %}params__{KEY}={VALUE}`{% endraw %} | Optional    | Return Zaps that have a specific key/value set in the params (settings) of the Zap. **Note the `app` parameter must be included as well.** |

#### EXAMPLE REQUEST

> `{% raw %}curl -H "Authorization: Bearer {token}" "https://api.zapier.com/v1/zaps"{% endraw %}`

#### Example Requests

Get all Zaps in the user's account (note this will only include the OAuth app that is associated with the Zapier app).

```
{% raw %}
curl -H "Authorization: Bearer {token}" -L "https://api.zapier.com/v1/zaps"
{% endraw %}
```

Get all Zaps in the user's account that have a particular Trello board (assuming the OAuth app is Trello).

```
{% raw %}
curl -H "Authorization: Bearer {token}" -L "https://api.zapier.com/v1/zaps?&params__board=BOARD_ID"
{% endraw %}
```

#### EXAMPLE RESPONSE

```{% raw %}
{
  "objects": [
    {
      "id": 125,
      "modified_at": "2017-03-22T09:38:11-05:00",
      "state": "on",
      "steps": [
        {
          "app": {
            "description": "Typeform helps you ask awesomely online! If you ever need to run a survey, questionnaire, form, contest etc... Typeform will help you achieve it beautifully across all devices, every time, using its next generation platform.",
            "hex_color": "8bcbca",
            "id": 4259,
            "image": "https://cdn.zapier.com/storage/developer/5e21b4c1e0a2a3346a801dbc0a2a5a6d_2.png",
            "images": {
              "url_128x128": "https://cdn.zapier.com/storage/developer/5e21b4c1e0a2a3346a801dbc0a2a5a6d_2.128x128.png",
              "url_16x16": "https://cdn.zapier.com/storage/developer/5e21b4c1e0a2a3346a801dbc0a2a5a6d_2.16x16.png",
              "url_32x32": "https://cdn.zapier.com/storage/developer/5e21b4c1e0a2a3346a801dbc0a2a5a6d_2.32x32.png",
              "url_64x64": "https://cdn.zapier.com/storage/developer/5e21b4c1e0a2a3346a801dbc0a2a5a6d_2.64x64.png"
            },
            "api": "TypeformDevAPI",
            "slug": "typeform",
            "title": "Typeform",
            "url": "https://zapier.com/apps/typeform/integrations"
          },
          "type_of": "read"
        },
        {
          "app": {
            "description": "Trello is team collaboration tool that lets you organize anything and everything to keep your projects on task.",
            "hex_color": "0079bf",
            "id": 4192,
            "image": "https://cdn.zapier.com/storage/services/da3ff465abd3a3e1b687c52ff803af74.png",
            "images": {
              "url_128x128": "https://cdn.zapier.com/storage/services/da3ff465abd3a3e1b687c52ff803af74.128x128.png",
              "url_16x16": "https://cdn.zapier.com/storage/services/da3ff465abd3a3e1b687c52ff803af74.16x16.png",
              "url_32x32": "https://cdn.zapier.com/storage/services/da3ff465abd3a3e1b687c52ff803af74.32x32.png",
              "url_64x64": "https://cdn.zapier.com/storage/services/da3ff465abd3a3e1b687c52ff803af74.64x64.png"
            },
            "api": "TrelloAPI",
            "slug": "trello",
            "title": "Trello",
            "url": "https://zapier.com/apps/trello/integrations"
          },
          "type_of": "write"
        }
      ],
      "title": "Create Trello cards from new Typeform entries",
      "url": "https://zapier.com/app/editor/125"
    },
    {
      "id": 123,
      "modified_at": "2017-03-21T22:04:05-05:00",
      "state": "off",
      "steps": [
        {
          "app": {
            "description": "Typeform helps you ask awesomely online! If you ever need to run a survey, questionnaire, form, contest etc... Typeform will help you achieve it beautifully across all devices, every time, using its next generation platform.",
            "hex_color": "8bcbca",
            "id": 4259,
            "image": "https://cdn.zapier.com/storage/developer/5e21b4c1e0a2a3346a801dbc0a2a5a6d_2.png",
            "images": {
              "url_128x128": "https://cdn.zapier.com/storage/developer/5e21b4c1e0a2a3346a801dbc0a2a5a6d_2.128x128.png",
              "url_16x16": "https://cdn.zapier.com/storage/developer/5e21b4c1e0a2a3346a801dbc0a2a5a6d_2.16x16.png",
              "url_32x32": "https://cdn.zapier.com/storage/developer/5e21b4c1e0a2a3346a801dbc0a2a5a6d_2.32x32.png",
              "url_64x64": "https://cdn.zapier.com/storage/developer/5e21b4c1e0a2a3346a801dbc0a2a5a6d_2.64x64.png"
            },
            "api": "TypeformDevAPI",
            "slug": "typeform",
            "title": "Typeform",
            "url": "https://zapier.com/apps/typeform/integrations"
          },
          "type_of": "read"
        },
        {
          "app": {
            "description": "Trello is team collaboration tool that lets you organize anything and everything to keep your projects on task.",
            "hex_color": "0079bf",
            "id": 4192,
            "image": "https://cdn.zapier.com/storage/services/da3ff465abd3a3e1b687c52ff803af74.png",
            "images": {
              "url_128x128": "https://cdn.zapier.com/storage/services/da3ff465abd3a3e1b687c52ff803af74.128x128.png",
              "url_16x16": "https://cdn.zapier.com/storage/services/da3ff465abd3a3e1b687c52ff803af74.16x16.png",
              "url_32x32": "https://cdn.zapier.com/storage/services/da3ff465abd3a3e1b687c52ff803af74.32x32.png",
              "url_64x64": "https://cdn.zapier.com/storage/services/da3ff465abd3a3e1b687c52ff803af74.64x64.png"
            },
            "api": "TrelloAPI",
            "slug": "trello",
            "title": "Trello",
            "url": "https://zapier.com/apps/trello/integrations"
          },
          "type_of": "write"
        }
      ],
      "title": "Create Trello cards from new Typeform entries",
      "url": "https://zapier.com/app/editor/123"
    }
  ]
}
{% endraw %}
```

#### The Zap Object

| attribute       | type            | notes                                          |
| --------------- | --------------- | ---------------------------------------------- |
| **id**          | Number          | The ID of the Zap.                             |
| **modified_at** | Date            | The last modified date time.                   |
| **state**       | String          | One of `'on'`, `'off'`, or `'draft'`           |
| **steps**       | Array<Zap Step> | An array steps in the Zap. See below.          |
| **title**       | String          | The name of the Zap, if any, otherwise `null`. |
| **url**         | String          | An absolute url to the Zap (to edit).          |

```
{% raw %}
{
  "id": 125,
  "modified_at": "2017-03-22T09:38:11-05:00",
  "state": "on",
  "steps": [{ "See Step object below ..." }],
  "title": "Create Trello cards from new Typeform entries",
  "url": "https://zapier.com/app/editor/125"
}
{% endraw %}
```

#### The Zap Step Object

| attribute   | type   | notes                                                                      |
| ----------- | ------ | -------------------------------------------------------------------------- |
| **type_of** | String | One of `'read'`, `'write'`, `'filter'`, `'search'`, or `'search_or_write'` |
| **app**     | App    | The app for the step. See below.                                           |

```
{% raw %}
{
  "app": {"See the App object below ..."},
  "type_of": "read"
}
{% endraw %}
```

### Zap Templates

|                 URL                 | Protected By |
| :---------------------------------: | :----------: |
| **api.zapier.com/v1/zap-templates** |  Client ID   |

#### Arguments

Available parameters to the Zap templates resource:

| parameter     | requirement | notes                                                                                                                    |
| ------------- | ----------- | ------------------------------------------------------------------------------------------------------------------------ |
| **client_id** | Required    | Your application client ID.                                                                                              |
| **templates** | Optional    | A comma separated list of specific Zap templates.                                                                        |
| **apps**      | Optional    | A comma separated list of Zapier Apps to match Zap templates against. **Note: Your app will always be one of the apps.** |
| **limit**     | Optional    | (defaults to 5, max of 100) Limit the number of Zap templates returned.                                                  |

#### Example Requests

Get all Zap templates for my app.

```
{% raw %}
curl -L "https://api.zapier.com/v1/zap-templates?client_id=${client_id}"
{% endraw %}
```

Get all Zap templates that include my app and another.

```
{% raw %}
curl -L "https://api.zapier.com/v1/zap-templates?client_id=${client_id}&apps=mailchimp"
{% endraw %}
```

#### EXAMPLE RESPONSE

```
{% raw %}
[{
  "description": "<p>Facebook Lead Ads are an excellent way to grow your list of individuals interested in learning more about your product or service, but taking a next step with those people can sometimes take a back seat to your other tasks. With this Facebook Lead Ads-MailChimp integration, you'll no longer need to think about adding new leads to a marketing campaign—each new lead is automatically added to the list of your choice.</p>\n\n<h2>How this Facebook Lead Ads-MailChimp integration works</h2>\n\n<ol>\n<li>Someone fills out one of your Facebook Lead Ads</li>\n<li>Zapier adds that individual to a specified list in MailChimp</li>\n</ol>\n\n<h2>Apps involved</h2>\n\n<ul>\n<li>Facebook Lead Ads</li>\n<li>MailChimp</li>\n</ul>\n",
  "title": "Subscribe new Facebook Lead Ad leads to a MailChimp list",
  "url": "https://zapier.com/apps/facebook-lead-ads/integrations/mailchimp/10127/subscribe-new-facebook-lead-ads-mailchimp-list",
  "type": "guided_zap",
  "status": "published",
  "description_raw": "Facebook Lead Ads are an excellent way to grow your list of individuals interested in learning more about your product or service, but taking a next step with those people can sometimes take a back seat to your other tasks. With this Facebook Lead Ads-MailChimp integration, you'll no longer need to think about adding new leads to a marketing campaign—each new lead is automatically added to the list of your choice.\r\n\r\n## How this Facebook Lead Ads-MailChimp integration works\r\n\r\n1. Someone fills out one of your Facebook Lead Ads\r\n2. Zapier adds that individual to a specified list in MailChimp\r\n\r\n## Apps involved\r\n\r\n- Facebook Lead Ads\r\n- MailChimp",
  "slug": "subscribe-new-facebook-lead-ads-mailchimp-list",
  "description_plain": "Facebook Lead Ads are an excellent way to grow your list of individuals interested in learning more about your product or service, but taking a next step with those people can sometimes take a back seat to your other tasks. With this Facebook Lead Ads-MailChimp integration, you'll no longer need to think about adding new leads to a marketing campaign—each new lead is automatically added to the list of your choice.\n\nHow this Facebook Lead Ads-MailChimp integration works\n\nSomeone fills out one of your Facebook Lead Ads\n\nZapier adds that individual to a specified list in MailChimp\n\nApps involved\n\nFacebook Lead Ads\n\nMailChimp",
  "steps": [
    {
      "description": "Facebook lead ads make signing up for business information easy for people and more valuable for businesses. The Facebook lead ad app is useful for marketers who want to automate actions on their leads.",
      "title": "Facebook Lead Ads",
      "url": "https://zapier.com/apps/facebook-lead-ads/integrations",
      "image": "https://cdn.zapier.com/storage/services/fd9fef95169fd589d6cda992c0057cf8.png",
      "api": "FacebookLeadsAPI",
      "slug": "facebook-lead-ads",
      "hex_color": "3b5998",
      "images": {
        "url_128x128": "https://cdn.zapier.com/storage/services/fd9fef95169fd589d6cda992c0057cf8.128x128.png",
        "url_64x64": "https://cdn.zapier.com/storage/services/fd9fef95169fd589d6cda992c0057cf8.64x64.png",
        "url_16x16": "https://cdn.zapier.com/storage/services/fd9fef95169fd589d6cda992c0057cf8.16x16.png",
        "url_32x32": "https://cdn.zapier.com/storage/services/fd9fef95169fd589d6cda992c0057cf8.32x32.png"
      },
      "id": 3535
    },
    {
      "description": "MailChimp is an email marketing service provider, founded in 2001. It has 6 million users that collectively send over 10 billion emails through the service each month.",
      "title": "MailChimp",
      "url": "https://zapier.com/apps/mailchimp/integrations",
      "image": "https://cdn.zapier.com/storage/services/5c727288d9c2f69a9eee136c5f5a0f72.png",
      "api": "MailChimpAPI",
      "slug": "mailchimp",
      "hex_color": "239AB9",
      "images": {
        "url_128x128": "https://cdn.zapier.com/storage/services/5c727288d9c2f69a9eee136c5f5a0f72.128x128.png",
        "url_64x64": "https://cdn.zapier.com/storage/services/5c727288d9c2f69a9eee136c5f5a0f72.64x64.png",
        "url_16x16": "https://cdn.zapier.com/storage/services/5c727288d9c2f69a9eee136c5f5a0f72.16x16.png",
        "url_32x32": "https://cdn.zapier.com/storage/services/5c727288d9c2f69a9eee136c5f5a0f72.32x32.png"
      },
      "id": 6
    }
  ],
  "create_url": "https://zapier.com/app/editor/template/10127?utm_campaign=Zap%20Templates%20Partners%20API&embedded=true&referrer=FacebookLeadsAPI&utm_source=partners&utm_medium=api&selected_apis=FacebookLeadsAPI,MailchimpCLIAPI@1.0.10",
  "id": 10127
}]
{% endraw %}
```

### My Zap Templates

Lookup a user's Zap templates that they've added (published or draft). **Note: We are limiting this endpoint to partners. This means that you will only see results for Zap templates that include your app in one of the steps.**

|                  URL                   |      Protected By       | Required Scopes |
| :------------------------------------: | :---------------------: | :-------------: |
| **api.zapier.com/v1/zap-templates/me** | Client ID, Access Token |   `templates`   |

#### Arguments

Available parameters to the Zap templates resource:

| parameter     | requirement | notes                                                                                                                    |
| ------------- | ----------- | ------------------------------------------------------------------------------------------------------------------------ |
| **client_id** | Required    | Your application client ID.                                                                                              |
| **templates** | Optional    | A comma separated list of specific Zap templates.                                                                        |
| **apps**      | Optional    | A comma separated list of Zapier Apps to match Zap templates against. **Note: Your app will always be one of the apps.** |
| **limit**     | Optional    | (defaults to 5, max of 100) Limit the number of Zap templates returned.                                                  |
| **status**    | Optional    | (defaults to `published`) Filter by specific status of a Zap template. Available statuses: `draft` and `published`.      |

#### Example Requests

Get all Zap templates for my app.

```
{% raw %}
curl -H "Authorization: Bearer {token}" -L "https://api.zapier.com/v1/zap-templates/me?client_id=${client_id}"
{% endraw %}
```

Get all Zap templates that include my app and another.

```
{% raw %}
curl -H "Authorization: Bearer {token}" -L "https://api.zapier.com/v1/zap-templates?client_id=${client_id}&apps=mailchimp"
{% endraw %}
```

Get all Zap templates for my app that are draft.

```
{% raw %}
curl -H "Authorization: Bearer {token}" -L "https://api.zapier.com/v1/zap-templates/me?client_id=${client_id}&status=draft"
{% endraw %}
```

#### EXAMPLE RESPONSE

```
{% raw %}
[{
  "description": "<p>Facebook Lead Ads are an excellent way to grow your list of individuals interested in learning more about your product or service, but taking a next step with those people can sometimes take a back seat to your other tasks. With this Facebook Lead Ads-MailChimp integration, you'll no longer need to think about adding new leads to a marketing campaign—each new lead is automatically added to the list of your choice.</p>\n\n<h2>How this Facebook Lead Ads-MailChimp integration works</h2>\n\n<ol>\n<li>Someone fills out one of your Facebook Lead Ads</li>\n<li>Zapier adds that individual to a specified list in MailChimp</li>\n</ol>\n\n<h2>Apps involved</h2>\n\n<ul>\n<li>Facebook Lead Ads</li>\n<li>MailChimp</li>\n</ul>\n",
  "title": "Subscribe new Facebook Lead Ad leads to a MailChimp list",
  "url": "https://zapier.com/apps/facebook-lead-ads/integrations/mailchimp/10127/subscribe-new-facebook-lead-ads-mailchimp-list",
  "type": "guided_zap",
  "status": "published",
  "description_raw": "Facebook Lead Ads are an excellent way to grow your list of individuals interested in learning more about your product or service, but taking a next step with those people can sometimes take a back seat to your other tasks. With this Facebook Lead Ads-MailChimp integration, you'll no longer need to think about adding new leads to a marketing campaign—each new lead is automatically added to the list of your choice.\r\n\r\n## How this Facebook Lead Ads-MailChimp integration works\r\n\r\n1. Someone fills out one of your Facebook Lead Ads\r\n2. Zapier adds that individual to a specified list in MailChimp\r\n\r\n## Apps involved\r\n\r\n- Facebook Lead Ads\r\n- MailChimp",
  "slug": "subscribe-new-facebook-lead-ads-mailchimp-list",
  "description_plain": "Facebook Lead Ads are an excellent way to grow your list of individuals interested in learning more about your product or service, but taking a next step with those people can sometimes take a back seat to your other tasks. With this Facebook Lead Ads-MailChimp integration, you'll no longer need to think about adding new leads to a marketing campaign—each new lead is automatically added to the list of your choice.\n\nHow this Facebook Lead Ads-MailChimp integration works\n\nSomeone fills out one of your Facebook Lead Ads\n\nZapier adds that individual to a specified list in MailChimp\n\nApps involved\n\nFacebook Lead Ads\n\nMailChimp",
  "steps": [
    {
      "description": "Facebook lead ads make signing up for business information easy for people and more valuable for businesses. The Facebook lead ad app is useful for marketers who want to automate actions on their leads.",
      "title": "Facebook Lead Ads",
      "url": "https://zapier.com/apps/facebook-lead-ads/integrations",
      "image": "https://cdn.zapier.com/storage/services/fd9fef95169fd589d6cda992c0057cf8.png",
      "api": "FacebookLeadsAPI",
      "slug": "facebook-lead-ads",
      "hex_color": "3b5998",
      "images": {
        "url_128x128": "https://cdn.zapier.com/storage/services/fd9fef95169fd589d6cda992c0057cf8.128x128.png",
        "url_64x64": "https://cdn.zapier.com/storage/services/fd9fef95169fd589d6cda992c0057cf8.64x64.png",
        "url_16x16": "https://cdn.zapier.com/storage/services/fd9fef95169fd589d6cda992c0057cf8.16x16.png",
        "url_32x32": "https://cdn.zapier.com/storage/services/fd9fef95169fd589d6cda992c0057cf8.32x32.png"
      },
      "id": 3535
    },
    {
      "description": "MailChimp is an email marketing service provider, founded in 2001. It has 6 million users that collectively send over 10 billion emails through the service each month.",
      "title": "MailChimp",
      "url": "https://zapier.com/apps/mailchimp/integrations",
      "image": "https://cdn.zapier.com/storage/services/5c727288d9c2f69a9eee136c5f5a0f72.png",
      "api": "MailChimpAPI",
      "slug": "mailchimp",
      "hex_color": "239AB9",
      "images": {
        "url_128x128": "https://cdn.zapier.com/storage/services/5c727288d9c2f69a9eee136c5f5a0f72.128x128.png",
        "url_64x64": "https://cdn.zapier.com/storage/services/5c727288d9c2f69a9eee136c5f5a0f72.64x64.png",
        "url_16x16": "https://cdn.zapier.com/storage/services/5c727288d9c2f69a9eee136c5f5a0f72.16x16.png",
        "url_32x32": "https://cdn.zapier.com/storage/services/5c727288d9c2f69a9eee136c5f5a0f72.32x32.png"
      },
      "id": 6
    }
  ],
  "create_url": "https://zapier.com/app/editor/template/10127?utm_campaign=Zap%20Templates%20Partners%20API&embedded=true&referrer=FacebookLeadsAPI&utm_source=partners&utm_medium=api&selected_apis=FacebookLeadsAPI,MailchimpCLIAPI@1.0.10",
  "id": 10127
}]
{% endraw %}
```

#### The Zap Template Object

| attribute             | type       | notes                                                                                                                         |
| --------------------- | ---------- | ----------------------------------------------------------------------------------------------------------------------------- |
| **create_url**        | String     | An absolute URL used to create the Zap.                                                                                       |
| **description**       | String     | The HTML-rendered description provided when the Zap template was created.                                                     |
| **description_plain** | String     | Plain text (HTML tags stripped) description. **Note: `\r` and `\n` replaced with space character. Artifacts may be present.** |
| **description_raw**   | String     | The [Markdown][markdown] description provided when the Zap template was created.                                              |
| **slug**              | String     | A URL/SEO friendly ID for the Zap template.                                                                                   |
| **steps**             | Array<App> | An array of two or more steps in the Zap template. See below.                                                                 |
| **title**             | String     | The name of the Zap template.                                                                                                 |
| **status**            | String     | The status of the Zap template (choices: `draft`, `published`).                                                               |
| **url**               | String     | An absolute url to the Zapbook Zap template Page.                                                                             |

```
{% raw %}
{
  "create_url": "https://zapier.com/app/editor/template/10127?utm_campaign=Zap%20Templates%20Partners%20API&embedded=true&referrer=FacebookLeadsAPI&utm_source=partners&utm_medium=api&selected_apis=FacebookLeadsAPI,MailchimpCLIAPI@1.0.10",
  "description": "<p>Facebook Lead Ads are an...",
  "description_plain": "Facebook Lead Ads ... ",
  "description_raw": "**Facebook Lead Ads** are an ...",
  "slug": "subscribe-new-facebook-lead-ads-mailchimp-list",
  "status": "published",
  "steps": [{"... see App Object below ..."}],
  "title": "Subscribe new Facebook Lead Ad leads to a MailChimp list",
  "url": "https://zapier.com/apps/inside-sales-box/integrations/zoho-crm/12084/add-new-leads-created-in-inside-sales-box-to-zoho-crm"
}
{% endraw %}
```

### `create_url` and Prefill Options

Always link the user with the `create_url` in order to create the Zap. Optionally, you can add additional parameters to the `create_url` so that the user's Zap is prefilled with the provided custom values. You will need to know the fields that your app requires per step.

> One tip is to use the [Zap template editor](https://zapier.com/developer/shared-zaps/) to find these fields.

Each parameter is in a flattened dictionary/object syntax. For example an object: `{a: {b: 2}}` would be flattened to: `a__b=2`. This allows you to provide countless prefills onbehalf of the user.

#### Example

Prefill Trello's board ID (field: `board`) in the second step of the Zap template:

`https://zapier.com/app/editor/template/2405?steps__1__params__board=12345`

Here's what it would look like in the editor:

![](https://cdn.zapier.com/storage/photos/1f3544e43787d1d2e0b528b08b909dcb.png)

If you'd like to provide a label for the value (e.g. a Board's name) you can do so by passing an additional parameter:

`https://zapier.com/app/editor/template/2405?steps__1__params__board=12345&steps__1__meta__parammap__board=My+Board`

![](https://cdn.zapier.com/storage/photos/86b71a90bc69e5b13024c08f1da4b812.png)

#### The App Object

| attribute       | type   | notes                                                                                                                                                 |
| --------------- | ------ | ----------------------------------------------------------------------------------------------------------------------------------------------------- |
| **description** | String | Plain text description of the app.                                                                                                                    |
| **hex_color**   | String | A Web Color Hex. Useful for icon/display background.                                                                                                  |
| **image**       | String | The app's logo in large format.                                                                                                                       |
| **images**      | Object | Thumbnails for the app image. <br><small>Available sizes (and respective keys):<br> `url_128x128`, `url_64x64`, `url_32x32`, and `url_16x16`.</small> |
| **slug**        | String | A URL/SEO friendly ID for the app.                                                                                                                    |
| **title**       | String | The name of the app.                                                                                                                                  |
| **url**         | String | An absolute url to the Zapbook Apps page.                                                                                                             |

```
{% raw %}
{
  "description": "Facebook lead ads make signing up for business information ...",
  "hex_color": "3b5998",
  "image": "https://cdn.zapier.com/storage/s/fd9fef95169fd589d6cda992c0057cf8.png",
  "images": {
    "url_128x128": "https://cdn.zapier.com/storage/services/fd9fef95169fd589d6cda992c0057cf8.128x128.png",
    "url_16x16": "https://cdn.zapier.com/storage/services/fd9fef95169fd589d6cda992c0057cf8.16x16.png",
    "url_32x32": "https://cdn.zapier.com/storage/services/fd9fef95169fd589d6cda992c0057cf8.32x32.png",
    "url_64x64": "https://cdn.zapier.com/storage/services/fd9fef95169fd589d6cda992c0057cf8.64x64.png"
  },
  "slug": "facebook-lead-ads",
  "title": "Facebook Lead Ads",
  "url": "https://zapier.com/apps/facebook-lead-ads/integrations"
}
{% endraw %}
```

### Changelog

|    Date    |                  Resource                  | Change                                                                                                                                                                                                                                                                          |
| :--------: | :----------------------------------------: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 2017-11-01 | All endpoints with access token protection | After security review, the access tokens granted **will no longer expire**. This may change in the future, however, based on endpoints provided by the API. In that event, we expect API consumers to provide the user with the authorize endpoint to get a fresh access token. |
| 2017-10-16 |                  `/zaps`                   | The endpoint will now return **all** Zaps regardless of the [Zapier CLI App's version](https://github.com/zapier/zapier-platform-cli) that was used when creating the Zap.                                                                                                      |

### See it in Action: How Unbounce Uses the API

The API allows for so much flexibility that it can be challenging to picture the end result. Here's how lead generation app, Unbounce, built Zapier integrations into the Unbounce UI. The end result? A seamless integration experience for their users who can now connect their new Unbounce leads to hundreds of apps right from their Unbounce dashboard.

Now when Unbounce users are logged in, there's a slew of Zapier-powered integrations alongside their forms.

![](https://cdn.zapier.com/storage/photos/9e769e34030c2bbcf2fb80b827d69c22.png)

When a user chooses an integration, pop-up Zap Template guides the user through setting up that Zap, with info from Unbounce pre-filled like the form, client, landing page - anything already known about the Unbounce form.

![](https://cdn.zapier.com/storage/photos/edcf17488c8250dca213ed2083846fc5.png)

Then, once that Zap is set up and turned on, it's right there in Unbounce, where it can be edited, toggled on/off, etc. That means users can set up and manage nearly 1,000 integrations without ever leaving Unbounce.

![](https://cdn.zapier.com/storage/photos/05fec8dfe5a382bcfbcfe44c6139f14e.png)

### Other Examples

- **Facebook** lets you search for and configure a Zap from within the [Lead Ad Campaign Manager](https://cdn.zapier.com/storage/photos/73d073d363d0eae104ccdb159eaba8cd.gif).
- **Trello** leverages the Partner API to let the user manage their Zapier experience from their [dashboard within Trello.](http://blog.trello.com/zapier-power-up-for-trello)
- **Zoho Connect** lets users set up Zaps from [within the Zoho Connect app.](https://cdn.zapier.com/storage/photos/e02db0c000ed037b3385b813b3f1303c.gif)

### Ready to get started?

[Request an API Key]({{ site.partner_api_invite_url }}) for your app's Zapier integration.
