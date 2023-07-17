---
title: Making Integration Changes in Platform UI and CLI
order: 6
layout: post-toc
---

# Making Integration Changes in Platform UI and CLI

Before making updates to your integration, it's important to consider the potential impact on user migration and existing Zaps. Ensuring your API and Zapier integration remains backwards compatible is crucial to avoid disruption to users. However, we acknowledge certain changes are sometimes necessary and avoidable. In such cases, consider the best practices for implementations.

## Affects of Different Changes (Versioning Matrix)

The matrix below illustrates the impact of different changes on promotions and migrations for public integration. Refer to our best practices to facilitate the upgrade process for you and your users.

* Update: Making a change to an existing component
* Replace: Deleting/deprecating an existing component and adding a new one in its place
* Breaking Change: any modification to the integration which renders existing Zaps incompatible with the new version

Several change scenarios are validated by the platform when you try to "Migrate" after a version promotion, but always be aware of the affects of any changes you make before you even begin implementing those changes.

| **Integration Change** | **Add** | **Update** | **Replace** | **Delete/Deprecate** | **Validated by platform?** |
| --- | --- | --- | --- | --- | --- |
| **Authentication schemes** | **BREAKING CHANGE** | n/a | **BREAKING CHANGE** | n/a | Yes |
| **Authentication fields - required** | **BREAKING CHANGE** | Depends | n/a | OK | |
| **Authentication fields - optional** | OK | OK | n/a | OK | |
| **Authentication field key(s) | n/a | **BREAKING CHANGE** | n/a | n/a | |
| **Authentication - token request** | n/a | OK | n/a | n/a | |
| **Authentication - test function** | n/a | OK | OK | n/a | |
| **Trigger/Action/Search - meta info (e.g.: label, description)** | n/a | OK | OK | n/a | |
| **Trigger/Action/Search - key | n/a | **BREAKING CHANGE** | **BREAKING CHANGE** | n/a | Yes |
| **Trigger/Action/Search - input field(s) - required** | Depends | Depends | Depends | OK | |
| **Trigger/Action/Search - input field(s) - optional** | OK | OK | OK | OK | |
| **Trigger/Action/Search - input field(s) - key** | n/a | **BREAKING CHANGE** | **BREAKING CHANGE** | n/a | |
| **Trigger/Action/Search - input field(s) - field type** | n/a | Depends | Depends | n/a | |
| **Trigger/Action/Search - output data - key(s)** | OK | **BREAKING CHANGE** | **BREAKING CHANGE** | **BREAKING CHANGE** | |
| **Trigger/Action/Search - output data - response structure** | n/a | **BREAKING CHANGE** | **BREAKING CHANGE** | n/a | |
| **Trigger/Action/Search - perform function** | n/a | Depends | Depends | n/a | |
| **Trigger type - polling/hook | n/a | **BREAKING CHANGE** | n/a | n/a | Yes |
| **Trigger (polling) - perform function** | n/a | Depends | Depends | n/a | |
| **Trigger (hook) - perform list** | n/a | Depends | Depends | n/a | |
| **Trigger (hook) - performSubscribe** | n/a | OK | OK | n/a | |
| **Trigger (hook) - performUnsubscribe** | n/a | OK | OK | n/a | |
| **Middleware** | Depends | Depends | Depends | Depends | |
| **Partner's API (overall)** | n/a | Depends | Depends | Depends | |
| **Product feature** | OK | n/a | n/a | n/a | |
| **Rebrand - (e.g. logo, app name)** | n/a | OK | n/a | n/a | |
| **Convert - UI to CLI** | n/a | Depends | OK | n/a | |
| **Convert - CLI to UI** | n/a | Depends | n/a | n/a | |
| **Edit - version of a converted Web Builder integration** | n/a | Depends | Depends | n/a | |
