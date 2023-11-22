---
title: Zapier integration structure for a CRM app
order: 2
layout: post-toc
redirect_from: 

---

# Zapier integration structure for a CRM app

CRM (customer relationship management) apps are detailed databases that link contacts with companies, companies with deals, and more. 

To add a CRM app integration in the Platform UI:

## Prerequisites 

- A [Zapier account](https://zapier.com/sign-up).
- If you haven’t used Zapier before, you'll want to learn the basics in our [Zapier Getting Started Guide](https://zapier.com/learn/zapier-quick-start-guide/).
- Familiarity with your app's API documentation and available endpoints.
- Review the [Platform UI Tutorial](https://platform.zapier.com/quickstart/ui-tutorial). 

## 1. Add triggers for common record types in the CRM

- Check out the [common record types](https://platform.zapier.com/build/recommended-integration-features#crm-customer-relationship-management) used as triggers by other CRM apps. 

- Build separate triggers for new and updated records. _Updated_ triggers for CRMs are most useful when users are able to specify which field(s) to watch for updates on, instead of triggering on any and all updates.

- Include filter options if your app lets users add custom filters or views. Displaying an optional [dynamic dropdown](https://platform.zapier.com/build/input-designer#dynamic-dropdown) of the user’s filters and ordering them by the most recently added is best practice. 

![Filter options in a CRM](https://cdn.zappy.app/6bb177088b4a484c7b72842a05177d5b.png)

## 2. Choose trigger type under API Configuration

### REST Hook trigger

- If your app supports webhook subscriptions that can be manipulated through a REST API, use [REST hooks](https://platform.zapier.com/build/trigger#rest-hook-trigger) for your trigger to send new records to Zapier as soon as they are added to the CRM.  

- Webhook triggers are marked as _Instant_ [in the Zap Editor](https://cdn.zappy.app/6b696dfaf34664b181b6df651067cfd3.png).  

- When your user has many app records created in a short space of time, webhooks make your integration more robust, preventing the possibility that a high number of new records will exceed the page size of polling results. 

- With REST hooks, Zapier won't need to repeatedly poll your API to check for new responses.

### Polling trigger

- When using a Polling trigger, and for the _Perform List_ URL for REST Hook triggers, the Polling URL should return the most recent record created or updated (if the trigger is an 'Updated Record' trigger)

- If there are no recent new records, return an empty array. Zapier will then encourage the user to create a sample and re-test their trigger in the Zap Editor to finish mapping their Zap.

## 3. Additional considerations for Updated Record triggers

- Users expect updated triggers to run whenever a record has new data added, or when relational data is added or removed. 

- For REST hook triggers, ensure that when relational data is reapplied to a record, your app sends Zapier that updated record.

- For polling triggers, to account for [deduplication](https://platform.zapier.com/build/dedupe), you will need to customize your API call's code to [add a timestamp](https://platform.zapier.com/build/dedupe#custom-or-multiple-id-fields) to the `id` field that is used for deduplication to trigger the Zap each time the record is updated.

### Include linked information in trigger response

- CRM records are one part of a linked ecosystem of data. For example, if your trigger is "New Contact" and newly added contacts are linked to organizations, users expect to see full organization data, too.

- Include both IDs for linked data in the response output so they can be mapped to your app’s action steps, as well as human-readable data such as individual fields for their name and contact info.

- If your record API endpoint does not automatically return additional linked data beyond the ID or name of the record, add custom code to your trigger API call to fetch relevant data linked to the record as well.

### Handle custom fields

- Use [pagination]((https://platform.zapier.com/build/trigger#how-to-use-pagination) to retrieve custom fields a user might expect.

### Handle tags

- Return tags on records as either an array of strings or a comma-delimited list in a single string, for users to be be able to easily map them into other app actions.

## 4. Include common search actions

- Users expect to have searches for common records available for CRM integrations and for those searches to have parity with the fields returned for those same record triggers. For example, a user might have a _New Contact_ trigger, and then want to find out more information about the organization the contact is associated with by using a _Find Organization_ search. If the _New Contact_ trigger only provides the associated organization ID, it doesn’t make sense for the _Find Organization_ search to only allow searches for the organization name.

- Configure the search to find an existing record, returning it in the same format the trigger returns records to give a consistent experience and allow the data to be used in the same manner in later actions.

- Offer multiple search key and value options where applicable. 

![Pipedrive Search Options](https://cdn.zappy.app/8b3b564da528667a3b0fc57fb105edfa.gif)

- Prevent deduplication problems for unique fields (such as email) though, by offering only a single search query for that field instead of multiple options. This prevents users from searching on a different field, trying to create a new record, and seeing an error that a record with that email already exists.

- If a record cannot be found, do not return an error. Instead return a `200` success response with an empty array. That way, users can pair the search with a _Create_ action to let users search for records and create them if they don't exist. Users will see a halted exception instead of an error. 

![No result found in Search](https://cdn.zappy.app/5e0bd80c41a78719f140e2382454cf99.gif)

_ Read more about pairing [searches and creates](https://platform.zapier.com/build/search-create-action).

## 5. Include common create actions

- Check out the [common record types](https://platform.zapier.com/build/recommended-integration-features#crm-customer-relationship-management) other CRM apps have create actions for.  

- Use the standard _Create_ or _Add_ naming pattern to show users that this action creates a new record in your app

- Add corresponding _Update_ actions with available _Search_ actions to make it easier for users to update the correct record. 

- Account for linked records in action input fields, so when your app’s UI allows users to create a contact and link it to existing companies or stages, the same action is available through Zapier, via a [dynamic dropdown](https://platform.zapier.com/build/input-designer#dynamic-dropdown) to fetch linked record options and let users select them. 

- Optionally link a [search connector](https://cdn.zappy.app/103626b1313602fa33c33711ed44ff56.png) to linked record input fields if users need to have the Zap find the correct related record, and map the found ID to the input field. To add that user prompt you'll need to work in the [Platform CLI](https://github.com/zapier/zapier-platform/blob/main/packages/cli/README.md#search-powered-fields). 

- Do not have a single action create multiple records. When a user creates a new contact through Zapier, this should only create new contacts, and should not also create other linked records at the same time. Rather include a separate action to create the other linked record, along with a contact update action to link the contact after the other record is created. This reduces the chance for errors and record redundancy.

- Account for [custom fields in action input fields](https://platform.zapier.com/build/dynamic-field), displaying the human-readable label instead of the internal ID.   

- The first version of your integration doesn't need to have every possible action available, but add compatible functionality users expect or request in future updates. 

## 6. Support in-app workflows

- If new records created in your app get automatically added to in-app workflows, sequences, follow-ups, or campaigns, make sure records created via the API by Zaps will also get automatically added to workflows. 

- Optionally add a boolean field to your action input fields to let users select if they want this contact added to a workflow, or include a [dynamic dropdown](https://platform.zapier.com/build/input-designer#dynamic-dropdown) to select the workflow they want.

## 7. Test your triggers and actions

Make Zaps with the following criteria to ensure your app integration works as expected:

- Add a record in your app with many custom fields, and create a Zap to watch for new records to make sure each field is included when it triggers and is mappable in subsequent steps
- Create a multi-step Zap with at least one trigger, search, and action step where every step uses your app integration, to check the ease of linking one step to another.
- If you've included the option to link records in your integration's actions, verify these are linked correctly when creating records via a Zap.