---
title: Security
order: 10
layout: post
redirect_from: 
    - /embed/faq
---

# Security

User security is paramount. By default, Zapier denies any embedding of our product unless you provide us with a list of domains that you expect to embed Zapier in. 

This protects the user from malicious activities like [Clickjacking](https://www.owasp.org/index.php/Clickjacking). An example of what the user would see if you were to attempt to embed Zapier and the embedding domain was not registered:

![](https://zappy.zapier.com/d417e90269bb019fcbe5718d18eb572d.png)

**NOTE:** the App Directory and Zap Template Elements are exempt from this as users are required to log in to their Zapier account after clicking on a Zap Template link.

## Provide a list of domains

- If you've already embedded our Product, this would have already been captured and your product domains are permitted. 

- To add domains, navigate to the Embed tab of your integration's [Platform UI](https://developer.zapier.com/), and add the missing domains under the `Full Zapier Experience` tab within _Manage Domains_ section.

![](https://cdn.zappy.app/758eb40169868f98fa26b845269d3d97.png)

- These specific domains are then permitted to embed Zapier. 

- The domains provided by you should be registered with your company with a public registrar. That is to say a `randomcnamedomain.com` is not valid for the same reason that a user or bad actor could register that domain.

## Troubleshooting

- `localhost`, `yourcomp.local` and `127.0.0.1` are not valid supported domains. An option during your embed development would be to use a tunnel service like [ngrok](https://ngrok.com/) and to register that ngrok tunnel with us. Be advised, that we will ask for a static domain from ngrok.com or similar tunneling service.

- If the domain you're embedding on is added to the allowlist within _Manage Domains_, but you're seeing the `This embed is blocked` error, the [CSP](https://developer.mozilla.org/en-US/docs/Web/HTTP/CSP) may be too restrictive/overly strict. You'll want to check Console/Network for the appropriate request to see the [referrer-policy](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Referrer-Policy) header. Using `strict-origin-when-cross-origin` as the referrer-policy is recommended. 
