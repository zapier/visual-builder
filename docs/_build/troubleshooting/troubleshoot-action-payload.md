---
title: Troubleshoot action payload size
order: 5
layout: post-toc
redirect_from: 
    - /build/operating-constraints#payload-size-actionssearches
    - /build/operating-constraints#payload-size-actionssearches-1
---

# Troubleshoot action payload size

## Testing action in Zap editor

### Constraint 

When a user clicks **Test and Review** or **Retest and Review** in the Zap editor, the response payload must be less than 6MB.

### Errors user will see if constraint is hit

- _“Scripting payload too large ('n' bytes but max is 6291456bytes).”_ - ('n' is the number of bytes in the payload.)

### Best practice

If your API endpoint supports request filtering, one option is to provide input fields in the action/search so a user can decide what record field data they want to return. If that is not available, you might look at having multiple endpoints for this record data. Your integration could then provide multiple action/searches for the user so they can get a full record.

## Action runs in a Zap

### Constraint

An action/search response payload must be less than 6 MB.

### Errors user will see if constraint is hit

- _“Scripting payload too large ('n' bytes but max is 6291456bytes).”_ - ('n' is the number of bytes in the payload.)

### Best practice

Use the simplest available endpoint on your API for the basic record data, and use Zapier platform [dehydration](https://platform.zapier.com/reference/cli-docs#dehydration) to request supplementary data from other endpoints. A dehydration pointer is created for each subsequent request, and this pointer will only be resolved if the Zap needs a hydrated property in a later step.