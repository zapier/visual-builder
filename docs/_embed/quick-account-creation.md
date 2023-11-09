# Support Quick Account Creation (QuAC)

Quick Account Creation (QuAC) is a streamlined, automatic sign-up feature allowing first time Zapier users to bypass our account creation flow and onboarding survey. This creates a seamless experience for your users during their Zap creation process.

Instead of being directed to a sign-up screen, users are presented with a consent page to connect to Zapier, then proceed to the Zap editor if consented. If an existing Zapier account under the email does not exist, users will receive an email prompting them to finish setting up their account. This allows users to dive directly into the Zap editor to accomplish the task at hand efficiently and without context switching.

Prerequisites:

- Implementation of the [Full Zapier Experience](https://platform.zapier.com/embed/full-zapier-experience) or the [Zap templates element](https://platform.zapier.com/embed/zap-templates).
- Access to your user’s first name, last name, and email on the page supporting QuAC.

To add support for Quick Account Creation:

1. Go to the [generator tool](https://zapier.com/partner/solutions/plug-and-play) for either the Full Zapier Experience or [Zap templates element](https://platform.zapier.com/embed/zap-templates).
2. Customize the visual design and features of the embed solution of choice.
3. Generate the embed code in HTML, Vanilla JS, React, Angular, or Vue.js.
4. Replace the placeholder values set to `client-id`, `sign-up-email`, `sign-up-first-name`, and `sign-up-last-name` in the code **Body**. All four values are required for user account creation.
5. Embed both the **Head** and **Body** code on your product's page.

You can embed the Full Zapier Experience or Zap templates element without support for Quick Account Creation. If the four required fields aren’t provided, the embed will use the default behaviour redirecting users to Zapier's signup page from your product's page.

When Quick Account Creation is enabled:
- If the user is already logged into Zapier, they are redirected to Zap editor.
- If the user’s email is already associated with a Zapier account, but the user is not logged in, they are redirected to Zapier's sign-in page.
- If the user's email is not associated with an existing Zapier account, they are redirect to the QuAC consent page.
  - If the user consents to the terms and selects "Continue", a Zapier account is created on their behalf and they are redirected to the Zap editor.
  - If the user closes the consent page, no Zapier account is created.
  - If there is an error creating an account, the user is redirected to an error page.
