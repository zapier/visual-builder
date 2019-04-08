---
title: How to Include Zapier in Your App and Website
order: 3
layout: post-toc
redirect_from: /docs/
---

# How to Include Zapier in Your App and Website

## Introduction

Zapier empowers apps to do together what they can’t on their own. With a bit of inspiration and creativity, your users can pull dozens of apps together into unique workflows to get more done with your app in far less time.

Zap Templates are readymade integrations or Zaps with the apps and core fields pre-selected. In a few clicks, they help people discover a use case, connect apps, and turn on the Zap. Zap Templates are the fastest way for your users to automate workflows.

<script type="text/javascript" src="https://zapier.com/apps/embed/widget.js?guided_zaps=192,111,162,1495,883"></script>

They’re also a great way to promote your app, as your Zap Templates are featured in:

- Zapier’s App Directory
- Zapier’s onboarding experience
- In many of Zapier's 1,300+ integration partners' apps and sites

Zap Templates can also be featured inside your site and content to help your users start using Zapier integrations. The more Zap Templates you create and the more users they have, the more likely they are to be featured. This helps your Zapier integration gain popularity and rise the ranks of the [Zapier Partner Program](https://zapier.com/platform/partner-program).

Before launching your Zapier integration, you need to build at least 10 Zap Templates in the [Zap Template Creator](https://zapier.com/developer/zap-templates/create) to help people start using your integration.

> Expected time to create a Zap Template: 10 minutes.

![Example Zap Template](https://cdn.zapier.com/storage/photos/c89bedd08435ca8e9dc42b348eca732c.gif)
_An example Zap Template that automatically saves Gmail attachments to Google Drive—a handy way to speed up email file management._

## 2. How to Build a Zap Template

Zap Templates take a few steps to build, similar to any other Zap. You first select the app and trigger you want to start the Zap, then add an action app and map the fields from the trigger app to the action—and optionally add additional steps. Then, add a title and description to help people quickly understand when to use your Zap.

For help as you build, you can follow this video or the written instructions below:

<div class="wistia_responsive_padding" style="padding:44.17% 0 0 0;position:relative;"><div class="wistia_responsive_wrapper" style="height:100%;left:0;position:absolute;top:0;width:100%;"><iframe src="https://fast.wistia.net/embed/iframe/0y50h71p98?seo=false&videoFoam=true" title="Zap template creator video howto" allowtransparency="true" frameborder="0" scrolling="no" class="wistia_embed" name="wistia_embed" allowfullscreen mozallowfullscreen webkitallowfullscreen oallowfullscreen msallowfullscreen width="100%" height="100%"></iframe></div></div>
<script src="https://fast.wistia.net/assets/external/E-v1.js" async></script>
<br>
<br>

## 1. Add a Trigger Step

![Zap Template select trigger app](https://cdn.zapier.com/storage/photos/800758ee8bf0437e6904dd7842760ac5.png)

Open Zapier’s [Zap Template creator](https://zapier.com/developer/zap-templates/create) at [zapier.com/developer/zap-templates/create](https://zapier.com/developer/zap-templates/create), or click the _Create Zap Template_ button in your [Zap Template dashboard](https://zapier.com/developer/zap-templates/). Select the trigger app, as you would when making a Zap for yourself. Select a popular app from the grid, or search for the app you need from the dropdown menu.

> **Tip:** You can select any app publicly available on Zapier or any beta apps you’ve built or have been invited to use—though Zapier will only publish Zap Templates for public integrations.

![Zap Template select trigger](https://cdn.zapier.com/storage/photos/ea3a3fb79b79782138180c0ce46e7ba5.png)

Choose the app’s trigger that starts your Zap. Select one of the default options, search for the trigger you want, or click _show less common options_ if you can’t find the trigger you need.

![Zap Template authentication](https://cdn.zapier.com/storage/photos/60167ed1a0c13415ebe471a591e7e62e.png)

For most triggers from apps that require authentication, Zapier loads sample data similar to the data the app would send Zapier when it’s connected with a live account. Click the _Save + Continue_ button to use that in the next steps.

![Zap Template not including sample data](https://cdn.zapier.com/storage/photos/73a293c63f75e05cf68744faec6c5c97.png)

Some triggers require authentication, but don't include sample data. If so, Zapier will note that in a message like the one above. You can still use that Zap in a Zap template, though when setting up the Zap's action step(s), you won't be able to pre-map fields for your users.

![Zap Template built-in trigger](https://cdn.zapier.com/storage/photos/5a8fab320d5e48196d24e57e8173ce00.png)

If your trigger includes options—or if you're using a triggers such as Zapier’s _RSS_ or _Schedule_ tool that don’t require authentication—Zapier will then show additional settings for this trigger. Fill in any form fields, select multi-choice options, and click _Continue_ to save them. Or leave the defaults to let users add info to the Zap themselves—in which case, click the _Test This Step_ link in the left sidebar to skip the options.

In the final trigger option, Zapier shows sample data from the app. You can click the down arrow on the sample data to see what details are included and the input fields you can use from this app in the rest of your workflow. Then again click _Continue_ to complete your Zap's trigger.

## 2. Add an Action Step

![Zap Template add action app](https://cdn.zapier.com/storage/photos/f23d74b8ceb233c51cf0b2c138473cdd.png)

Now add the action step to your Zap. Select the action app, either from the popular apps list or from the search menu.

![Zap Template select action step](https://cdn.zapier.com/storage/photos/8dc73de8622e7fdde9e1da7286b96fd3.png)

Choose the create or search action for your Zap, again using the search menu or _Show less common options_ tools if needed. You may then be prompted to use sample data as before; click _Continue_ to accept.

> **Note**: If you use a search action, you need to also add a second action step to use the data from the trigger and search steps.

As in the trigger step, when setting up most actions, you'll see a screen where your users will authenticate the action app—only in the Zap Template creator, Zapier uses this to pull in sample fields for the app.

![Zap Template form fields](https://cdn.zapier.com/storage/photos/0871b7f9a9665d358465d81856f2432e.png)

Now for the most crucial part of your Zap Template: Map the input fields from the trigger app to the form fields in this action app. The action step’s template shows every field that Zapier can send to the app, with required and optional fields. For the best Zap Templates, you want to fill in as many form fields as possible to help users set up Zaps quickly.

> **Note**: Zap Templates' action fields _never_ show custom fields from apps, including spreadsheet columns, custom CRM fields, and other fields that are added by users, as Zapier's Template creator is not authenticated with an app account and custom fields will vary depending on the user. Your users will always need to add details to custom fields themselves.

For most form fields, you need to add input fields from the trigger to the appropriate form field. Click the `+` button on the right of the field to see every input field from the trigger step. Select the input field that fits the action field best. For example, you might select Gmail’s _Attachment_ field to upload the attachment via Google Drive’s _File_ form field, or you might add Stripe’s _Email_ field to Mailchimp’s _Subscriber Email_ form field to add customers to an email list.

> **Tip**: Use [Zapier’s date and time syntax](https://zapier.com/help/modifying-dates-and-times/) to modify dates and times in action form fields.

Most dropdown menus are used to select folders, projects, and other user-generated data and should be left blank by default. You can, however, select options for dropdowns for boolean yes/no fields if you're certain which option is best for this Zap Template.

![Zap Template required fields](https://cdn.zapier.com/storage/photos/da280e25dbcb49ec47133874c0265e73.png)

Zap Template action forms include _required for user_ and _optional for user_ fields. When users set up your Zap Template, they will see the required fields by default, and  _must_ fill them in before turning on the Zap. Try to map as many required input fields as possible. Then, less-critical fields will often be marked as optional, and are hidden by default when users set up the Zap Template. If you know the best data to map to those fields, add them to make sure your users' Zaps include as much detail as possible.

> **Note**: Do not enter plain text into an action form field unless _every_ user of this Zap Template would want the text included in the action.

![Finish Zap Template Action](https://cdn.zapier.com/storage/photos/0bf7bddc4ac8cd16d90a4929f2baaaa3.png)

Zapier then shows a test screen similar to what users see when setting up the Zap. Since you’re building a Zap Template, Zapier doesn’t create or add anything to your apps—the screen confirms everything should work correctly.

## 3. (Optional) Add Filters or Additional Action Steps

Now you have a choice: You can add another step to your Zap, or finish and save this Zap Template with only two steps.

Most Zap Templates only need two steps, with a Trigger to watch for data from an app and an Action to do something with that data. Sometimes, though, you need more steps for advanced workflows, including:

- **Additional create actions** to add additional automations to your workflow
- **[Filters](https://zapier.com/help/filter/)** to watch for specific items from trigger or action step(s)
- **[Search actions](https://zapier.com/learn/getting-started-guide/search-actions/)** to find specific data from apps, recommended especially to find customers, tickets, projects, and more before creating new items with Zaps
- **[Formatter actions](https://zapier.com/help/formatter/)** to split and customize data before adding it to an action step
- **[Delay actions](https://zapier.com/help/delay/)** to wait for a specified amount of time before performing another action step

> **Note**: You cannot build Paths in Zap Templates at this time.

To add another search or create action to your Zap, click the _Add a Step_ button after setting up your action above, then repeat step 2 and set up the additional action. To add a _delay_ action, select the _Delay by Zapier_ app when adding a new action.

![Add Filter step to Zap Template](https://cdn.zapier.com/storage/photos/5a4b65b9cff4bd8bf951a171299794c6.png)

To add a filter, click the `+` button in the left sidebar and select _Filter_. You could add it between the trigger and action step to have the Zap only run when specific items come in from the trigger app, or you can add it after the action to watch for particular results (then add subsequent action steps to do more with data if it passes the filter criteria).

![Customize Zapier Filter](https://cdn.zapier.com/storage/photos/e8e45015feffaae49d57a01a8e1162d6.png)

Then add details to the filter, if this Zap should always watch for the same data. Select the field the filter should watch, then choose the filter criteria (if the text exists, doesn’t exist, if a number is greater than this value, etc.), and finally type in the text you need Zapier to find. If you need additional conditions in your filter, click the `+ AND` or `+ OR` buttons to add other criteria.

Alternately, leave the filter details blank and let users customize the filter to their needs.

> **Note**: Most Zap Templates don’t need filters, and most filters should be added by users later if required. However, including a filter in a Zap Template can be useful if your Zap Template is only useful with a filter to remove extraneous data.

<a id="shared-zaps-description"></a>
## 4. Add a Title and Description

![Zap Template Description](https://cdn.zapier.com/storage/photos/771335061cfa2e631707662981f7e7cb.png)

Now for the final step: add Zap Template’s title and description, then submit your Zap Template for review.

Zap Templates need to showcase a use case and describe it effectively. They provide inspiration for how to automate popular apps and workflows. Your Zap Template's description and title help sell that idea to users.

The title is the first thing people see. Embedded Zaps inside Zapier, your app, and blog posts and other content show the Zap's title and app icons. Titles need to fit in well in each environment and sell the use case at a glance.

Descriptions, then, are what users see when they click the Zap Template. They explain the use case and tell how the Zap works. The title grabs interest; the description gets people to invest the minute or three it takes to turn on the Zap.

### How to write a Zap Template title

![Example Zap Template Title](https://cdn.zapier.com/storage/photos/fc6854d9f356bca06d8879a50ef41036.png)

Zap Template titles clearly and briefly state the apps the Zap connects and the workflow it accomplishes. They include the trigger and action apps and the actions they perform. They use present tense, active voice, and sentence case.

Most Zap Template titles read something like this: `Add new Gmail emails to Google Sheets as rows`. The title mention what happens in the trigger app followed by what Zapier does in the action app, with a template like:

`Add new Trigger App items as Action App items`

Replace the defaults with your trigger and action apps, the items Zapier watches for and creates in each, and a verb at the beginning of the sentence that fits the workflow. For example:

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

### How to write a Zap Template description

Zap Template descriptions share more detail about what the Zap does and scenarios in which to use it in two to four sentences. They tell readers what this Zap does for them and how it works.

Start your description with the user's problem or need. Then explain how Zapier meets that need, when the Zap will run, and what the Zap does when it runs. Explain the trigger and action items in plain language that show the workflow's value.

Keep these guidelines in mind:

- **Use present tense and active voice** as in the Zap title.
- **1 paragraph, 2-4 sentences** is enough for most Zap Template descriptions.
- **Don’t use Zapier-specific terminology** including Zap, Zap Template, trigger, action, or terms that Zapier doesn’t support, such as sync. Instead, use generic words, such as `integration` or `automation`, that are universally understood.
- **Use same terms as the integrations themselves**. If an app calls the results of a form an “entry” don’t call it a “submission,” or if an email app uses "tags," don’t refer to "folders."
- **Include tips at the end**. If your Zap Template requires extra setup for filters or other steps, or if it doesn't cover all use cases users may expect, include a sentence at the end to clarify. Start the tip with `Note:`, and format the entire note in italics with [Markdown](https://zapier.com/blog/beginner-ultimate-guide-markdown/) formatting. For example: `*Note: Add the tag you want to the Zap's [Filter](https://zapier.com/learn/getting-started-guide/filters/) step.*`

> **Note**: Always write unique descriptions for each Zap Template—we will reject Zap Templates that use the same descriptions but only replace app names.

***

Once you've written and added your Zap Template title and description, it's time to save and test your work. Select `Draft` from the _Zap Template Visibility_ menu and click the _Save_ button.

![Test Zap Template](https://cdn.zapier.com/storage/photos/87a8cdc2f4d28b3ca8f743d0b332e84c.png)

You should then try using the Zap Template to make sure it works as expected. Open your [Zap Template dashboard](https://zapier.com/developer/zap-templates/), click the gear icon beside the Zap Template you built, and select _Copy Link_. Open that link in a new tab or window, and follow the steps to set up and turn on the Zap—and make sure everything looks and works correctly.

Optionally, you can let your team help test Zap Templates as well. When saving your Zap Template, choose `Shared` instead of draft, then share its link with others on your team so they can try the Zap Template.

<a id="submit-your-zap-templates"></a>
## 5. Submit Zap Template for Review

Finally, when your Zap Template is ready for public release, select the `For review` option on your Zap Template Visibility menu, and click _Save_ again. That submits the Zap Template to our team to review the Zap Template and ensure it works as expected and meets our standards. We'll then contact you, typically within a couple of weeks, after reviewing your Zap Template(s). If your Zap Templates pass the tests, we will mark them as public to automatically have them show up on your app's App Directory page, inside select partners' apps and sites, and in Zapier's onboarding experience.

Then make some more Zap Templates. Every Zapier integration must have at least 10 Zap Templates, and the more you make, the easier it will be to start using your Zapier integration. Open the [Zap Template Creator](https://zapier.com/developer/zap-templates/create) again and create any more Zap Templates you want.

## 3. Promote Your Zap Templates

It’s not enough to turn your ideal workflows into Zap Templates. You need to get them in front of everyone who should use your Zaps. Zapier automatically promotes your Zap Templates in our App Directory and in partner apps with embedded Zaps if your Zap Templates include their apps. You can promote them further with a list of your Zap Templates on your site, or include built-in Zap Template embeds inside your app.

## Zapier App Directory

![Zapier App Directory Page](https://cdn.zapier.com/storage/photos/b625939587cb8a8c7242f375c714d6aa.png)

The easiest way to find Zap Templates is in Zapier’s [App Directory](https://zapier.com/apps/) where we have individual pages for each of the 1,300+ apps that integrate with Zapier. Want to find Gmail integrations? Go to [zapier.com/apps/gmail/integrations](https://zapier.com/apps/gmail/integrations/) to see the top apps connected with Gmail on Zapier, followed by a list of popular Gmail Zap Templates and Zapier content about Gmail use cases.

Find your app’s App Directory page at `zapier.com/apps/YourApp/integrations`, replacing `YourApp` with your app’s name.

![Zapier App Directory two-app page](https://cdn.zapier.com/storage/photos/ca6556adda39eeb6f8477a873122d444.png)

Want to find ways to connect two specific apps? Click one of the top apps on any App Directory page to see our two-app pages, such as the one above for Trello and Gmail. It shows the most popular use cases for those two apps together.

Find your app’s two-app pages at `zapier.com/apps/YourApp/integrations/OtherApp`, substituting `YourApp` with your app’s name and `OtherApp` with the other app connected to your app.

Zapier also shows these top use cases to logged in users, promoting your app’s top Zap Templates to people who have connected Zapier to your app.

## Embed Zap Templates in Blog and Content Pages

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

Include the additional options at the end of the script text with an ampersand, such as:

`<script src="https://zapier.com/apps/embed/widget.js?services=APP&container=true&limit=10&theme=dark"></script>`

## Embed Zap Templates in Your App

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

* Getting the container element by ID and appending the script
* Using a ref={} in the component for a parent element that will contain the script
* Appending the script to the document body

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
