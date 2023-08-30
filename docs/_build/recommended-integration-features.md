---
title: Recommended Integration Features
order: 13
layout: post-toc
---

# Recommended Integration Features

Whether you're just starting to scope out a new Zapier integration build or already have a successfully launched one in our App Directory, it's helpful to know what features users find the most valuable and thus, are the most widely used, across Zapier's various [app categories](https://zapier.com/apps). Ensuring your integration covers the foundational triggers, actions, and searches applicable to your app will provide more utility to your users.

## Top Triggers, Actions, and Searches by App Category

The lists provided are not meant to encompass every possible model or object specific to individual apps. Rather, they represent a more general overview of the most frequently observed ones in each category to serve as a guide to apply to your own app. The key point to remember is to maintain consistent terminology between your Zapier integration and platform so users have a clear connection between the two.

Let's use a CRM app as an example. Maybe on your platform, new entries are referred to as 'Contacts'. On another, they could be called 'Leads', 'Clients', 'Persons', or any term unique to the platform, such as 'Hoomans' or 'Zaperonis'. You may not find 'Zaperonis' listed below, but if you see a similar concept like a 'New Contact' trigger, you can apply the same logic with a ‘New Zaperoni’ trigger for your integration.

If you don't see a list for your specific category, we may not have sufficient integrations within it to surface best practices or may be working on it. Reach out via our [Partner support channel](https://developer.zapier.com/contact) to request a category.

### Accounting

| Triggers               | Actions                         | Searches                     | Search or Creates                     |
|------------------------|---------------------------------|------------------------------|--------------------------------------|
| New Payment            | Create Invoice/Bill             | Find Customer/Client/Contact | Find or Create Customer/Client/Contact|
| New Invoice/Bill       | Create Payment                  | Find Product(s)              |                                      |
| New Customer/Contact/Client| Create Customer/Contact/Client| Find Invoice                 |                                      |
| New Expense            | Create/Record Sale/Sales Receipt|                              |                                      |
| New Quote/Estimate     | Send Invoice                    |                              |                                      |
| New Transaction        | Create Expense                  |                              |                                      |

### Ads & Conversions

| Triggers                     | Actions                             | Searches | Search or Creates |
| ---------------------------- | ----------------------------------- | -------- | ----------------- |
| New Lead/Subscriber/Visit    | *Send Event/Conversion/Measurement  |          |                   |
| New Form Response/Entry      | Add Contact/Email to List/Audience  |          |                   |

*Be sure your actions cover all types of events or conversions your app supports, such as ‘offline’, ‘lead’, ‘funnel’, etc.

### AI Tools

| Triggers                | Actions                     | Searches                               | Search or Creates                |
|-------------------------|-----------------------------|----------------------------------------|----------------------------------|
| (Chat) New Message      | Send Prompt                 |                                        |                                  |
| New Transcription/Recording/Video/Image Ready | Request/Generate Image/Transcription/Video/etc. |                               |                                  |

### Bookmark Managers

| Triggers                | Actions                     | Searches                               | Search or Creates                |
|-------------------------|-----------------------------|----------------------------------------|----------------------------------|
| New Item/Bookmark       | Bookmark/Add Page/Item      |                                        |                                  |
| New Favorited Item      |                             |                                        |                                  |
| New Tagged Item         |                             |                                        |                                  |

### Calendar

| Triggers                | Actions                     | Searches                               | Search or Creates                |
|-------------------------|-----------------------------|----------------------------------------|----------------------------------|
| New or Updated Event/Meeting | Create Event             | Find Event                             | Find or Create Event             |
| Event Started           | Add Attendee to Event       |                                        |                                  |
| Event Ended             | Update Event                |                                        |                                  |
| Event Cancelled         | Delete Event                |                                        |                                  |

### Call Tracking

| Triggers                | Actions                     | Searches                               | Search or Creates                |
|-------------------------|-----------------------------|----------------------------------------|----------------------------------|
| Call completed          |                             |                                        |                                  |
| New Call/Call Started   |                             |                                        |                                  |
| Call tagged             |                             |                                        |                                  |

### Contact Management

| Triggers | Actions | Searches | Search or Creates |
| --- | --- | --- | --- |
| New Contact/Lead/Person/Company | Create Contact/Lead/Person/Company | Find Contact/Lead/Person/Company | Find or Create Contact/Lead/Person/Company |
| New Form Submission/Entry	| Update Contact/Lead/Person/Company	| 	|   |
| Updated Contact/Lead/Person/Company	| *Create or Update Contact/Lead/Person/Company	|   |   |
|   | Add Contact to Group/Tag/List |   |   |

*If you’re adding a “Create or Update” action instead of an “Update” action along with a “Find or Create” action, it’s best practice to return in the response payload if the action taken was a create or update. This way, users can add appropriate next steps to their Zap depending on the scenario.

### Customer Support

| Triggers | Actions | Searches | Search or Creates |
| --- | --- | --- | --- |
| New Ticket/Request | Create Ticket/Request/Conversation | Find Customer/User/Lead | Find or Create Customer/User/Lead |
| New Chat/Message/Conversation | Create or Update User/Lead/Contact | Find Ticket/Request | |
| New Customer/User/Lead | Add/Remove Tag on User/Ticket/Lead | | |
| Finished/Closed Chat | Add Comment/Note on Ticket | | |
| Tag Added to Customer/User/Lead | Send Message | | |

### CRM (Customer Relationship Management)

| Triggers | Actions | Searches | Search or Creates |
| --- | --- | --- | --- |
| New Record | *Create Record/X | *Find Record/X (most importantly Contacts/Lead/Person) | *Find or Create Record/X (most importantly Contacts/Lead/Person) |
| New Contact/Lead/Person | *Update Record/X |   |   |
| *New X | Add Lead to Campaign/Group |   |   |
| **Updated Record/Contact/Lead/Person/X | *Add Tag to X |   |   |
| Updated Stage/Status on Deal/Opportunity | Update Stage |   |   |
| Tag Added/Removed | Attach/Upload File |   |   |

*"X" represents your app’s various models or objects such as Deal, Project, etc. Make sure to cover the most popular models at a minimum. You can create individual triggers, actions, and searches for each or a single ones where users can select different models in an input field.

**“Updated” triggers for CRMs are often most useful when users are able to specify which field(s) to watch for updates on, instead of triggering on any and all updates. 

### Databases

| Triggers             | Actions               | Searches                                     | Search or Creates                     |
|----------------------|-----------------------|----------------------------------------------|---------------------------------------|
| New Record/Row       | Create Record/Row     | Find Record/Row - return a single result      | Find or Create Record/Row             |
| Updated Record/Row   | Update Record/Row     | *Find Record(s)/Row(s) - return multiple results |                                      |
|                      | Find Record/Row via Custom Query |                                              |                                       |

*Zapier searches automatically return only the first result in the response. To return multiple results, return the set of results as an array of objects under a descriptive key.

### Documents

| Triggers                         | Actions                       | Searches                 | Search or Creates       |
|----------------------------------|-------------------------------|--------------------------|-------------------------|
| New Document                     | Create Document (from template) | Find Document            | Find or Create Document |
| Document Completed               | Upload Document               |                          |                         |
| Document Status Updated          |                               |                          |                         |
| Document Sent                    |                               |                          |                         |
| Document Signed                  |                               |                          |                         |

### Drip Email

| Triggers                | Actions                                                                    | Searches                                                    | Search or Creates                                                 |
|-------------------------|----------------------------------------------------------------------------|-------------------------------------------------------------|-------------------------------------------------------------------|
| New Subscriber/Prospect | Add/Remove Tag from Subscriber/Lead/Prospect/Contact                       | Find Subscriber/Lead/Prospect/Contact                      | Find or Create Subscriber/Lead/Prospect/Contact                   |
| New Tagged Subscriber    | Create Subscriber/Lead/Prospect/Contact                                   |                                                             |                                                                   |
| New Unsubscribe         | Update Subscriber/Lead/Prospect/Contact                                   |                                                             |                                                                   |
| New Reply               | Add Subscriber/Lead/Prospect/Contact to Sequence/Campaign/List/Audience    |                                                             |                                                                   |

### eCommerce

| Triggers                           | Actions         | Searches         | Search or Creates      |
|-----------------------------------|-----------------|------------------|-----------------------|
| New Order/Purchase/Sale (with line-item support)  | Create Order  | Find Customer | Find or Create Customer |
| New Paid Order/Payment Received      | Create Customer | Find Order       |                       |
| New Customer                         | Update Customer | Find Product     |                       |
| New Cancelled Order/Subscription     | Create Product  |                  |                       |
| Abandoned Cart                       |                 |                  |                       |

### Email

| Triggers                         | Actions                       | Searches                 | Search or Creates       |
|----------------------------------|-------------------------------|--------------------------|-------------------------|
| New Email Matching Search        | Send Email                    | Find Email               | Find or Create Contact  |
| New Email                        | Create Draft Email            | Find Contact             | Find or Create Email    |
| New Labeled/Tagged/Starred Email | Validate Email (if applicable)|                          |                         |
| New Attachment                   | Create Contact                |                          |                         |
|                                  | Add Label to Email            |                          |                         |

### Email Newsletter

| Triggers                          | Actions                                  | Searches                                  | Search or Creates                        |
|-----------------------------------|------------------------------------------|-------------------------------------------|-------------------------------------------|
| New Subscriber/Contact            | *Create or Update Subscriber/Contact      | Find Subscriber/Contact                   | Find or Create Subscriber/Contact         |
| New Subscriber/Contact in List/Audience/Tag | Unsubscribe Subscriber/Contact   |                                           |                                           |
| New Unsubscriber                   | Add/Subscribe Contact to List/Audience/Tag |                                           |                                           |
| Email Opened                       | Send Email/Campaign                       |                                           |                                           |

*If you’re adding a “Create or Update” action instead of an “Update” action along with a “Find or Create” action, it’s best practice to return in the response payload if the action taken was a create or update. This way, users can add appropriate next steps to their Zap depending on the scenario.

### Event Management

| Triggers              | Actions              | Searches          | Search or Creates             |
|-----------------------|----------------------|-------------------|-------------------------------|
| New Contact/Attendee/Lead | Create Contact/Attendee/Lead | Find Contact/Attendee/Lead | Find or Create Contact/Attendee/Lead |
| New Registrant/RSVP | Add Registrant to Event |                     |                                     |
| New Order/Booking/Ticket | Create Event |                             |                                     |

### File Management & Storage

| Triggers                         | Actions                       | Searches                 | Search or Creates       |
|----------------------------------|-------------------------------|--------------------------|-------------------------|
| New File in Folder               | Upload File                   | Find File                | Find or Create File     |
| New File                         | Create Folder                 | Find Folder              | Find or Create Folder   |
| New Folder                       | Create File                   |                          |                         |
| Updated File                     | Move File                     |                          |                         |

### Fundraiser

| Triggers                  | Actions                    | Searches                    | Search or Creates                      |
|---------------------------|----------------------------|-----------------------------|----------------------------------------|
| New Donation/Transaction/Pledge | Create Member/Donor/Contact  | Find Member/Donor/Contact   | Find or Create Member/Donor/Contact    |
| New Member/Donor/Contact       | Create Donation/Transaction/Pledge   |                             |                                        |

### Marketing Automation

| Triggers                            | Actions                                            | Searches                            | Search or Creates                |
|------------------------------------|----------------------------------------------------|------------------------------------|----------------------------------|
| New Contact/Lead/Subscriber         | *Create or Update Contact/Lead/Deal/Opportunity/Order | Find Contact/Lead/Subscriber       | Find or Create Contact/Lead/Subscriber |
| New Contact in List/Audience/Segment | Add/Subscribe Contact to Campaign/List/Group        | Find Deal                          | Find or Create Deal              |
| Tag Added/Removed from Contact/Lead/Subscriber | Add/Remove Tag from Contact/Lead/Subscriber      |                                    |                                  |
| Updated Deal/Pipeline Stage          |                                                    |                                    |                                  |
| New or Updated Deal/Opportunity     |                                                    |                                    |                                  |
| New Order/Purchase/Sale             |                                                    |                                    |                                  |
| New Form Entry/Submission           |                                                    |                                    |                                  |

*If you’re adding a “Create or Update” action instead of an “Update” action along with a “Find or Create” action, it’s best practice to return in the response payload if the action taken was a create or update. This way, users can add appropriate next steps to their Zap depending on the scenario.

### Notes

| Triggers                         | Actions                       | Searches                 | Search or Creates       |
|----------------------------------|-------------------------------|--------------------------|-------------------------|
| New Note                         | Create Note                   |                          |                         |
| New Note in Notebook/Section/Tag | Append to Note                |                          |                         |

### Notifications


| Triggers                         | Actions                       | Searches                 | Search or Creates       |
|----------------------------------|-------------------------------|--------------------------|-------------------------|
| New Notification/Message         | Send Notification/Message     |                          |                         |

### Online Courses

| Triggers                           | Actions                            | Searches                          | Search or Creates              |
|------------------------------------|------------------------------------|-----------------------------------|-------------------------------|
| New Enrollment/Subscription        | Enroll User/Student                | Find User/Student                 | Find or Create User/Student   |
| New Order/Sale/Purchase            | Unenroll User/Student              |                                   |                               |
| New User/Student                   | Create Credentials/Grant Access/Issue Credentials|                                 |                               |
| Course/Lesson Completed            | Create User/Student                |                                   |                               |

### Payment Processing

| Triggers                            | Actions                             | Searches           | Search or Creates          |
|-------------------------------------|-------------------------------------|---------------------|----------------------------|
| New Payment                         | Create Customer                     | Find Customer       | Find or Create Customer    |
| New Subscription/Order/Sale/Transaction/Invoice | Create Payment Link (if applicable) | Find Subscription  |                            |
| New Customer                        | Update Customer                     |                     |                            |
| New Paid Order/Invoice              |                                     |                     |                            |
| New Refund                          |                                     |                     |                            |
| Canceled Subscription/Order/Sale    |                                     |                     |                            |
| Failed Payment                      |                                     |                     |                            |
| Checkout Session Completed          |                                     |                     |                            |

### Phone & SMS
| Triggers                         | Actions                       | Searches                 | Search or Creates       |
|----------------------------------|-------------------------------|--------------------------|-------------------------|
| New SMS/Message Received         | Create or Update Contact      | Find Contact             | Find or Create Contact  |
| New Call                         | Send SMS/Message              |                          |                         |
| New Recording                    | Create Contact                |                          |                         |
|                                  | Opt-in Contact                |                          |                         |
|                                  | Call Phone Number             |                          |                         |

### Product Management

| Triggers                          | Actions                                | Searches                               | Search or Creates                |
|-----------------------------------|----------------------------------------|----------------------------------------|----------------------------------|
| New Feedback/Form Submitted/Request | Create Note/Feature/Task/Idea           |                                        |                                  |
| New Note/Comment                   |                                        |                                        |                                  |

### Project Management

| Triggers                          | Actions                                | Searches                               | Search or Creates                |
|-----------------------------------|----------------------------------------|----------------------------------------|----------------------------------|
| New Task/Item/Issue                | Create Task/Item/Issue                  | Find Task/Item/Issue                    | Find or Create Task/Item/Issue   |
| Task/Item/Issue Status Changed     | Update Task/Item/Issue                  | Find User                              | Find or Create Project/Board     |
| New Label/Tag on Task/Item/Issue   | Add Comment/Note to Task/Item/Issue     | Find Project/Board                      |                                  |
| New Event/Activity                 | Attach/Upload file to Task/Item/Issue   |                                        |                                  |
| Completed Task/Item/Issue          | Create Project/Board                    |                                        |                                  |
| Updated Task/Item/Issue            | Add Label/Tag to Task/Item/Issue        |                                        |                                  |
| Specific Value on Task/Item/Issue Changed |                                    |                                        |                                  |

### Proposal & Invoice Management

| Triggers                | Actions                     | Searches                   | Search or Creates         |
|-------------------------|-----------------------------|----------------------------|---------------------------|
| Proposal/Estimate/Quote Accepted | Create Client/Contact/Lead | Find Client/Contact/Lead   | Find or Create Client/Contact/Lead |
| Proposal Signed         | Create Proposal/Estimate/Quote | Find Proposal/Estimate/Quote |                           |
| Proposal Won            | Create Invoice              |                            |                           |
| Proposal Sent           | Create Project              |                            |                           |
| New Proposal/Estimate/Quote |                             |                            |                           |

### Scheduling & Booking

| Triggers | Actions | Searches | Search or Creates   |
|----------|---------|----------|--------------------|
| New Booking/Appointment | Create Client/Customer | Find Client | Find or Create Client  |
| New Cancellation | Create Booking/Appointment/Request/Job | Find Booking/Appointment |     |
| New Client/Customer |       |        |               |
| Booking/Appointment Completed |       |        |               |

### Server Monitoring

| Triggers                           | Actions                    | Searches                           | Search or Creates            |
|------------------------------------|----------------------------|------------------------------------|-----------------------------|
| New or Updated Ticket/Request/Incident | Create Alert           | Find Ticket/Request/Incident   |                               |
| New Alert                           | Create Ticket/Request         |                                    |                               |

### Signatures

| Triggers                      | Actions                       | Searches                     | Search or Creates          |
|-------------------------------|-------------------------------|-------------------------------|----------------------------|
| Document/Contract Completed   | *Create Document/Contract     | Find Document/Contract       |                            |
| Document/Contract Signed      | Send Signature Request        |                               |                            |
| Document/Contract Sent        |                               |                               |                            |

*Create Document/Contract actions typically allow for users to select a template in the action’s setup.

### Social Media Accounts

| Triggers                        | Actions                  | Searches                 | Search or Creates       |
| ------------------------------- | ------------------------ | ------------------------ | ----------------------- |
| New Post/Message/Media (by me)   | Create Post/Message/Media|                          |                         |
| New Post/Message/Media by User  | Publish Post/Message/Media|                          |                         |

### Spreadsheets

| Triggers                          | Actions                                | Searches                               | Search or Creates                |
|-----------------------------------|----------------------------------------|----------------------------------------|----------------------------------|
| New Row                           | Create/Add Row                         | Lookup/Find Row(s) (with line-item support) | Find or Create Row               |
| Updated Row                       | Create Row(s)                          | Find Spreadsheet                       |                                  |
| New Spreadsheet/Worksheet         | Update Row                             |                                        |                                  |
|                                    | Delete Row                             |                                        |                                  |
|                                    | Create Spreadsheet                     |                                        |                                  |

### Task Management

| Triggers                          | Actions                                | Searches                               | Search or Creates                |
|-----------------------------------|----------------------------------------|----------------------------------------|----------------------------------|
| New Task                           | Create/Add Task                         | Find Task                              | Find or Create Task              |
| Completed Task                     | Complete Task                           |                                        |                                  |
|                                    | Update Task                             |                                        |                                  |

### Team Chat

| Triggers                          | Actions                                | Searches                               | Search or Creates                |
|-----------------------------------|----------------------------------------|----------------------------------------|----------------------------------|
| New Message in Channel             | Send Channel Message                    | Find User (by email, name, username)   |                                  |
| New Reaction on Message            | Send Direct/Private Message             |                                        |                                  |
| New Mention                        | Set Status                              |                                        |                                  |
| New User                           | Add User/Role                           |                                        |                                  |

### Time Tracking Software

| Triggers                          | Actions                                | Searches                               | Search or Creates                |
|-----------------------------------|----------------------------------------|----------------------------------------|----------------------------------|
| New Time Entry                     | Start Time Entry                        | Find Client                            | Find or Create Client            |
| New Time Entry/Timer Started       | Create Time Entry                       |                                        | Find or Create Project           |
|                                    | Create Project                          |                                        |                                  |
|                                    | Create Client                           |                                        |                                  |
|                                    | Create Task                             |                                        |                                  |

### Transactional Emails

| Triggers        | Actions       | Searches  | Search or Creates |
| --------------- | ------------- | --------- | ----------------- |
| Failed Delivery | *Send Email   |           |                   |
| Bounced Email   |               |           |                   |
| Open/Clicked Event |             |           |                   |

*Send Email actions often allowed users to select and use a template in the action’s setup.

### Transcription

| Triggers                   | Actions                   | Searches      | Search or Creates       |
| -------------------------- | ------------------------- | --------------| ----------------------- |
| New Transcript             | Create Transcription/Upload Audio or File |               |                         |

### Video & Audio

| Triggers                   | Actions              | Searches        | Search or Creates |
|----------------------------|----------------------|-----------------|-------------------|
| New Video (in Channel/Playlist) | Upload Video         | Find Track      |                   |
| New Track in Playlist      | Add Track to Playlist |                 |                   |

### Video Conferencing

| Triggers        | Actions          | Searches  | Search or Creates |
| --------------- | ---------------- | --------- | ----------------- |
| New Recording   | Create/Add Registrant |           |                   |
| New Registrant  | Create Meeting   |           |                   |
| New Meeting     |                  |           |                   |

### Webinars

| Triggers                      | Actions                    | Searches               | Search or Creates            |
| ----------------------------- | -------------------------- | ---------------------- | ---------------------------- |
| New Registration/Registrant   | Create Registration/Registrant | Find Registrant     |                                |
| New Attendee or Webinar/Event Joined   | Register to an Event | Find Session       |                                |
| Attendee Stays Until/% of time |                            |                        |                                |