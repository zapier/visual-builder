---
title: Planning and implementing integration changes
order: 1
layout: post-toc
redirect_from: /manage/making-changes
---

# Planning and implementing integration changes

Before making updates to your integration, it's important to consider the potential impact on user migration and existing Zaps. Ensuring your API and Zapier integration remains backwards compatible is crucial to avoid disruption to users. However, we acknowledge certain changes are sometimes necessary and unavoidable. In such cases, consider the best practice for implementation.

## Effects of Different Changes (Versioning Matrix)

The matrix below illustrates the impact of different changes on ypur users. For public integrations, this will affect promotion and whether migration is possible. Refer to our best practices to facilitate the upgrade process for yourself and your users.

Columns:
* Add: Adding a net new component
* Update: Making a change to an existing component
* Replace: Deleting/deprecating an existing component and adding a new one in its place
* Delete/Deprecate: Removing an existing component completely

Matrix Key:
* Breaking Change: A modification to the integration which renders existing Zaps incompatible with the new version
* Depends: A modification which may render existing Zaps incompatible with the new version, depending on the implementation
* ✓: A modification to the integration which renders existing Zaps compatible with the new version
* -: Not applicable

Common changes that can affect the ability to migrate users are detailed in the documentation linked in the matrix. Look for your change and pay attention to the recommended best practices.  

Several change scenarios are validated by the platform when you try to _Migrate_ after a version promotion, but always be aware of the effects of any changes you make before you even begin implementing those changes. 

Change scenarios marked as _Depends_ with no linked best practice can vary widely across integrations, so a generalized best practice is not provided; reach out to [support](https://developer.zapier.com/contact) if you need help with your specific change scenario.

| Integration Change | Add | Update | Replace | Delete/Deprecate | Validated by platform? |
| --- | :---: | :---: | :---: | :---: | :---: |
| **AUTHENTICATION CHANGES**  |
|------------------------|---------------------------------|------------------------------|--------------------------------------|
| **Authentication schemes** | [BREAKING CHANGE](https://platform.zapier.com/manage/auth-scheme) | - | [BREAKING CHANGE](https://platform.zapier.com/manage/auth-scheme) | - | ✓ |
| **Authentication fields - required** | [BREAKING CHANGE](https://platform.zapier.com/manage/auth-required) | [Depends](https://platform.zapier.com/manage/auth-required) | - | ✓ | - |
| **Authentication fields - optional** | ✓ | ✓ | - | ✓ | - |
| **Authentication field key(s)** | - | [BREAKING CHANGE](https://platform.zapier.com/manage/auth-keys) | - | - | - |
| **Authentication - token request** | - | ✓ | - | - | - |
| **Authentication - test function** | - | ✓ | ✓ | - | - |
| **TRIGGER/ACTION CHANGES** |
| **Trigger/Action - meta info (e.g.: label, description)** | - | ✓ | ✓ | - | - |
| **Trigger/Action - key** | - | [BREAKING CHANGE](https://platform.zapier.com/manage/change-keys) | [BREAKING CHANGE](https://platform.zapier.com/manage/change-keys) | - | ✓ |
| **Trigger/Action - input field(s) - required** | [Depends](https://platform.zapier.com/manage/required-input) | [Depends](https://platform.zapier.com/manage/required-input) | [Depends](https://platform.zapier.com/manage/required-input) | ✓ | - |
| **Trigger/Action - input field(s) - optional** | ✓ | ✓ | ✓ | ✓ | - |
| **Trigger/Action - input field(s) - key** | - | [BREAKING CHANGE](https://platform.zapier.com/manage/input-key) | [BREAKING CHANGE](https://platform.zapier.com/manage/input-key) | - | - |
| **Trigger/Action - input field(s) - field type** | - | Depends | Depends | - | - |
| **Trigger/Action - output data - key(s)** | ✓ | [BREAKING CHANGE](https://platform.zapier.com/manage/output-key) | [BREAKING CHANGE](https://platform.zapier.com/manage/output-key) | [BREAKING CHANGE](https://platform.zapier.com/manage/output-key) | - |
| **Trigger/Action - output data - response structure** | - | [BREAKING CHANGE](https://platform.zapier.com/manage/output) | [BREAKING CHANGE](https://platform.zapier.com/manage/output) | - | - |
| **Trigger/Action - perform function** | - | Depends | Depends | - | - |
| **Trigger type - polling to hook type** | - | [BREAKING CHANGE](https://platform.zapier.com/manage/change-trigger) | - | - | ✓ |
| **Trigger (polling) - perform function** | - | [Depends](https://platform.zapier.com/manage/change-perform) | [Depends](https://platform.zapier.com/manage/change-perform) | - | - |
| **Trigger (hook) - perform list** | - | Depends | Depends | - | - |
| **Trigger (hook) - performSubscribe** | - | ✓ | ✓ | - | - |
| **Trigger (hook) - performUnsubscribe** | - | ✓ | ✓ | - | - |
| **OTHER CHANGES** |
| **Middleware** | Depends | Depends | Depends | Depends | - |
| **Partner's API (overall)** | - | Depends | Depends | Depends | - |
| **Product feature** | ✓ | - | - | - | - |
| **Rebrand - (e.g. logo, app name)** | - | ✓ | - | - | - |
| **Export UI to CLI** | - | [Depends](https://platform.zapier.com/manage/export-cli) | ✓ | - | - |
| **Export CLI to UI** | - | [Depends](https://platform.zapier.com/manage/export-ui) | - | - | - |
| **Edit Legacy Web Builder integration** | - | [Depends](https://platform.zapier.com/manage/versions-legacy) | [Depends](https://platform.zapier.com/manage/versions-legacy) | - | - |



If your change is not listed, make sure to still consider whether it changes keys, requires users to provide _new_ info, or revokes functionality.