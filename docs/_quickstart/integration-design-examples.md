---
title: Integration design examples
order: 5
layout: post-toc
redirect_from: /quickstart/
---

# Integration design examples

Each app has its own unique features, but there are also a number of similarities between apps in similar categories. Here are some examples to keep in mind when designing a [form](#form), [CRM](#crm), or [project management](#pm) app integration:

<a id="form"></a>

## Add a form or survey app to Zapier

Form and Survey apps—along with similar apps for polls, applications, and mobile data collection—are ideal apps to integrate with Zapier. Whenever someone fills out the form, that new data needs to go somewhere. Zapier can connect that form to create new contacts, document templates, messages, and more.

Here are things to keep in mind when adding a form-based app to Zapier.

### Triggers

#### Add a new entry/response trigger

![Form app on Zapier](https://cdn.zapier.com/storage/photos/419a35068b794c36a9253a31a309e21d.png)

The most common trigger for a form or survey app is a "New Form Entry/Submission" or "New Survey Response" respectively.

Using our standard "New xxx" naming pattern makes it clear to users that Zapier only retrieves new entries, not existing ones.

#### Let users select a specific form

![Select Form in Zapier](https://cdn.zapier.com/storage/files/f951d24a065e5a2c56665e51002e7e17.gif)

Most users will have many forms or surveys in your app, so your Zapier integration needs a field where they can choose which form or survey they want to receive results from.

Add a [dynamic dropdown](https://platform.zapier.com/build/input-designer#how-to-add-dynamic-and-custom-fields) that retrieves the form names exactly as they are listed in your app. Consider ordering the dropdown list by the most recently added to make it easier for users to find the form they need.

You could make the form selector required, so the trigger only watches for results from this one form, which is the recommended option. Or, you could make the field optional so it would trigger for responses to any form; if so, add help text to let users know what to expect if they do not select a form.

### Format trigger response

#### Question and answer fields

![Example Form field names](https://cdn.zapier.com/storage/photos/554f4fc4856a555714398088f7a162b2.png)

Each form field or survey question needs to include the same name as that form field shows in your app.

For example, in a form that asks for contact information, the question/field “What’s your email?” might internally use an ID like `1839dod38k01` or a generic label such as `Question 1`.

Make sure to include the field's friendly name that the user added in your app, so they'll recognize which field to use when mapping data to action steps. Zapier can also show the raw field ID beside the friendly name.

For example, a common use case is to log responses in spreadsheets, with each answer field mapped to different columns. Using `q_1_answer` as a key name for a question is sensible, but it's not intuitive for users. Specify the full question instead.

Consider including the question number as a prefix to the label as well, to make it even easier for users to find specific questions and fields.

#### Multiple choice fields

![Multiple Choice Fields](https://cdn.zapier.com/storage/photos/033953ce0537c18a6efbe47f783ddf5a.png)

If a multiple choice question is based on a spectrum of values (e.g., from "not really" to "very"), it’s sometimes useful to return the choice values (such as `1` to `5`) as well as the actual answer. This can be especially useful for tracking responses in a spreadsheet.

#### Multi-select fields

![multi-select field](https://cdn.zapier.com/storage/photos/e922d705c9f9d61c46f32b31ba03e53f.png)

If a user can select multiple responses (perhaps in a list of checkboxes or buttons as above), it can be challenging to use this data with Zapier.

![multi-select as individual fields](https://cdn.zapier.com/storage/photos/a71b26a4a333fa9cb6b4a8c77607c426.png)

Consider returning these responses individually. Split each individual response to those questions into its own field, with data if it is selected and a blank response if not selected. This is often easier to map into Zap steps because users can map all responses into one field separated by the correct delimiter, or can take action on specific responses.

![multi-select as comma separated fields](https://cdn.zapier.com/storage/photos/02fd5f03f00a7e3c6953c95366013473.png)

Or, return all the selected values in a single, comma separated response. Users can then easily split the responses themselves with Zapier's [Formatter](https://help.zapier.com/hc/en-us/articles/8496030096013-How-to-use-Formatter-Functions#using-split-text-0-3) tool, or could map the responses together to another field.

#### Date fields

![Date field from form](https://cdn.zapier.com/storage/photos/291cb5f3b048bcf6cda769f93408128d.png)

Return the timestamp when the response was completed, at a minimum, in [ISO 8601 format](https://platform.zapier.com/publish/intergration-brand-design-guidelines#date). Also return any dates users can select in the form or survey in ISO 8601 format.

Consider also including a human-friendly date for the response completion and any other selected dates from the form.

#### File attachments

If users can attach files to form responses, include those in the response data as well. Zapier can request the full file via [file dehydration](https://zapier.github.io/zapier-platform-cli/#file-dehydration), or your app can return a URL for the file.

### Technical configuration

#### REST hooks

If possible, use [REST hooks](https://platform.zapier.com/build/trigger#rest-hook-trigger) for your trigger, as they will send new form entries to Zapier as soon as the form is filled out. If you have a lot of form entries in a short space of time, webhooks can make your integration more robust, as with polling, there is a chance the number of new entries will exceed your page size of polling results. Additionally, with REST hooks, Zapier won't repeatedly poll your API to check for new responses.

The format of the key/values in a hook should match the format for a polling URL item.

#### Polling URL

If using a Polling trigger, or for the _Perform List_ URL for REST hook triggers, the Polling URL should return the most recent form entry for the chosen form. That lets users set up a Zap using a real entry they recognize.

If there are no entries, you should return an empty list rather than a hard coded sample. We recommend this because every form/survey will be unique to each user, so there’s no way to provide usable static sample data for forms.

#### Sample Results

Zapier requests sample results for every trigger and action, so users can still set up Zaps even if the test API call returns no data. However, with a form app and their dynamic fields from users, it's impossible to define sample fields that work for every form.

Instead, include the bare set of common form fields from every result, such as the form ID and timestamp.

### Form or survey tntegration test checklist

Once you’ve built a “New Form Entry” trigger, make Zaps for the following items to ensure your integration works well:

* A form that already has completed entries, where you should check that your polling URL is returning the latest form entry first (reverse chronological)
* A brand new form that has no entries, where you should make sure your form sends an appropriate error
* A form that is composed of required and optional questions, where you should make sure all the questions are mappable regardless of whether the latest response only had a few questions answered.
* A form that has questions with multi select answers, where you should choose one or more options to check that all the values come through

Then submit new entries to your form to check that the Zaps run as expected when turned on.

<a id="crm"></a>

## Add a CRM or contacts app to Zapier

CRM—or customer relationship management—apps are more than just a list of contact details. They're detailed databases that link contacts with companies, companies with deals, and more. That makes them a bit more tricky to integrate with Zapier than many other apps where each bit of data stands alone.

Here are things to keep in mind to make your CRM integration deliver the experience your users expect.

### Triggers

#### Include triggers for every common ttem

Users typically expect the following types of triggers for CRM apps. If your app uses a different name for these items, use the name that appears in your UI so your customers know exactly what to expect:

* New Contact (also: Person, Lead)
* New Deal (also: Opportunity)
* New Company (also: Organization)
* New Tag
* New Note
* New Tag Added to Contact
* New Contact in View (also: Filter)—useful to trigger when contacts meet specific criteria
* New Deal in Stage (also: Group, Segment, or Contact in Stage)—useful to trigger when a deal progresses, if your CRM includes a way to track deal stages

#### Use Separate new and updated triggers

Use "New x" triggers only for new items. If you want a way to track updated items, add "Updated x" triggers for those items. That way users can build Zaps that fit their workflows depending on if a contact is new or updated.

#### Include filter options

![Filter options in a CRM](https://cdn.zapier.com/storage/photos/5dddfc827be95b7125cec7c27ab716bc.png)

Some apps, such as Pipedrive and Salesforce, let users add custom filters or views. If your app has this ability we recommend displaying an optional [dynamic dropdown](https://platform.zapier.com/build/input-designer#how-to-add-dynamic-and-custom-fields) of the user’s filters. That way, they can use existing filters instead of re-creating them in Zapier.

Ordering the dropdown list by most recently added so users can easily find the filter or view they need.

### Technical configuration

#### REST hooks

We recommend you use [REST hooks](https://platform.zapier.com/build/trigger#rest-hook-trigger) if possible, so new contacts start Zaps as soon as they're added. This is especially helpful if users import hundreds of contacts to your app, which a paging trigger's API response may not be able to handle.

#### Update Triggers

Updated triggers should run whenever an item has new data added, or when relational data is added or removed. If you are using REST hook triggers, which we recommend, ensure that when relational data is reapplied your app sends Zapier that updated record.

If you are using polling triggers, this may cause issues with [how Zapier performs deduplication](https://platform.zapier.com/build/dedupe), as we don’t consider the status, stage, or tag to be newly applied to that contact anymore. You may need to customize your API call's code to add a timestamp to the id field you’re using for deduplication so that the Zap triggers each time the record is updated.

### Trigger response format

#### Polling URL

The polling URL should return the most recent record created, so users can set up their Zap using a real entry they recognize.

If there are no recent new records, return an empty array. Zapier will then encourage the user to create a sample then re-test their trigger and finish mapping their Zap.

#### Obtaining linked information 

Records in CRMs don't stand alone—they are only one part of a linked ecosystem of data. Getting the full context of linked information is useful. For example, if your trigger is "New Contact" and newly added contacts are linked to organizations, users expect to get full organization data, too.

Linked information should include both IDs to easily map them to your app’s action steps, as well as human-readable data such as individual fields for their name and contact info.

If your record API endpoint does not automatically return additional linked data beyond the ID or name of the record, you will need to add custom code to your trigger API call to fetch the linked record as well.

#### Custom fields

If your customers typically use custom fields, make sure Zapier pulls in every custom field with [pagination](https://platform.zapier.com/build/trigger#how-to-use-pagination).

#### Tags

If possible, return tags on records as an array of strings or a comma-delimited list in a single string, so users will be able to easily map them into other apps.

### Searches

#### Include common search actions

Users typically expect to have the following searches for a CRM integration:

* Find Contact (also: Person, Lead)
* Find Deal (also: Opportunity)
* Find Company (also: Organization)

Each should find an existing record, and return it in the same format that the trigger returns records. This ensures that the user gets a consistent experience and can use data from triggers and searches the same way.

### Offer multiple search options

![Infusionsoft Zapier Search Options](https://cdn.zapier.com/storage/files/5395ac18091a4fe7506d5b5e4a8ced60.gif)

If possible, let users search for items by a search key as well as a search value. The search key should be a static dropdown of different fields users can search by, followed by a text input field where users can add the text or item they wish to search for.

For a "Find Contact" search, for example, consider letting users search by Email, ID, or Name.

### Prevent deduplication problems

If your CRM doesn’t allow multiple records that have the same value for a field (such as email), consider offering only a single search query for that field instead of providing multiple options. This prevents users from searching on a different field, trying to create a new record, and then being told that a record with that email already exists.

### Offer parity across triggers

Ensure that the field(s) you offer for search are fields that are returned by the trigger steps. For example, a user might use a *New Contact* trigger, and then want to find out more information about the organization the contact is associated with by using a *Find Organization* search. If the *New Contact* trigger only provides the associated organization ID, it doesn’t make sense for the *Find Organization* search to only allow searches for the organization name.

In the same vein, include linked information in search results as in triggers.

#### Error handling

![Halt a Zap instead of showing an error](https://cdn.zapier.com/storage/files/a57ed995196cb44caf4dd813ac6c60aa.gif)

If a record cannot be found, ensure that it returns a halted exception instead of an error. That way, you can pair the search with a _Create_ action to let users search for items and create them if they don't exist.

*→ Learn more about [searches and creates](https://platform.zapier.com/build/search-create-action).*

### Actions

#### Include common create actions

Users typically expect to have the following types of create actions for CRM apps, with either *Create* or *Add* as the first word in the title:

* Create Contact (also: Person, Lead)
* Create Deal (also: Opportunity)
* Create Company (also: Organization)
* Create Note

It’s also useful to include Update actions, as information on records in CRMs tend to change frequently. Any Update action you include should have a corresponding Search action to make it easier for users to update the correct record. For example, an *Add Contact to Stage* create action needs to be paired with a *Find Contact* search.

* Update Contact (also: Deal, Person, Opportunity, Lead)
* Update Company (also: Organization)
* Add Tag to Contact
* Add Contact to Stage (also: Group, Segment)
* Add Contact to Workflow (also: Sequence, Follow-up, Campaign)

You don't need to add all of these actions in the first version of your integration, but over time these are all actions that may be good to add into your integration

#### Allow linked records

![Linked Record](https://cdn.zapier.com/storage/photos/19fad8f7f1b3ae44be4425760901329c.png)

Your CRM integration will be especially powerful if users can link other record types when creating a record. For example, in your app’s UI, users may be able to create a contact and link it to existing companies or stages. Offer the same through Zapier, with [dynamic dropdown](https://platform.zapier.com/build/input-designer#dropdown) to fetch the linked record options and let users select them. Also, link it to a search, so users can either manually select an item, have Zapier find the correct item for this record, or map an ID from a previous step to this field.

That said, do not have one action create multiple items. When a user creates a new contact through Zapier, this should only create new contacts, and should not also create other linked records at the same time. Instead, include a separate action to create the other linked record, along with a contact update action to link the contact after the other record is created. This reduces the chance for errors and record redundancy.

#### Bring in all custom fields

Custom fields should be displayed with a human-readable label instead of the internal ID. If the custom fields are radio selects, booleans, or can only accept certain values, add them as [static or dynamic dropdowns](https://platform.zapier.com/build/input-designer#dropdown) in Zapier.

#### Support workflows

![CRM workflows in Zapier](https://cdn.zapier.com/storage/photos/ce412bf1bf164bdcde6f624c3ec59fe8.png)

If your app has the lets new records get automatically added to in-app workflows, sequences, follow-ups, or campaigns, make sure records created by Zapier will also get automatically added to workflows. You can also add a boolean field to your action input field to let users select if they want this contact added to a workflow, or include a dynamic dropdown to select the workflow they want.

### CRM integration test checklist

Once you've built your CRM integration, create Zaps for the following scenarios to test your integration and ensure it works as expected:

* Add a record with many custom fields, and make a Zap to watch for new records to make sure each field comes in and what they look like in subsequent steps.
* Make a multi-step Zap (we recommend one trigger, search, and action step) where every step uses your app integration, to check the ease of linking one step to another.
* If you have the option to link records in your integration's actions, check to see that these are linked correctly when creating records.

<a id="pm"></a>

## Add a project management or tasks app to Zapier

You often can't automate the work in your projects, but you can automatically add tasks, spin up new projects, and keep track of what's done with a Zapier product management app integration. Here are the things your users will expect in your integration

### Triggers

#### Include popular triggers

Be sure to include at least the following triggers, depending on what your app supports:

* New Project
* New Task (also: Todo, Subtask, Card)
* New File
* New Comment (also: Note)
* New Event
* New Account (also: Member)

![new activity trigger](https://cdn.zapier.com/storage/photos/77fad901c962b2ef853f01c88e4b1d7c.png)

You could also consider including a _New Activity_ trigger, with options to let users choose which type of activity should trigger the Zap. That can be helpful in fitting project management activity into wider workflows.

Then, consider adding update triggers as well. More than in most other apps, users really want to see updates triggers in project management integrations because updates affect their work. They need to know if the task deadline changed, if details were added or the scope was redefined, or if someone completed something. And if they're using multiple task apps, they need Zaps that can move the changes. Here are some popular update triggers to include:

* Updated Project
* Updated Task (also: Todo, Subtask, Card)
* Updated Event
* Completed Task
* Completed Project
* Project moved to Stage (also: Project Changed Status)

#### Watch out for permissions

Project Management apps are typically used in a team, so it’s important to ensure that Zaps also trigger on teammates’ activity. For example, if user A creates a Zap that collects comments on projects, they’ll want to know if user B comments on projects as well. 

Permissions may also fluctuate depending on if someone is an admin/creator of a record or not. Typically users expect to be able to automate off any record that is shared with them, regardless if they’re an admin/creator or not, so we strongly recommend ensuring that any trigger behavior encompasses all updates that are visible to a logged-in user in the UI. For example, if I can see that a teammate has made an update to a Project that we are all assigned to, their updates should trigger Zaps connected to my account as well.

If this is not possible with your API, we recommend making this clear in the Trigger description. For example, for a _New Note_ trigger, add help text such as "Triggers when the connected user account adds a note to a project."

#### Include trigger options

![Trigger Options](https://cdn.zapier.com/storage/photos/4fad8819e9d09ca9fc3b590afe64d947.png)

Add Trigger options so users can select which records they want to receive. For example, a *New Task* trigger could trigger when tasks are added to any project *or* to one specific project. Include [dynamic dropdowns](https://platform.zapier.com/build/input-designer#how-to-add-dynamic-and-custom-fields) to fetch accounts, projects, lists, and other items users would want to filter.

Order the dropdown list by most recently added to make it easier for users to find their current project.

#### Obtain linked information

![Linked Data in Podio Zapier](https://cdn.zapier.com/storage/photos/8ec62dd77f8278ff1626b9c2cf1be47d.png)

Project Management apps, much like CRM apps, are powerful thanks to linked data. Users expect triggers to include any data linked to an item as well. If the data is visible in that item in your app, they expect to use it in Zapier as well. For example, a "New Task" trigger should include details about the task's project as well.

Linked information should include IDs to map to your app’s action steps, as well as human-readable data including the project name and description.

If your API doesn't return linked data by default, add custom code to your API call to make a secondary request for the linked data.

### Searches

#### Include popular searches

Users typically expect to be able to find the broader items that organize their projects, including:

* Find Project
* Find Account (also: Member)
* Find Event

Users will typically want to find top-level records so they can add child-level details. For example, a Project can have many Tasks, and some projects may have the same or similar tasks. Users are more likely to want a *Find Project* search so they can add tasks to projects, rather than a Find Task search which may not return the precise item they need.

Searches should find an already existing record, and return it in the same format and with the same data as triggers use, for a consistent experience.

#### Offer multiple search options

![Project Management Search Options](https://cdn.zapier.com/storage/photos/df5c2a77049abfa967e32f043d14811e.png)

If possible, offer multiple ways to search for items, with a dropdown menu to select the search key and a text field to enter what to find. For example, a *Find Project* search should let users search by project ID and name. The former is useful for searching based on data in previous steps, where the latter is useful to find projects with human input.

Additionally, project name searches should exact matches first. It’s likely that users will have similarly named projects, for example, "Promotional Advertisement November" and “Promotional Advertisement September.” Be sure to note how your app returns search results in the help text, as in the Asana screenshot above.

### Actions

#### Include popular create actions

Users typically expect to be able to create everything they could in your app. Use *Create* or *Add* to prefix each action:

* Create Project
* Create Task (also: Todo, Subtask, Card)
* Create File
* Create Comment (also: Note)
* Create Event

Because projects are very dynamic and are often organized across several apps, we strongly recommend adding updates actions as well, such as:

* Update Project
* Complete Task (also: Todo, Subtask, Card. You might try "Update Task Status" if it’s appropriate for your API as well.)
* Update Event

#### Let user link records

![Create Action Search](https://cdn.zapier.com/storage/photos/acd4cd6c45be3b17d74b597c1327f282.png)

Your integration will be especially powerful if users can link other record types when creating a record. For example, in your app’s UI, users may be able to create an Event and link it to existing Project. They will want to do the same in Zapier, so include a [dynamic dropdown](https://platform.zapier.com/build/input-designer#dropdown) where they can select items to link. Also try to include searches for each linked record type to let Zapier automatically find the correct item to link for users.

Only create one record with one Zapier action, though. When a user creates a new Event through Zapier, this should only create new Events, and should not also create other linked records at the same time. This reduces opportunity for error as well as record redundancy for the user.

### Project management integration test checklist

Once you've built your project management app integration, set up a few Zaps to test out popular scenarios:

* Connect your integration with [other project management apps](https://zapier.com/apps/categories/project-management), to see if the data your integration returns blends well with our common apps. Companies frequently use integration to copy tasks and projects across a blend of project management apps to keep track of work between teams.
* If your integration supports events or tasks with due dates, try connecting them to a popular [calendar or scheduling app](https://zapier.com/apps/categories/calendar) to see if they integrate well.
* If your integration has many nested items (such as projects containing sub-projects with tasks and sub-tasks), try setting up a few Zaps to see if the behavior across nested objects is the same as parent objects. Data returned should always be the same format; if your API doesn’t enable access to nested objects, note that in the help text for that trigger/search/action.