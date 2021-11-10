---
title: Elements
order: 2
layout: post-toc
redirect_from: 
  - /partner_api/embedding
---

# Elements

## Introduction
Elements are prebuilt UI components that offer the quickest—and easiest—way to surface your Zapier integration, available app connections, popular Zap templates, and Zaps your users set up inside your product. 

Our Element generators let you customize the visual design and features of Zapier you want to include, and generate JavaScript code snippets that can be copied and pasted directly into your site. No programming experience is required!

## App Directory Element
![](https://zapier.com/partner/_next/static/image/public/img/app-directory-page/app-directory-anydo.345cf1d1f5b0808e6994ef0cf84aad0f.png?w=1080&q=75)

A customized version of Zapier’s App Directory for users to search and build new Zaps with your Zapier integration. 

Open the [App Directory Element generator](https://zapier.com/partner/embed/app-directory/create) and type in your app's name. Using the sidebar panel in the tool, you can change the theme, add an introduction, include a search bar, display (or exclude) popular apps and categories, showcase your Zap templates, and more! When it's ready, you generate the correct codes and add them anywhere on your site. 

> If you prefer to have a video overview of the App Directory Element, see below
<iframe width="560" height="315" src="https://www.youtube.com/embed/4-SkPIV1L84" title="Embedding the App Directory element video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

## Zap Template Element

![](https://cdn.zapier.com/zapier/images/partners/in-your-product-wave.png)

Zap templates are pre-made Zaps that help users discover popular use cases for automating their work. Each template features a specific use case and the apps (including yours!) needed for it to work.

Select your app in our [Zap Template generator](https://zapier.com/partner/embed), choose the number of Zap templates you want to display, then copy the code that's generated.

Want to embed specific individual Zap Templates instead? Copy the Zap ID number from your [Zap Templates Dashboard](https://zapier.com/developer/zap-templates/) by clicking the [gear icon](https://cdn.zappy.app/486616954fc147c65285248eea031841.png) beside a Zap template and selecting the Copy ID option. Then, include it in place of 1234 in the text below:

```javascript
<script type="text/javascript" src="https://zapier.com/apps/embed/widget.js?guided_zaps=1234"></script>
```

Want to embed multiple Zap Templates? Include each of their IDs in a comma separated list, such as:

```javascript
<script type="text/javascript" src="https://zapier.com/apps/embed/widget.js?guided_zaps=1234,9876,3456"></script>
```

You can additionally use these options to customize your Zap Template embeds:
- `limit=10` to set the number of Zaps to display; use any number you want
- `theme=dark` for a dark-colored embed, instead of the default light background
- `categories=CATEGORYNAME` to show only Zap Templates with apps from a specific category, with `CATEGORYNAME` replaced with the name of a category from [Zapier’s App Directory](https://zapier.com/apps/)
- `categories=-CATEGORYNAME` to _not_ show Zap Templates with apps from a specific category
- `services=APP,APP` to show only Zap Templates between two (or more) apps 
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

```javascript
<script src="https://zapier.com/apps/embed/widget.js?services=APP&borderColor=green&limit=10&theme=dark"></script>
```

You can load templates asynchronously (without blocking the rest of your page’s content) by adding the `async` attribute and `html_id` parameter to the script tag, like so:
```javascript
<div id="foo"></div>
<script async src="https://zapier.com/apps/embed/widget.js?services=mailchimp&html_id=foo"></script>
```

> *Note:* The `html_id` parameter must point to a valid element `id` on the page you wish to be the direct parent of the embed.

Using React or another client-side rendering library? See documentation on how to integrate with these here: [https://platform.zapier.com/partners/zap-templates#support-for-react](https://platform.zapier.com/partners/zap-templates#support-for-react).

> If you prefer to have a video overview of the Zap Template Element, see below
<iframe width="560" height="315" src="https://www.youtube.com/embed/xWwECaAfdPo" title="Embedding the Zap Template element video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

## Zap Manager Element
![](https://zapier.com/partner/_next/image?url=%2Fpartner%2Fimg%2Fzap-manager%2Fpreview2-dark-large.png&w=1920&q=75)

Our Zap Manager Element lets your users see the Zaps they've set up with your app directly inside your product. They can view their Zaps and see their status at a glance without having to go through Zapier first.

Once you [request access](https://zapier.typeform.com/to/tzFDFLsm) using our [Zap Manager generator](https://zapier.com/partner/embed/zap-manager/create), you'll get a client ID, which you can use to generate your specific code. All you need to do is copy and paste! Then, once inside your product, your users will have the option to log into Zapier, where their Zaps will be displayed. 
