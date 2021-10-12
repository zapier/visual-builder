---
title: Transfer
order: 23
layout: post-toc
redirect_from: /docs/
exclude: true
---

# Adding Support for Transfer

**Transfer is a beta feature and is subject to changes prior to launch.**

> ## Intended Audience
> This is a quick guide for development teams who:
>  
> - Already have a published Zapier integration
> - Understand how Zapier’s triggers, actions, and Zaps work today
> - Are interested in being among the first to try out a new Zapier feature, [Transfer](https://transfer.zapier.com/)

## What is Transfer?

Transfer is a new Zapier service that enables users to perform bulk operations using their historical data. Today Zaps only process new data and events created after the user turns on their Zap. Transfer lets users reach back and use existing data. Think of it as allowing your users to leverage Zapier for ETL (“Extract, Transform, Load”)  tasks.

Some example usage scenarios:

- A user has new email campaign software and they want to load all the leads from their CRM into it.
- A user ran a survey, but didn't build a Zap ahead of time to move those responses to their email marketing tool. They can use Transfer to reach back and pull those responses into their software of choice.
- A user wants to choose specific leads that previously ran through a Zap, and send them to a different tool.

## How Transfer Works

In simple terms, Transfer works by running Zaps, just as you’re familiar with. The difference is that normally, when a user turns a Zap on, the Zap will ignore past data, and only process future data and events. Transfer operates by pulling in all of the data from your Trigger and making it available for the user to select and send through the Zap. This will execute perhaps thousands of tasks at once.

Transfer will invoke the trigger of the Zap, repeatedly, pulling back all the data available. It then gives the user the ability to choose which of the data objects to process with the Zap. 

Transfer leverages a long-standing platform feature, API request pagination. Before Transfer, pagination was only used for triggers that populate dynamic dropdowns, enabling the “load more data” feature. Transfer calls the trigger’s perform/performList function, repeatedly, incrementally requesting additional “pages” of data until the endpoint signals it’s returned all of its data.

## Implementing Support for Transfer

**Implementation Checklist**

1. Identify which of your triggers’ API endpoints meet the requirements
1. Choose which triggers to add to Transfer
1. Identify whether your endpoint uses a page/limit approach or cursor to allow the API client to ask for more data. 
1. Write code to check whether the request is coming from Transfer, and configure a paginated API request accordingly.
1. Review and implement the best practices
1. Test your trigger using Transfer
1. Send an email to the team to get your trigger included in Transfer Beta

### Requirements

- You’ll need to have a Zapier integration published before your trigger can be made available within the Transfer tool.
- To make this work your API needs an endpoint that allows the client to fetch a large number of records. For most APIs, this means supporting paginated requests - the ability for the API client to fetch a set, or “page”, of data, then request the next set, the next set, until the end of the data set is reached.
- You’ll need to publish a trigger in your integration that is able to make paginated requests when invoked from Transfer, but also returns the most recent page of data otherwise. 
- Your integration will need to be running on the current Developer Platform, whether it’s built with the Platform UI or the Zapier CLI. Legacy Web Builder integrations are not supported. 

### Developing in the CLI vs. the Platform UI

We really recommend working with the latest version of the Zapier CLI ( >= ver 11.1.x) if you’re not already. Implementing support for pagination and any conditional request handling you might do will require working in JavaScript code, and it’s  generally easier to write and test code the CLI. The CLI also offers full support for Transfer, and will receive updates sooner than the UI as Transfer moves through Beta. 

That said, if your integration is currently based in the Platform UI, you can add support for Transfer with one narrow exception. You can also easily [move your work to the CLI](https://platform.zapier.com/docs/export), but you don’t need to do so. The instructions that follow apply equally if you’re working in the UI, assuming you switch the API configuration to “code mode”.  **If your trigger is a REST hook type trigger and your API uses cursor based pagination, you’ll need to work in the CLI to support Transfer currently.**

Legacy Web Builder integrations are not supported. The legacy platform will be end-of-lifed soon. Please migrate to the current platform to add support for Transfer.

### Page/Limit vs Cursor Based API Pagination

There’s two supported models for API pagination, and you’ll need to use the approach that fits with your API

_Page/Limit:_ Many APIs paginate by allowing the client to say “Give me 1000 rows starting at the 8000th row.” These will work by passing a page size and an offset to the API. When Zapier is invoking your API from Transfer we’ll pass you a page number in the bundle.meta.page variable. We’ll increment this value on each subsequent request. Multiply that by your page size and you’ll have the appropriate offset to use to request the next page of data that Transfer needs. 

_Cursor Based Pagination:_ Some APIs paginate with cursors. Cursors are “opaque” values, i.e. that can’t simply be derived from knowing whether it’s the first, second, third request. Each paginated API response, contains information about how to fetch the next result set. The developer needs to store the value, and on each request retrieve the cursor data from the last result in order to construct the new request. Zapier provides a utility to make this easy. When you set the canPaginate flag to true, the Platform will make available a z.cursor.get and z.cursor.set method to store state between paginated API requests.

### `canPaginate` 

When you add support for pagination to your trigger, be sure to set the canPaginate flag to true. That tells the platform to enable support for z.cursor.

![](https://cdn.zappy.app/c187390d43cc943999332f89cdc28b82.png)

![](https://cdn.zappy.app/8fa6ccf28e6cd5e4fafa71cfbb439ed0.png)

### `bundle.meta.isBulkRead`

When you’re supporting a request to page through all of an endpoint’s results you’ll need to code that request a little differently than if you’re fetching the latest data for a polling trigger. When transfer invokes your trigger the bundle.meta.isBulkRead will be set to true. Use that to control any conditional handling you need to implement.

### When There’s No More Data

When your endpoint has no more pages of data to return, return an empty array.

### Support for Both Polling Triggers and REST Hook Triggers

Zapier CLI version 11 adds support for implementing pagination in a performList method of a REST Hook trigger. Be sure to select “canPaginate” to true.

### Testing

- Go to https://transfer.zapier.com and log in
- Select your App and the trigger that supports Transfer. You’ll be able to see the integration for which you are the developer and every trigger.  Your users will not see your app here until you reach out to the Transfer team to get it included.
- Follow the directions to create and run a Transfer Zap. 
- Confirm that it is making paginated requests to your API. Confirm in your logs that the HTTP activity is correct. Make sure that all data available from the endpoint is presented in the UI, and correctly makes it in the target app. 

### When You’re Ready to Make Your Trigger Available in Transfer

When you’ve finished testing your Transfer-capable trigger and you want to make it available to your users, send an email to partners@zapier.com and request a review by the Transfer team. Be sure to identify which trigger or triggers are ready for Transfer. Be sure your Transfer support is in the current public version of your integration.

### Examples

```javascript
const getList = async (z, bundle) => {
  // if paginating then use the current page (ie. a dropdown or bulk read)
  // otherwise use the first page (ie. pulling in Zap samples)
  const page = bundle.meta.page ? bundle.meta.page + 1 : 1;
  const attendees = await getAttendees(z, bundle, page);
  let attendees = []
  if (bundle.meta.isBulkRead || bundle.meta.prefill) {
    // if paginating then use the current page
    const page = bundle.meta.page ? bundle.meta.page + 1 : 1;
    attendees = await getAllAttendees(z, bundle, page);
  } else {
    // when pulling in attendee samples in the editor we want the most recent
    attendees = await getRecentAttendees(z, bundle);
  }
  ```
Example of a trigger perform. This API uses the page/offset approach to paging. Here we check `bundle.meta.page` to differential handling for a Transfer request vs. a regular Zap handling which just returns the most recent objects.

### References

- [CLI Reference on Pagination](https://zapier.github.io/zapier-platform/#whats-the-deal-with-pagination-when-is-it-used-and-how-does-it-work)

## Considerations & Known Limitations

- Transfer is a beta product. As such we’re on the lookout for issues, scaling concerns, usability improvement opportunities. - Things are likely to change prior to being officially launched.
- Currently Transfer will fetch every object from your endpoint before allowing the user to interact with the data. As a result if the endpoint for your trigger might return more than a few thousand objects it’s not a good fit to expose through transfer at this time.
- If you are using hydration, be aware of the performance characteristics when your trigger is invoked from Transfer. If each row of data you return requires a separate API request to enrich that record’s data, Transfer will be making N+1 API requests for every page of data your trigger returns. The processing of each page must complete within ~60 seconds. The team is working on ways to improve this, but for now, tune the number of results you’re returning per request conservatively if you are relying on hydration.
- We’ll be introducing a way for developers to identify, within the app definition, which triggers support Transfer. Today this is done manually by you working with the Transfer team or your Zapier Partnerships representative. Bear in mind that we’ll be requiring you to make some updates to your integration, to set an attribute on the trigger, and update your CLI version, etc, prior to Transfer moving out of beta. There may be other changes to your integration required as we shake out any issues uncovered during beta. Please budget some development time accordingly.
- We recommend developing with the Zapier CLI. If you are adding pagination support when developing in the Platform UI, be aware that the built in API test component does not support z.cursor operations. You’ll need to test your trigger by making a Zap
