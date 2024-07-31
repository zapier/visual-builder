---
title: Integration publishing requirements
order: 3
layout: post-toc
redirect_from:
  - /partners/integration-review-guidelines
  - /publish/integration-publishing-guidelines
---

# Integration publishing requirements

We’re excited you are creating an integration for the [Zapier Platform](https://zapier.com/developer-platform). We’re here to help you understand our platform and its requirements so that you can successfully prepare your Zapier integration for publishing. Thousands of partners have built integrations on the Zapier Platform that enable our mutual users to set up Zaps as easily and quickly as possible.

When your Zapier integration meets these requirements, it will pass the review for the publishing process quickly and smoothly. The requirements help maintain quality and consistency for all integrations listed in our [App Directory](https://zapier.com/apps).

Please review these requirements carefully before submitting to ensure your integration is compliant. Integrations and their associated apps must meet all requirements to be published.

**Important**: integrations for prohibited apps will be removed from the platform. Integrations for restricted apps or that do not meet all requirements will be allowed to remain [private](https://platform.zapier.com/quickstart/private-vs-public-integrations).

Work through each section and ask the [PublishBot](https://publishbot.zapier.app/) or write in via the [contact form](https://developer.zapier.com/contact) for any questions.

## Key considerations

- Because the Zapier Platform is always changing and improving to keep up with the needs of our customers, this is a living document.

- If you prefer your integration to be accessible to a limited group of users, or if the Zapier integration review requirements do not align with your needs, you might want to consider maintaining your integration as private. Learn more about [private vs public integrations](https://platform.zapier.com/quickstart/private-vs-public-integrations).

- We encourage diversity on the Zapier Platform, provided your integration respects users with varying viewpoints and ensures a high-quality user experience. Any integration found to contain or exhibit behavior deemed inappropriate, discriminatory, or crossing acceptable boundaries will be rejected.

- We reserve the right to reject publishing requests or to remove users and integrations from the Zapier Platform if we believe these requirements, the [Platform Agreement](https://zapier.com/platform/tos), or our [Terms of Service](https://zapier.com/legal/terms-of-service) have not been met. This includes attempts to exploit the review process, illicitly acquire user data, or manipulate test users.

## Sections

1. [Prohibited integrations](https://platform.zapier.com/publish/integration-publishing-requirements#1-prohibited-integrations)
2. [Restricted integrations](https://platform.zapier.com/publish/integration-publishing-requirements#2-restricted-integrations)
3. [Ownership and permissions](https://platform.zapier.com/publish/integration-publishing-requirements#3-ownership-and-permissions)
4. [Data security and user privacy](https://platform.zapier.com/publish/integration-publishing-requirements#4-data-security-and-user-privacy)
5. [Quality and functionality](https://platform.zapier.com/publish/integration-publishing-requirements#5-quality-and-functionality)
6. [Integration listing](https://platform.zapier.com/publish/integration-publishing-requirements#6-integration-listing)
7. [Support](https://platform.zapier.com/publish/integration-publishing-requirements#7-support)
8. [Submission process](https://platform.zapier.com/publish/integration-publishing-requirements#8-submission-process)

## 1. Prohibited integrations

Integrations built for the following apps aren't permitted and will be removed from the Zapier Platform:

### 1.1 Apps from a restricted country

Apps/integrations must not be from companies in or under the control of any country against which the United States currently has sanctions, as per section 6(d)(iv) of the [Zapier Platform Agreement](https://zapier.com/developer-platform/tos).

### 1.2 Apps from a competitor

Apps/integrations must not be from companies we deem to be competing with Zapier, as per section 2(i) of the [Zapier Platform Agreement](https://zapier.com/developer-platform/tos).

### 1.3 Apps that do not meet Zapier or third-party agreements

Apps/integrations must comply with all Zapier and other third-party agreements, including but not limited to the [Zapier Platform Agreement](https://zapier.com/developer-platform/tos) and the [Zapier Terms of Service](https://zapier.com/legal/terms-of-service). Should we ask you to supply it, you must be ready to provide supporting documentation of permission from third parties.

### 1.4 Integrations that make financial transactions

Integrations must not facilitate any form of financial transaction, transfer of assets, or payment processing. This includes the transmission of ownership of any tokens or assets in the case of blockchain or cryptocurrency apps.

### 1.5 Apps that have misleading or malicious functionality

Apps/integrations must not mislead users. Do not create a Zapier integration that can be used to spam, phish, or send unsolicited messages to users. If you attempt to cheat the system (for example, by trying to trick the review process, steal user data, or fake real users) your integration will be removed from Zapier and you could be expelled from submitting any integrations in the future. False information and features, including inaccurate data or joke functionalities, such as fake phone calls or SMS are prohibited.

### 1.6 Apps that have objectionable content

Apps/integrations should not include content that is discriminatory, defamatory, offensive, mean-spirited, or insensitive with regard to gender, religion, sexual orientation, age, race, national/ethnic origin, or other targeted groups.

## 2. Restricted integrations

Integrations built for the following apps will not be published but will be allowed to remain [private](https://platform.zapier.com/quickstart/private-vs-public-integrations):

### 2.1 Replacement integrations

The integration should not have an equivalent that has already been published in our [app directory](https://zapier.com/apps). Each published integration should represent a distinct, independent app to ensure the best experience for our mutual customers. If you're attempting to replace an existing public integration, please refer to the guide on [versions](https://platform.zapier.com/manage/versions) and how to [plan changes](https://platform.zapier.com/manage/planning-changes). Publishing separate integrations for the same app brand is not permitted.

### 2.2 Multiple integrations

Do not create separate integrations for functionality that share the same authentication method and interact with the same API, unless each integration is for a separate product or service (not feature) that is clearly marketed independently. Instead, consolidate the functionality into one, high-level integration.

## 3. Ownership and permissions

### 3.1 APIs

You own or have permission to use all APIs used by the integration. Details of those permissions are supplied on request.

The account owning the integration must have proper access to the associated platform and APIs, either by working for, being associated with, or being contracted by the company whose integration is in review. This is so we can reach out with questions or support issues during the review and after the integration is public. If it’s not obvious to us that the owning account is associated with your integration’s company (largely by email domain), we will request proof via an email from a matching domain as the platform or confirmation from someone at the company.

Scenarios in which integrations are permitted on the Zapier Platform by status, ownership, and intention:

| Private                                                                                                                                                                                                    | Public                                                                                                                                                                                                                                                                       | Not Allowed                                                                                                                                        |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------- |
| Anyone that accepts [Zapier Terms of Service](https://zapier.com/platform/tos) can build a private integration.                                                                                            | Integrations by developers who work for the company owning the API or have been contracted by the API owner can go public.                                                                                                                                                   | Integrations by developers who are building on an API they own but for a competing product with Zapier.                                            |
| Integrations by developers building on a private API with no intention of going public, are permitted to remain private/invite-only indefinitely.                                                          | Integrations by developers who work for or third-party developers (preferably a [trusted developer](https://platform.zapier.com/quickstart/trusted-developers)) hired by the company owning the API and intended to go public, are permitted as private before going public. | Integrations by developers who do not own the API used in the integration or who have not been given explicit permission by the owners of the API. |
| Integrations by developers who are building on a public API they do not own, and routing traffic to their own servers. Exceptions apply when building on an approved third-party API.                      |                                                                                                                                                                                                                                                                              |                                                                                                                                                    |
| Integrations by developers building on a public API they do not own and intend to share with their team (within their company or organization, family and friends, etc.) are only permitted to be private. |                                                                                                                                                                                                                                                                              |                                                                                                                                                    |
| Integrations by developers building on a public API they do not own and intend to sell access to the integration, are only permitted to be private.                                                        |                                                                                                                                                                                                                                                                              |                                                                                                                                                    |
| Integrations by developers building with sandbox/test/dev environments or endpoints are only permitted to be private.                                                                                      |                                                                                                                                                                                                                                                                              |                                                                                                                                                    |

### 3.2 Trademarks

You own or have permission to use all trademarks used in the integration. Details of those permissions are supplied on request.

Zapier trademarks can't be used in an integration name, but they can be used in the description and partner marketing material in accordance with our [brand guidelines](https://brand.zapier.com/).

## 4. Data security and user privacy

### 4.1 Integration handles data appropriately

The integration does not facilitate or encourage end users to transmit or receive sensitive personal data in violation of the [Zapier Terms of Service](https://zapier.com/legal/terms-of-service).

### 4.2 Integration uses HTTPS

For security reasons, all API endpoints used by an integration (including authentication and login pages) must utilize HTTPS instead of HTTP.

### 4.3 Integration stores credentials securely

Do not hard code credentials such as API Keys, Client IDs, Client Secrets, etc. into your integration. Use the appropriate section in the Platform UI (e.g. Application Credentials) or use [environment variables](https://platform.zapier.com/build/env) instead.

## 5. Quality and functionality

### 5.1 App has been publicly launched

Your app has been fully launched to the public and isn't an invite-only or “beta” app.

### 5.2 App APIs are documented

Your app’s API and all other non-Zapier APIs used in the integration have clear, accurate, up-to-date, documentation covering all API endpoints. Links to this documentation are supplied in your publishing submission.

### 5.3 Integration is production-ready

The integration has been fully tested and does not have any unexpected or unhandled errors. All integration triggers, actions, and searches have been tested using Zaps in a Zapier account. Every test Zap has been turned on and has at least one successful run in the [Zap history](https://zapier.com/app/history).

Do not delete these Zaps or Zap runs. We may ask you to share your test Zaps with us when you submit your integration for review.

Use the Monitoring page in the Platform UI to check integration events and ensure the integration does not have unexpected or unhandled errors.

For more information and guidance, refer to [Integration Build Guidelines](https://platform.zapier.com/publish/integration-build-guidelines) and [Test and monitor your integration in your Zapier account](https://platform.zapier.com/build/test-monitoring).

### 5.4 Integration uses production APIs

The integration uses production API endpoints. Integrations using sandbox/test/dev endpoints will not be published

### 5.5 Integration requests authentication credentials appropriately

Authentication credentials are only requested from users via the [Authentication](https://platform.zapier.com/build/auth) configuration. Integrations that request authentication credentials to be entered in other configurations, such as triggers, actions, or searches, will not be published.

### 5.6 Integration has a valid connection label

[Connection labels](https://platform.zapier.com/build/connection-label) are optional but can help users identify which account each [app connection](https://help.zapier.com/hc/en-us/articles/8496258785421-Connect-your-app-accounts-to-Zapier) uses. Suitable values include account name, email address, and name.

Sensitive information such as API keys, secrets, and lengthy ID values are not allowed. Do not hard code values such as the application’s name or words like “success”, as these are already communicated in the UI.

### 5.7 Integration uses English language

Currently, the Zapier Platform supports only English. All user-facing text, such as the name and description of your integration, trigger/action/search names, field names, output field labels, help texts, and error messages, must be in English. However, data sent to and received from your API can be in your product's native language.

### 5.8 Integration follows naming conventions

Triggers, actions, searches, and input fields should be named according to platform conventions. For more information, refer to [Trigger Copy](https://platform.zapier.com/publish/integration-build-guidelines#trigger-design-and-copy), [Trigger input fields](https://platform.zapier.com/publish/integration-build-guidelines#trigger-input-fields), [Action Copy](https://platform.zapier.com/publish/integration-build-guidelines#action-design-and-copy), [Action input fields](https://platform.zapier.com/publish/integration-build-guidelines#action-input-fields), [Search Copy](https://platform.zapier.com/publish/integration-build-guidelines#search-design-and-copy), and [Search input fields](https://platform.zapier.com/publish/integration-build-guidelines#search-input-fields).

## 6. Integration listing

### 6.1 Integration name is unique and matches your application’s core branding

Enter your application name exactly as it appears in your core branding. Search our [app directory](https://zapier.com/apps) to make sure your integration name is not already in use.

Do not include trademark or copyright identifiers like a TM suffix or words like "app" or "integration." Do not include your website's domain (e.g., `.ai`) or your company name unless they are always used in your core branding when referring to your app.

### 6.2 Integration description follows convention

Enter a short description of your application’s core features and use cases, that leads with your app name in the form of `<Integration Name> is a....`. The description should not include links or mentions of Zapier or other apps, or make it appear your integration is associated with or endorsed by Zapier. Focus less on selling the application, instead, provide a clear explanation of what your application actually does.

**Examples**:

- `Trello is a team collaboration tool to organize anything on a kanban board.`, **not** `Trello is the best project management tool`.
- `Dropbox lets you store files online, sync them to all your devices, and share them easily.`, **not** `A file storage app`.

### 6.3 Integration homepage URL correctly set

Enter the URL of your application’s marketing website, not the application URL or login page, etc.

## 7. Support

### 7.1 Application has a valid test account

The submission includes a valid test account created in the application. The test account allows Zapier support staff to view your app's interface for troubleshooting and assisting our shared users once an integration is published.

- The test account must be non-expiring and use this email address: integration-testing@zapier.com.
- Zapier support staff must be able to change the account password unless the account uses “passwordless authentication,” such as OTP or “magic link.”
- Ensure all necessary features are enabled for testing Zap steps (triggers and actions). Include any required paid features and avoid trial limitations.
- Provide a demo video or detailed documentation for any complex features. Supply all account credentials required to log in and configure the account appropriately, avoiding super admin access or internal-only features.

### 7.2 Integration has a qualifying team member

Integrations must have at least one [admin team member](https://platform.zapier.com/manage/add-team) with an email address from the application or API’s top-level domain, or the company owning the API used in the integration. Add new team members to an integration by following this guide: [Invite team members to your integration](https://platform.zapier.com/manage/add-team).

## 8. Submission process

### 8.1 Repeated submissions

Submitting multiple integrations that are essentially the same delays the Zapier process and risks rejection of all submissions. Please avoid flooding the Zapier team with consecutive submissions of the same integration during the review process. Violating this policy may result in slower review times or further penalties.

### 8.2 Approval discretion

At our discretion, we reserve the right to reject publishing requests or to remove users and integrations from the Zapier Platform if we believe these requirements, the [Platform Agreement](https://zapier.com/platform/tos), or our [Terms of Service](https://zapier.com/legal/terms-of-service) have not been met. This includes attempts to exploit the review process, illicitly acquire user data, or manipulate test users
