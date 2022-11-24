---
title: How to Build and Publish a Zapier Integration
order: 1
layout: post-toc
redirect_from: /partners/
---

## 1. Plan Your Zapier Integration

No app can do everything on its own. The best apps are instead focused on their core features, then rely on integrations with dozens of other great apps to do the rest. That is what the Zapier platform enables. It brings the best of every app together.

A Zapier integration connects your app to {{ site.partner_count }} of the best business and productivity apps so millions of Zapier users can add it to their workflows.

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

While you're building your integration, it's best to test authentication, triggers, and actions as you add them to your app. In the Platform UI, you can test each step live in the editor as it's built. With both Platform UI and CLI, have a separate tab open in your browser to the user-facing [Zap editor](https://zapier.com/app/editor), then refresh anytime you add a new trigger or action to test it live immediately.

> **Note:** You may have to refresh a few times for new triggers and actions to appear.

After you're done building, invite users to try your integration before making it available to a wider audience.

#### Invite Others to Help Test Your Integration

As you're getting close to finishing development, you’ll want others to try out your app using Zapier. You can invite co-workers or your users to provide feedback. Invitees must have a Zapier account, which they can create for free during the invite process.

You can invite people directly to your integration from Zapier's Platform UI, whether you built it in the Platform UI or CLI. Open Zapier's developer platform at [zapier.com/app/developer](https://zapier.com/app/developer), select your app, then click the _Sharing_ tab on the left. There, you can enter contacts' email addresses to invite them to your integration, or can copy a public invite link to share with those whom you want to test. The link will invite users to all versions of your app, while email invites allow you to select specific version(s) to share.

![Invite screen](https://cdn.zapier.com/storage/photos/d7e6f91a029c9ae740f70e475c97081d.png)

When users accept your invite or click the link, they'll see a page that explains that you have invited them to your app, covers some common questions about Zapier, and explains that you will support your app while in beta.

After accepting the invite, users land in the Zapier editor, where they are prompted to build a Zap with your product.

It's a good idea to reach out to the users you invited and check in on their experience using your integration with Zapier so that you can identify any usability issues.

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

Read our [App Review Guidelines](https://platform.zapier.com/partners/integration-review-guidelines) to help you better prepare your integration before submitting it for review.

Then, navigate to the Publishing page for your app, fill out the form, and click _Submit for Review_.

![](https://cdn.zappy.app/0055e6014cceb63fdb90ad671eb13229.png)

Expect to hear from us within a week.

<a id="early"></a>

### Your App is Now a Part of the Zapier Platform!

Your app will be listed with a dedicated page in [Zapier's App Directory](https://zapier.com/apps). All Zapier users can discover your app and start building Zaps with your integration. Your new integration will feature a Beta tag when it's first published. At this point you'll have access to build Zap Templates, which are the best way to help new users discover specific useful things they can do with your integration.

### What's the Next Step?

As your integration continues to accumulate users, our team will watch the growth of your integration. Once your integration [reaches 50 users](https://zapier.com/developer/documentation/v2/app-lifecycle/#1-wait-for-an-invite-from-the-zapier-team), our partner team will reach out and talk about next steps working with Zapier to grow your business and share Zapier with your users.

## 4. Launch with the Partner Program

We may invite your company to officially launch your Zapier integration and join the [Zapier Integration Partner Program](https://zapier.com/platform/partner-program). Once you launch, you will automatically join the free **Zapier Integration Partner Program** and can access the program's [many co-marketing benefits](https://zapier.com/platform/partner-program) including:

- A [dedicated blog post](https://cdn.zapier.com/storage/photos/208bc1f088e3f2153b4631b6896f8cfe.png), [email](https://cdn.zapier.com/storage/photos/c7f8293e9d9cbc5b64051ae6ecca1b8c.png), and social media campaign about the launch of your integration
- [Get leads](https://cdn.zapier.com/storage/photos/961169e674f45d11ff50e2c0510ff200.png) from your page in [Zapier's App Directory](https://zapier.com/apps)
- Exposure within Zapier's product and on the sites of Zapier's {{ site.partner_count }} integration partners

Here are the steps to take to officially launch and join the program:

<a id="wait"></a>

### **1. Build, test, and publish your Beta integration**

See previous section on building and publishing a new integration.

As mentioned above, you’ll need to complete the following tasks before the Beta tag is removed from your app listing:

- Create at least 10 Zap Templates
- Submit Help Docs
- Reach 50 users OR embed your Zap Templates into your own product

Remember, once you fulfill the criteria above, you’ll automatically join the free Zapier Partner Program to earn co-marketing benefits as your integration grows.

Up next, we’ll dive into these requirements more.

### Create 10 Zap Templates

***Estimated time to complete:*** _1-2 hours_

***Who to involve:*** _Your product or marketing team_

As soon as your app is published and in beta you can begin creating and sharing [Zap Templates](https://zapier.com/developer/zap-templates). Zap Templates are readymade integrations or Zaps with the apps and core fields pre-selected. In a few clicks, they help people discover a use case, connect apps, and turn on the Zap. We’ll look for a least 10 of these in place before an official partnership launch.

### Help our team create Help Docs on Zapier.com

***Estimated time to complete:*** _5 minutes_

***Who to involve:*** _Your product or marketing team_

The Zapier team provides frontline support for your integration and, in order to provide the best experience for your users, we also host help documentation about your integration on our site. Help our support team create accurate documentation by filling out [this form](https://eu.jotform.com/form/202233475923352).

### Reach 50 users

While your integration is in beta, we'll monitor how it's performing. When your integration reaches 50 users, our team will get in touch to invite you to start the official partner program launch process.

<a id="beta"></a>

### Easily embed your Zapier integration into your product

***Estimated time to complete:*** _5-10 minutes for an engineering or technical resource_

***Who to involve:*** _Your product and development team_

The best way to ensure users are able to discover how to connect your app to {{ site.partner_count }} other apps is to surface your integration where your users are looking for it. Using Zapier’s embedding technology, you can present your most popular Zap Templates to your users in your app’s UI, help docs, FAQs, blog posts, and more.

There are lots of ways to embed Zapier workflows into your product. Jump into the Embed section of your developer dashboard for an interactive sandbox, but the high-level breakdown is below.

> **Tip:** Looking for buy-in from your team on embedding Zapier into your product? Share examples and how it’ll make your customers happier, more loyal, and more successful with [this resource](https://zapier.com/partner/solutions). 

**Option 1**
The Full Zapier Experience and embedding Zap Templates: Embed quickly by copying and pasting a few simple lines of code

Use our [plug and play solutions](https://zapier.com/partner/solutions/plug-and-play) to generate your own Full Zapier Experience or embed Zap Templates that features your app. This small snippet of code allows you to quickly and easily embed the Full Zapier Experience and/or your Zap Templates on your site and in your product.

Here is an example of what it looks like for MailChimp:

<zapier-zap-templates theme="light" apps="mailchimp" create-without-template="hide" limit="5" use-this-zap="show"></zapier-zap-templates>

**Option 2**
The Partner API: Embed in a customized way to fit the style of your product

Our [Partner API](https://platform.zapier.com/partners/zap-templates#embed-zapier-into-your-app-with-zapier-partner-api) gives you total control over the look and feel of the Zapier experience inside your app.

Here is an example of how our partner Unbounce implemented the Partner API inside their product:

![](https://cdn.zapier.com/storage/photos/9e769e34030c2bbcf2fb80b827d69c22.png)

### Create help documentation for the integration on your site

***Estimated time to complete:*** _1 day_

***Who to involve:*** _Your support or marketing team_

Make sure your users of your Zapier integration can get their questions answered easily. Create help documentation on your site like our partner Autopilot did:

![](https://cdn.zapier.com/storage/photos/90186e0afa54eab0817ae1f66488d380.gif)

We've put together [this template](https://docs.google.com/document/d/1eg3CaU9ytf5QH38FuaxAyQgmFN2HYZFbBN7E3l9kZZg/edit) to help you get your page up quickly.

### **2. Create a marketing campaign for your integration’s full launch**

***Estimated time to complete:*** _1-2 weeks_

***Who to involve:*** _Your marketing team_

After you've passed the Beta phase, work with your marketing team to create a launch campaign to let your users know that they can now connect your product to {{ site.partner_count }} web apps. Marketing campaigns help you get more users on your integration right away, so you can rise the ranks of the Zapier Partner Program more quickly.

Here's some inspiration from some of our most successful partners:

- Write a blog post about the integration like [Evernote](https://evernote.com/blog/speed-up-evernote-workflows-with-zapier/) did
- Send an [email](https://cdn.zapier.com/storage/photos/c760446e7cd5a1448ba66aeb6b7b002a.png) to your users to announce the integration like Wunderlist did
- Send an [in-app announcement](https://cdn.zapier.com/storage/photos/6ddd0d8aeb90f73590673cfa569c192f.png) like Feedly did
- Promote the integration on social media like [Hootsuite](https://cdn.zapier.com/storage/photos/71c1d98949f7063bbbd210de211f0e47.png) did
- Feature your Zapier integration in your product's onboarding sequence like [Base CRM](https://cdn.zapier.com/storage/photos/9b1c3ac4d870456e5f4ceedc85159878.png) does
- Add your Zapier integration to your website's [integration directory](https://cdn.zapier.com/storage/photos/edaae7a3799ad14ecc970daa0ea49b8f.gif) like Zoho Connect

Make sure to check out [Zapier's brand guidelines](https://zapier.com/resources/partner-marketing) as you're planning!

## 5. Get Zapier Integration Support

![](https://cdn.zapier.com/storage/photos/352d5dea5b77da6d6e0c930c67d90be4.png)

Once you've launched your Zapier integration in the partner program, you're enrolled in the [Zapier Partner Program](https://zapier.com/platform/partner-program) and are eligible for a variety of benefits. Congrats! You'll receive monthly emails from us about how your integration is doing, plus updates on where you stand and what benefits you're eligible for.

- Have questions about how the Zapier Partner Program works? [Check out our FAQ page](https://platform.zapier.com/partners/partner-faq#zapier-partner-program-faqs).
- Curious about how to increase usage and move up levels in the program? Here are some [tips on getting more users](https://platform.zapier.com/partners/partner-faq), according to top Zapier partners.

_Have any other questions about the Partner Program? Please [email us](mailto:partners@zapier.com)._
