---
title: Change input form field key
order: 7
layout: post-toc
redirect_from: /manage/making-changes#changing-form-field-keys
---

# Change input form field key

## Change scenario

You want to change the key of one or more form field inputs within a trigger, action, or search.

## Impact to users

Modifying the key of a form field input is a breaking change.

Unless precautions are taken, changing the key of an existing form field input will break the field’s mapping within the step using it. The previously-mapped value will be dropped, resulting in missed data and/or errors.

## Best practices

- Avoid changing form field input keys

If your API endpoint needs a different property in the request, consider changing the property key instead of modifying the form field input’s key.

Form field input keys do not necessarily need to match the properties expected by your API.

Let’s say you have a form field input with the key `first_name` (right) and are sending the field’s value to your API using a property with the same name, `first_name` (left):

![example one](https://cdn.zappy.app/cf7d34d12c1a1c42f75a89815409d20e.png)

```js
body: {
  first_name: bundle.inputData.first_name; // original
}
```

Then, your API changes and expects the request property to be `firstname` (one word) instead. As shown below, you can change the request property key (left) as needed (`firstname`) while still referring to the form field input (right) based on its original key (`first_name`):

![example two](https://cdn.zappy.app/b6b1776d964f52eed12d64ff264b8cac.png)

```js
body: {
  firstname: bundle.inputData.first_name; // new - request key and field key can differ
}
```

- Handle both the old and new keys

If it’s not possible to simply change a hardcoded request property’s key:

We recommend that you design the trigger or action to handle both the old and new key

Using the same example above, let’s say that instead of hardcoding your request properties, you were spreading `bundle.inputData` into the body of the API request, so there was a one-to-one relationship between field keys and request properties.

```js
body: {
  ...bundle.inputData // original - request keys tied to field keys
}
```

Instead of changing form field input keys, you can use Code Mode (Platform UI) or code (Platform CLI) to modify the request.

For example, below, we create a new object, payload, with all the fields from `bundle.inputData` AND the updated property, `firstname`. Then we delete the old property, `first_name`, and send the updated object in the request:

```js
// copy bundle, add updated property
const payload = { ...bundle.inputData, firstname: bundle.inputData.first_name };

// delete old property
delete payload.first_name;

body = {
  ...payload, // send updated payload
};
```

With this approach, or one like it, you can change the request as needed without modifying field keys and breaking users’ mappings.