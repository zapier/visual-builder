---
title: Embed your Zapier integration with the Partner API
order: 4
layout: post-toc
redirect_from:
  - /partner_api/authentication
  - /partner_api/examples
  - /partner_api/changelog
  - /partner_api/errors
  - /partner_api/endpoints
  - /partner_api/best-practices
---

# Embed your Zapier integration with the Partner API

The Partner API is the best tool for complete style control over a user's Zapier experience within your app. It allows you to customize how you present Zapier within your product without sacrificing your app's look, feel, and flow.

Think of it as a native Zapier integration, helping you showcase your best Zapier-powered workflows where it's most helpful to your users (within the flow of your tool). Customize styling, streamline Zap set-up for users and expose relevant Zap information.

Embed features are available for public integrations. To enable embed features, [update your Intended Audience](https://platform.zapier.com/quickstart/private-vs-public-integrations) to public and [submit your integration for review](https://platform.zapier.com/publish/public-integration#4-submit-your-integration-for-app-review) to be published in the Zapier App Directory. 

Once your integration is public, the integration's client ID needed to call the Partner API will be revealed under the `Embed > Settings` or `Embed > Partner API endpoints` section of that integration in the [Developer Platform](https://developer.zapier.com/).

## Highlighted capabilities

- Get a list of all the apps available in Zapier’s app directory to power your own app directory and show your users all the integration possibilities with your Zapier integration.
- Have complete style control over how you present Zap templates in your product. The Partner API gives you access to the raw Zap Template data so you can give your users access to your Zap template with your product’s style, look and feel.
- Get access to all your Zap templates and give your users the ability to search to quickly find the one they need.
- Streamline Zap setup by pre-filling fields on behalf of your users.
- Show users the Zaps they have set up from right within your product, keeping them on your site longer and giving them complete confidence in your Zapier integration.
- [Embed our Zap Editor](https://platform.zapier.com/embed/zap-editor) to allow your users to create new Zaps and modify existing ones, without needing to leave your product.