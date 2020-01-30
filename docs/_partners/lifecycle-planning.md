---
title: How to Build and Publish a Zapier Integration
order: 1
layout: post-toc
redirect_from: /partners/
---

## 1. Plan Your Zapier Integration

No app can do everything on its own. The best apps are instead focused on their core features, then rely on integrations with dozens of other great apps to do the rest. That is what the Zapier platform enables. It brings the best of every app together.

A Zapier integration connects your app to 1,300+ of the best business and productivity apps so millions of Zapier users can add it to their workflows.

If you haven't yet, please read [How Zapier Works](https://zapier.com/help/how-zapier-works/) and set up a few Zaps to get a sense of the user experience.

Then, before you start building, think through how your Zapier integration will work, and plan out what triggers and actions to build.

Building on the Zapier platform is different from other platforms. Instead of defining an entire app's end-to-end user experience, you're creating discrete triggers and actions .

However, it is similar in the sense that end user experience still matters **a lot**. Simply building triggers and actions from your public API endpoints isn't enough. You'll want to strongly consider workflows your app will support and what the user experience looks like while setting up a Zap with your app.

The most successful integrations on Zapier only have two or three triggers and actions to start. You can always add more over time as users request them. If you need help figuring out what might be useful to your users, you can browse the [App Directory](https://zapier.com/apps) for similar apps and see what triggers and actions are supported.

Start out by reading through our [Zapier Integration Planning guide](https://platform.zapier.com/partners/planning-guide), which includes the guidelines and considerations needed when building a Zapier integration:

- [How to Brand Your Zapier Integration](https://platform.zapier.com/partners/planning-guide#how-to-brand-your-zapier-integration)
- [How to Design Successful Zapier Authentication Flow](https://platform.zapier.com/partners/planning-guide#authentication)
- [How to Design Successful Zapier Triggers](https://platform.zapier.com/partners/planning-guide#triggers)
- [How to Design Successful Zapier Actions](https://platform.zapier.com/partners/planning-guide#actions)
- [How to Design Successful Zapier Searches](https://platform.zapier.com/partners/planning-guide#searches)

### Learn From Popular Zapier Integration Categories

Each type of app has its own special considerations on Zapier. Form apps, for example, need to return values from multiple choice questions, while CRMs need to manage a wide variety of related data. Check our category-specific guides to learn from these best practices before building your app's Zapier integration.

- [Add a Form or Survey App to Zapier](https://platform.zapier.com/partners/integration-examples#form)
- [Add a CRM or Contacts App to Zapier](https://platform.zapier.com/partners/integration-examples#crm)
- [Add a Project Management App to Zapier](https://platform.zapier.com/partners/integration-examples#pm)

## 2. Build Your Integration

Building a Zapier integration means keeping one eye on the technical bits and one eye on the user experience.

Some of the best Zapier integrations are built when pairing an engineer and a product manager together. But anyone can build a Zapier integration, as long as you follow the guidelines in our [integration design guide](https://platform.zapier.com/partners/planning-guide) and [developer docs](https://platform.zapier.com/quickstart/introduction).

There are two ways to build Zapier integrations on Zapier's Platform:our UI-based visual builder or CLI. The visual builder lets you create a Zapier integration in your browser without code—then can customize the integration with code if needed. The CLI, instead, lets you build integrations in your local development environment, collaborate with version control and CI tools, and push new versions of your integration from the command line. Both run on the same Zapier platform, so choose the tool that fits your workflow the best.

Learn how to use the Zapier Platform with our [visual builder Quick Start tutorial](https://platform.zapier.com/quickstart/introduction) or our [CLI Quick Start tutorial](https://zapier.com/developer/start/introduction). Then visit [zapier.com/app/developer](https://zapier.com/app/developer/) or enter `zapier init` in Terminal to build a new integration.

### Test Your Integration

While you're building your integration, it's best to test authentication, triggers, and actions as you add them to your app. In Platform UI, you can test each step live in the editor as its built. With both Platform UI and CLI, have a separate tab open in your browser to the user-facing [Zap editor](https://zapier.com/app/editor), then refresh anytime you add a new trigger or action to test it live immediately.

> **Note:** You may have to refresh a few times for new triggers and actions to appear.

After you're done building, you will want to invite users to try your integration before making it available to a wider audience.

#### Invite Others to Help Test Your Integration

![Invite people to use Zapier integration](https://cdn.zapier.com/storage/photos/4fb2802664a2fe72f44d223e892ca88e.png)

As you're getting close to finishing development, you’ll want others to try out your app using Zapier. You can invite co-workers or your users to provide feedback. Invitees must have a Zapier account, which they can create for free during the invite process.

You can invite people directly to your integration from Zapire's Platform UI, whether you built it in the Platform UI or CLI. Open Zapier's developer platform at [zapier.com/app/developer](https://zapier.com/app/developer), select your app, then click the _Visibility_ tab on the left. There, you can enter contacts' email addresses to invite them to your integration, or can copy a public invite link to share privately with those who you want to test.

![Invite screen](https://cdn.zapier.com/storage/photos/d7e6f91a029c9ae740f70e475c97081d.png)

When users accept your invite or click the link, they'll see a page that explains that you have invited them to your app, covers some common questions about Zapier, and explains that you will support your app while in beta.

After accepting the invite, users will land in the Zapier editor, where they are prompted to build a Zap with your product.

It's a good idea to reach out to the users you invited and check in on their experience using your integration with Zapier so that you can identify any problematic usability issues.

#### Manage Your Integration Versions

As you work on your integration, start getting feedback from testers, and eventually release it to the public, you will want to add and change things over time. Zapier's Platform UI and CLI both support versioning to make minor or major versions of your integration. Each version is kept separate, so you can make changes to your integration without affecting other users.

Find out more in our _[How to Maintain Your Zapier Integration](https://platform.zapier.com/partners/feature-requests-bugs)_ guide.

## 3. Publish Your Integration to the App Directory

Now that you're finished developing and testing your Zapier integration, it's time to share it with the world! When you publish your integration, your product will get a dedicated page in [Zapier's App Directory](https://zapier.com/apps). Just follow these steps:

### **1. Ensure your integration follows the Zapier Integration Development Guide**

The [Integration Development Guide](https://platform.zapier.com/partners/planning-guide) is written with the user in mind, ensuring a consistent experience across Zapier. Hundreds of companies have launched Zapier integrations and the Integration Development Guide is a list of best practices learned, so your users have the best experience with your Zapier integration.

We recommend your Zapier integration have no more than 5 of each (trigger, action, or search) at first; we suggest starting with your most popular 2-3 use cases.

### **2. Have at least 1 live Zap for each of your integration's visible Triggers, Actions, and Searches**

Clone your integration and place it into invite-only mode. Doing so provides you a link to share this instance of your Zapier integration with prospective users.

The intention of this step is to ensure any show-stopping bugs are worked out and verify existing user demand. Towards this end, your users should be non-QA emails and external or outside of your company.

### **3. Prepare your team to support and maintain your integration**

Zapier's support team serves as frontline support for your Zapier integration. If your users find bugs with your integration, we will surface them to your team. We expect your team to promptly reply to those requests from your users and to maintain your integration.

### **4. Submit your integration for review by the Zapier team**

Read our [App Review Guidelines](https://platform.zapier.com/partners/integration-review-guidelines) to help you better prepare your integration before submitting it for review. Navigate to the Visibility tab for your app and click the _Make this App Public_ button. Expect to hear from us within a week.

Legacy builder:

![](https://zappy.zapier.com/511FFD77-85D4-4B93-A7BC-C2D1F52624AC.png)

New visual builder:

![](https://zappy.zapier.com/6193B587-6437-47E8-B0C1-47ABB4B05291.png)

<a id="early"></a>

### Your App is Now a Part of the Zapier Platform!

Your app will be listed with a dedicated page in [Zapier's App Directory](https://zapier.com/apps).  All Zapier users can discover your app and start building Zaps with your integration.  Your new integration will feature a Beta tag when it's first published.  At this point you'll have access to build Zap Templates, which are the best way to help new users discover specific useful things they can do with your integration.

### What's the Next Step?

As your integration continues to accumulate users, our team will watch the growth of your integration. Once your integration [reaches 50 users](https://zapier.com/developer/documentation/v2/app-lifecycle/#1-wait-for-an-invite-from-the-zapier-team), our partner team will reach out and talk about next steps working with Zapier to grow your business and share Zapier with your users.

## 4. Launch with the Partner Program

We may invite your company to officially launch your Zapier integration and join the [Zapier Integration Partner Program](https://zapier.com/platform/partner-program). Once you launch, you will automatically join the free **Zapier Integration Partner Program** and can access the program's [many co-marketing benefits](https://zapier.com/platform/partner-program) including:

- A [dedicated blog post](https://cdn.zapier.com/storage/photos/208bc1f088e3f2153b4631b6896f8cfe.png), [email](https://cdn.zapier.com/storage/photos/c7f8293e9d9cbc5b64051ae6ecca1b8c.png), and social media campaign about the launch of your integration
- [Get leads](https://cdn.zapier.com/storage/photos/961169e674f45d11ff50e2c0510ff200.png) from your page in [Zapier's App Directory](https://zapier.com/apps)
- Exposure within Zapier's product and on the sites of Zapier's 1,300+ integration partners

Here are the steps to take to officially launch and join the program:

<a id="wait"></a>

### **1. Build, Test, and Publish Your Integration**

See previous section on building and publishing a new integration.

### **2. Create 10 Zap Templates**

As soon as your app is published and in beta you can and should begin creating and sharing Zap Templates.  This is a great way to help your users discover specific, useful things they can do with your integration.  We'll look for a least 10 of these in place before an official partnership launch.

_Estimated time to complete: 1-2 hours_

_Who to involve: Your product or marketing team_

Zap Templates are readymade integrations or Zaps with the apps and core fields pre-selected. In a few clicks, they help people discover a use case, connect apps, and turn on the Zap. Zap Templates are the fastest way for your users to automate workflows. Think of 10 use cases for your integration, and [get started](https://zapier.com/developer/zap-templates) creating 10 Zap Templates for your users.

### **3. Help Our Team Create Help Docs on Zapier.com**

_Estimated time to complete: 5 minutes_

_Who to involve: Your product or marketing team_

The Zapier team provides frontline support for your integration and, in order to provide the best experience for your users, we also host help documentation about your integration on our site. Help our support team create accurate documentation by filling out [this form](https://form.jotformeu.com/73104550800343).

### **4. Reach 50 Users to Receive an Invite from the Zapier Team**

While your integration is in the Early Access stage, we'll monitor how it's performing. When your integration reaches 50 users, our team will get in touch to invite you to start the official launch process. You must receive an invite from our team before you can start the rest of this process.

<a id="beta"></a>


### **5. Surface Your Zap Templates In Your Product and On _Your_ Site**

_Estimated time to complete: 5-10 minutes for an engineering or technical resource_

_Who to involve: Your product and development team_

The best way to ensure users are able to discover how to connect your app to 1,300+ other apps is to surface your integration where your users are looking for it. Using Zapier’s embedding technology, you can present your most popular Zap Templates to your users in your app’s UI, help docs, FAQs, blog posts, and more

There are two ways to add embed your Zap Templates on your site:

**Option 1**
The Embed Widget: Embed quickly by copying and pasting a simple line of code

Use our [Embed Widget Generator](https://zapier.com/partner/embed/) to generate your own Embed Widget that features your app. This small snippet of Javascript allows you to quickly and easily embed your Zap templates on your site and in your product.

Here is an example of what it looks like for MailChimp:

<script src="https://zapier.com/zapbook/embed/widget.js?services=mailchimp&container=true&limit=5"></script>

**Option 2**
The Partner API: Embed in a customized way to fit the style of your product

Our [Partner API](https://platform.zapier.com/partners/zap-templates#embed-zapier-into-your-app-with-zapier-partner-api) gives you total control over the look and feel of the Zapier experience inside your app.

Here is an example of how our partner Unbounce implemented the Partner API inside their product:

![](https://cdn.zapier.com/storage/photos/9e769e34030c2bbcf2fb80b827d69c22.png)

### **6. Create Help Documentation for The Integration on Your Site**

_Estimated time to complete: 1 day_

_Who to involve: Your support or marketing team_

Make sure your users of your Zapier integration can get their questions answered easily. Create help documentation on your site like our partner Autopilot did:

![](https://cdn.zapier.com/storage/photos/90186e0afa54eab0817ae1f66488d380.gif)

We've put together [this template](https://docs.google.com/document/d/1A_eNBcoy8V8aB1bkVdZ386_U4WD-GkLPRDSvNBu-cCQ/edit) to help you get your page up quickly.

### **7. Create a Marketing Campaign for The Integration's Launch**

_Estimated time to complete: 1-2 weeks_

_Who to involve: Your marketing team_

Work with your marketing team to create a launch campaign to let your users know that they can now connect your product to 1,300+ web apps. Marketing campaigns help you get more users on your integration right away, so you can rise the ranks of the Zapier Partner Program more quickly.

Here's some inspiration from some of our most successful partners:

- Write a blog post about the integration like [Evernote](https://evernote.com/blog/speed-up-evernote-workflows-with-zapier/) did
- Send an [email](https://cdn.zapier.com/storage/photos/c760446e7cd5a1448ba66aeb6b7b002a.png) to your users to announce the integration like Wunderlist did
- Send an [in-app announcement](https://cdn.zapier.com/storage/photos/6ddd0d8aeb90f73590673cfa569c192f.png) like Feedly did
- Promote the integration on social media like [Hootsuite](https://cdn.zapier.com/storage/photos/71c1d98949f7063bbbd210de211f0e47.png) did
- Feature your Zapier integration in your product's onboarding sequence like [Base CRM](https://cdn.zapier.com/storage/photos/9b1c3ac4d870456e5f4ceedc85159878.png) does
- Add your Zapier integration to your website's [integration directory](https://cdn.zapier.com/storage/photos/edaae7a3799ad14ecc970daa0ea49b8f.gif) like Zoho Connect

Make sure to check out [Zapier's brand guidelines](https://zapier.com/brand/) as you're planning!

## 5. Get Zapier Integration Support

![](https://cdn.zapier.com/storage/photos/352d5dea5b77da6d6e0c930c67d90be4.png)

Once you've launched your Zapier integration in the partner program, you're enrolled in the [Zapier Partner Program](https://zapier.com/platform/partner-program) and are eligible for a variety of benefits. Congrats! You'll receive monthly emails from us about how your integration is doing, plus updates on where you stand and what benefits you're eligible for.

- Have questions about how the Zapier Partner Program works? [Check out our FAQ page](https://platform.zapier.com/partners/partner-faq#zapier-partner-program-faqs).
- Curious about how to increase usage and move up levels in the program? Here are some [tips on getting more users](https://platform.zapier.com/partners/partner-faq), according to top Zapier partners.

_Have any other questions about the Partner Program? Please [email us](mailto:partners@zapier.com)._
