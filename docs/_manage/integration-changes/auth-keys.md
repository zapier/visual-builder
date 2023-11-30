---
title: Change authentication field keys
order: 4
layout: post-toc
redirect_from: /manage/making-changes#changing-authentication-field-keys
---

# Change authentication field keys

## Change scenario

You want to change the key of one or more [authentication input fields](https://platform.zapier.com/build/basicauth#1-build-an-input-form) required when a user authenticates your app to Zapier.

## Impact to users

This is a **breaking change**.

Modifying the key of an existing authentication field constitutes a breaking change. Without adequate precautions, existing app connections may break as [migration](https://platform.zapier.com/manage/migrate) is not possible. Users will need to establish a new connection to your integration and manually refresh each of their Zaps.

## Best practices

We strongly encourage you to **avoid changing authentication field keys** whenever possible.

### Workaround

If your API endpoint requires a different property for authentication, think about adjusting the property key rather than amending the form field input’s key.
This modification must be made in each trigger, action, search request, as well as in the authentication.

>NOTE: Form field input keys do not need to match directly with the properties your API expects.

For example, let's say you have a form field input with the key `API-KEY`and are sending the field's value to your API using the same property name of `API-KEY`. 

![](https://cdn.zappy.app/daef0487a89a2cbb17ec719cbbd50577.png)

```
headers: {
  "API-KEY": bundle.authData.api_key; // original
}
```

Next, your API changes and expects the request property to be `X-API-KEY` instead. You can change the request property key (left) as needed. But still refer to the original form field input (right). 

![](https://cdn.zappy.app/bf4cdfe3183752e0e57707001260e9e3.png)

```
headers: {
  "X-API-KEY": bundle.authData.api_key; // new - request key and field key can differ
}
```
