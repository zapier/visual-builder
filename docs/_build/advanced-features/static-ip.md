---
title: Enable static IP address connection for customers
order: 6
layout: post-toc
redirect_from: 
---

# Enable static IP address connection for customers

To enable customers to access your integration by static IP address, all outbound traffic from Zapier to your integration will need to be routed through a smaller set of consistent IP addresses. Any app owner/developer can request to enable the static IP address feature on a private or public app.

## Traffic from Zapier

Traffic from Zapier uses the following IP addresses:
  - 44.214.195.64/28 (us-east-1)
  - 18.246.81.208/28 (us-west-2)

Enabling this feature will increase the volume of requests to your server received from these IP addresses. This means this change would affect all users of your integration who are on a Zapier Teams, Company, or Enterprise plan.

Review our documentation on how the [static IP address functions within Zapier](https://help.zapier.com/hc/en-us/articles/15406083674509-Use-a-static-IP-address-to-connect-to-Zapier).

## How to enable static IP address connection

1. **Consult with your Security team:** They can confirm if a static IP address is permitted within your network security policies and advise on any potential conflicts with existing security measures.

2. **[Contact Zapier Support](https://developer.zapier.com/contact)**: They can help you enable static IP addresses for your private app integration. The turnaround time is typically within 1 business day.