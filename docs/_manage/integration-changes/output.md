---
title: Change output data response
order: 9
layout: post-toc
redirect_from: /manage/making-changes#changing-output-data
---

# Change output data response

## Change scenario

Certain changes made to a trigger, action, or search's output data structure can be breaking changes for users. Even if the output field key(s) remain the same, significant changes to the data structure or format returned from one or more of these fields can affect users’ Zaps.

Examples of potential breaking change scenarios:

- An output field representing datetime is updated to return data in ISO-8601 format instead of full date format (Thursday, April 10, 2023 6:30:00 AM)
- A `results` field in a search now returns a list of all search results instead of the single, last created result
- A previously comma-separated list value is updated to return line-items

## Impact to users

Updated output fields from your integration steps can impact the way subsequent actions run in a user's Zap when they are mapped to input fields in those actions.

For example, if a user has set up a Formatter step to parse out the day of the week from the `added_date` field before adding it to a CRM, changing the date format to ISO-8601 will cause the Formatter to process unexpected values, which may lead to issues in the user's Zap.

Another example is a user's Zap configured with a search that always returns a single result based on the latest created date in the `results` field. If the search is updated to return all results, subsequent actions in the Zap may not be set up to handle multiple results, leading to potential problems.

## Best practices

- Use custom code to add your newly formatted data to the existing output data. By doing this, you ensure that users who have already set up their Zaps with the previous data structure will not experience issues due to the changes.
- _For example:_  Add a `created_date_ISO` field with the ISO-8601 formatted created date to the output data, instead of updating the current `created_date` value to be in ISO-8601 format. Define clear [output field labels](https://platform.zapier.com/build/sample-data) to help users differentiate the fields; updates to field labels are non-breaking.
- Add an optional, boolean input field that users can toggle to choose between returning old and the new data structure. This way, users can decide which data structure best suits their needs for existing and new Zaps. Make sure to set a default value for the input field to automatically return data as your previous version did.
- If you’re looking to update a search to return multiple or all search results, instead of the default one result, create a new, separate search for the purpose. This way, users can choose which one to use without encountering issues in their existing Zaps. Differentiate the searches by pluralizing the search: “Find Lead” vs “Find Lead(s)”.