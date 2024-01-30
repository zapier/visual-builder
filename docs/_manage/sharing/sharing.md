---
title: Share your integration
order: 1
layout: post-toc
redirect_from: 
    - /private_integrations/share-your-private-integration
    - /manage/share-integration
---
# Share your integration

Once an integration is public, all users would have access to it when searching for an app's name in the Zap Editor, or in the [Zapier App Directory](https://zapier.com/apps). 

For private integrations, there are two ways to share access with users:

## 1. Invite users with a public link

You can share a link with users to all versions of your integration. 

* You can’t view a list of users that have accessed the public link.
* You can’t revoke a link invite, once shared. If you require control over who accesses your integration, we recommend inviting users by email. 

- [Log into the Platform UI](https://zapier.com/app/developer)
- Select **My Integration**.
- In the *Integrations* section, select your **integration**.
- In the left sidebar, under *Manage* click **Sharing**.
- Click <img style="vertical-align: middle; width:24px;" src="https://res.cloudinary.com/zapier-media/image/upload/zinnia-icons/actionCopy.svg" alt="ICON NAME icon"> to copy the invite public link. 
- You can access the public link in this way for integrations built in the Platform UI or the Platform CLI.
- Generating a public sharing link for one specific version only is  available in the [Platform CLI](https://github.com/zapier/zapier-platform/blob/main/packages/cli/README.md#sharing-an-app-version), but not the Platform UI. 

Share the invite link with users via your website or other method. The link will take users to your integration landing page where they can follow the on-screen instructions to accept your invite to all versions of the integration. 

## 2. Invite users by email

Inviting users by email gives you the option to select which version of your integration they can access. All users invited by email are tracked in the Sharing tab, allowing you to view and control who has access to your integration.

* You can only invite 200 users by email.

- [Log into the Platform UI](https://zapier.com/app/developer) or refer to the [Platform CLI documentation](https://github.com/zapier/zapier-platform/blob/main/packages/cli/README.md#sharing-an-app-version).
- Select **My Integration**.
- In the *Integrations* section, select your **integration**.
- In the left sidebar, under *Manage* click **Sharing**.
- In the *Email* field, insert the **user’s email**.
- (Optional) In the *Versions* dropdown menu, select which **version** of your integration you want your user to access.
- Click **Invite**. This will instantly send the user an email from notifications@mail.zapier.com. 
- You can send invitations in this way for integrations built in the Platform UI or the Platform CLI.

The user’s email will be added to the table in your Sharing settings. From there, you can track the status of their invite. They will need to accept the email invite in order to be able to access the integration.  

## Revoke invites sent by email

Revoking invites will remove a user’s access from that integration version, and all Zaps will immediately be paused. The user won't be able to use your app again until they're re-invited or it has gone public. In practice, this is not used often as it's very disruptive to users.

### Revoke public link invite

It’s not possible to revoke a user's access to or change a public link invite once it has been shared. 

### Revoke email invite 

There are two ways to revoke email invites using either the Platform UI or Platform CLI.

#### Zapier Platform UI

1. [Log into the Platform UI](https://zapier.com/app/developer) 
2. Select **My Integration**.
3. In the *Integrations* section, select your **integration**.
4. In the left sidebar, under *Manage* click **Sharing**.
5. In the row for your user, click **Delete**.
6. Click **Really?** to revoke the access for that user. 

#### Zapier Platform CLI

> **Note**: This method will remove users from all versions of your integration.

1. In your terminal, navigate to the directory of your integration (the directory with the `.zapierapprc` file).
2. Run zapier `users:remove user@example.com`. Replace `user@example.com` with the email address that you’d like to revoke access for.
3. The CLI will prompt you to confirm your revocation, type `Y` and click `Enter`.
