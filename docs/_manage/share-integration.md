---
title: Share integration to users
order: 2
layout: post-toc
redirect_from: /manage/
---
# Share integration to users

After you’ve built your integration, you can invite users to start using your integration in their Zaps. There are two ways you can share your integration with users:

## Invite users with a public link

You can share a link with users to all versions of your integration. 

> Note:
> * You can’t view invited users via a public link.
> * You can’t revoke a link invite, once shared. If you require control over who accesses your integration, we recommend inviting users by email. 

1. [Log into the Platform UI](https://zapier.com/app/developer) or refer to the [Platform CLI documentation](https://platform.zapier.com/quickstart/platform-cli-tutorial#invite-users-to-your-app).
2. Select **My Integration**.
3. In the *Integrations* section, select your **integration**.
4. In the left sidebar, under *Manage* click **Sharing**.
5. Click <img style="vertical-align: middle; width:24px;" src="https://res.cloudinary.com/zapier-media/image/upload/zinnia-icons/actionCopy.svg" alt="ICON NAME icon"> to copy the invite public link. 

Now you can share the invite link with users. The link will take users to your integration landing page where they can follow the on-screen instructions to accept your invite. 
<br>
<br>

## Invite users by email

You can invite new users by emailing them. You also have the option to select what version of your integration they can have. All users invited by email are tracked in your Sharing settings, allowing you to control who has access to your integration.

> **Note**: You can only invite 100 users by email.

1. [Log into the Platform UI](https://zapier.com/app/developer) or refer to the [Platform CLI documentation](https://platform.zapier.com/quickstart/platform-cli-tutorial#invite-users-to-your-app.
2. Select **My Integration**.
3. In the *Integrations* section, select your **integration**.
4. In the left sidebar, under *Manage* click **Sharing**.
5. In the *Email* field, insert the **user’s email**.
6. (Optional) In the *Versions* dropdown menu, select what **version** of your integration you want your user to access.
7. Click **Invite**. This will instantly send the user an email from notifications@mail.zapier.com. 

The user’s email will be added to the table in your Sharing settings. From there, you can track the status of their invite. 
<br>
<br>

## Revoke invites sent to users 

Revoking invites will remove a user’s access to use your integration in their Zaps, and all Zaps will immediately turn off. 

### Revoke public link invite

It’s not possible to revoke a public link invite once it’s been shared. 

### Revoke email invite 

There are two ways to revoke email invites using either the Zapier Platform UI or Zapier Platform CLI.

#### Zapier Platform UI

1. [Log into the Platform UI](https://zapier.com/app/developer) 
2. Select **My Integration**.
3. In the *Integrations* section, select your **integration**.
4. In the left sidebar, under *Manage* click **Sharing**.
5. In the row for your user, click **Delete**.
6. Click **Really?** to revoke the invite email sent to the user. 

#### Zapier Platform CLI

> **Note**: This method will remove users from all versions of your integration.

1. In your terminal, navigate to the directory of your integration (the directory with the `.zapierapprc` file).
2. Run zapier `users:remove user@example.com`. Replace `user@example.com` with the email address that you’d like to revoke.
3. The CLI will prompt you to confirm your revocation, type `Y` and click `Enter`.
