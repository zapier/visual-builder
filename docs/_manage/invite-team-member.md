---
title: Add team members to integration
order: 1
layout: post-toc
redirect_from: 
    - /quickstart/
    - /quickstart/invite-team-member
---

# Add team members to integration

## Roles & permissions

Invite team members to join your Zapier integration so they can start collaborating! The Zapier Platform has user roles so you can feel confident with assigning different team members the right level of access. Note: some permissions depend on your integration’s publish status (private vs beta / public).

### Admin

Admins have full access to build, manage, and edit your Zapier integration. Admin access is recommended for developers and others who directly contribute to building and maintaining your integration.

### Collaborator

Collaborators have view-only access to your Zapier integration (including integration details, history, and analytics). Collaborators are unable to build/edit but can view performance data, comment on feature requests and bugs, and access tools to embed Zapier integrations inside your UI to rack up user adoption. Collaborator access is recommended for product, leadership, partnership, marketing, and support teams, and others that do not contribute directly to the creation and maintenance of the integration.

### Subscriber (legacy)

Subscribers receive monthly email updates only. This is a legacy role that is no longer available. We recommend using the Collaborator role.

| **Permission**                                                    	| **Admin** 	| **Collaborator** 	| **Subscriber** (Legacy) 	|
|-------------------------------------------------------------------	|-----------	|------------------	|-------------------------	|
| View Partner Program                                              	| ✓         	| ✓                	| -                       	|
| View Integration Settings                                         	| ✓         	| ✓                	| -                       	|
| Edit Integration Settings (private integrations only)             	| ✓         	| ✓                	| -                       	|
| Validate Integration                                              	| ✓         	| ✓                	| -                       	|
| Publish Integration (private integrations only)                   	| ✓         	| -                	| -                       	|
| View Authentication, Trigger and Action pages (no sensitive info) 	| ✓         	| ✓                	| -                       	|
| Edit Integration                                                  	| ✓         	| -                	| -                       	|
| View Integration Versions                                         	| ✓         	| ✓                	| -                       	|
| Manage Integration Versions                                       	| ✓         	| -                	| -                       	|
| View and Comment on Bug and Feature Requests                      	| ✓         	| ✓                	| -                       	|
| Invite Users to Use Integration                                   	| ✓         	| ✓                	| -                       	|
| View Team Members                                                 	| ✓         	| ✓                	| -                       	|
| Add Admins as Team Members                                        	| ✓         	| -                	| -                       	|
| Add Collaborators as Team Members                                 	| ✓         	| ✓                	| -                       	|
| Remove Team Members                                               	| ✓         	| -                	| -                       	|
| View Analytics                                                    	| ✓         	| ✓                	| -                       	|
| Monitor Events and Logs                                           	| ✓         	| -                	| -                       	|
| View Historical Audit Logs                                        	| ✓         	| ✓                	| -                       	|
| Zapier Command Line Interface (CLI)                               	| ✓         	| -                	| -                       	|
| Embed Zapier Partner Tools                                        	| ✓         	| ✓                	| -                       	|
| Receive Integration Issue Notification Email                      	| ✓         	| ✓                	| -                       	|
| Receive Monthly Partner Newsletter Email                          	| ✓         	| ✓                	| ✓                       	|

## Integration Ownership

Integrations are not owned by individuals, but rather by a team. Any Zapier user who is added as an Admin to the integration team will have complete read/write access to the integration. Think of integration Admins as the "integration owners."

When you access your integration on the developer platform, the “Manage Team” page will display a list of current integration Admins and Collaborators. From this page, you can invite other users to become either an Admin or Collaborator for the integration. Note that Admins can invite both new Admins and Collaborators, whilst Collaborators can only invite new Collaborators.

![Screenshot showing steps to invite new team members](https://cdn.zappy.app/bae7d5d6224b6b0d8cca85458154574a.png)

Once you invite a new team member as an Admin and they accept the invite, they will be able to access the integration through their own Zapier account. They can then choose to remove you as an Admin from the integration, if desired.

An integration can have as many Admins and Collaborators as necessary. However, please note that if you are removed as an Admin, you will only be able to regain Admin access if invited by an existing Admin. Zapier is unable to restore Admin access.

## Manage Team - Settings

### Allow team members with specific email domains to join your integration as a Collaborator

This setting allows anyone with an email address associated with an approved email domain to join your integration as a Collaborator on their own, without waiting for an admin invitation. This makes it easy for your team members to join and view but not make changes to the integration. When a team member joins your integration this way, all the admins will receive an email notification.

If you entered a Homepage URL in the Integration Settings page, that URL is used as an approved email domain. You can then edit, delete, or add more approved email domains. If there are no approved email domains, your team members cannot join your integration on their own, even if this setting has been enabled.

![ManageTeamSettings](https://cdn.zappy.app/ba32ec04e4bb8fb6fa98c6f0f6c2c0c2.png)

![EmailDomains](https://cdn.zappy.app/7c423f6e7166c70d4622393859cedb9b.png)

## Join as a collaborator

To sign up as a collaborator, log in to Zapier (or sign up for Zapier if you don’t already have an account) then join your integration on the my integrations page.

![JoinIntegrationFromDashbaord](https://cdn.zappy.app/5a3452ea8e72049a2083aab5dac59069.png)

![JoinIntegration](https://cdn.zappy.app/b47f3a9b672533df505667cf3933a9ee.png)

## Managing Partner Email Subscriptions

### General Partner Marketing Updates

Zapier sends out general partner marketing updates related to your integration and the Zapier platform. These emails include:
* Monthly Partner Newsletter with integration data insights
* Outreach about partnership and co-marketing opportunities 

To control your subscription for these emails, visit the [email preferences page](https://developer.zapier.com/partner-settings/email) in the developer dashboard and opt in or out per integration as needed.

### Platform and Partner Program Updates

We'll keep you in the loop with Zapier Platform and Partner Program Updates. These emails include:
* Alerts about user [Bugs and Feature Requests](https://platform.zapier.com/manage/analyze-integration-performance#bugs)
* Critical Platform and Program Updates

You cannot unsubscribe from Zapier Platform and Partner Program Updates unless an existing integration team member removes you from the integration team entirely. These emails deliver essential announcements about the Partner Program, Zapier Platform features, product updates, and compliance with integration quality standards to ensure you're always up-to-date with changes that could impact your use of the Zapier Platform.

> **Note: An Admin can remove another Admin or Collaborator from the integration team. A Collaborator can only remove other Collaborators from the integration team.**

### Opting Team Members Into Emails

If you want to ensure that your team members receive partner marketing emails:

1. [Invite your team members](https://platform.zapier.com/manage/invite-team-member) to the integration team as either an Admin or Collaborator and ensure they accept the invite
2. Team members who accept the invite will automatically receive Platform and Partner Program Updates
3. If they want to receive General Partner Marketing updates, have them visit their [email preferences](https://developer.zapier.com/partner-settings/email) in the developer platform and ensure they’re opted into emails for the integration you want them to receive alerts for