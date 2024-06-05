---
title: Validate domain and subdomain input fields during authentication
order: 11
layout: post-toc
redirect_from: 
---

# Validate domain and subdomain input fields during authentication

When adding a subdomain input field, commonly used in OAuth implementations, additional validation is strongly recommended to prevent a potential security vulnerability. If not taken into account, an attacker could utilize a maliciously constructed subdomain field (like `attacker-domain.com/`) in order to redirect OAuth connection requests to that attacker-controlled domain (because `attacker-domain.com/.your-domain.com` resolves to the attacker's domain instead of the expected one).
Taking the following steps prevents the potential for an attacker to access your integration's sensitive authentication information, such as the OAuth client ID or secret.

## Prerequisites

- An authentication method that uses pre-configured tokens or secret values (for example, OAuth 2)
- User is able to input a domain or subdomain when authenticating within Zapier
- Your integration stores sensitive authentication details (in environment variables, for example) which are used as part of the authentication process 

## Steps

1. If your integration allows for the user to provide a domain, validate the input against an allow-list of trusted domains.


2. If your integration allows for the user to provide a subdomain, add conditional validation for the subdomain string whenever you include the value in your OAuth HTTP requests. This change will prevent potential exploitation of the subdomain vulnerability.

### Handle subdomain validation in Platform UI

- Update the _Access Token Request_ and related sections under the _OAuth v2 Endpoint Configuration_ options, using the [Code Mode](https://platform.zapier.com/build/code-mode) editor.
- Example code for handling subdomain validation in integrations built using the Platform UI, via Code Mode: 

```js
// --- UPDATE: add your validation for the subdomain field before using it ---
if (!/^[a-z0-9-]+$/.test(bundle.authData.yourSubdomainField)) {
 throw new Error(
   "Subdomain can only contain letters, numbers and dashes (-)."
 );
}


const options = {
 url: `https://${bundle.inputData.yourSubdomainField}.mydomain.com/oauth/access-token`,
 method: 'POST',
 json: {
   'code': bundle.inputData.code,
   'client_id': process.env.CLIENT_ID,
   'client_secret': process.env.CLIENT_SECRET,
   'grant_type': 'authorization_code',
 },
}


return z.request(options)
 .then((response) => {
   const results = response.json;
   return results.data;
 });

```

### Handle subdomain validation in Platform CLI

- If you're using OAuth-based authentications, update the `getAccessToken` and optional `refreshAccessToken` configuration methods. If the integration uses [shorthand HTTP requests](https://github.com/zapier/zapier-platform/blob/main/packages/cli/README.md#shorthand-http-requests), switching to [manual HTTP requests](https://github.com/zapier/zapier-platform/blob/main/packages/cli/README.md#manual-http-requests) will allow you to perform this manual subdomain validation.
- Example code for handling subdomain validation in integrations built using the Platform CLI:

```js
const refreshAccessToken = async (z, bundle) => {
 // --- UPDATE: add your validation for the subdomain field before using it ---
 if (!/^[a-z0-9-]+$/.test(bundle.authData.yourSubdomainField)) {
   throw new Error(
     "Subdomain can only contain letters, numbers and dashes (-)."
   );
 }


 const response = await z.request({
   url: `https://${bundle.authData.yourSubdomainField}.mydomain.com/oauth/token`,
   method: "POST",
   body: {
     client_id: process.env.CLIENT_ID,
     client_secret: process.env.CLIENT_SECRET,
     grant_type: "refresh_token",
     refresh_token: bundle.authData.refresh_token,
     redirect_uri: bundle.inputData.redirect_uri,
   },
 });


 return {
   access_token: response.data.access_token,
   refresh_token: response.data.refresh_token,
 };
};

```