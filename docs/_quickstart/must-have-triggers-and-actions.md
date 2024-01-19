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
|------------------------|---------------------------------|------------------------------|---------------------------------------|
| New Payment            | Create Customer/Contact/Client  | Find Invoice                 | Find or Create Customer/Client/Contact|
| New Invoice/Bill       | Create Invoice/Bill             | Find Customer/Client/Contact |                                       |
| New Expense            | Send Invoice                    |                              |                                       |
| New Customer/Contact/Client | Create Payment/Sale/Sales Receipt |                       |                                       |
| New Quote/Estimate     |                                 |                              |                                       |
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
| New or Updated Event/Meeting | Create Event           | Find Event                             | Find or Create Event             |
| Event Started           | Add Attendee to Event       |                                        |                                  |
| New Event/Meeting       |                             |                                        |                                  |
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
| Triggers                                    | Actions                            | Searches                         | Search or Creates                |
|---------------------------------------------|------------------------------------|----------------------------------|----------------------------------|
| New or Updated Contact/Lead/Person/Company  | Create Contact/Lead/Person/Company | Find Contact/Lead/Person/Company | Find or Create Contact/Lead/Person/Company |
| New Form Submission/Entry                   | Add Contact to Group/Tag/List      |                                  |                                  |
| New Contact/Lead/Person/Company             | Update Contact/Lead/Person/Company |                                  |                                  |
{% endcapture %}
{{ styled_table | markdownify | replace: '<table>', '<table class="even-columns">' }}

View [example apps](https://zapier.com/apps/categories/contacts).

### Customer Support
{% capture styled_table %}
| Triggers                         | Actions                              | Searches                               | Search or Creates                 |
|----------------------------------|--------------------------------------|----------------------------------------|-----------------------------------|
| Tag Added to Customer/User/Lead  | Create Ticket/Request/Conversation   | Find Customer/User/Lead                | Find or Create Customer/User/Lead |
| New Ticket/Request               | Update Ticket/Request/Conversation   | Find Ticket/Request/Conversation       |                                   |
| New Customer/User/Lead           | Add/Remove Tag on User/Ticket/Lead   |                                        |                                   |
| New Chat/Message/Conversation    | Send Message                         |                                        |                                   |
| New Closed/Finished Conversation | *Create or Update Customer/User/Lead |                                        |                                   |
|                                  | Add Comment/Note on Ticket/Request   |                                        |                                   |
|                                  | Create Customer/User/Lead/Company    |                                        |                                   |
{% endcapture %}
{{ styled_table | markdownify | replace: '<table>', '<table class="even-columns">' }}

*If you’re adding a _Create or Update_ action instead of the [recommended _Update_ action to go along with a _Find or Create_ action](https://platform.zapier.com/publish/integration-publishing-guidelines#56-create-or-update-functionality), it’s best practice to return in the response payload whether the action taken was a create or update. This way, users can add appropriate next steps to their Zap depending on the scenario.

View [example apps](https://zapier.com/apps/categories/customer-support).

### CRM (Customer Relationship Management)
{% capture styled_table %}
| Triggers                         | Actions                              | Searches                               | Search or Creates                              |
|----------------------------------|--------------------------------------|----------------------------------------|------------------------------------------------|
| *New Record/Module Entry         | *Create Record/Module Entry          | *Find Record/Module Entry              | *Find or Create Record/Module Entry            |
| New Contact/Lead/Person/Company  | *Update Record/Module Entry          | Find Lead/Contact/Person/Company       | Find or Create Lead/Contact/Person/Company     |
| New Deal/Opportunity/Job/Inquiry | Create Contact/Lead/Person/Company   | Find Deal/Opportunity                  | Find or Create Deal/Opportunity                |
| Tag Added or Removed             | Update Contact/Lead/Person/Company   |                                        |                                                |
| **Updated Record/Module Entry    | *Create or Update Contact/Lead/Person/Company   |                             |                                                |
| Updated X Stage/Status (i.e. deal, opportunity, project, lead) | Create Deal/Opportunity |                       |                                                |
|                                  | Update Deal/Opportunity              |                                        |                                                |
|                                  | Create Note                          |                                        |                                                |
|                                  | Add Contact/Lead to Campaign/Group   |                                        |                                                |
|                                  | Create Activity/Event                |                                        |                                                |
|                                  | Add Tag to X (i.e. Contact, Record, Opportunity) |                            |                                                |
{% endcapture %}
{{ styled_table | markdownify | replace: '<table>', '<table class="even-columns">' }}

*Cover the most popular models of your platform at a minimum. You can create individual triggers, actions, and searches for each model such as, "New Customer", "New Deal", "Create Customer", and "Create Deal". Or create a singular trigger, action, and search that each support multiple models by requiring users to select which model they're taking action on via an input field, such as "New Record" and "Create Record".

**_Updated_ triggers for CRMs are often most useful when users are able to specify which field(s) to watch for updates on, instead of triggering on any and all updates. 

View [example apps](https://zapier.com/apps/categories/crm).

### Databases
{% capture styled_table %}
| Triggers                  | Actions               | Searches                                     | Search or Creates                     |
|---------------------------|-----------------------|----------------------------------------------|---------------------------------------|
| New Record/Row            | Create Record/Row     | Find Record/Row                              | Find or Create Record/Row             |
| New or Updated Record/Row | Update Record/Row     |                                              |                                       |
{% endcapture %}
{{ styled_table | markdownify | replace: '<table>', '<table class="even-columns">' }}

*Zapier searches automatically return only the first result in the response. To return multiple results, [return the set of results](https://platform.zapier.com/build/response-types) as an array of objects under a descriptive key.

View [example apps](https://zapier.com/apps/categories/databases).

### Documents
{% capture styled_table %}
| Triggers                         | Actions                       | Searches                 | Search or Creates       |
|----------------------------------|-------------------------------|--------------------------|-------------------------|
| New Document                     | Create Document (from template) | Find Document          | Find or Create Document |
| Document Completed/Signed        | Add to Document               |                          |                         |
| Document Status Updated          |                               |                          |                         |
| Document Sent                    |                               |                          |                         |
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
|------------------------------------|-----------------|------------------|------------------------|
| New Order/Purchase/Sale            | Create Order    | Find Order       | Find or Create Customer|
| New Paid Order/Payment Received    | Create Customer | Find Customer    |                        |
| Abandoned Cart                     | Create Product  | Find Product     |                        |
| New Customer                       |                 |                  |                        |
{% endcapture %}
{{ styled_table | markdownify | replace: '<table>', '<table class="even-columns">' }}

View [example apps](https://zapier.com/apps/categories/ecommerce).

### Email
{% capture styled_table %}
| Triggers                         | Actions                       | Searches                 | Search or Creates       |
|----------------------------------|-------------------------------|--------------------------|-------------------------|
| New Email Matching Search        | Send Email                    | Find Email               | Find or Create Email    |
| New Email                        | Create Draft Email            |                          | Find or Create Contact  |
| New Labeled/Tagged/Starred Email | Create Contact                |                          |                         |
| New Attachment                   |                               |                          |                         |
|                                  |                               |                          |                         |
{% endcapture %}
{{ styled_table | markdownify | replace: '<table>', '<table class="even-columns">' }}

View [example apps](https://zapier.com/apps/categories/email).

### Email Newsletters
{% capture styled_table %}
| Triggers                          | Actions                                  | Searches                                  | Search or Creates                         |
|-----------------------------------|------------------------------------------|-------------------------------------------|-------------------------------------------|
| New Subscriber/Contact in List/Audience/Tag | *Create or Update Subscriber/Contact | Find Subscriber/Contact             | Find or Create Subscriber/Contact         |
| New Subscriber/Contact            | Send Email/Campaign                      |                                           |                                           |
| Email Opened/Link Clicked         | Add/Subscribe Contact to List/Audience/Tag     |                                     |                                           |
|                                   | Create Subscriber/Contact                |                                           |                                           |
{% endcapture %}
{{ styled_table | markdownify | replace: '<table>', '<table class="even-columns">' }}
*If you’re adding a _Create or Update_ action instead of the [recommended _Update_ action to go along with a _Find or Create_ action](https://platform.zapier.com/publish/integration-publishing-guidelines#56-create-or-update-functionality), it’s best practice to return in the response payload whether the action taken was a create or update. This way, users can add appropriate next steps to their Zap depending on the scenario

View [example apps](https://zapier.com/apps/categories/email-newsletters).

### Event Management
{% capture styled_table %}
| Triggers                  | Actions                        | Searches          | Search or Creates             |
|---------------------------|--------------------------------|-------------------|-------------------------------|
| New Registrant/RSVP       | Create Attendee/Add Registrant |                   |                               |
| New Order/Booking/Ticket  | Create Event                   |                   |                               |
| New Event | Create Event  |                                |                   |                               |
| New Attendee/Contact/Lead |                                |                   |                               |
{% endcapture %}
{{ styled_table | markdownify | replace: '<table>', '<table class="even-columns">' }}

View [example apps](https://zapier.com/apps/categories/event-management).

### File Management & Storage
{% capture styled_table %}
| Triggers                         | Actions                       | Searches                 | Search or Creates       |
|----------------------------------|-------------------------------|--------------------------|-------------------------|
| New File in Folder               | Upload File                   | Find File                | Find or Create Folder   |
| New Folder                       | Create Folder                 | Find Folder              |                         |
| New File                         | Create File                   |                          |                         |
| Updated File                     | Move File                     |                          |                         |
{% endcapture %}
{{ styled_table | markdownify | replace: '<table>', '<table class="even-columns">' }}

View [example apps](https://zapier.com/apps/categories/files).

### Forms & Surveys
{% capture styled_table %}
| Triggers                           | Actions                               | Searches                            | Search or Creates       |
|------------------------------------|---------------------------------------|-------------------------------------|-------------------------|
| New Entry/Form Response/Submission | Create Entry/Form Response/Submission | Find Entry/Form Response/Submission |                         |
| New Lead                           | Send Form                             |                                     |                         |
{% endcapture %}
{{ styled_table | markdownify | replace: '<table>', '<table class="even-columns">' }}

View [example apps](https://zapier.com/apps/categories/forms).

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
| Triggers                             | Actions                                            | Searches                           | Search or Creates                      |
|--------------------------------------|----------------------------------------------------|------------------------------------|----------------------------------------|
| New Contact/Lead/Subscriber          | *Create or Update Opportunity/Deal                 | Find Contact/Lead/Subscriber       | Find or Create Contact/Lead/Subscriber |
| New Contact in List/Audience/Segment | *Create or Update Contact/Lead/Subscriber          | Find Deal                          |                                        |
| Tag Added/Removed from Contact/Lead/Subscriber | Update Opportunity/Deal                  |                                    |                                        |
| Updated Deal/Pipeline Stage          | Add Contact/Lead/Subscriber to Campaign/List/Group |                                    |                                        |
| New Order/Purchase/Sale              | Update Contact/Lead/Subscriber                     |                                    |                                        |
| New Form Entry/Submission            | Create Opportunity/Deal/Order                      |                                    |                                        |
| Updated Contact/Lead/Subscriber      | Create Contact/Lead/Subscriber                     |                                    |                                        |
|                                      | Add/Remove Tag fro Contact/Lead/Subscriber         |                                    |                                        |
{% endcapture %}
{{ styled_table | markdownify | replace: '<table>', '<table class="even-columns">' }}

*If you’re adding a _Create or Update_ action instead of the [recommended _Update_ action to go along with a _Find or Create_ action](https://platform.zapier.com/publish/integration-publishing-guidelines#56-create-or-update-functionality), it’s best practice to return in the response payload whether the action taken was a create or update. This way, users can add appropriate next steps to their Zap depending on the scenario.

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
| Triggers                           | Actions                            | Searches                          | Search or Creates             |
|------------------------------------|------------------------------------|-----------------------------------|-------------------------------|
| New Order/Sale/Purchase/Subscription | Enroll User/Add User to Course   | Find User/Student                 | Find or Create User/Student   |
| New Enrollment                     | Create Credentials/Grant Access/Issue Credentials |                    |                               |
| Course/Lesson Completed            | Subscribe User to List/Add User to Group |                             |                               |
| New User/Student                   | Unenroll User/Student              |                                   |                               |
{% endcapture %}
{{ styled_table | markdownify | replace: '<table>', '<table class="even-columns">' }}

View [example apps](https://zapier.com/apps/categories/it-operations-education).

### Payment Processing
{% capture styled_table %}
| Triggers                            | Actions                             | Searches                         | Search or Creates          |
|-------------------------------------|-------------------------------------|----------------------------------|----------------------------|
| New Payment or Payment Paid         | Create Customer                     | Find Invoice/Payment/Transaction | Find or Create Customer    |
| New Subscription/Order/Sale/Transaction/Invoice | Create Payment Link (if applicable) | Find Customer        |                            |
| New Customer                        | Update Customer                     | Find Subscription                |                            |
| Canceled Subscription/Order/Sale    |                                     |                                  |                            |
| Failed Payment                      |                                     |                                  |                            |
| New Refund                          |                                     |                                  |                            |
{% endcapture %}
{{ styled_table | markdownify | replace: '<table>', '<table class="even-columns">' }}

View [example apps](https://zapier.com/apps/categories/payment-processing).

### Phone & SMS
{% capture styled_table %}
| Triggers                         | Actions                       | Searches                 | Search or Creates       |
|----------------------------------|-------------------------------|--------------------------|-------------------------|
| New SMS/Message Received         | Create or Update Contact      | Find Contact (by phone number) | Find or Create Contact  |
| New Call                         | Send SMS/Message              |                          |                         |
| New Recording                    | Create Contact                |                          |                         |
| Call Completed                   | Call Phone Number             |                          |                         |
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
| New Task/Item/Issue               | Create Task/Item/Issue                 | Find Task/Item/Issue                   | Find or Create Task/Item/Issue   |
| Task/Item/Issue Status Changed    | Update Task/Item/Issue                 | Find User                              | Find or Create Project/Board     |
| New Label/Tag on Task/Item/Issue  | Add Comment/Note to Task/Item/Issue    | Find Project/Board                     |                                  |
| Completed Task/Item/Issue         |                                        |                                        |                                  |
| New Event/Activity                |                                        |                                        |                                  |
| Updated Task/Item/Issue           |                                        |                                        |                                  |
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
| Triggers                        | Actions                                | Searches                 | Search or Creates         |
|---------------------------------|----------------------------------------|--------------------------|---------------------------|
| New Client/Customer             | Create Client/Customer                 | Find Booking/Appointment | Find or Create Client     |
| New Booking/Appointment         | Create Booking/Appointment/Request/Job |                          |                           |
| New Cancellation                |                                        |                          |                           |
| Rescheduled Booking/Appointment |                                        |                          |                           |
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
| Triggers                      | Actions                       | Searches                      | Search or Creates          |
|-------------------------------|-------------------------------|-------------------------------|----------------------------|
| Document/Contract Sent        | *Create Document/Contract     | Find Document/Contract        |                            |
| Document/Contract Completed   | Send Signature Request        |                               |                            |
| Document/Contract Signed      |                               |                               |                            |
{% endcapture %}
{{ styled_table | markdownify | replace: '<table>', '<table class="even-columns">' }}

*_Create Document/Contract_ actions typically allow for users to select a template in the action’s setup.

View [example apps](https://zapier.com/apps/categories/signatures).

### Social Media Accounts
{% capture styled_table %}
| Triggers                        | Actions                  | Searches                 | Search or Creates       |
| ------------------------------- | ------------------------ | ------------------------ | ----------------------- |
| New Post/Message/Media (by me)  | Create Post/Message/Media|                          |                         |
| New Post/Message/Media          |                          |                          |                         |
{% endcapture %}
{{ styled_table | markdownify | replace: '<table>', '<table class="even-columns">' }}

View [example apps](https://zapier.com/apps/categories/social).

### Spreadsheets
{% capture styled_table %}
| Triggers                          | Actions                                | Searches                               | Search or Creates                |
|-----------------------------------|----------------------------------------|----------------------------------------|----------------------------------|
| New or Updated Row                | Create/Add Row                         | Find Row                               | Find or Create Row               |
| New Row                           | Create Row(s)                          | Find Row(s) (with line-item support)   |                                  |
|                                   | Update Row                             |                                        |                                  |
{% endcapture %}
{{ styled_table | markdownify | replace: '<table>', '<table class="even-columns">' }}

View [example apps](https://zapier.com/apps/categories/spreadsheets).

### Task Management
{% capture styled_table %}
| Triggers                          | Actions                                | Searches                               | Search or Creates                |
|-----------------------------------|----------------------------------------|----------------------------------------|----------------------------------|
| New Task                          | Create Task                            | Find Task                              | Find or Create Task              |
|                                   | Update Task                            |                                        |                                  |
{% endcapture %}
{{ styled_table | markdownify | replace: '<table>', '<table class="even-columns">' }}

View [example apps](https://zapier.com/apps/categories/todo-lists).

### Team Chat
{% capture styled_table %}
| Triggers                          | Actions                                | Searches                               | Search or Creates                |
|-----------------------------------|----------------------------------------|----------------------------------------|----------------------------------|
| New Message in Channel            | Send Channel Message                   | Find User (by email, name, username)   |                                  |
| New Reaction on Message           | Send Direct/Private Message            |                                        |                                  |
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
| Triggers                          | Actions                 | Searches        | Search or Creates |
|-----------------------------------|-------------------------|-----------------|-------------------|
| New Video (in Channel/Playlist)   | Upload Video            | Find Track      |                   |
| New Track in Playlist/Saved Track | Add Listener/Subscriber |                 |                   |
|                                   | Add Track to Playlist   |                 |                   |

{% endcapture %}
{{ styled_table | markdownify | replace: '<table>', '<table class="even-columns">' }}

View [example apps](https://zapier.com/apps/categories/video).

### Video Conferencing
{% capture styled_table %}
| Triggers        | Actions          | Searches  | Search or Creates |
| --------------- | ---------------- | --------- | ----------------- |
| New Recording   | Create/Add Registrant |           |                   |
| New Registrant  | Create Meeting   |           |                   |
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

### Website Builders
{% capture styled_table %}
| Triggers                           | Actions                    | Searches               | Search or Creates            |
| ---------------------------------- | -------------------------- | ---------------------- | ---------------------------- |
| New Form Submission/Review/Message | Create Post/Content        |                        |                              |
| New Member/User/Lead               | Create/Invite User/Member  |                        |                              |
| New Post/Content                   |                            |                        |                              |
{% endcapture %}
{{ styled_table | markdownify | replace: '<table>', '<table class="even-columns">' }}

View [example apps](https://zapier.com/apps/categories/cms).