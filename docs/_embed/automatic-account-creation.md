---
title: Automatic account creation
order: 6
layout: post
redirect_from: 
  - /embed/
  - /partner_api/
---

# Automatic account creation

Save time and reduce friction for your users by having a Zapier account created on their behalf when using one of our product embeds.  Users no longer need to worry about the hassle of signing up to a new service.

Zapier accomplishes this by being an OpenID Connect relaying party.  Partners who support being an identity provider and are able to communicate via OpenID Connect can take advantage of this new communication channel.

In order to help customers feel secure during this exchange of profile information, Zapier has added an acknowledgement page that will be presented before the partner’s OpenID Connect consent screen.  This acknowledgement page informs the end user why their profile information is being exchanged and that a new account is being created on their behalf.

Following account creation the end user will be sent an email to let them know a Zapier account has been created, how to set a password on their new account, and highlight the partner that brought them to Zapier.

<a class="button" style="background-color:#20272B;color:white" href="https://zapier.typeform.com/to/OlPloIcW/?utm_source=zapier_marketing_website&utm_medium=embed_experience&utm_campaign=solutions_marketing_page">Enable this for your product</a>

## Example Implementation

The below video shows the signup flow on Google's embed experience without automatic account creation. To sign up, users are required to manually provide first and last name, email address, and go through a multi-step onboarding survey before arriving at the Zap Editor:

<iframe allowtransparency="true" title="Wistia video player" allowFullscreen frameborder="0" scrolling="no" class="wistia_embed" name="wistia_embed" src="https://fast.wistia.net/embed/iframe/tqz0movaqf" width="640" height="360"></iframe>


In comparison, the below videeo shows the signup flow with automatic account creation enabled. To sign up, users confirm on a consent screen and then are directed to the Zap Editor:

<iframe allowtransparency="true" title="Wistia video player" allowFullscreen frameborder="0" scrolling="no" class="wistia_embed" name="wistia_embed" src="https://fast.wistia.net/embed/iframe/e66sqvvd20" width="640" height="360"></iframe>


## Requirements

The minimum requirements need to be met by the partner in order to enable Automatic Account Creation
- Zapier recommends supporting the [Authorization Code](https://auth0.com/docs/get-started/authentication-and-authorization-flow/authorization-code-flow) flow
  - If there is a need to use an alternative flow please reach out to [Zapier Support](mailto:partners@zapier.com)
- Support the [OpenID Connect](https://auth0.com/docs/authenticate/protocols/openid-connect-protocol) identity layer on top of OAuth 2.0
- The end user on the partner site must have an email address on file, and that address must be present in the email [claim](https://openid.net/specs/openid-connect-core-1_0.html#ScopeClaims)
- The Identity provider allow list redirects include `https://zapier.com/oidc/return/`

## Identity Provider Examples

Below are just a few examples of services that offer being an identity provider.

- [Google Identity](https://developers.google.com/identity/protocols/oauth2/openid-connect)
- [Auth0](https://auth0.com/docs/authenticate/protocols/openid-connect-protocol)
- [Azure Active Directory](https://docs.microsoft.com/en-us/azure/active-directory/develop/v2-protocols-oidc)

## FAQ

- What Zapier features work with Automatic Account Creation?
  - Automatic Account Creation works out-of-the-box for all Zapier Embed offerings.
- How does Automatic Account Creation differ from setting up an integration and enabling OAuth Authentication in the developer platform?
  - To provide flexibility to our partners we allow customizing these features independently of each other.  However, partners can choose to reuse the same `client_id`, `client_secret`, and endpoints for both features if desired.

