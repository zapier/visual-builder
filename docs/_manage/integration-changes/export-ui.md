---
title: Export integration to Platform UI
order: 14
layout: post-toc
redirect_from: /manage/making-changes#converting-cli-to-ui
  
---

# Export integration to Platform UI

The Zapier Platform UI is the easiest way for anyone with API experience to build Zapier integrations. It is for users more comfortable with a visual form editor.

Some advanced calls and response parsing can still be performed in the Platform UI when using [Code Mode](https://platform.zapier.com/build/code-mode).

The Platform UI has the following advantages over the CLI:

- A graphic user-interface with form-based editor.
- A live form preview that shows how changes made to your integration would appear in the Zap editor.

If you have an integration in the Platform CLI that you would like to edit in the Platform UI instead, you can create a new version in the Platform UI.

When moving an app from CLI to the Platform UI, we cannot migrate users from previous versions or apps. Existing users will be able to continue using the version they’re on, but must upgrade to the new version manually. Existing users would see this [prompt in the Zap editor](https://help.zapier.com/hc/en-us/articles/18755649454989-Update-to-the-latest-app-version-in-Zaps) to optionally encourage them to make the update. 

Zapier does not automatically notify all existing users of a new version’s availability, but new users would only see the currently promoted/Public version when searching for the app name.  We also recommend announcing the changes/new integration version to your general user base via in-app or email marketing to encourage users to switch over.

To export your existing Platform CLI integration to Platform UI:

## 1. Contact Developer Support to create an empty version of your integration

Hiding an app and replacing it with a new app ID built in the preferred tool is [not supported](https://platform.zapier.com/publish/integration-publishing-requirements#23-replacement-integration). To export your Platform CLI integration to the Platform UI, contact the [Developer Support](https://developer.zapier.com/contact) team to create an empty version associated with the same app ID.

## 2. Rebuild the integration from scratch

Rebuild the integration from scratch on this newly created empty version in the Platform UI and ensure that this new version has feature parity to the previous CLI version. This new version can then be maintained in the Platform UI by your team. For [Public apps](https://platform.zapier.com/quickstart/private-vs-public-integrations), this avoids a repeat of the app review process; as well as retaining previous versions, associated bug reports and feature requests.

> Allow users to remain on the (now legacy) CLI version until they switch over manually, as long as the endpoints are functional. If [Deprecation](https://platform.zapier.com/manage/deprecate) is necessary, please note this is significantly more disruptive to our mutual users and should be considered carefully.

When the conversion has been completed, you will be able to see this version and the previous CLI versions in the Platform UI's **Manage > Versions** section. 

While you can see the previous CLI versions in the Platform UI, you would not be able edit those versions there. The previous CLI versions would show a lock icon on the various attributes under the _Build_ section as they can only be edited from the CLI environment.

You can however, manage the integration, set up and manage embeds (for public integrations) and view the partner dashboard for the integration from the Platform UI.