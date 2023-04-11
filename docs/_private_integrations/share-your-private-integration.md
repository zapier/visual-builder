---
title: Share your private integration to users
order: 3
layout: post-toc
redirect_from: /private_integrations/
---
# Share your private integration to users

After you’ve built your private integration, you can invite users to start using your integration in their Zaps. There are two ways you can share your private integration with users:

## Invite users with a public link

You can share a link with users to all versions of your integration. 

> Note:
> * You can’t view invited users via a public link.
> * You can’t revoke a link invite, once shared. If you require control over who accesses your private integration, we recommend inviting users by email. 


<ol> 
 <li><a href="https://zapier.com/app/developer">Log into the Zapier Platform UI</a> or refer to the <a href="https://platform.zapier.com/cli_tutorials/getting-started#invite-users-to-your-app">Zapier Platform CLI documentation</a>.</li>
 <li>Select <b>My Integration</b>.</li>
 <li>In the <i>Integrations</i> section, select your <b>integration</b>.</li>
 <li>In the left sidebar, under <i>Manage</i> click <b>Sharing</b>.</li>
 <li>Click <img style="vertical-align: middle;" src="https://res.cloudinary.com/zapier-media/image/upload/zinnia-icons/actionCopy.svg" alt="ICON NAME icon" width="24"> to copy the invite public link.</li>
</ol>


Now you can share the invite link with users. The link will take users to your private integration landing page where they can follow the on-screen instructions to accept your invite. 
<br>
<br>

## Invite users by email

You can invite new users by emailing them. You also have the option to select what version of your private integration they can have. All users invited by email are tracked in your Sharing settings, allowing you to control who has access to your private integration.

> **Note**: You can only invite 100 users by email.
<ol>
 <li><a href="https://zapier.com/app/developer">Log into the Zapier Platform UI</a> or refer to the <a href="https://platform.zapier.com/cli_tutorials/getting-started#invite-users-to-your-app">Zapier Platform CLI documentation</a>.</li>
 <li> Select <b>My Integration</b>.</li>
 <li>In the <i>Integrations</i> section, select your <b>integration</b>.</li>
 <li> In the left sidebar, under <i>Manage</i> click <b>Sharing</b>.</li>
 <li>In the <i>Email</i> field, insert the <b>user’s email</b>.</li>
 <li> [Optional] In the <i>Versions</i> dropdown menu, select what <b>version</b> of your private integration you want your user to access.</li>
<li>Click <b>Invite</b>. This will instantly send the user an email from notifications@mail.zapier.com.</li>
</ol>

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

<ol>
 <li> <a href="https://zapier.com/app/developer">Log into the Zapier Platform UI</a> </li>
 <li>Select <b>My Integrations</b>. </li>
 <li> In the <i>Integrations</i> section, select your <b>integration</b>.</li>
 <li> In the left sidebar, under <i>Manage</i> click <b>Sharing</b>.</li>
 <li> In the row for your user, click <b>Delete</b>.</li>
 <li> Click <b>Really?</b>. This will revoke the invite email sent to the user.</li>
</ol>

#### Zapier Platform CLI

> **Note**: This method will remove users from all versions of your integration.

<ol>
<li>  In your terminal, navigate to the directory of your integration (the directory with the <code>.zapierapprc</code> file).</li>
<li> Run <code>zapier users:remove user@example.com</code>. Replace <i>user@example.com</i> with the email address that you’d like to revoke.</li>
<li>  The CLI will prompt you to confirm your revocation, type <b>Y</b> and click <b>Enter</b>.</li>
</ol>

