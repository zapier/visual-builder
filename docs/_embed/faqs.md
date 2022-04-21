---
title: FAQs
order: 7
layout: post
redirect_from: /partner_api/
---

# FAQs

- **Why do you need to block the iframe embed by default?** This is a more secure option!
- **Why do I need to provide Zapier with a list of domains I intend to embed Zapier in?** We'll use this to permit these specific domains to embed our product.
- **Which domains are appropriate and which ones are not, if any?** We do not support wildcard, or other patterns, within domains. Being explicit about the specific domains ensures we do not inadvertedly allow custom/user domains from being permitted. Example: `{username}.github.io` is a scheme used by Github to allow any user to create their own websites. In this example, only `github.io` would be permitted but not any subdomain of that domain. Moreover, the domains provided by you should be registered with your company with a public registrar. That is to say a `randomcnamedomain.com` is not valid for the same reason that a user or bad actor could register that domain.
- **What about when I'm developing the embed?** Indeed this is tricky because `localhost`, `yourcomp.local` and `127.0.0.1` are not valid domains that we support. An option would be to use a tunnel service like [ngrok](https://ngrok.com/) and to register that ngrok tunnel with us. Be advised, that we will ask for a static domain from ngrok.com or similar tunneling service.
- **What if my product requires wildcard support (e.g. `{account}.myproduct.com`)?** While this is unsupported, we'd like to [chat with you](mailto:partners@zapier.com) to understand your use case and to discuss other options.
