---
title: Defining sample data and output fields
order: 5
layout: post-toc
redirect_from: 
    - /build/faq#how-do-sample-data-and-output-fields-work
    - /build/faq#output-fields
    - build/faq/#output-fields
---

# Defining sample data and output fields

This guide will explain what sample data and output fields are and how to modify them in your triggers or actions. 

## Sample data

Sample data gives Zapier example data if users don't test the trigger or action. Though optional, it is especially important for triggers and also useful in actions. 

In the Zap editor, Zapier will attempt to retrieve or create existing data to test triggers and actions. With triggers, Zapier will try to fetch recently added or updated items during the test. If the connected account doesn’t have any data for this item (polling triggers) or the Perform List is not defined (REST Hook triggers), the user will see an error that no items are available.

Users can also opt to skip those test steps. In both cases, Zapier shows the sample data instead, to allow users to map fields correctly in subsequent Zap steps. 

![Trigger step with no available live sample data](https://cdn.zappy.app/05e9be8a62a663f42ab25cf2b17591b8.png)

![Sample Data in subsequent Action step](https://cdn.zappy.app/42353c3702ca94af6000e3efb926a3f2.png)

Sample data must be JSON-formatted and use the same field names as your app's API. Either click the _Use Response from Test Data_ button to import the fields your app sent to Zapier in the previous test, or add your own JSON-formatted fields. No personally identifiable data should be included, and the copy must be safe for work. 

Only include fields that are present every time a Zap runs. If a field is provided in the sample, it can be mapped into a field in a later action by any user.

If that mapped field is then not available when a user's Zap runs, the action field will be empty, causing errors or unexpected results for users. For example, suppose your sample data looks like this:

```json
{
  "id": 1,
  "first_name": "Jane",
  "last_name": "Suarez",
  "email_address": "janesz@example.com",
  "job_title": "Executive Director"
}
```

A user might map the `job_title` information into a required field in another app, such as a CRM. Then, when the Zap runs, `job_title` is only included in the live result if it happens to be available, and the data the Zap receives looks like this:

```json
{
  "id": 5,
  "first_name": "Jacob",
  "last_name": "Giotto",
  "email_address": "jacob@example.com"
}
```

The user's Zap run will error when the request to the CRM's API attempts to add the person, because `job_title` is a required field in the CRM but there's no data in it. To avoid this, there are several [integration checks](https://platform.zapier.com/publish/integration-checks-reference) that require sample and live Zap run data to match.

## Output fields

Output fields give your API's response data user-friendly labels in subsequent Zap steps.

By default, Zapier uses a basic human-friendly transformation of field names, capitalizing words and adding spaces instead of underscores. You can customize this further with Output Fields.


## How to modify your sample data and output fields


In your trigger or action settings:
1. Click *Step 3 Define your Output* to expand this section.
2. In the *Sample Data* field, add in your **JSON formatted sample data output**.
3. Click **Generate Output Field Definitions**. 
4. In **Output fields** you'll see a table of fields with keys on the left, and field types on the right. Add a **human-friendly name** for each field in the center Label column, and select the **field type** in the right hand column.
5. Click **Save Output & Finish**.

For example, if you use GitHub's API to watch for new issues, the API calls the issue name `title`. Users may expect that field to be called _Issue_ or _Issue Title_, so you could define the Output Field as having the name _Issue Title_, rather than the default transformation of "Title". 


![Adding Sample Data to Zapier integration](https://cdn.zappy.app/293b09e9593b591de3c735988f1a5f19.png)