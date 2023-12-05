---
title: Support Quick Account Creation
order: 6
layout: post-toc
---

# Support Quick Account Creation

Quick Account Creation is a seamless, accelerated sign-up feature allowing first time Zapier users to skip the standard sign-up procedure and onboarding survey. Enabling Quick Account Creation as part of your embed tool code helps provide a more frictionless experience for end users.

Instead of being directed to a sign-up screen, users are presented with a consent page to connect to Zapier, then proceed to the Zap editor if consented. If an existing Zapier account under the email does not exist, users will receive an email prompting them to finish setting up their account. This allows users to dive directly into the Zap editor to accomplish the task at hand efficiently and without context switching.

## Example implementation

This video shows an example implementation of Quick Account Creation with the Zap template element embedded within Adalo's platform, providing their users with an accelerated, sign-up experience:

<iframe allowtransparency="true" title="Search or create" allowFullscreen frameborder="0" scrolling="no" class="wistia_embed" name="wistia_embed" src="https://cdn.zappy.app/v1f21dbddbc570407248253c13859a5d9.mp4" width="640" height="360"></iframe>

## Case study

Signups to use Adalo's integration jumped 40% after embedding Zapier with Quick Account Creation into their app builder. [Read more about Adalo's user experience and results.](https://zapier.com/blog/adalo-user-experience-with-zapier/)

## Prerequisites

- New or existing implementation of the [Full Zapier Experience](https://platform.zapier.com/embed/full-zapier-experience), [Zap templates element](https://platform.zapier.com/embed/zap-templates), or [Partner API](https://platform.zapier.com/embed/partner-api).
- Access to your user’s first name, last name, and email on the page supporting Quick Account Creation.

## Add support for Quick Account Creation on embed elements

1. Go to the [generator tool](https://zapier.com/partner/solutions/plug-and-play) for either the Full Zapier Experience or [Zap templates element](https://platform.zapier.com/embed/zap-templates).
2. Customize the visual design and features of the embed solution of choice.
3. Generate the embed code in HTML, Vanilla JS, React, Angular, or Vue.js.
4. Replace the placeholder values set to `client-id`, `sign-up-email`, `sign-up-first-name`, and `sign-up-last-name` in the code **Body**. All four values are required for Quick Account Creation.
5. Embed both the **Head** and **Body** code on your product's page.

You can still embed the Full Zapier Experience and Zap templates element, or utilize the Partner API without support for Quick Account Creation. If the four required fields aren’t provided, the embed will use the default behaviour redirecting users to Zapier's signup page from your product's page.

If you have an existing Full Zapier Experience or Zap templates element embed, you can add the new required fields for Quick Account Creation to your current code implementation, instead of re-customizing and regenerating the code. Make sure the **Body** code includes the below four fields with the placeholder values replaced:
- client-id="your_integration_client_id"
- sign-up-email="email_of_your_user@example.com"
- sign-up-first-name="first_name_of_your_user"
- sign-up-last-name="last_name_of_your_user"

## Add support for Quick Account Creation with the Partner API

1. Retrieve your integration's name from the "title" field returned from the [`/apps` endpoint](https://platform.zapier.com/embed/partner-api#get-v1apps).
2. Redirect users to the acknowledgement page URL below:
`https://zapier.com/partner/acknowledgment?sign-up-last-name=<sign-up-last-name>&next=%2Fapp%2Fdashboard&type=quac&name=<Partner Name>&sign-up-first-name=<sign-up=first-name>&sign-up-email=<sign-up-email>`
3. Replace the following query parameter placeholders in the URL, using the "title" value from step 1 for the "name" parameter:
- sign-up-first-name=<sign-up-first-name>
- sign-up-last-name=<sign-up-last-name>
- sign-up-email=<sign-up-email>
- name=<Partner Name>

After an account is created, a [user token still needs to be procured](https://platform.zapier.com/embed/partner-api#access-token) to access specific Partner API endpoints. Generally, since the user will already be signed in to their newly created account in an active session on Zapier, users won't have to explicitly sign in again when prompted with Zapier's OAuth flow.

## When Quick Account Creation is enabled

- If the user is already logged into Zapier, they are redirected to Zap editor.
- If the user’s email is already associated with a Zapier account, but the user is not logged in, they are redirected to Zapier's sign-in page.
- If the user's email is not associated with an existing Zapier account, they are redirect to the consent page.
  - If the user consents to the terms and selects "Continue", a Zapier account is created on their behalf and they are redirected to the Zap editor.
  - If the user closes the consent page, no Zapier account is created.
  - If there is an error creating an account, the user is redirected to an error page.
