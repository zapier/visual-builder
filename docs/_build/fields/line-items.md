---
title: Add line item group field to actions
order: 4
layout: post-toc
redirect_from: 
---

# Add line item group field to actions

Input fields in Zapier add one item each time the Zap runs. But, if you want users to be able to add multiple items in a single Zap run, then this can be achieved by using a line item group. This group takes line items, which are comma-separated values, and adds each instance of the values to the app in a single Zap run. 

> **Tip**: Learn more about line items from Zapier’s [guide](https://zapier.com/blog/formatter-line-item-automation/) and [help documentation](https://help.zapier.com/hc/en-us/articles/8496277737997).

Line items can be challenging for users to work with as a concept, so make sure to consider what a user would be inputting and do not add line item group fields unless there is a clear use case for them.

## Before adding a line item group

Before adding a line item group to an action:

- You should have already added an [action](https://platform.zapier.com/build/action) where this line item group would be added.
- Your app’s API should be able to accept and work with line item values.


## Add a line item group

To add line item group to an action:

1. Log into the [Platform UI](https://zapier.com/app/developer).
2. Select your **integration**. 
3. In the _Build_ section in the left sidebar, click the **name of your action**.
4. Click the Input Designer tab
5. Click **Add <img style="vertical-align: middle;" src="https://cdn.zapier.com/storage/photos/9f549e9320881f1dcda37fce73ace8ca.png" alt="Arrow down icon" width="24">** dropdown menu and select **Line Item Group**.
6. In the **Line Item Group Label** field, add a name for the Line Item Group. This should be something users would recognize as being a set of values where each one would be added individually.
4. In the **Line Item Group Key** add a key for the Line Item Group. This will let Zapier identify this group internally.
5. Click the **Add Line Item** button. 
6. Add in the relevant fields as you would for a [input field](https://platform.zapier.com/build/input-designer#add-fields). Each field that you add here will be received as line item values. Note the *Allows Multiples* and *Alters Dynamic Field* options will not appear as those options cannot be used in line item fields as they are mutually exclusive.
7. After adding all the line item fields, click **Save**.

Your new Line Item groups will show up in the Zap editor as a separate block with the different line item input fields within:

![](https://cdn.zappy.app/41f81ef42d5101767810a9ffc5626e95.png)

Users will need to map line item values from earlier steps in their Zap into the fields within the line item group. They would be sent to your API as an array of individual objects. Users cannot input comma separated values into a line item field, they need to be provided from the trigger or a prior action in line item format for them to be sent this way. 

![](https://cdn.zappy.app/533efc7f7719fa85587f72b04204371f.png)

![](https://cdn.zappy.app/a7bad08984545eb39e96ed2782660737.png)