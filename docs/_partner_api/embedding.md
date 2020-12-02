---
title: Embedding
order: 8
layout: post
redirect_from: /partner_api/
---

# Embedding Zapier in your Product

There are two ways to embed Zapier in your product: the [embed widget](#widget) or the Partner API (using an [iframe](#iframe)).

## widget.js

![](https://cdn.zapier.com/zapier/images/partners/in-your-product.png)

Learn more about embedding with the widget.js and creating your own widget [here](https://zapier.com/partner/embed/).

Want to embed specific individual Zap Templates instead? Copy the Zap ID number from your [Zap Templates Dashboard](https://zapier.com/developer/zap-templates/) by clicking the gear icon beside a Zap and selecting the _Copy ID_ option. Then, include it in place of `1234` in the text below:

`<script type="text/javascript" src="https://zapier.com/apps/embed/widget.js?guided_zaps=1234"></script>`

Want to embed multiple Zap Templates? Include each of their IDs in a comma separated list, such as:

`<script type="text/javascript" src="https://zapier.com/apps/embed/widget.js?guided_zaps=1234,9876,3456"></script>`

<a id="embed-widget-options"></a>
You can additionally use these options to customize your Zap Template embeds:

- `limit=10` to set the number of Zaps to display; use any number you want
- `theme=dark` for a dark-colored embed, instead of the default light background
- `categories=CATEGORYNAME` to show only Zap Templates with apps from a specific category, with `CATEGORYNAME` replaced with the name of a category from [Zapier’s App Directory](https://zapier.com/apps/)
- `categories=-CATEGORYNAME` to _not_ show Zap Templates with apps from a specific category
- `services=-APP,-APP` to exclude specific apps
- `borderColor=%23333` to set the color of the borders to any css value or “none”. Use "%23" in place of "#" for HEX values.
- `backgroundColor=green` to set the background of each row to any css value including “transparent”
- `buttonColor=%23000000` to set the background color of the primary button to any css value
- `inheritFont=true` to disable the widget font styling allowing it to inherit from the parent container
- `buttonType=outline` to set the button type. Type `outline` (currently the only option) sets the `buttonColor` as a border around the button with a transparent background
- `title=TITLE` to set a styled header to the widget
- `textColor=red` to set the text color of the widget (template titles)
- `button=BUTTONTEXT` to set the primary button text (default: Use This Zap)
- `width=600` to set a fixed width to the widget. By default, the widget markup is fully responsive with a max width of 100% of its parent’s width.

Include the additional options at the end of the script text with an ampersand, such as:

`<script src="https://zapier.com/apps/embed/widget.js?services=APP&borderColor=green&limit=10&theme=dark"></script>`

<span id="iframe"><!-- helper anchor for simpler linking --></span>

## Partner API (using an iframe)

![](https://cdn.zapier.com/storage/photos/edcf17488c8250dca213ed2083846fc5.png)

**Overview**

1. Lookup Zap templates for your app using the [Zap templates endpoint](/partner_api/endpoints#get_v1zaptemplates)
2. Display the Zap templates to the user (see [Examples page](/partner_api/examples) for inspiration)
3. Upon the user clicking to create a Zap based on the Zap template, use the `create_url` (see [Zap template object](/partner_api/endpoints#zap-template) definition) as the `src` attribute in an iframe injected in your page. Note that Zapier blocks embeds if they are not registered with us. Learn more in the [Security section](#security) on this page.
4. Your product can listen to `postMessages` sent by the iframe out to any listener when a user turns on the Zap (message: `zap:unpause`,)
5. The above can be repeated for Zaps returned from the [Zap endpoint](/partner_api/endpoints#get_v1zaps), instead of the `create_url` use the Zap's `url` (see [Zap object](/partner_api/endpoints#zap) definition) in the iframe's `src` attribute.

**Example**

Create a Zap from a Zap template `create_url`

```html
<iframe src="https://zapier.com/partner/embed/trello/create/113"></iframe>
```

Edit a Zap from a Zap's `url`

```html
<iframe src="https://zapier.com/app/editor/123456"></iframe>
```

<span id="security"><!-- helper anchor to security section --></span>

**Security**

Our user's security is paramount. By default, we deny any embedding of our product unless you provide us with a list of domains that you expect to embed Zapier in. This protects the user from malicious activities like [Clickjacking](https://www.owasp.org/index.php/Clickjacking). An example of what the user would see if you were to attempt to embed Zapier and the embedding domain was not registered with us:

![](https://zappy.zapier.com/d417e90269bb019fcbe5718d18eb572d.png)

To provide us a list of unique domains you'll embed Zapier in:

- if you've already embedded our Product, you're in luck! We should have already captured this and have permitted your product domains. Should we have missed any, please [reach out to us](mailto:partners@zapier.com) so we can add your domain.
- else if you've already applied for a Partner API access: contact [partners@zapier.com](mailto:partners@zapier.com) and include the domains you'd like to register.
- otherwise, when you [apply for the Partner API access]({{ site.partner_api_invite_url }}) you'll have the opportunity to supply us the embedding domains inside of the form.

Common Questions:

- **Why do you need to block the iframe embed by default?** This is a more secure option!
- **Why do I need to provide Zapier with a list of domains I intend to embed Zapier in?** We'll use this to permit these specific domains to embed our product.
- **Which domains are appropriate and which ones are not, if any?** We do not support wildcard, or other patterns, within domains. Being explicit about the specific domains ensures we do not inadvertedly allow custom/user domains from being permitted. Example: `{username}.github.io` is a scheme used by Github to allow any user to create their own websites. In this example, only `github.io` would be permitted but not any subdomain of that domain. Moreover, the domains provided by you should be registered with your company with a public registrar. That is to say a `randomcnamedomain.com` is not valid for the same reason that a user or bad actor could register that domain.
- **What about when I'm developing the embed?** Indeed this is tricky because `localhost`, `yourcomp.local` and `127.0.0.1` are not valid domains that we support. An option would be to use a tunnel service like [ngrok](https://ngrok.com/) and to register that ngrok tunnel with us. Be advised, that we will ask for a static domain from ngrok.com or similar tunneling service.
- **What if my product requires wildcard support (e.g. `{account}.myproduct.com`)?** While this is unsupported, we'd like to [chat with you](mailto:partners@zapier.com) to understand your use case and to discuss other options.
