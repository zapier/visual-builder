---
title: Zap templates
order: 4
layout: post-toc
redirect_from: /partners/zap-templates
---

# Zap templates

> **Note:** Only public integrations can be used in Zap templates. Zap templates do not currently support private integrations.

Zapier empowers apps to do together what they can’t on their own. With a bit of inspiration and creativity, your users can pull dozens of apps together into unique workflows to get more done with your app in far less time.

Zap templates are ready made Zaps with the apps and core fields pre-selected, for publicly available Zapier integrations. In a few clicks, they help people discover a use case, connect apps, and turn on the Zap. Zap templates are the fastest way for your users to automate workflows.

<script type="text/javascript" src="https://zapier.com/apps/embed/widget.js?guided_zaps=192,111,162,1495,883"></script>

They’re also a great way to promote your app, as your Zap templates are featured in:

- Zapier’s app directory
- Zapier’s onboarding experience
- In many of Zapier's {{ site.partner_count }} integration partners' apps and sites

Zap templates can also be featured inside your site and content to help your users start using Zapier integrations. The more Zap templates you create and the more users they have, the more likely they are to be featured. This helps your Zapier integration gain popularity and rise the ranks of the [Zapier Partner Program](https://zapier.com/developer-platform/partner-program). To learn more about embedding Zap templates (and other experiences) into your app or website, see our dedicated [embed](https://platform.zapier.com/embed/overview) section.

> Expected time to create a Zap Template: 10 minutes.

![Example Zap Template](https://cdn.zappy.app/0d6ffaf492b547878ef8c06924a714f1.gif)
_An example Zap Template that automatically saves Gmail attachments to Google Drive — a handy way to speed up email file management._

## How to build a Zap template

Zap templates take a few steps to build, similar to any other Zap. You first select the app and trigger you want to start the Zap, then add an action app and map the fields from the trigger app to the action — and optionally add additional steps. Then, add a title and description to help people quickly understand when to use your Zap.

To get started, go to Zapier’s [Zap template creator](https://zapier.com/app/editor/zap-template/) or from the [Zap Template dashboard](https://developer.zapier.com/zap-templates), click _Create Zap Template_.

### 1. Add a Trigger Step

![Zap Template select trigger app](https://cdn.zappy.app/64e407ae2b8e5f3ecaf9bedbbacd11d4.png)

Select the trigger app by searching for the app by name from the menu.

> **Note:** You can use Zapier integrations that have been launched publicly.

Choose the app’s trigger from the dropdown that starts your Zap.

![Zap Template select trigger](https://cdn.zappy.app/bcf87bac5267b210d520cb97ac0e5612.png)

You won't be able to auth an account when creating Zap templates. Instead, the Zap template creator will load the sample data available for the selected trigger. If there are fields you want to use that aren't available, it means the integration developer did not add those fields to the integration's sample data. You can still use the trigger event in a Zap template, though when setting up the Zap’s action step(s), you might not be able to pre-map fields for your users. If the trigger includes options, fill in any fields or leave the defaults to let users add info to the Zap themselves. On the `Test trigger` pane, you can view the sample data available. Click _Continue_ to move to the next step.

![Zap Template sample](https://cdn.zappy.app/d90a46d02a04c72341c2534c3c77e353.png)

### 2. Add an Action Step

Select the action app by searching for the app by name from the menu.

![Zap Template add action app](https://cdn.zappy.app/ff77e3d0297f9a61bad2b6250472a059.png)

> **Note:** You can use Zapier integrations that have been launched publicly.

Choose the app’s action from the dropdown that you want to follow the trigger. Same as the trigger, the Zap template creator will load the sample data available for the selected action.

![Zap Template select action step](https://cdn.zappy.app/667f2e42d0ad4b367f2b86fd1e00398b.png)

> **Note**: If you use a search action, you will need to add a second action step to use the data from the trigger and search steps.

Now for the most crucial part of your Zap template: Map the input fields from the trigger app to the form fields in this action app. The action step will show the fields that are statically available. Dynamic fields that populate based on the input in another field will not be available. For the best Zap template experience, fill in as many form fields as possible to help users set up Zaps quickly.

![Zap Template form fields](https://cdn.zappy.app/42933f0f6a425d029429dbe918b0a107.png)

> **Note**: In addition to not showing dynamic fields, custom fields from apps (added by users) will not be available. This is because the Zap template creator is not authenticated with an app account to fetch that data. When users create a Zap from your template, they'll be able to leverage dynamic and custom fields.

For most form fields, you’ll need to add input fields from the trigger to the appropriate form field. Click into the form field and then `Show all options` button to see every input field from previous steps. Select the input field that fits the action field best. For example, you might select Gmail’s _Attachment_ field to upload the attachment via Google Drive’s _File_ form field. Or you might add Stripe’s _Email_ field to Mailchimp’s _Subscriber Email_ form field to add customers to an email list.

> **Tip**: Use [Zapier’s date and time syntax](https://help.zapier.com/hc/en-us/articles/8496275717261-Insert-the-time-your-Zap-runs-into-a-field) to modify dates and times in action form fields.

Most dropdown menus are used to select folders, projects, and other user-generated data and should be left blank by default. You can, however, select options for dropdowns for boolean yes/no fields if you're certain which option is best for all users of this Zap template.

Zap Template action forms include _required_ and _optional_ fields. When users set up your Zap Template, they will see the required fields by default, and _must_ fill them in before turning on the Zap. Try to map as many required input fields as possible. Then, less-critical fields will often be marked as optional, and are hidden by default when users set up the Zap Template. If you know the best data to map to those fields, add them to make sure your users' Zaps include as much detail as possible.

![Zap Template required fields](https://cdn.zappy.app/e4222e2c4934485dd27454ef50f17ec0.png)

> **Note**: Do not enter plain text into an action form field unless _every_ user of this Zap Template would want the text included in the action.

Zapier then shows a `Test action` pane, similar to what users see when setting up Zaps. You won't be able to test your action steps when building a Zap template. The `Test action` pane will default to showing a successful test.

![Finish Zap Template Action](https://cdn.zappy.app/6e87adbfde77b00ae144b487c4185c20.png)

### 3. (Optional) Add filters or additional action steps

Choose to add another step to your Zap, or finish and save this Zap template with only two steps.

Most Zap templates only need two steps, with a trigger to watch for data from an app and an action to do something with that data in another app. Sometimes, though, you need more steps for advanced workflows, including:

- **[Additional create actions](https://help.zapier.com/hc/en-us/articles/8496257774221-Set-up-your-Zap-action)** to add additional automations to your workflow
- **[Filters](https://help.zapier.com/hc/en-us/articles/8496276332557)** to watch for specific items from trigger or action step(s)
- **[Search actions](https://help.zapier.com/hc/en-us/articles/8496241402253)** to find specific data from apps, recommended especially to find customers, tickets, projects, and more before creating new items with Zaps

> **Note**: You cannot build Paths in Zap templates at this time.

To add another search or create action to your Zap, click the _+_ button where you want to insert the additional step. Then repeat step 2 and set up the additional action. To add a _delay_ action, select the _Delay by Zapier_ app when adding a new action.

> **Note**: Code, custom webhook, Looping and custom Formatter steps are not allowed in Zap Templates.

You might want to add a filter to your Zap template. For example, you could add it between the trigger and action step to have the Zap only run when specific data is received. [Learn more about filters](https://help.zapier.com/hc/en-us/articles/8496276332557-Add-conditions-to-Zaps-with-filters). You can define a filter in the Zap template, or leave it blank and let users customize the filter to their needs.

![Add Filter step to Zap Template](https://cdn.zappy.app/23309a53e37648bd8547e0a7ec0c993e.png)

![Customize Zapier Filter](https://cdn.zappy.app/db5c3975470b1b2ba7be62b0ceb244ac.png)

> **Note**: Most Zap templates don’t need filters, and most filters should be added by users later if required. However, including a filter in a Zap template can be useful if your Zap Template is only useful with a filter to remove extraneous data.

### 4. Add a title and description

The final step is to add a title and description, then submit your Zap template for review.

![Zap Template Description](https://cdn.zappy.app/6f02ec2e5eac6cc7130ecfafb03a64dc.png)

Zap templates need to showcase a use case and describe it effectively. They provide inspiration for how to automate popular apps and workflows. Your Zap template's description and title help illustrate that idea to users.

The title is the first thing people see. Zap templates embedded inside your app, blog posts and other content show the Zap's title and app icons. Titles need to fit in well in each environment and describe the use case at a glance.

Descriptions are what users see when they click the Zap template. They explain the use case in further detail and tell how the Zap works. The title grabs interest; the description gets people to invest the minute or three it takes to turn on the Zap.

#### How to write a Zap template title

Zap template titles clearly and briefly state the apps the Zap connects and the workflow it accomplishes. They include the trigger and action apps and the actions they perform. They use present tense, active voice, and sentence case.

![Example Zap Template Title](https://cdn.zapier.com/storage/photos/fc6854d9f356bca06d8879a50ef41036.png)

Most Zap template titles read something like this: `Add new Gmail emails to Google Sheets as rows`. The title mentions what happens in the trigger app followed by what Zapier does in the action app. Some examples of good titles:

- `Create Trello cards for new Wufoo form entries`
- `Get Slack notifications for new Google Drive files in a folder`
- `Subscribe new Gumroad customers to a MailChimp list`
- `Save new liked SoundCloud tracks to Google Drive`

> **Tip**: Use your discretion whether to mention the action or trigger app first. The trigger app works best first in most cases, but sometimes it sounds awkward — if so, go with the action app first.

Follow these rules in your Zap template titles:

- **Start with an appropriate verb**. Zap templates start with an action verb that describes what the Zap does in the action app, such as `Create`, `Add`, `Make`, `Insert`, `Update`, `Subscribe`, or `Get`. Use unique verbs when possible, and use the most appropriate verb for the action Zapier performs with the app. For example:
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

#### How to write a Zap template description

Zap template descriptions share more detail about what the Zap does and scenarios in which to use it in two to four sentences. They tell readers what this Zap does for them and how it works.

Start your description with the user's problem or need. Then explain how Zapier meets that need, when the Zap will run, and what the Zap does when it runs. Explain the trigger and action items in plain language that show the workflow's value. Some good examples:

> Find yourself spending too much time adding event attendees to your CRM by hand? Now with the help of Zapier, the tedious work is done for you. This integration will add every new Eventbrite attendee to Zoho CRM as a new contact, saving you time for more important work.

> After someone fills out a form on your site, you'll want to hear about it or send them a follow-up email. This Zapier automation handles both gracefully, sending an email via Gmail to you or the form respondent whenever you get a new Typeform entry. You'll never have to send the same message over and over again.

> Expedient order processing makes for happy customers. Make sure you act on every new delivery with this Zapier automation. It will capture every new order placed on your Shopify store after being set up, creating a delivery task for it on Onfleet so your team can fulfill it without delay.

Keep these guidelines in mind:

- **Use present tense and active voice** as in the Zap title.
- **1 paragraph, 2-4 sentences** is enough for most Zap Template descriptions.
- **Don’t use Zapier-specific terminology** including Zap, Zap template, trigger, action, or terms that Zapier doesn’t support, such as sync. Instead, use generic words, such as `integration` or `automation`, that are universally understood.
- **Use same terms as the integrations themselves**. If an app calls the results of a form an “entry” don’t call it a “submission,” or if an email app uses "tags," don’t refer to "folders."
- **Don't include links**. Do not include links of any kind, whether Zapier-owned or third-party owned.
- **Include tips at the end**. If your Zap Template requires extra setup for filters or other steps, or if it doesn't cover all use cases users may expect, include a sentence at the end to clarify. Start the tip with `Note:`, and format the entire note in italics with [Markdown](https://zapier.com/blog/beginner-ultimate-guide-markdown/) formatting. For example: `*Note: Add the tag you want to the Zap's Filter step.*`

> **Note**: Always write unique descriptions for each Zap template — Zap templates that use the same descriptions but only replace app names, or those that duplicate the Zap template title, will be rejected.

---

Once you've added your Zap template title and description, click `Save Draft` under "Finish Up Your Zap Template".

![Save Draft](https://cdn.zappy.app/fb9a10e41c4ba4d794dc758e6c970f7f.png)

Now try using the Zap template to make sure it works as expected. Open your [Zap Template dashboard](https://zapier.com/zap-templates/), click the gear icon beside the Zap template you built, and select `Copy Link`. Open that link in a new tab or window, set up and turn on the Zap, and verify everything works correctly.

![Test Zap Template](https://cdn.zappy.app/c06a94f004e20748235d5de67efa2960.png)

<a id="submit-your-zap-templates"></a>

### 5. Submit Zap template for review

Finally, when your Zap template is ready for public release, click `Submit for Review` under "Finish Up Your Zap Template". This will submit the Zap template to our team to review to ensure it works as expected and meets our standards.

![Submit for review](https://cdn.zappy.app/09d633673809c700778cfa945b63d4ba.png)

We'll send you an automated email with the subject line _We've reviewed your Zap templates!_, typically within 2 weeks, after reviewing your Zap template(s). If your Zap template(s) passes the review, we will mark them as public to have them appear on your app's directory page and in our embed solutions.

If your Zap template is rejected, the automated email will provide a justification what's required to amend the template before re-submitting for review.

Then make some more Zap templates. The more you make, the easier it will be for users to start using your Zapier integration.

## Manual field mapping (custom pills)

When creating a Zap template, you typically map data between steps by selecting from a list of fields (or "pills") that have been added as sample data by the integration developer. Field mapping is what allows data to carry from one step to another. Custom pills take this a step further by letting you map fields that you know are returned by an integration, but haven’t been added as sample data. For example, if you wanted to map the field `eventType` between the trigger and step 2 of your Zap template, but `eventType` isn’t available in the trigger's sample data, you could create a custom pill to pull this field dynamically. Here’s how to create custom pills.

**Step 1: Identify the step position**

- The trigger is in position 1, with subsequent steps numbered sequentially

![Screenshot showing position 1-3](https://cdn.zappy.app/ad95202cb4726f214d234f0711e6c1fe.png)

**Step 2: Determine the field name**

- Because the sample data doesn't include the field you want, we suggest setting up a live Zap replicating the Zap template you want to create
- After publishing your Zap, let the Zap run live and then review its Zap history
- From the Zap history, you can identify the exact name of the field you want to pull data from
- In this example, we can see Google Calendar > New Event returns the field `eventType`

![Screenshot showing eventType field](https://cdn.zappy.app/d0025c224ba67f6470ef9e2629dce890.png)

**Step 3: Combine step position and field name**

- Once you have both the step position and field name, you can combine them to create a custom pill
- Start with 2 open curly braces {% raw %}`{{`{% endraw %}
- Add the step position folllowed by 2 underscores {% raw %}`__`{% endraw %}
- Next, add the field name
- Finally, finish with 2 closed curly braces {% raw %}`}}`{% endraw %}

Example: the `eventType` field isn’t returned in the sample data for Google Calendar > New Event. If you want to map that field in a Zap template, you can do so using the custom pill {% raw %}`{{1__eventType}}`{% endraw %}.

**Step 4: Insert custom pill**

- You can insert the custom pill into any field in any step that comes after the field that returns the data

**Additional Notes**

- Custom pills work in both Zap templates and regular Zaps. [Learn more about creating custom pills in Zaps](https://community.zapier.com/featured-articles-65/how-to-manually-map-fields-that-do-not-appear-in-the-sample-data-aka-custom-pill-mapping-9738).
- Custom pills will only work when a live Zap run returns the field used in the custom pill. If the field isn't returned during a live Zap run, fields where the custom pill has been mapped will remain empty
- The methodology described above only works for top-level fields. If a field is nested under another field (or multiple fields), each nest would be separated by double underscores.
- For example, if the trigger returned the following and you wanted to retrieve the response for question 3, your custom pill would look like this: {% raw %}`{{1__questions__3}}`{% endraw %}

![Screenshot showing nested fields](https://cdn.zappy.app/a64282d282a776319c77cc73f7aa504f.png)

By following these steps, you should be able to effectively add custom pills to your Zap Templates.


## Promote your Zap templates

It’s not enough to turn your ideal workflows into Zap templates. You need to get them in front of your end-users. Zapier automatically promotes your Zap templates in our SEO, app directory, and on partner sites using our embed tools (where both your and their apps are used in the template). You can promote Zap templates further by embedding them into your site (user dashboards, blog posts, help articles) using our [Zap template element](https://platform.zapier.com/embed/zap-templates).

### Zapier app directory

Your published Zap templates will appear on your directory page. Zap templates are loosely ordered by popularity, helping users easily discover common use-cases. Users can also search for Zap templates that connect your app with another.
![Zapier App Directory Page](https://cdn.zappy.app/f56ac65d2c36314bae02f21b00f983e4.png)

## Manage your Zap templates

Over time, you’ll likely make dozens of Zap templates. You can manage them — in draft, review, or publicly available — from your [Zap templates](https://zapier.com/zap-templates/) dashboard alongside Zapier’s Developer Platform tools.

![Zap Template List](https://cdn.zappy.app/35809b4d266dcfb55f1190cd8224ff1d.png)

Filter through your Zap templates by status on the left sidebar, click a Zap template to edit it, or select the gear icon on the right of a Zap template to copy its public link, test it, or delete it.

If you have any Zap templates in your _Rejected_ list, edit them to fix the issues then re-submit them. You cannot edit public Zap templates, but if you notice something that you need to change in your existing Zap Templates, please [submit our contact form](https://developer.zapier.com/contact) with the Zap template ID. We can set the Zap as _Draft_ again so you can edit and re-submit it for review with any changes.

### Promoting new versions of your integration

When promoting a new version of your integration, all Zap templates using the integration and having no breaking changes with the existing version will be updated to use the promoted version. The following are considered breaking changes:

- A trigger/action is hidden or deleted
- A trigger/action key is changed
- A trigger/action input field key is changed or removed
- A trigger/action output field key is changed or removed

If breaking changes exist between the previous and newly promoted integration versions, existing Zap templates will not be automatically updated and will continue to use the previous version. This can result in an older version acquiring new users over time. Consider the user impacts of [changes made in new versions](https://platform.zapier.com/manage/making-changes).

### Deprecating versions of your integration

When deprecating a version of your integration, any Zap templates using the integration will automatically be marked as _Invalid_ within 24 hours of the deprecation.

While invalid, the Zap template will not be _Public_ until it is adjusted to use a non-deprecated version, re-submitted for review and approved. This ensures users won’t use deprecated and broken Zap templates to make Zaps. If you’re having trouble accessing _Invalid_ templates, please [submit a ticket.](https://developer.zapier.com/contact)

## Frequently Asked Questions

**Why do I see Zap templates on my app's directory page that don’t appear under my [Zap Templates](https://developer.zapier.com/zap-templates)?**

Your integration’s directory page will show all published Zap templates that use your integration. The developer platform will only show Zap templates created by the currently logged in user.


**Who can publish Zap templates using my integration?**

Any user on Zapier is able to create and publish Zap templates using any integration that is in beta or public status. Zapier also identifies real-world usage and automatically generates Zap templates to help users discover use cases, enhance integration usage, and create more engaged users on both platforms. All Zap templates are subject to the same review process to ensure our quality standards are met.


**Can I opt out of Zapier-generated Zap templates for my integration?**

Currently, we do not offer the option for integrations to opt out of Zapier-generated Zap templates. These templates are designed based on real-world usage to enhance the end-user experience by highlighting commonly implemented workflows. They also aim to boost adoption for both Zapier and our integration partners.


**Can we remove or hide Zap templates that include our competitors from our directory page?**

Zap templates, once published on your integration’s directory page, remain in place to ensure our ecosystem is open, inclusive, and offers a wide range of options to users. This includes showcasing integrations that might combine your services with those of competitors. While direct removal of these templates isn’t aligned with our approach, we offer a proactive solution. By leveraging our [Zap Template embed tool](https://platform.zapier.com/embed/zap-templates), you have the power to highlight specific Zap templates you prefer, directly within your own platform. This empowers you to curate and showcase the integrations most relevant to your users’ needs.


**How can I make changes to a published Zap template?**

Once a Zap template is published, you are unable to self-serve changes to it. To request changes, please submit our [contact form](https://developer.zapier.com/contact). When submitting the contact form, please ensure you provide the Zap template ID and the change you’re requesting per Zap template. The Zap template ID can be found by clicking on the [3-dot icon](https://cdn.zappy.app/227b0c1da48e72115ced60cdb8c06a97.png) in the developer platform, or [in the URL](https://cdn.zappy.app/c913c363b267fd1c4c33b5395e092460.png) when viewing a Zap template landing page. Please note the following when requesting changes:
- Zap templates should work for the broadest audience. Try to avoid requesting changes that will exclude an audience segment from successfully using a Zap template
- Every partner on Zapier has their own style and tone. We will not update titles or descriptions of Zap templates created by other partners to better accommodate your preferences. While a title and description might not match your tone and style, it could very well for the partner that published the Zap template
  - If you believe you found an error with a title or description (eg the title references the wrong action), we will review and consider making the correction
- When requesting a functional change to a Zap template created by another partner, clearly state the Zap templates current behavior and the expected behavior to justify the requested change


**How can I re-order Zap templates on my directory page?**

Our current sorting system prioritizes Zap templates based on popularity and user engagement, ensuring users who land on your integration’s page on Zapier see the most helpful examples of real workflows. The sort order cannot be modified.


**How can I exclude specific Zap templates on my directory page?**

All published Zap templates that use your integration will appear on your directory page. You are unable to exclude published Zap templates from appearing on that page. Note when embedding Zap templates using the [Zap Template Element](https://platform.zapier.com/embed/zap-templates), you can specify which Zap templates to embed.


**How can I view all Zap templates created by my integration team?**

You cannot view Zap templates in the developer platform created by other users, even if you’re on the same integration team. If required, we can help to transfer ownership of Zap templates created by your integration team members to a singular account. You can [submit our contact form](https://developer.zapier.com/contact) to learn more about this.


**How can I unpublish a Zap template?**

Zap templates are a key driver of traffic for your integration. Promoting Zap templates is a part of our SEO strategy, and they appear throughout our embed network. For these reasons, we err against unpublishing Zap templates where possible. For Zap templates you own, you can unpublishing them by [deleting them](https://cdn.zappy.app/c0f9036c4b6f166b4c8289034558c201.png). If you wish to unpublish a Zap template without deleting it, you can request this by submitting our [contact form](https://developer.zapier.com/contact). Be sure to include the Zap template ID. When requesting to unpublish a Zap template created by another partner, please justify the request (eg duplicate Zap template, Zap template broken) for our consideration.


**Why were my Zap templates rejected?**

Zap templates can be rejected due to different reasons. The day after your Zap templates are rejected, you'll receive an email notification that will include feedback as to why a Zap template might have been rejected. Some common reasons for why Zap templates are rejected include:
- The title and/or description of the Zap template does not comply with our [style guide's](https://platform.zapier.com/publish/zap-templates#4-add-a-title-and-description) uniqueness requirements
- Fields in the trigger step have not been correctly mapped to corresponding fields in the action step(s)
- The use case for the Zap template is considered too narrow or specific for general use
- A Zap template with a similar use case already exists
- The Zap template title and/or description was written in a language other than English
- The Zap template includes a code, custom webhook, or custom formatter step which is currently not allowed
- The Zap template contains hardcoded values such as phone numbers, emails, or IDs which should be dynamically mapped from the trigger or another action step
- Submitting a large number of Zap templates for an integration with a low active user count can lead to rejection. We aim to ensure that our review resources are allocated fairly across all partners. When a disproportionate amount of submissions comes from a single source, it negatively impacts the review process for others. To maintain a balanced and efficient review process, we enforce limits based on the size and usage of the app


**Can I select which Zap templates to display in my embed?**

Yes, but only through our [Zap Templates](https://platform.zapier.com/embed/zap-templates) embed solution. You can choose between Popular Zap templates or Specific Zap templates, to highlight to your users.


**How many users are using a particular Zap Template?**

Although we don’t provide specific data around how many users are using a particular Zap template, you can track the number of active Zaps as well as activation rates by Trigger or Action. This information is available within your developer dashboard on the Dashboard page. You can learn more about the insights avilable on the Dashboard page [here](https://platform.zapier.com/manage/integration-insights). Zap templates are also loosely ordered by popularity on your integration’s directory page.


**How many Zap templates should my integration have?**

The more the merrier! One Zap template isn’t enough—you’ll want to make Zap templates for each of your app’s most popular use cases. Although there’s not a set number, we recommend adding 5 to 10 Zap templates to your integration, for a start. Learn more about Building Zap templates [here](https://platform.zapier.com/publish/zap-templates#how-to-build-a-zap-template).


**Why did my Zap Templates stop working?**

Common reasons your Zap template stopped working include breaking changes, versioning, migration, and authentication. Adding, updating, replacing, or deleting components can have various effects. Learn more about [planning and implementing integration changes](https://platform.zapier.com/manage/planning-changes).


**Which use cases should my Zap templates highlight?**

Your triggers, actions, and searches should focus on the main use cases of your platform. Check similar integrations in [Zapier’s App Directory](https://zapier.com/apps) and [recommended features](https://platform.zapier.com/build/recommended-integration-features) by app category for ideas on which items to include in your integration.


**Can I add filters/other conditions to my Zap templates?**

Yes. Most Zap templates only need a trigger and two action steps. However, we know sometimes you may need more steps for advanced workflows. Learn more [here](https://platform.zapier.com/publish/zap-templates#3-optional-add-filters-or-additional-action-steps).


**Do users need to have an account to create their own Zaps?**

All users requires their own Zapier account in order to create Zaps, even if the Zap originates from a Zap template. The account the Zap is owned by will add and store authentications for each app used in the Zap. To help reduce friction for new users, you should pair your embed solution with our [Quick Account Creation](https://platform.zapier.com/embed/quick-account-creation). This seamless, accelerated sign-up feature allows first-time Zapier users to skip the standard sign-up procedure and onboarding survey.