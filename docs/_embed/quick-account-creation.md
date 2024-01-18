---
title: Quick Account Creation
order: 2
layout: post-toc
---

# Quick Account Creation

Quick Account Creation is a seamless, accelerated sign-up feature allowing first time Zapier users to skip the standard sign-up procedure and onboarding survey. Enabling Quick Account Creation as part of your embed tool code helps provide a more frictionless experience for end users.

Instead of being directed to a sign-up screen, users are presented with a consent page to connect to Zapier, then proceed to the Zap editor if consented. If an existing Zapier account under the email does not exist, users will receive an email prompting them to finish setting up their account. This allows users to dive directly into the Zap editor to accomplish the task at hand efficiently and without context switching.

## Case study

Signups to use Adalo's integration jumped 40% after embedding Zapier with Quick Account Creation into their app builder. [Read more about Adalo's user experience and results.](https://zapier.com/blog/adalo-user-experience-with-zapier/)

## Example implementation

This video demonstrates how to implement Quick Account Creation using the Zap template element within Adalo's platform. This provides users with a faster, seamless sign-up experience.

<iframe allowtransparency="true" title="Search or create" allowFullscreen frameborder="0" scrolling="no" class="wistia_embed" name="wistia_embed" src="https://cdn.zappy.app/v1f21dbddbc570407248253c13859a5d9.mp4" width="640" height="360"></iframe>

## Prerequisites

- New or existing implementation of the [Full Zapier Experience](https://platform.zapier.com/embed/full-zapier-experience), [Zap templates element](https://platform.zapier.com/embed/zap-templates), or [Partner API](https://platform.zapier.com/embed/partner-api).
- Access to your user’s first name, last name, and email on the page supporting Quick Account Creation.

## Add support on embed elements

1. Go to the [generator tool](https://zapier.com/partner/solutions/plug-and-play) for either the [Full Zapier Experience]((https://platform.zapier.com/embed/full-zapier-experience)) or [Zap templates element](https://platform.zapier.com/embed/zap-templates).
2. Customize the visual design and features of the embed solution of choice.
3. Generate the embed code in HTML, Vanilla JS, React, Angular, or Vue.js.
4. Replace the placeholder values set to `sign-up-email`, `sign-up-first-name`, and `sign-up-last-name` in the code **Body**. All three values and the client ID are required for Quick Account Creation.
5. Embed both the **Head** and **Body** code on your product's page.

You can still embed the Full Zapier Experience and Zap templates element, or utilize the Partner API without support for Quick Account Creation. If the four required fields aren’t provided, the embed will use the default behaviour redirecting users to Zapier's signup page from your product's page.

If you have an existing Full Zapier Experience or Zap templates element embed, you can add the new required fields for Quick Account Creation to your current code implementation, instead of re-customizing and regenerating the code. Make sure the **Body** code includes the below four fields with the placeholder values replaced:
- client-id="your_integration_client_id"
- sign-up-email="email_of_your_user@example.com"
- sign-up-first-name="first_name_of_your_user"
- sign-up-last-name="last_name_of_your_user"

## Add support to the Partner API

1. Use the URL below to initiate Quick Account Creation, then redirect users into the Zap editor with the Zap template set in the parameters:
```
https://zapier.com/webintent/create-zap?template=<zap-template-id>&utm_source=partner&utm_medium=embed&utm_campaign=partner_api&utm_content=partner_quick_account_creation&entry-point-location=partner_embed&referer=<referer>&referrer=<referrer>&sign-up-first-name=<sign-up-first-name>&sign-up-last-name=<sign-up-last-name>&sign-up-email=<sign-up-email>&client-id=<client-id>
```

2. Replace the following query parameter placeholders in the URL:

|      Parameter          | Requirement | Explanation                                                                                        |
| :---------------------: | :---------: | -------------------------------------------------------------------------------------------------- |
| **client_id**           |  Required   | Your application Client ID.                                                                        |
| **template**            |  Required   | An ID of a Zap Template.                                                                           |
| **sign-up-first-name**  |  Required   | First name of the user signing up.                                                                 |
| **sign-up-last-name**   |  Required   | Last name of the user signing up.                                                                  |
| **sign-up-email**       |  Required   | Email address of the user signing up.                                                              |
| **refer** or **referrer**|  Required   | URL of the page where the user clicked the link.                                                   |

After an account is created, a [user token still needs to be procured](https://platform.zapier.com/embed/partner-api#access-token) to access specific Partner API endpoints. Generally, since the user will already be signed in to their newly created account in an active session on Zapier, users won't have to explicitly sign in again when prompted with Zapier's OAuth flow.

## When Quick Account Creation is enabled

- If the user is already logged into Zapier, they are redirected to the Zap editor.
- If the user’s email is already associated with a Zapier account, but the user is not logged in, they are redirected to Zapier's sign-in page.
- If the user's email is not associated with an existing Zapier account, they are redirected to the consent page.
  - If the user consents to the terms and selects "Continue", a Zapier account is created on their behalf and they are redirected to the Zap editor. They receive an email to finish setting up their account shortly after the account is created.
  - If the user closes the consent page, no Zapier account is created.
  - If there is an error creating an account, the user is redirected to an error page.
