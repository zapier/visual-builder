---
title: Private vs public integrations
order: 3
layout: post-toc
redirect_from: 
    - /private_integrations/private-vs-public-integrations
    - /embed/zapier-plugin-chatgpt
---
# Private vs public integrations

When building an integration on the Zapier Platform, you must specify the intended audience. The intended audience determines whether the integration will be private or public:

* Public integration: For access to all Zapier customers and published in the [Zapier App Directory](https://zapier.com/apps).
* Private integration: For personal, internal (e.g. with your team) or controlled-access use.

- Building a private or public integration on the Zapier Platform is free.
- There are no fees for sharing or publishing an integration.
- Users of your integration are responsible for their own Zapier plans and billing.
- Partners do not incur fees as a result of the usage of their integration.

Both private and public integrations can connect to Zapier’s app directory of over [{{ site.partner_count }} integrations](https://zapier.com/apps). Depending on your intended audience, there will be different features available and limitations to what the integration can do. 

> **Note**: The intended audience is different from your integration’s status. All integrations, regardless of intent, start with a private status. Learn more in [Zapier integration publishing requirements](https://platform.zapier.com/publish/integration-publishing-guidelines).


## Public integrations

Public integrations are suitable for the following use cases:

* Connect your app product to Zapier for public use.
* Gain exposure from Zapier’s 3 million+ users.

 By creating a public integration, you’ll have access to these features:

* Join the [Zapier Partner Program](https://zapier.com/platform/partner-program).
* Publish your integration in [Zapier’s app directory](https://zapier.com/apps).
* [Create Zap templates](https://platform.zapier.com/publish/zap-templates).
* [Embed Zapier in your product](https://platform.zapier.com/embed/overview).
* [Embed Zap Templates in your product](https://platform.zapier.com/embed/zap-templates).
* Use [Zapier Issue Manager](https://platform.zapier.com/manage/user-feedback#3-consider-zapier-issue-manager) to manage bugs and feature requests.
* Users of your integration can [share a template of their Zaps](https://help.zapier.com/hc/en-us/articles/8496292155405-Share-a-copy-of-your-Zap).
* Users of your integration can use [Zapier's ChatGPT plugin](https://help.zapier.com/hc/en-us/articles/14058263394573).

### Limitations

If you’re building a public integration, there are specific limitations to be aware of: 

* To create a public integration, you need to meet the [Integration Ownership criteria](https://platform.zapier.com/publish/integration-publishing-guidelines#21-integration-ownership).
* You can have up to [100 admins and collaborators](https://platform.zapier.com/manage/add-team). 
* You can’t restrict who uses your public integration.



## Private integrations

Private integrations are suitable for the following use cases: 

* Connect your internal tool or system to Zapier.
* Connect your app product to Zapier to exclusively allow your team to build workflows.  
* Create an integration for a staging or testing environment.

> **Note**: We strongly recommend against the use of an independent private integration for staging purposes in the case of an existing public integration. Instead, use a private [version](https://platform.zapier.com/manage/versions) for this purpose. 

By creating a private integration:

* You control who has access to your integration.
* Your private integration won’t appear within [Zapier’s app directory](https://zapier.com/apps).

### Limitations

If you’re building a private integration, there are specific limitations to be aware of: 

* Rate limits depend on the Zapier plan of the integration owner. When using your private app in their Zaps, users' Zap runs will be [held](https://help.zapier.com/hc/en-us/articles/8496291148685-View-and-manage-your-Zap-history) if the cumulative calls across all users of your private integration exceed the following limits on the integration owner's plan:

    - Free and Professional plans: 100 calls every 60 seconds.
    - Team and Enterprise plans: 5000 calls every 60 seconds.
    - To increase a private integration rate limit for your users, [upgrade your Zapier plan](https://help.zapier.com/hc/en-us/articles/8496277302157-Change-or-cancel-your-Zapier-plan). 
    - To request an increase in the rate limit for your private integration beyond 5000 calls, contact our [Sales team](https://zapier.com/l/contact-sales).

* You can have up to [100 admins and collaborators](https://platform.zapier.com/manage/add-team). 
* You can invite up to [100 users by email](https://platform.zapier.com/manage/sharing#2-invite-users-by-email). There’s no limit when [sharing access using a public link](https://platform.zapier.com/manage/sharing#1-invite-users-with-a-public-link), but note this access cannot be revoked once a user accepts the invitation link.
* [Embedding](https://platform.zapier.com/embed/overview) Zapier and [Zap templates](https://platform.zapier.com/publish/zap-templates) are not supported.
* [Sharing a template of Zaps](https://help.zapier.com/hc/en-us/articles/8496292155405-Share-a-copy-of-your-Zap) is not supported. 
* Your app won't appear as an option on [Zapier's ChatGPT plugin](https://help.zapier.com/hc/en-us/articles/14058263394573).