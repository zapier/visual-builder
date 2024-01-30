---
title: Field definitions and types
order: 1
layout: post-toc
redirect_from: 
    - /docs/input-designer
    - /build/input-designer 
---

# Field definitions and types

Three types of fields exist for users to see in the Zap editor: 

- Input fields
- Dynamic fields
- Line item groups

## Input fields

Input fields are most commonly used and include 9 types that look and act differently in the Zap editor. Depending on the type, users can either enter plain text data, make a selection or map variables from previous triggers and actions. Zapier does not validate the data to ensure users added the correct item for that field type.


### String
The default input field, which accepts text input. Typically used to gather individual text values such as a name or email address.

![Zapier String Field](https://cdn.zappy.app/b6abd9f3b9048e4a0b8010c79ac78ca7.png)

### Text
Displays large, `<textarea>`-style entry box, accepts longer text input. Often used to enter notes.

![Zapier Text Field](https://cdn.zappy.app/6936573528e1c7dc72b33e5b8178aac7.png)

### Integer
Accepts integer number values, shown with a `1 2 3` tag beside the field in Zaps. Typically used along with a dropdown type field to select ID numbers for objects in your app, also used to gather whole numbers.

![Zapier Integer Field](https://cdn.zappy.app/4c3d21a485c1329720209fa9ee1664f7.png)

### Number 
Accepts any numeric value, including decimal numbers, shown with a `1.0` tag beside the field in Zaps.

![Zapier Number Field](https://cdn.zappy.app/0d149da9dd979e6aa0a628a1a4abf2b7.png)

### Boolean 
Allows users to select between `yes` and `no` values in a dropdown in their Zap to send a corresponding `1` or `0` in the request to your app's API.

![Zapier Boolean Field](https://cdn.zappy.app/da36e8486e9aec5d685650be5c5b194d.png)

### Datetime 
Accepts both [precise and human-readable date-time values](https://help.zapier.com/hc/en-us/articles/8496259603341-Different-field-types-in-Zaps#date-time-fields-0-0). Sends an [ISO-formatted](https://www.iso.org/iso-8601-date-and-time-format.html) time string in the request to your app's API.

![Zapier DateTime Field](https://cdn.zappy.app/68097e2927567b360f9fb9b65647369c.png)

### Password
Displays entered characters as hidden, accepts text input, just like standard string fields. Does not accept input from previous steps.

![Zapier Password Field](https://cdn.zappy.app/872c6d1ce250bb054460643701df646a.png)

### Dictionary
Users enter their own value sets, with a plain text name followed by a String field to enter or map data from previous Zap steps. Click the + button on the right to add additional dictionary field entries.

![Zapier Dictionary Field](https://cdn.zappy.app/74689dc7f73a75c3cf5ab9b858f651b1.png)

### Copy 
Does not allow users enter data and is not passed to your app's API. Shows the Help Text field copy in a display-only formatted note, with no input field. Supports [Markdown](https://zapier.com/blog/beginner-ultimate-guide-markdown/). Typically used for important notices to users. 

![Zapier Copy field](https://cdn.zappy.app/eebc20fad3362197a0448edd8a52e27e.png)

## Dynamic fields

Dynamic fields make a request to your app's API, showing the returned data in a dropdown menu in live time. Users select the object needed. Typically used for folders, projects, assignees, and other data that would need to be chosen from within your app. Only available in Platform UI actions. 

## Line item groups

Line item groups allow users to input line items provided from the trigger or prior action. Those items will then be sent in the request as an array of individual objects. Users cannot input comma separated values into a line item field, they need to be provided from the trigger or a prior action in line item format for them to be sent this way. Typically used to add multiple lines of similar details to an app, for example in invoice and accounting apps. Only available in [Platform UI actions](https://platform.zapier.com/quickstart/ui-vs-cli). 