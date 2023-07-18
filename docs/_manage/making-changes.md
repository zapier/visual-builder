---
title: Making Integration Changes in Platform UI and CLI
order: 6
layout: post-toc
---

# Making Integration Changes in Platform UI and CLI

Before making updates to your integration, it's important to consider the potential impact on user migration and existing Zaps. Ensuring your API and Zapier integration remains backwards compatible is crucial to avoid disruption to users. However, we acknowledge certain changes are sometimes necessary and unavoidable. In such cases, consider the best practice for implementation.

## Affects of Different Changes (Versioning Matrix)

The matrix below illustrates the impact of different changes on promotions and migrations for a public integration. Refer to our best practice to facilitate the upgrade process for yourself and your users.

Matrix Key:
* Update: Making a change to an existing component
* Replace: Deleting/deprecating an existing component and adding a new one in its place
* Breaking Change: A modification to the integration which renders existing Zaps incompatible with the new version
* Depends: A modification which may render existing Zaps incompatible with the new version, depending on the implementation
* ✓: A modification to the integration which renders existing Zaps compatible with the new version
* -: Not applicable

Several change scenarios are validated by the platform when you try to "Migrate" after a version promotion, but always be aware of the effects of any changes you make before you even begin implementing those changes.

| **Integration Change** | **Add** | **Update** | **Replace** | **Delete/Deprecate** | **Validated by platform?** |
| --- | --- | --- | --- | --- | --- |
| **Authentication schemes** | **BREAKING CHANGE** | - | **BREAKING CHANGE** | - | ✓ |
| **Authentication fields - required** | **BREAKING CHANGE** | Depends | - | ✓ | |
| **Authentication fields - optional** | ✓ | ✓ | - | ✓ | |
| **Authentication field key(s)** | - | **BREAKING CHANGE** | - | - | |
| **Authentication - token request** | - | ✓ | - | - | |
| **Authentication - test function** | - | ✓ | ✓ | - | |
| **Trigger/Action/Search - meta info (e.g.: label, description)** | - | ✓ | ✓ | - | |
| **Trigger/Action/Search - key** | - | **BREAKING CHANGE** | **BREAKING CHANGE** | - | ✓ |
| **Trigger/Action/Search - input field(s) - required** | Depends | Depends | Depends | ✓ | |
| **Trigger/Action/Search - input field(s) - optional** | ✓ | ✓ | ✓ | ✓ | |
| **Trigger/Action/Search - input field(s) - key** | - | **BREAKING CHANGE** | **BREAKING CHANGE** | - | |
| **Trigger/Action/Search - input field(s) - field type** | - | Depends | Depends | - | |
| **Trigger/Action/Search - output data - key(s)** | ✓ | **BREAKING CHANGE** | **BREAKING CHANGE** | **BREAKING CHANGE** | |
| **Trigger/Action/Search - output data - response structure** | - | **BREAKING CHANGE** | **BREAKING CHANGE** | - | |
| **Trigger/Action/Search - perform function** | - | Depends | Depends | - | |
| **Trigger type - polling/hook** | - | **BREAKING CHANGE** | - | - | ✓ |
| **Trigger (polling) - perform function** | - | Depends | Depends | - | |
| **Trigger (hook) - perform list** | - | Depends | Depends | - | |
| **Trigger (hook) - performSubscribe** | - | ✓ | ✓ | - | |
| **Trigger (hook) - performUnsubscribe** | - | ✓ | ✓ | - | |
| **Middleware** | Depends | Depends | Depends | Depends | |
| **Partner's API (overall)** | - | Depends | Depends | Depends | |
| **Product feature** | ✓ | - | - | - | |
| **Rebrand - (e.g. logo, app name)** | - | ✓ | - | - | |
| **Convert - UI to CLI** | - | Depends | ✓ | - | |
| **Convert - CLI to UI** | - | Depends | - | - | |
| **Edit - version of a converted Web Builder integration** | - | Depends | Depends | - | |
