---
title: Troubleshoot custom fields
order: 6
layout: post-toc
redirect_from: 
    - /build/operating-constraints#step-configuration-with-custom-fields
---

# Troubleshoot custom fields

## Configuring the trigger/action in Zap editor

### Constraint

If your trigger, action, or search supports retrieving custom fields from your API, these are limited to 1000 custom fields, the output of the method to retrieve the fields must be returned within 30 seconds and the response payload must be less than 6MB.

### Errors user will see if constraint is hit

- Slow rendering of the step when it is added or edited in the Zap editor
- Custom fields might not display
- Not all output fields will be available for mapping in later steps
- _“The app did not respond in-time. It may or may not have completed successfully.”_
- _“Scripting payload too large ('n' bytes but max is 6291456bytes).”_ - ('n' is the number of bytes in the payload.)

### Best practice

Here is an example of the way one integration works around all three of these constraints. [Hubspot](https://zapier.com/apps/hubspot/integrations) offers a CRM product, and users often have thousands of custom fields for Company records. 

In the **_Create Company_** action, instead of presenting an overwhelming number of custom fields, they present a set of default fields that all companies have, then allow the user to select the other fields they might need from an **_Additional Properties to Retrieve_** dropdown menu field. 

The fields chosen are then retrieved by the Zap editor for user editing. This helps in both making sure the request can be accomplished within the time and size limits, and making sure the user can easily find the custom fields important to their specific workflow.

![](https://cdn.zappy.app/4ac409c47f194303c54adff79fcd693f.png)