---
title: Zapier Integration Tips and FAQs
order: 6
layout: post-toc
redirect_from: /partners/
---

# Zapier Integration Partner Tips and FAQs

Before developing your Zapier integration, it’s important to be familiar with the criteria Zapier uses to review all new integrations. Follow our [Integration Branding and Design Guidelines](https://platform.zapier.com/partners/planning-guide) when building your integration.

The following tips are based on the most common issues we encounter and will help you successfully launch your integration. Check out [Common Migration Errors](/partners/common-migration-errors) for tips if you're ready to deploy a new version of your integration.

## Get Familiar with Zapier

If you haven't used Zapier before, [sign up](https://zapier.com/sign-up/) for a free account and try a few popular integrations before building your own. This helps you understand how Zapier works, how your users will set up Zaps, and how your integration can best fit into Zap workflows.

## Focus on Key Use Cases

Your initial Triggers, Actions, and Searches should cover the main functionality users perform on your platform to maximize utility. Check similar integrations in [Zapier's App Directory](https://zapier.com/apps/) to get ideas on which items to include in your integration. Consistently monitor feature requests from users to fill in any gaps in functionality.

## Test Early With Real Users

Hopefully, you have a bunch of keen users waiting to get their hands on your Zapier integration; don't be afraid to reach out to them for early testing. Active usage gives us confidence your integration is useable and functionally valuable for numerous users. Make sure to test the integration early and often in the Zap Editor yourself!

## Maintain Consistency in Your Integration Style

Users should be familiar with the terminology used in your Zapier integration. The input and output field labels, and trigger/action/search names must be consistent with the terminology used in your platform's own UI. It should also be consistent with the style used in other popular Zapier integrations.

We strive to give users a consistent experience throughout Zapier. Be sure to follow [Zapier's standards for app branding](https://platform.zapier.com/partners/planning-guide#how-to-brand-your-zapier-integration) so your integration fits well into the Zapier ecosystem.

## Make Connecting New Accounts Easy

Connecting to Zapier must be easy for the user. OAuth v2 is the preferred authentication scheme; otherwise, users must be able to easily retrieve or generate an API Key or other credentials themselves without needing support. Both authentication and test authentication requests should return actionable, user-friendly error messages to guide users in successfully connecting their accounts.

## Ensure Your Integration is Complete and Platform Consistent

Only submit your integration for review when it is complete and ready to be published. Make sure to thoroughly test your integration for edge cases, fix all bugs, and address [integration checks](https://platform.zapier.com/docs/integration-checks-reference) before submitting. Confirm your integration adheres to our [Integration Review Guidelines](https://platform.zapier.com/partners/integration-review-guidelines) thoroughly. Please ensure both your platform and integration work consistently without errors.

## Provide a Valid Test Account

When submitting your integration for review, we require a valid, non-expiring test account under `integration-testing@zapier.com`. During the review and going forward after launch, our team may need occasional access for troubleshooting support issues. Please ensure the account is not under a trial and all necessary paid/premium features are unlocked.

## Avoid Misleading or Malicious Functionality

Your integration must perform as advertised and must not give users a false impression. If it appears to promise certain features and functionalities, it needs to deliver. Do not create a Zapier integration that can be used to spam, phish, or send unsolicited messages to users.

Violations of the review process or guidelines can have your integration removed from Zapier, and you could be banned from submitting more in the future.

---

## Contact Zapier

Can't find the answer you need here or in Zapier's [integration planning guide](https://platform.zapier.com/partners/planning-guide)? Feel free to get in touch with our team:

### Join Zapier's Developer Community

Zapier's Platform team has a [community](https://community.zapier.com/developer-discussion-13) dedicated to helping developers with new and existing integrations. We're a worldwide team, so there's usually someone around to answer your questions. We'd love to hear about your experience building on Zapier.

### Contact Zapier's Platform Team

For questions about the developer platform and partnerships, [contact us through our help center](https://developer.zapier.com/contact), where our Platform Support team can help resolve issues you encounter while building Zapier integrations, and our Partnerships team can help with any launch questions.

If you have issues with Zaps or core Zapier account, please reach out to [our support team](https://zapier.com/app/get-help). Our support team is best equipped with the most recent logs and other details to assist you.

### Find a Zapier Integration Partner

We're excited to help you with your Zapier integration, but we can't build it for you. If you're looking for someone to take over the technical reins, check our list of [Zapier Trusted App Developers
](/partners/trusted-developers) to find someone who can help develop a Zapier integration for you.
