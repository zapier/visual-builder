---
title: Must-have triggers and actions
order: 1
layout: post-toc
redirect_from:
    - /build/recommended-integration-features
    - /quickstart/integration-design-examples
---

<style>
table {
    width: 1000px;
    margin-left: auto;
    margin-right: auto;
  }

.even-columns th, .even-columns td {
    width: 25%;
    text-align: left; /* or center, if you prefer */
  }
</style>

# Must-have triggers and actions

Whether you're just starting to scope out a new Zapier integration build or have successfully launched your app in the Zapier App Directory, it's helpful to know what features users find the most valuable and are the most widely used across Zapier's various [app categories](https://zapier.com/apps). Ensuring your integration covers the foundational triggers, actions, and searches applicable to your app will provide more utility to your users.

## Top Triggers, Actions, and Searches by App Category

The lists provided do not encompass every possible model or object specific to individual apps. Rather, they represent a more general overview of the most frequently observed ones in each category to serve as a guide to apply to your own app. Remember to maintain consistent terminology between your Zapier integration and app platform so users have a clear connection between the two.

Maybe your CRM platform, refers to new entries as _Contacts_. On another, they could be called _Leads_, _Clients_, _Persons_, or any term unique to the platform, such as _Hoomans_ or _Zaperonis_. You may not find _Zaperonis_ listed below, but if you see a similar concept like a _New Contact_ trigger, you can apply the same logic with a _New Zaperoni_ trigger for your integration.

If you don't see a list for your specific category, there may not have sufficient integrations within it to surface best practices. Reach out to [Partner support](https://developer.zapier.com/contact) to request a category.


### Accounting
{% capture styled_table %}
| Triggers               | Actions                         | Searches                     | Search or Creates                     |
|------------------------|---------------------------------|------------------------------|--------------------------------------|
| New Payment            | Create Invoice/Bill             | Find Customer/Client/Contact | Find or Create Customer/Client/Contact|
| New Invoice/Bill       | Create Payment                  | Find Product(s)              |                                      |
| New Customer/Contact/Client| Create Customer/Contact/Client| Find Invoice                 |                                      |
| New Expense            | Create/Record Sale/Sales Receipt|                              |                                      |
| New Quote/Estimate     | Send Invoice                    |                              |                                      |
| New Transaction        | Create Expense                  |                              |                                      |
{% endcapture %}
{{ styled_table | markdownify | replace: '<table>', '<table class="even-columns">' }}

View [example apps](https://zapier.com/apps/categories/accounting).

### Ads & Conversions
{% capture styled_table %}
| Triggers                     | Actions                             | Searches | Search or Creates |
| ---------------------------- | ----------------------------------- | -------- | ----------------- |
| New Lead/Subscriber/Visit    | *Send Event/Conversion/Measurement  |          |                   |
| New Form Response/Entry      | Add Contact/Email to List/Audience  |          |                   |
{% endcapture %}
{{ styled_table | markdownify | replace: '<table>', '<table class="even-columns">' }}

*Be sure your actions cover all types of events or conversions your app supports, such as ‘offline’, ‘lead’, ‘funnel’, etc.

View [example apps](https://zapier.com/apps/categories/ads-conversion).

### AI Tools
{% capture styled_table %}
| Triggers                | Actions                     | Searches                               | Search or Creates                |
|-------------------------|-----------------------------|----------------------------------------|----------------------------------|
| (Chat) New Message      | Send Prompt                 |                                        |                                  |
| New Transcription/Recording/Video/Image Ready | Request/Generate Image/Transcription/Video/etc. |                               |                                  |
{% endcapture %}
{{ styled_table | markdownify | replace: '<table>', '<table class="even-columns">' }}

View [example apps](https://zapier.com/apps/categories/ai-tools).

### Bookmark Managers
{% capture styled_table %}
| Triggers                | Actions                     | Searches                               | Search or Creates                |
|-------------------------|-----------------------------|----------------------------------------|----------------------------------|
| New Item/Bookmark       | Bookmark/Add Page/Item      |                                        |                                  |
| New Favorited Item      |                             |                                        |                                  |
| New Tagged Item         |                             |                                        |                                  |
{% endcapture %}
{{ styled_table | markdownify | replace: '<table>', '<table class="even-columns">' }}

View [example apps](https://zapier.com/apps/categories/bookmarks).

### Calendar
{% capture styled_table %}
| Triggers                | Actions                     | Searches                               | Search or Creates                |
|-------------------------|-----------------------------|----------------------------------------|----------------------------------|
| New or Updated Event/Meeting | Create Event             | Find Event                             | Find or Create Event             |
| Event Started           | Add Attendee to Event       |                                        |                                  |
| Event Ended             | Update Event                |                                        |                                  |
| Event Cancelled         | Delete Event                |                                        |                                  |
{% endcapture %}
{{ styled_table | markdownify | replace: '<table>', '<table class="even-columns">' }}

View [example apps](https://zapier.com/apps/categories/calendar).

### Call Tracking
{% capture styled_table %}
| Triggers                | Actions                     | Searches                               | Search or Creates                |
|-------------------------|-----------------------------|----------------------------------------|----------------------------------|
| Call Completed          |                             |                                        |                                  |
| New Call/Call Started   |                             |                                        |                                  |
| Call Tagged             |                             |                                        |                                  |
{% endcapture %}
{{ styled_table | markdownify | replace: '<table>', '<table class="even-columns">' }}

View [example apps](https://zapier.com/apps/categories/call-tracking).

### Contact Management
{% capture styled_table %}
| Triggers | Actions | Searches | Search or Creates |
| --- | --- | --- | --- |
| New Contact/Lead/Person/Company | Create Contact/Lead/Person/Company | Find Contact/Lead/Person/Company | Find or Create Contact/Lead/Person/Company |
| New Form Submission/Entry | Update Contact/Lead/Person/Company |  |   |
| Updated Contact/Lead/Person/Company | *Create or Update Contact/Lead/Person/Company |   |   |
|   | Add Contact to Group/Tag/List |   |   |
{% endcapture %}
{{ styled_table | markdownify | replace: '<table>', '<table class="even-columns">' }}

*If you’re adding a _Create or Update_ action instead of the recommended _Update_ action  to go along with a _Find or Create_ action, it’s best practice to return in the response payload whether the action taken was a create or update. This way, users can add appropriate next steps to their Zap depending on the scenario.

View [example apps](https://zapier.com/apps/categories/contacts).

### Customer Support
{% capture styled_table %}
| Triggers | Actions | Searches | Search or Creates |
| --- | --- | --- | --- |
| New Ticket/Request | Create Ticket/Request/Conversation | Find Customer/User/Lead | Find or Create Customer/User/Lead |
| New Chat/Message/Conversation | Create or Update User/Lead/Contact | Find Ticket/Request | |
| New Customer/User/Lead | Add/Remove Tag on User/Ticket/Lead | | |
| Finished/Closed Chat | Add Comment/Note on Ticket | | |
| Tag Added to Customer/User/Lead | Send Message | | |
{% endcapture %}
{{ styled_table | markdownify | replace: '<table>', '<table class="even-columns">' }}

View [example apps](https://zapier.com/apps/categories/customer-support).

### CRM (Customer Relationship Management)
{% capture styled_table %}
| Triggers | Actions | Searches | Search or Creates |
| --- | --- | --- | --- |
| New Record | *Create Record/X | *Find Record/X (most importantly Contacts/Lead/Person) | *Find or Create Record/X (most importantly Contacts/Lead/Person) |
| New Contact/Lead/Person | *Update Record/X |   |   |
| *New X | Add Lead to Campaign/Group |   |   |
| **Updated Record/Contact/Lead/Person/X | *Add Tag to X |   |   |
| Updated Stage/Status on Deal/Opportunity | Update Stage |   |   |
| Tag Added/Removed | Attach/Upload File |   |   |
{% endcapture %}
{{ styled_table | markdownify | replace: '<table>', '<table class="even-columns">' }}

*"X" represents your app’s various models or objects such as Deal, Project, etc. Make sure to cover the most popular models at a minimum. You can create individual triggers, actions, and searches for each or a single one where users can select different models in an input field.

*_Updated_ triggers for CRMs are often most useful when users are able to specify which field(s) to watch for updates on, instead of triggering on any and all updates. 

View [example apps](https://zapier.com/apps/categories/crm).

### Databases
{% capture styled_table %}
| Triggers             | Actions               | Searches                                     | Search or Creates                     |
|----------------------|-----------------------|----------------------------------------------|---------------------------------------|
| New Record/Row       | Create Record/Row     | Find Record/Row - return a single result      | Find or Create Record/Row             |
| Updated Record/Row   | Update Record/Row     | *Find Record(s)/Row(s) - return multiple results |                                      |
|                      | Find Record/Row via Custom Query |                                              |                                       |
{% endcapture %}
{{ styled_table | markdownify | replace: '<table>', '<table class="even-columns">' }}

*Zapier searches automatically return only the first result in the response. To return multiple results, [return the set of results](https://platform.zapier.com/build/response-types) as an array of objects under a descriptive key.

View [example apps](https://zapier.com/apps/categories/databases).

### Documents
{% capture styled_table %}
| Triggers                         | Actions                       | Searches                 | Search or Creates       |
|----------------------------------|-------------------------------|--------------------------|-------------------------|
| New Document                     | Create Document (from template) | Find Document            | Find or Create Document |
| Document Completed               | Upload Document               |                          |                         |
| Document Status Updated          |                               |                          |                         |
| Document Sent                    |                               |                          |                         |
| Document Signed                  |                               |                          |                         |
{% endcapture %}
{{ styled_table | markdownify | replace: '<table>', '<table class="even-columns">' }}

View [example apps](https://zapier.com/apps/categories/documents).

### Drip Email
{% capture styled_table %}
| Triggers                | Actions                                                                    | Searches                                                    | Search or Creates                                                 |
|-------------------------|----------------------------------------------------------------------------|-------------------------------------------------------------|-------------------------------------------------------------------|
| New Subscriber/Prospect | Add/Remove Tag from Subscriber/Lead/Prospect/Contact                       | Find Subscriber/Lead/Prospect/Contact                      | Find or Create Subscriber/Lead/Prospect/Contact                   |
| New Tagged Subscriber    | Create Subscriber/Lead/Prospect/Contact                                   |                                                             |                                                                   |
| New Unsubscribe         | Update Subscriber/Lead/Prospect/Contact                                   |                                                             |                                                                   |
| New Reply               | Add Subscriber/Lead/Prospect/Contact to Sequence/Campaign/List/Audience    |                                                             |                                                                   |
{% endcapture %}
{{ styled_table | markdownify | replace: '<table>', '<table class="even-columns">' }}

View [example apps](https://zapier.com/apps/categories/drip-emails).

### eCommerce
{% capture styled_table %}
| Triggers                           | Actions         | Searches         | Search or Creates      |
|-----------------------------------|-----------------|------------------|-----------------------|
| New Order/Purchase/Sale (with line-item support)  | Create Order  | Find Customer | Find or Create Customer |
| New Paid Order/Payment Received      | Create Customer | Find Order       |                       |
| New Customer                         | Update Customer | Find Product     |                       |
| New Cancelled Order/Subscription     | Create Product  |                  |                       |
| Abandoned Cart                       |                 |                  |                       |
{% endcapture %}
{{ styled_table | markdownify | replace: '<table>', '<table class="even-columns">' }}

View [example apps](https://zapier.com/apps/categories/ecommerce).

### Email
{% capture styled_table %}
| Triggers                         | Actions                       | Searches                 | Search or Creates       |
|----------------------------------|-------------------------------|--------------------------|-------------------------|
| New Email Matching Search        | Send Email                    | Find Email               | Find or Create Contact  |
| New Email                        | Create Draft Email            | Find Contact             | Find or Create Email    |
| New Labeled/Tagged/Starred Email | Validate Email (if applicable)|                          |                         |
| New Attachment                   | Create Contact                |                          |                         |
|                                  | Add Label to Email            |                          |                         |
{% endcapture %}
{{ styled_table | markdownify | replace: '<table>', '<table class="even-columns">' }}

View [example apps](https://zapier.com/apps/categories/email).

### Email Newsletter
{% capture styled_table %}
| Triggers                          | Actions                                  | Searches                                  | Search or Creates                        |
|-----------------------------------|------------------------------------------|-------------------------------------------|-------------------------------------------|
| New Subscriber/Contact            | *Create or Update Subscriber/Contact      | Find Subscriber/Contact                   | Find or Create Subscriber/Contact         |
| New Subscriber/Contact in List/Audience/Tag | Unsubscribe Subscriber/Contact   |                                           |                                           |
| New Unsubscriber                   | Add/Subscribe Contact to List/Audience/Tag |                                           |                                           |
| Email Opened                       | Send Email/Campaign                       |                                           |                                           |
{% endcapture %}
{{ styled_table | markdownify | replace: '<table>', '<table class="even-columns">' }}
*If you’re adding a _Create or Update_ action instead of the recommended _Update_ action  to go along with a _Find or Create_ action, it’s best practice to return in the response payload whether the action taken was a create or update. This way, users can add appropriate next steps to their Zap depending on the scenario

View [example apps](https://zapier.com/apps/categories/email-newsletters).

### Event Management
{% capture styled_table %}
| Triggers              | Actions              | Searches          | Search or Creates             |
|-----------------------|----------------------|-------------------|-------------------------------|
| New Contact/Attendee/Lead | Create Contact/Attendee/Lead | Find Contact/Attendee/Lead | Find or Create Contact/Attendee/Lead |
| New Registrant/RSVP | Add Registrant to Event |                     |                                     |
| New Order/Booking/Ticket | Create Event |                             |                                     |
{% endcapture %}
{{ styled_table | markdownify | replace: '<table>', '<table class="even-columns">' }}

View [example apps](https://zapier.com/apps/categories/event-management).

### File Management & Storage
{% capture styled_table %}
| Triggers                         | Actions                       | Searches                 | Search or Creates       |
|----------------------------------|-------------------------------|--------------------------|-------------------------|
| New File in Folder               | Upload File                   | Find File                | Find or Create File     |
| New File                         | Create Folder                 | Find Folder              | Find or Create Folder   |
| New Folder                       | Create File                   |                          |                         |
| Updated File                     | Move File                     |                          |                         |
{% endcapture %}
{{ styled_table | markdownify | replace: '<table>', '<table class="even-columns">' }}

View [example apps](https://zapier.com/apps/categories/files).

### Fundraising
{% capture styled_table %}
| Triggers                  | Actions                    | Searches                    | Search or Creates                      |
|---------------------------|----------------------------|-----------------------------|----------------------------------------|
| New Donation/Transaction/Pledge | Create Member/Donor/Contact  | Find Member/Donor/Contact   | Find or Create Member/Donor/Contact    |
| New Member/Donor/Contact       | Create Donation/Transaction/Pledge   |                             |                                        |
{% endcapture %}
{{ styled_table | markdownify | replace: '<table>', '<table class="even-columns">' }}

View [example apps](https://zapier.com/apps/categories/fundraising).

### Marketing Automation
{% capture styled_table %}
| Triggers                            | Actions                                            | Searches                            | Search or Creates                |
|------------------------------------|----------------------------------------------------|------------------------------------|----------------------------------|
| New Contact/Lead/Subscriber         | *Create or Update Contact/Lead/Deal/Opportunity/Order | Find Contact/Lead/Subscriber       | Find or Create Contact/Lead/Subscriber |
| New Contact in List/Audience/Segment | Add/Subscribe Contact to Campaign/List/Group        | Find Deal                          | Find or Create Deal              |
| Tag Added/Removed from Contact/Lead/Subscriber | Add/Remove Tag from Contact/Lead/Subscriber      |                                    |                                  |
| Updated Deal/Pipeline Stage          |                                                    |                                    |                                  |
| New or Updated Deal/Opportunity     |                                                    |                                    |                                  |
| New Order/Purchase/Sale             |                                                    |                                    |                                  |
| New Form Entry/Submission           |                                                    |                                    |                                  |
{% endcapture %}
{{ styled_table | markdownify | replace: '<table>', '<table class="even-columns">' }}

*If you’re adding a _Create or Update_ action instead of the recommended _Update_ action  to go along with a _Find or Create_ action, it’s best practice to return in the response payload whether the action taken was a create or update. This way, users can add appropriate next steps to their Zap depending on the scenario.

View [example apps](https://zapier.com/apps/categories/marketing-automation).

### Notes
{% capture styled_table %}
| Triggers                         | Actions                       | Searches                 | Search or Creates       |
|----------------------------------|-------------------------------|--------------------------|-------------------------|
| New Note                         | Create Note                   |                          |                         |
| New Note in Notebook/Section/Tag | Append to Note                |                          |                         |
{% endcapture %}
{{ styled_table | markdownify | replace: '<table>', '<table class="even-columns">' }}

View [example apps](https://zapier.com/apps/categories/notes).

### Notifications
{% capture styled_table %}
| Triggers                         | Actions                       | Searches                 | Search or Creates       |
|----------------------------------|-------------------------------|--------------------------|-------------------------|
| New Notification/Message         | Send Notification/Message     |                          |                         |
{% endcapture %}
{{ styled_table | markdownify | replace: '<table>', '<table class="even-columns">' }}

View [example apps](https://zapier.com/apps/categories/notifications).

### Online Courses
{% capture styled_table %}
| Triggers                           | Actions                            | Searches                          | Search or Creates              |
|------------------------------------|------------------------------------|-----------------------------------|-------------------------------|
| New Enrollment/Subscription        | Enroll User/Student                | Find User/Student                 | Find or Create User/Student   |
| New Order/Sale/Purchase            | Unenroll User/Student              |                                   |                               |
| New User/Student                   | Create Credentials/Grant Access/Issue Credentials|                                 |                               |
| Course/Lesson Completed            | Create User/Student                |                                   |                               |
{% endcapture %}
{{ styled_table | markdownify | replace: '<table>', '<table class="even-columns">' }}

View [example apps](https://zapier.com/apps/categories/it-operations-education).

### Payment Processing
{% capture styled_table %}
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
{% endcapture %}
{{ styled_table | markdownify | replace: '<table>', '<table class="even-columns">' }}

View [example apps](https://zapier.com/apps/categories/payment-processing).

### Phone & SMS
{% capture styled_table %}
| Triggers                         | Actions                       | Searches                 | Search or Creates       |
|----------------------------------|-------------------------------|--------------------------|-------------------------|
| New SMS/Message Received         | Create or Update Contact      | Find Contact             | Find or Create Contact  |
| New Call                         | Send SMS/Message              |                          |                         |
| New Recording                    | Create Contact                |                          |                         |
|                                  | Opt-in Contact                |                          |                         |
|                                  | Call Phone Number             |                          |                         |
{% endcapture %}
{{ styled_table | markdownify | replace: '<table>', '<table class="even-columns">' }}

View [example apps](https://zapier.com/apps/categories/phone).

### Product Management
{% capture styled_table %}
| Triggers                          | Actions                                | Searches                               | Search or Creates                |
|-----------------------------------|----------------------------------------|----------------------------------------|----------------------------------|
| New Feedback/Form Submitted/Request | Create Note/Feature/Task/Idea           |                                        |                                  |
| New Note/Comment                   |                                        |                                        |                                  |
{% endcapture %}
{{ styled_table | markdownify | replace: '<table>', '<table class="even-columns">' }}

View [example apps](https://zapier.com/apps/categories/product-management).

### Project Management
{% capture styled_table %}
| Triggers                          | Actions                                | Searches                               | Search or Creates                |
|-----------------------------------|----------------------------------------|----------------------------------------|----------------------------------|
| New Task/Item/Issue                | Create Task/Item/Issue                  | Find Task/Item/Issue                    | Find or Create Task/Item/Issue   |
| Task/Item/Issue Status Changed     | Update Task/Item/Issue                  | Find User                              | Find or Create Project/Board     |
| New Label/Tag on Task/Item/Issue   | Add Comment/Note to Task/Item/Issue     | Find Project/Board                      |                                  |
| New Event/Activity                 | Attach/Upload file to Task/Item/Issue   |                                        |                                  |
| Completed Task/Item/Issue          | Create Project/Board                    |                                        |                                  |
| Updated Task/Item/Issue            | Add Label/Tag to Task/Item/Issue        |                                        |                                  |
| Specific Value on Task/Item/Issue Changed |                                    |                                        |                                  |
{% endcapture %}
{{ styled_table | markdownify | replace: '<table>', '<table class="even-columns">' }}

View [example apps](https://zapier.com/apps/categories/project-management).

### Proposal & Invoice Management
{% capture styled_table %}
| Triggers                | Actions                     | Searches                   | Search or Creates         |
|-------------------------|-----------------------------|----------------------------|---------------------------|
| Proposal/Estimate/Quote Accepted | Create Client/Contact/Lead | Find Client/Contact/Lead   | Find or Create Client/Contact/Lead |
| Proposal Signed         | Create Proposal/Estimate/Quote | Find Proposal/Estimate/Quote |                           |
| Proposal Won            | Create Invoice              |                            |                           |
| Proposal Sent           | Create Project              |                            |                           |
| New Proposal/Estimate/Quote |                             |                            |                           |
{% endcapture %}
{{ styled_table | markdownify | replace: '<table>', '<table class="even-columns">' }}

View [example apps](https://zapier.com/apps/categories/invoices).

### Scheduling & Booking
{% capture styled_table %}
| Triggers | Actions | Searches | Search or Creates   |
|----------|---------|----------|--------------------|
| New Booking/Appointment | Create Client/Customer | Find Client | Find or Create Client  |
| New Cancellation | Create Booking/Appointment/Request/Job | Find Booking/Appointment |     |
| New Client/Customer |       |        |               |
| Booking/Appointment Completed |       |        |               |
{% endcapture %}
{{ styled_table | markdownify | replace: '<table>', '<table class="even-columns">' }}

View [example apps](https://zapier.com/apps/categories/scheduling).

### Server Monitoring
{% capture styled_table %}
| Triggers                           | Actions                    | Searches                           | Search or Creates            |
|------------------------------------|----------------------------|------------------------------------|-----------------------------|
| New or Updated Ticket/Request/Incident | Create Alert           | Find Ticket/Request/Incident   |                               |
| New Alert                           | Create Ticket/Request         |                                    |                               |
{% endcapture %}
{{ styled_table | markdownify | replace: '<table>', '<table class="even-columns">' }}

View [example apps](https://zapier.com/apps/categories/server-monitoring).

### Signatures
{% capture styled_table %}
| Triggers                      | Actions                       | Searches                     | Search or Creates          |
|-------------------------------|-------------------------------|-------------------------------|----------------------------|
| Document/Contract Completed   | *Create Document/Contract     | Find Document/Contract       |                            |
| Document/Contract Signed      | Send Signature Request        |                               |                            |
| Document/Contract Sent        |                               |                               |                            |
{% endcapture %}
{{ styled_table | markdownify | replace: '<table>', '<table class="even-columns">' }}

*_Create Document/Contract_ actions typically allow for users to select a template in the action’s setup.

View [example apps](https://zapier.com/apps/categories/signatures).

### Social Media Accounts
{% capture styled_table %}
| Triggers                        | Actions                  | Searches                 | Search or Creates       |
| ------------------------------- | ------------------------ | ------------------------ | ----------------------- |
| New Post/Message/Media (by me)   | Create Post/Message/Media|                          |                         |
| New Post/Message/Media by User  | Publish Post/Message/Media|                          |                         |
{% endcapture %}
{{ styled_table | markdownify | replace: '<table>', '<table class="even-columns">' }}

View [example apps](https://zapier.com/apps/categories/social).

### Spreadsheets
{% capture styled_table %}
| Triggers                          | Actions                                | Searches                               | Search or Creates                |
|-----------------------------------|----------------------------------------|----------------------------------------|----------------------------------|
| New Row                           | Create/Add Row                         | Lookup/Find Row(s) (with line-item support) | Find or Create Row               |
| Updated Row                       | Create Row(s)                          | Find Spreadsheet                       |                                  |
| New Spreadsheet/Worksheet         | Update Row                             |                                        |                                  |
|                                    | Delete Row                             |                                        |                                  |
|                                    | Create Spreadsheet                     |                                        |                                  |
{% endcapture %}
{{ styled_table | markdownify | replace: '<table>', '<table class="even-columns">' }}

View [example apps](https://zapier.com/apps/categories/spreadsheets).

### Task Management
{% capture styled_table %}
| Triggers                          | Actions                                | Searches                               | Search or Creates                |
|-----------------------------------|----------------------------------------|----------------------------------------|----------------------------------|
| New Task                           | Create/Add Task                         | Find Task                              | Find or Create Task              |
| Completed Task                     | Complete Task                           |                                        |                                  |
|                                    | Update Task                             |                                        |                                  |
{% endcapture %}
{{ styled_table | markdownify | replace: '<table>', '<table class="even-columns">' }}

View [example apps](https://zapier.com/apps/categories/todo-lists).

### Team Chat
{% capture styled_table %}
| Triggers                          | Actions                                | Searches                               | Search or Creates                |
|-----------------------------------|----------------------------------------|----------------------------------------|----------------------------------|
| New Message in Channel             | Send Channel Message                    | Find User (by email, name, username)   |                                  |
| New Reaction on Message            | Send Direct/Private Message             |                                        |                                  |
| New Mention                        | Set Status                              |                                        |                                  |
| New User                           | Add User/Role                           |                                        |                                  |
{% endcapture %}
{{ styled_table | markdownify | replace: '<table>', '<table class="even-columns">' }}

View [example apps](https://zapier.com/apps/categories/team-chat).

### Time Tracking Software
{% capture styled_table %}
| Triggers                          | Actions                                | Searches                               | Search or Creates                |
|-----------------------------------|----------------------------------------|----------------------------------------|----------------------------------|
| New Time Entry                     | Start Time Entry                        | Find Client                            | Find or Create Client            |
| New Time Entry/Timer Started       | Create Time Entry                       |                                        | Find or Create Project           |
|                                    | Create Project                          |                                        |                                  |
|                                    | Create Client                           |                                        |                                  |
|                                    | Create Task                             |                                        |                                  |
{% endcapture %}
{{ styled_table | markdownify | replace: '<table>', '<table class="even-columns">' }}

View [example apps](https://zapier.com/apps/categories/time-tracking).

### Transactional Emails
{% capture styled_table %}
| Triggers        | Actions       | Searches  | Search or Creates |
| --------------- | ------------- | --------- | ----------------- |
| Failed Delivery | *Send Email   |           |                   |
| Bounced Email   |               |           |                   |
| Open/Clicked Event |             |           |                   |
{% endcapture %}
{{ styled_table | markdownify | replace: '<table>', '<table class="even-columns">' }}

*_Send Email_ actions often allowed users to select and use a template in the action’s setup.

View [example apps](https://zapier.com/apps/categories/transactional-email).

### Transcription
{% capture styled_table %}
| Triggers                   | Actions                   | Searches      | Search or Creates       |
| -------------------------- | ------------------------- | --------------| ----------------------- |
| New Transcript             | Create Transcription/Upload Audio or File |               |                         |
{% endcapture %}
{{ styled_table | markdownify | replace: '<table>', '<table class="even-columns">' }}

View [example apps](https://zapier.com/apps/categories/transcription).

### Video & Audio
{% capture styled_table %}
| Triggers                   | Actions              | Searches        | Search or Creates |
|----------------------------|----------------------|-----------------|-------------------|
| New Video (in Channel/Playlist) | Upload Video         | Find Track      |                   |
| New Track in Playlist      | Add Track to Playlist |                 |                   |
{% endcapture %}
{{ styled_table | markdownify | replace: '<table>', '<table class="even-columns">' }}

View [example apps](https://zapier.com/apps/categories/video).

### Video Conferencing
{% capture styled_table %}
| Triggers        | Actions          | Searches  | Search or Creates |
| --------------- | ---------------- | --------- | ----------------- |
| New Recording   | Create/Add Registrant |           |                   |
| New Registrant  | Create Meeting   |           |                   |
| New Meeting     |                  |           |                   |
{% endcapture %}
{{ styled_table | markdownify | replace: '<table>', '<table class="even-columns">' }}

View [example apps](https://zapier.com/apps/categories/video-calls).

### Webinars
{% capture styled_table %}
| Triggers                      | Actions                    | Searches               | Search or Creates            |
| ----------------------------- | -------------------------- | ---------------------- | ---------------------------- |
| New Registration/Registrant   | Create Registration/Registrant | Find Registrant     |                                |
| New Attendee or Webinar/Event Joined   | Register to an Event | Find Session       |                                |
| Attendee Stays Until/% of time |                            |                        |                                |
{% endcapture %}
{{ styled_table | markdownify | replace: '<table>', '<table class="even-columns">' }}

View [example apps](https://zapier.com/apps/categories/webinars).