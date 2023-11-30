---
title: Change authentication scheme
order: 2
layout: post-toc
redirect_from: /manage/making-changes#changing-authentication-scheme
---

## Change scenario

If your API’s authentication method changes, or your app rolls out different endpoints for integration users; you would need to change the method Zapier uses to authenticate user accounts.

## Impact to users

Changing the authentication type (e.g., Basic Auth, API Key, or OAuth) of an integration is regarded as a breaking change. Notably, migration is impracticable since all pre-existing connected accounts would stop working if migrated. Users would need to make a new connection to your integration and manually modify each of their Zaps.

## Best practices

**Creating a New Version**
- [Clone](https://platform.zapier.com/manage/clone) your app, generating a new version.
- [Remove](https://platform.zapier.com/build/auth#how-to-remove-or-change-zapier-integration-authentication-scheme) the existing authentication method and incorporate the new one.
- Once configured, [promote](https://platform.zapier.com/manage/promote) this version, making it available for new users to select during the connection of your integration to Zapier.

**Managing Existing Users**
- If users with existing authentications can retain their connection using the old method, enabling them to stick to the old version is recommended.
- However, they will be prompted to form a new connection for any new Zaps since only the promoted version is available during a name-based app search.


**Deprecating legacy authentication scheme**
- If existing authentications are set to be non-functional in the future, then [Deprecation](https://platform.zapier.com/manage/deprecate) is required.
- Be mindful that this can be notably disruptive for our mutual users and thus should be considered carefully.

>NOTE: this method is not possible with apps built in the legacy web builder. To update the authentication, you would need to update all triggers/actions/searches as well; as deleting the authentication method and re-adding it in the new builder would not be compatible with existing triggers/actions/searches built in the legacy web builder.