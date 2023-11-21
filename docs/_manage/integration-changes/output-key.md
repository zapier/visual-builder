---
title: Change output field key
order: 8
layout: post-toc
redirect_from: /manage/making-changes#changing-output-field-keys
---

# Change output field key

## Change scenario

You may want to update or remove existing output field keys in your Zapier integration. This can happen when you need to clean up output data, remove unnecessary fields, or due to changes in your API's response data.

## Impact to users

If a user has mapped one of the affected fields to an input field in a subsequent step of their Zap, the change can affect that step and potentially the entire Zap's functionality. Imagine if you updated the output field key or removed an output field altogether that a user had mapped to a required field in the next step of their Zap - the step would now error every time.

## Best practices

To minimize disruptions to your users, follow these best practices when updating or removing existing output field keys:

- Remove extraneous fields carefully: If you're cleaning up output data and removing non-essential fields (such as HTTP request data like 'request type' or 'request URL'), you should be able to safely remove them. Be cautious and avoid removing fields that users might have mapped to required fields in subsequent Zap actions.
- Maintain backward compatibility: If you're using the Zapier Platform CLI, you can use custom code to ensure backward compatibility with updated response data from your API. Modify the perform methods in your code appropriately to handle these changes.
- Update the static sample: When you have made any changes to output fields, make sure to update the [static sample data](https://platform.zapier.com/build/sample-data) accordingly. This ensures that the sample data used for testing and Zap setup by users remains accurate.