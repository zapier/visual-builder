---
title: Security
order: 7
layout: post
redirect_from: 
    - /embed/
    - /partner_api/
---

# Security

Our user's security is paramount. By default, we deny any embedding of our product unless you provide us with a list of domains that you expect to embed Zapier in. This protects the user from malicious activities like [Clickjacking](https://www.owasp.org/index.php/Clickjacking). An example of what the user would see if you were to attempt to embed Zapier and the embedding domain was not registered with us:

![](https://zappy.zapier.com/d417e90269bb019fcbe5718d18eb572d.png)

**NOTE:** the App Directory and Zap Template Elements are exempt from this as users are required to log in to their Zapier account after clicking on a Zap Template link.

To provide us a list of unique domains you'll embed Zapier in:

- if you've already embedded our Product, you're in luck! We should have already captured this and have permitted your product domains. Should we have missed any, navigate to the Embed > Settings section of the [Developer Platform](https://developer.zapier.com/), and add the missing domains under the `Embedding Domains` tab.
