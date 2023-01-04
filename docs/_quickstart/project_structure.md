---
title: Project Structure
order: 5
layout: post-toc
redirect_from: /quick-start/
---

# Build Your Integration

## Project Structure

![Zapier Visual Builder new integration](https://cdn.zappy.app/86ebc2be692ec2f0ca729b92667ee74b.png)

_Build and manage your app's integration in the Zapier Platform UI_

[Zapier's Platform Visual Builder](https://developer.zapier.com/){:target="_blank"} includes everything needed to build a new Zapier integration. The left sidebar outlines the core project structure. Each part of your integration definition for the Zapier platform is in the _Build_ tabs:

- _Authentication_ sets how users authenticate with your API, using basic, API key, digest, session, or OAuth v2 authentication.
- _Triggers_ control how Zapier gets data from your API into a Zap, with `GET` HTTP calls or webhooks.
- _Actions_ control how Zapier sends data to your API, including:
	- _Create Actions_  to send new data from a Zap to your API, with `POST` or `PUT` HTTP calls to create or update items.
	- _Search Actions_  to perform lookups through your API using `GET` calls.
- _Advanced_ manages environment variables to store secret data your integration needs to communicate with your API, including API keys or client secrets.

To build an integration, you need to define the core details of your API and build input forms so users can enter the data that Zapier will send to your API. The Zapier platform then automatically handles the authentication flow, [deduplication](https://platform.zapier.com/docs/dedupe), and keeps track of which things have already been processed.

This is where you need to think through your integration. What outputs from your app would make useful triggers for users’ Zaps, and what inputs would your app need to create items from a Zap’s action? For an email service, say, a *Send Email* action would need a recipient email address, subject, and message body.

For our example integration, we want to make an action that creates GitHub issues, which need an issue title, body, and repository name. List each detail needed to build items in your app, as you'll need to build a form to gather that data while creating your Zapier integration. Check API documentation for available endpoints and required fields. For our GitHub example, we used the documentation [here](https://docs.github.com/en/rest/quickstart?apiVersion=2022-11-28).

Back in the Zapier Visual Builder, there are a few more tools under the _Manage_ tab to maintain your Zapier integration with versions, analytics, logs and, for published apps; bugs and feature requests reported by users.

First, though, you need to build that integration. Let’s start with authentication.
