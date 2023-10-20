---
title: Response types Zapier expects
order: 6
layout: post-toc
redirect_from: 
    - /build/faq#what-response-type-does-zapier-expect
---

# Response types Zapier expects

With every API call, Zapier expects the response data to be returned in a specific response type. This can vary depending on what part of your integration you're working on.  Use the table below to identify the correct response type to use:


| Method | Response type | Notes |
|---------|-------------|-------------|
| **Authentication** | Object | Single JSON-formatted object with any specific fields for auth scheme. |
| **Authentication testing** | Object | Object |
| **Trigger** | Array | JSON-formatted array with the results in reverse chronological order. Results are parsed and passed through [deduplication](https://platform.zapier.com/build/dedupe). Empty arrays will not trigger. |
| **Create action** | Object | Individual fields within object are parsed for mapping into subsequent Zap steps. |
| **Search action** | Array | JSON-formatted array sorted with the best match first. Only the first item will be returned. For no match found, return a `200` with an empty array.  |
 
> **Note**:
- If your app's API call does not return a response, Zapier will show a timeout error. 
- If you use line items in your integration, note that not all Zapier integrations support line items. Use the recommended response type in the table to reduce users possibility of needing to reformat this data to use in their Zaps. Learn more on [how line items work in Zaps](https://help.zapier.com/hc/en-us/articles/8496277737997). 


## Return your data as line items for search or create actions

Line items are used to present multiple items associated with a single transaction, such as an order or an invoice.  To return line items in the data for your users in their search or create actions, you'll need to return the multiple items you want to show as an array of objects under a descriptive key. This may be as part of another object (like items in an invoice) or as multiple top-level items.

For example, a Create Order action returning an order with multiple items might look like this:

```
order = {
  name: 'Zap Zaplar',
  total_cost: 25.96,
  items: [
    { name: 'Zapier T-Shirt', unit_price: 11.99, quantity: 3, line_amount: 35.97, category: 'shirts' },
    { name: 'Orange Widget', unit_price: 7.99, quantity: 10, line_amount: 79.90, category: 'widgets' },
    { name:'Stuff', unit_price: 2.99, quantity: 7, line_amount: 20.93, category: 'stuff' },
    { name: 'Allbird Shoes', unit_price: 2.99, quantity: 7, line_amount: 20.93, category: 'shoes' },
  ],
  zip: 01002
}
```

While a Find Users search action could return multiple items under an object key within an array, like this:

```
result = [{
  users: [
      { name: 'Zap Zaplar', age: 12, city: 'Columbia', region: 'Missouri' },
      { name: 'Orange Crush', age: 28, city: 'West Ocean City', region: 'Maryland' },
      { name: 'Lego Brick', age: 91, city: 'Billund', region: 'Denmark' },
    ],
  }];
```

A standard search returns only the inner array of users, and only the first user would be provided as a final result. Returning line items instead means that the first result return is the object containing all the user details within it.