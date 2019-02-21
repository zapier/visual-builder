---
title: Project Structure
order: 4
layout: post
redirect_from: /quick-start/
---

## Build Your Integration

### Project Structure

![Zapier visual builder new integration](https://cdn.zapier.com/storage/photos/2316a669768c5c2ee9f4b1e84c70d1d0.png)

_Build and manage your app's integration in the Zapier Visual Builder_

[Zapier visual builder](https://zapier.com/app/developer/){:target="_blank"} includes everything needed to build a new Zapier integration. The left sidebar outlines the core project structure. Each part of your integration definition for the Zapier platform is in the _Build_ tabs:

- _Authentication_ sets how users authenticate with your API, using basic, API key, digest, session, or OAuth2 authentication.
- _Triggers_ control how Zapier gets data from your API into a Zap, with `GET` HTTP calls or webhooks.
- _Actions_ control how Zapier sends data to your API, including:
	- _Create Actions_  to send new data from a Zap to your API, with `POST` or `PUT` HTTP calls to create or update items.
	- _Search Actions_  to perform lookups through your API using `GET` calls.
- _Advanced_ manages environment variables to store secret data your integration needs to communicate with your API, including API keys or client secrets.

To build an integration, you need to define the core details of your API and build input forms so users can enter the data that Zapier will send to your API. The Zapier platform then automatically handles the authentication flow, deduplication, and keeps track of which things have already been processed.

This is where you need to think through your integration. What outputs from your app would make good Zapier triggers, and what inputs would your app need to create items in Zapier actions? For an email service, say, a *New Email* would need a recipient email address, subject, and message body.

For our example integration, we want to make GitHub issues, so would need an issue name, body, and repository name. List each detail needed to build items in your app, as you'll need to build a form to gather that data while creating your Zapier integration.

Back in the Zapier visual builder, there are a few more tools under the _Manage_ tab to maintain your Zapier integration with stats, logs, bugs, feature requests, and versions.

First, though, you need to build that integration. Let’s start with authentication.