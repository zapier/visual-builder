---
title: Add team members to integration
order: 1
layout: post-toc
redirect_from: 
    - /quickstart/invite-team-member
    - /manage/invite-team-member
    - /manage/
---

# Invite team members to your integration

Integrations do not have a dedicated owner, instead they are managed by a team that can be modified as needed. Add team members to your integration to collaborate, contribute, and view analytics data for your integration on the Developer Platform. Your integration team can have up to 200 team members, regardless of whether your integration is Private or Public. Team members added to your integration will be assigned one of the following roles:

- **Admin**: Admins are granted read and write access to the integration. This role is ideal for developers and individuals actively involved in building and maintaining the integration.

- **Collaborator**: Collaborators are granted read-only access to the integration. Collaborator access is recommended for product, leadership, partnership, marketing, and other teams seeking access to integration data for analysis and record-keeping without direct involvement in its creation and maintenance. While they cannot make direct changes to the integration, they can:

    * View performance data
    * View the integration history
    * Review and comment on feature requests and bug reports
    * Access tools to embed your integration throughout your site to drive user adoption

## Invite team members

To add team members to your integration, follow these steps:

1. Log into the [Developer Platform](https://zapier.com/app/developer)
2. Choose your integration
3. In the _Manage_ section on the left sidebar, select _Manage Team_
4. Select _Invite Team Member_
5. Enter the email address of the team member that you want to invite
6. Select the role that you wish to assign to the team member
7. A note will be included in the invitation email. You can either use the default message provided, or customize it with your own text
8. Click _Send Invite_.

> **Note**: Admins can invite both Admins and Collaborators, while Collaborators can only invite Collaborators.

Once you click _Send Invite_, an email invitation will be sent to the invitee, requesting their acceptance. If the invitee does not already have a Zapier account associated with the invited email, they will need to create an account first. Upon accepting the invitation, they will gain access to the integration through their Zapier account on the Developer Platform.

## Self-serve Collaborator access

Depending on your [integration settings](https://cdn.zappy.app/b2637f3ad910c36c4e8c8224c349beee.png), users have the option to self-serve and join an integration team as Collaborators. This feature employs domain-name verification and is managed by integration Admins. Currently, this feature is only available for integrations listed in [Zapier's directory](https://zapier.com/apps).

### Enable or disable self-serve Collaborator access

To toggle the “Join an Integration as Collaborators” feature, please follow these steps:
1. Log into the [Developer Platform](https://zapier.com/app/developer)
2. Choose your integration
3. In the _Manage_ section on the left sidebar, select _Manage Team_
4. Select _Settings_
5. Click the toggle to enable or disable self-serve join as Collaborator

### Manage eligible email domains for self-serve Collaborator access
1. Log into the [Developer Platform](https://zapier.com/app/developer)
2. Choose your integration
3. In the _Manage_ section on the left sidebar, select _Manage Team_
4. Select _Settings_
5. Click “Edit email domains”
6. Add/remove the domain(s) to be allowed

### Join an integration team via self-serve Collaborator access
1. Log into the [Developer Platform](https://zapier.com/app/developer)
2. Click “Get Access” under Join an Integration as Collaborators
3. Search for and select your integration, then click “Submit”
4. If the Zapier account you're using is associated with an approved domain, you'll receive an invitation to join via email

## View and remove team members

You can view a list of invited team members (both accepted and pending invites) from the _Manage Team_ page. Admins have the ability to remove team members (both other Admins and Collaborators) from this page. Collaborators can only remove other Collaborators. You can also remove yourself from the team, regardless of your role. It’s important to note that if you are removed as an Admin, you can regain Admin access only if invited by an existing Admin.

## Assign marketing and technical contacts

Admins have the ability to assign dedicated marketing and technical contacts on the integration team. Assigning these contacts allows us to better streamline outbound communication, and ensures the right contacts receive timely information. Please note that Zapier's support teams might reach out to the technical contact for technical support. E.g. we might contact this person so we can collaborate on trickier Customer Support tickets on Zaps that involve your integration.

### How to assign contacts

1. Navigate to the “Manage team” page in the developer platform
2. Click the “Settings” icon for the user you want to assign a role to
3. Click either “Set marketing contact” or “Set technical contact”
4. Users will be tagged with the role they are assigned

![Screenshot showing options to select contact type](https://cdn.zappy.app/6e7b628f49cccb820ea693b224619da8.png)
![Screenshot shoting marketing and techincal contact tags](https://cdn.zappy.app/473075ad407c94a93cbccd1504173268.png)

### Notes

* Each integration team can have only one designated marketing contact and one designated technical contact at a time
* A single user can be labelled as both the technical and marketing contact, they do not need to be separate users
* Users are not alerted when they are assigned or removed from a role
* Only Admins can assign roles, Collaborators cannot assign roles
* You can manually remove a role from a user by clicking the “Settings” icon and selecting “Revoke technical contact” or “Revoke marketing contact”
* You do not need to remove a role from a user before assigning the role to another user
* Assigning a role to a new user that’s already been assigned to another user will cause the role to automatically be removed from the original user
* Only integration team members that have accepted a role can be assigned a role (ie team members that are Invitation Pending cannot be assigned a role)
* The user assigned as the marketing contact will be shown as the contact on private invite sharing pages

![Screenshot showing private invite sharing page](https://cdn.zappy.app/defb445b2a2807fd2c6d0e45dde346b5.png)

## Manage email subscriptions relating to your integration

### General marketing updates

Zapier sends out general partner marketing updates related to your integrations and the Developer Platform. These emails include:

* Monthly Partner Newsletter with integration data insights
* Outreach about partnership and co-marketing opportunities 

To control your subscription for these emails, visit the [email preferences page](https://developer.zapier.com/partner-settings/email) in the developer dashboard and opt in or out per each integration you are a team member of. 

### Platform and Partner Program updates

All members of your integration's team will also receive Zapier Platform and Partner Program Updates. These emails include:
* Alerts about user [Bugs and Feature Requests](https://platform.zapier.com/manage/analyze-integration-performance#bugs)
* Critical Platform and Program Updates

You cannot unsubscribe from Zapier Platform and Partner Program Updates unless an existing integration team member removes you from the integration team entirely. These emails deliver essential announcements about the Partner Program, Zapier Platform features, product updates, and compliance with integration quality standards to ensure you're always up-to-date with changes that could impact your use of the Zapier Platform.

> **Note: An Admin can remove another Admin or Collaborator from the integration team. A Collaborator can only remove other Collaborators from the integration team.**

### Opting team members into emails

If you want to ensure that your team members receive partner marketing emails:

1. [Invite your team members](https://platform.zapier.com/manage/add-team) to the integration team as either an Admin or Collaborator and ensure they accept the invite.
2. Team members who accept the invite will automatically receive Platform and Partner Program Updates.
3. If they want to receive General Partner Marketing updates, have them visit their [email preferences](https://developer.zapier.com/partner-settings/email) in the developer platform and ensure they’re opted into emails for the integration you want them to receive alerts for.
