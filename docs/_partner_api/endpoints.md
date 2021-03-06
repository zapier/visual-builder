---
title: Endpoints
order: 6
layout: post-toc
redirect_from: /partner_api/
---

# Endpoints

## GET /v1/apps

|            URL             | Protected By |
| :------------------------: | :----------: |
| **api.zapier.com/v1/apps** |  Client ID   |

> **Notes**
>
> - Your own app will not be returned.
> - Zapier built-in apps will not be returned.
> - Order of the result is by app popularity.

**Arguments**

Available parameters to the Apps resource:

| parameter     | requirement | notes                                                                                  |
| ------------- | ----------- | -------------------------------------------------------------------------------------- |
| **client_id** | Required    | Your application client ID.                                                            |
| **per_page**  | Optional    | (defaults to 100, max of 100) Limit the number of apps returned.                       |
| **page**      | Optional    | (defaults to 1) The page number. Page number 1 refers to the first page in the result. |

**Example Requests**

Get apps that can be integrated with my app.

```bash
curl -L "https://api.zapier.com/v1/apps?client_id=${client_id}"
```

Get apps that can be integrated with my app, returning only 5 results per page

```bash
curl -L "https://api.zapier.com/v1/apps?client_id=${client_id}&per_page=5"
```

**Example Response**

> Refer to the [App object](#app) reference for all the available fields.

```json
{
  "prev_url": "https://api.zapier.com/v1/apps?per_page=2&page=1",
  "page": 2,
  "objects": [
    {
      "description": "Slack is a platform for team communication: everything in one place, instantly searchable, available wherever you go. Offering instant messaging, document sharing and knowledge search for modern teams.",
      "links": {
        "mutual:zap_templates": "https://api.zapier.com/v1/zap-templates?apps=slack"
      },
      "title": "Slack",
      "url": "https://zapier.com/partner/embed/apps/trello/integrations/slack",
      "image": "https://cdn.zapier.com/storage/developer/57b336375384ab62cc06e7e83d5c3622_2.png",
      "images": {
        "url_16x16": "https://cdn.zapier.com/storage/developer/57b336375384ab62cc06e7e83d5c3622_2.16x16.png",
        "url_32x32": "https://cdn.zapier.com/storage/developer/57b336375384ab62cc06e7e83d5c3622_2.32x32.png",
        "url_128x128": "https://cdn.zapier.com/storage/developer/57b336375384ab62cc06e7e83d5c3622_2.128x128.png",
        "url_64x64": "https://cdn.zapier.com/storage/developer/57b336375384ab62cc06e7e83d5c3622_2.64x64.png"
      },
      "slug": "slack",
      "categories": [
        {
          "slug": "team-chat"
        },
        {
          "slug": "top-100"
        }
      ]
    },
    {
      "description": "Share your ideas with MailChimp email newsletters\u2014then use its landing page and form builders to grow your lists and take marketing further with drip and transactional emails.",
      "links": {
        "mutual:zap_templates": "https://api.zapier.com/v1/zap-templates?apps=mailchimp"
      },
      "title": "MailChimp",
      "url": "https://zapier.com/partner/embed/apps/trello/integrations/mailchimp",
      "image": "https://cdn.zapier.com/storage/services/5c727288d9c2f69a9eee136c5f5a0f72.png",
      "images": {
        "url_16x16": "https://cdn.zapier.com/storage/services/5c727288d9c2f69a9eee136c5f5a0f72.16x16.png",
        "url_32x32": "https://cdn.zapier.com/storage/services/5c727288d9c2f69a9eee136c5f5a0f72.32x32.png",
        "url_128x128": "https://cdn.zapier.com/storage/services/5c727288d9c2f69a9eee136c5f5a0f72.128x128.png",
        "url_64x64": "https://cdn.zapier.com/storage/services/5c727288d9c2f69a9eee136c5f5a0f72.64x64.png"
      },
      "slug": "mailchimp",
      "categories": [
        {
          "slug": "email-newsletters"
        },
        {
          "slug": "top-100"
        }
      ]
    }
  ],
  "next_url": "https://api.zapier.com/v1/apps?per_page=2&page=3",
  "per_page": 2,
  "total": 1193,
  "pages": 597
}
```

## GET /v1/zap-templates

|                 URL                 | Protected By |
| :---------------------------------: | :----------: |
| **api.zapier.com/v1/zap-templates** |  Client ID   |

**Arguments**

Available parameters to the Zap templates resource:

| parameter     | requirement | notes                                                                                                                                                            |
| ------------- | ----------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **client_id** | Required    | Your application client ID.                                                                                                                                      |
| **templates** | Optional    | A comma separated list of specific Zap templates.                                                                                                                |
| **apps**      | Optional    | A comma separated list of Zapier Apps to match Zap templates against. **Note: Your app will always be one of the apps.**                                         |
| **limit**     | Optional    | (defaults to 5, max of 100) Limit the number of Zap templates returned.                                                                                          |
| **offset**    | Optional    | (defaults to 0) The number of Zap templates to skip before beginning to return the Zap templates. The default value is 0, which is the offset of the first item. |

**Example Requests**

Get all Zap templates for my app.

```bash
curl -L "https://api.zapier.com/v1/zap-templates?client_id=${client_id}"
```

Get all Zap templates that include my app and another.

```bash
curl -L "https://api.zapier.com/v1/zap-templates?client_id=${client_id}&apps=mailchimp"
```

**Example Response**

> Refer to the [Zap template](#zap-template) reference for all the available fields.

```json
[
  {
    "description": "<p>Facebook Lead Ads are an excellent way to grow your list of individuals interested in learning more about your product or service, but taking a next step with those people can sometimes take a back seat to your other tasks. With this Facebook Lead Ads-MailChimp integration, you'll no longer need to think about adding new leads to a marketing campaign—each new lead is automatically added to the list of your choice.</p>\n\n<h2>How this Facebook Lead Ads-MailChimp integration works</h2>\n\n<ol>\n<li>Someone fills out one of your Facebook Lead Ads</li>\n<li>Zapier adds that individual to a specified list in MailChimp</li>\n</ol>\n\n<h2>Apps involved</h2>\n\n<ul>\n<li>Facebook Lead Ads</li>\n<li>MailChimp</li>\n</ul>\n",
    "title": "Subscribe new Facebook Lead Ad leads to a MailChimp list",
    "url": "https://zapier.com/apps/facebook-lead-ads/integrations/mailchimp/10127/subscribe-new-facebook-lead-ads-mailchimp-list",
    "type": "guided_zap",
    "status": "published",
    "description_raw": "Facebook Lead Ads are an excellent way to grow your list of individuals interested in learning more about your product or service, but taking a next step with those people can sometimes take a back seat to your other tasks. With this Facebook Lead Ads-MailChimp integration, you'll no longer need to think about adding new leads to a marketing campaign—each new lead is automatically added to the list of your choice.\r\n\r\n## How this Facebook Lead Ads-MailChimp integration works\r\n\r\n1. Someone fills out one of your Facebook Lead Ads\r\n2. Zapier adds that individual to a specified list in MailChimp\r\n\r\n## Apps involved\r\n\r\n- Facebook Lead Ads\r\n- MailChimp",
    "slug": "subscribe-new-facebook-lead-ads-mailchimp-list",
    "description_plain": "Facebook Lead Ads are an excellent way to grow your list of individuals interested in learning more about your product or service, but taking a next step with those people can sometimes take a back seat to your other tasks. With this Facebook Lead Ads-MailChimp integration, you'll no longer need to think about adding new leads to a marketing campaign—each new lead is automatically added to the list of your choice.\n\nHow this Facebook Lead Ads-MailChimp integration works\n\nSomeone fills out one of your Facebook Lead Ads\n\nZapier adds that individual to a specified list in MailChimp\n\nApps involved\n\nFacebook Lead Ads\n\nMailChimp",
    "steps": [
      {
        "description": "Facebook lead ads make signing up for business information easy for people and more valuable for businesses. The Facebook lead ad app is useful for marketers who want to automate actions on their leads.",
        "title": "Facebook Lead Ads",
        "url": "https://zapier.com/apps/facebook-lead-ads/integrations",
        "image": "https://cdn.zapier.com/storage/services/fd9fef95169fd589d6cda992c0057cf8.png",
        "api": "FacebookLeadsAPI",
        "slug": "facebook-lead-ads",
        "hex_color": "3b5998",
        "images": {
          "url_128x128": "https://cdn.zapier.com/storage/services/fd9fef95169fd589d6cda992c0057cf8.128x128.png",
          "url_64x64": "https://cdn.zapier.com/storage/services/fd9fef95169fd589d6cda992c0057cf8.64x64.png",
          "url_16x16": "https://cdn.zapier.com/storage/services/fd9fef95169fd589d6cda992c0057cf8.16x16.png",
          "url_32x32": "https://cdn.zapier.com/storage/services/fd9fef95169fd589d6cda992c0057cf8.32x32.png"
        },
        "id": 3535
      },
      {
        "description": "MailChimp is an email marketing service provider, founded in 2001. It has 6 million users that collectively send over 10 billion emails through the service each month.",
        "title": "MailChimp",
        "url": "https://zapier.com/apps/mailchimp/integrations",
        "image": "https://cdn.zapier.com/storage/services/5c727288d9c2f69a9eee136c5f5a0f72.png",
        "api": "MailChimpAPI",
        "slug": "mailchimp",
        "hex_color": "239AB9",
        "images": {
          "url_128x128": "https://cdn.zapier.com/storage/services/5c727288d9c2f69a9eee136c5f5a0f72.128x128.png",
          "url_64x64": "https://cdn.zapier.com/storage/services/5c727288d9c2f69a9eee136c5f5a0f72.64x64.png",
          "url_16x16": "https://cdn.zapier.com/storage/services/5c727288d9c2f69a9eee136c5f5a0f72.16x16.png",
          "url_32x32": "https://cdn.zapier.com/storage/services/5c727288d9c2f69a9eee136c5f5a0f72.32x32.png"
        },
        "id": 6
      }
    ],
    "create_url": "https://zapier.com/app/editor/template/10127?utm_campaign=Zap%20Templates%20Partners%20API&embedded=true&referrer=FacebookLeadsAPI&utm_source=partners&utm_medium=api&selected_apis=FacebookLeadsAPI,MailchimpCLIAPI@1.0.10",
    "id": 10127
  }
]
```

**Paging through results using limit and offset**

By default, this API returns the first 5 Zap templates. To get a different set of items,
you can use the `offset` and `limit` parameters in the query string.

For example, to get 20 Zap templates, skipping the first 20 results:

```bash
curl -H "Authorization: Bearer {token}" \
  -L "https://api.zapier.com/v1/zap-templates?client_id=${client_id}&limit=20&offset=20"
```

## GET /v1/zap-templates/me

Lookup a user's Zap templates that they've added (published or draft). **Note: We are limiting this endpoint to partners. This means that you will only see results for Zap templates that include your app in one of the steps.**

|                  URL                   |      Protected By       | Required Scopes |
| :------------------------------------: | :---------------------: | :-------------: |
| **api.zapier.com/v1/zap-templates/me** | Client ID, Access Token |   `templates`   |

**Arguments**

Available parameters to the Zap templates resource:

| parameter     | requirement | notes                                                                                                                                                            |
| ------------- | ----------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **client_id** | Required    | Your application client ID.                                                                                                                                      |
| **templates** | Optional    | A comma separated list of specific Zap templates.                                                                                                                |
| **apps**      | Optional    | A comma separated list of Zapier Apps to match Zap templates against. **Note: Your app will always be one of the apps.**                                         |
| **limit**     | Optional    | (defaults to 5, max of 100) Limit the number of Zap templates returned.                                                                                          |
| **status**    | Optional    | (defaults to `published`) Filter by specific status of a Zap template. Available statuses: `draft` and `published`.                                              |
| **offset**    | Optional    | (defaults to 0) The number of Zap templates to skip before beginning to return the Zap templates. The default value is 0, which is the offset of the first item. |

**Example Requests**

Get all Zap templates for my app.

```bash
curl -H "Authorization: Bearer {token}" -L "https://api.zapier.com/v1/zap-templates/me?client_id=${client_id}"
```

Get all Zap templates that include my app and another.

```bash
curl -H "Authorization: Bearer {token}" -L "https://api.zapier.com/v1/zap-templates?client_id=${client_id}&apps=mailchimp"
```

Get all Zap templates for my app that are draft.

```bash
curl -H "Authorization: Bearer {token}" -L "https://api.zapier.com/v1/zap-templates/me?client_id=${client_id}&status=draft"
```

**Example Response**

> Refer to the [Zap template](#zap-template) reference for all the available fields.

```json
[
  {
    "description": "<p>Facebook Lead Ads are an excellent way to grow your list of individuals interested in learning more about your product or service, but taking a next step with those people can sometimes take a back seat to your other tasks. With this Facebook Lead Ads-MailChimp integration, you'll no longer need to think about adding new leads to a marketing campaign—each new lead is automatically added to the list of your choice.</p>\n\n<h2>How this Facebook Lead Ads-MailChimp integration works</h2>\n\n<ol>\n<li>Someone fills out one of your Facebook Lead Ads</li>\n<li>Zapier adds that individual to a specified list in MailChimp</li>\n</ol>\n\n<h2>Apps involved</h2>\n\n<ul>\n<li>Facebook Lead Ads</li>\n<li>MailChimp</li>\n</ul>\n",
    "title": "Subscribe new Facebook Lead Ad leads to a MailChimp list",
    "url": "https://zapier.com/apps/facebook-lead-ads/integrations/mailchimp/10127/subscribe-new-facebook-lead-ads-mailchimp-list",
    "type": "guided_zap",
    "status": "published",
    "description_raw": "Facebook Lead Ads are an excellent way to grow your list of individuals interested in learning more about your product or service, but taking a next step with those people can sometimes take a back seat to your other tasks. With this Facebook Lead Ads-MailChimp integration, you'll no longer need to think about adding new leads to a marketing campaign—each new lead is automatically added to the list of your choice.\r\n\r\n## How this Facebook Lead Ads-MailChimp integration works\r\n\r\n1. Someone fills out one of your Facebook Lead Ads\r\n2. Zapier adds that individual to a specified list in MailChimp\r\n\r\n## Apps involved\r\n\r\n- Facebook Lead Ads\r\n- MailChimp",
    "slug": "subscribe-new-facebook-lead-ads-mailchimp-list",
    "description_plain": "Facebook Lead Ads are an excellent way to grow your list of individuals interested in learning more about your product or service, but taking a next step with those people can sometimes take a back seat to your other tasks. With this Facebook Lead Ads-MailChimp integration, you'll no longer need to think about adding new leads to a marketing campaign—each new lead is automatically added to the list of your choice.\n\nHow this Facebook Lead Ads-MailChimp integration works\n\nSomeone fills out one of your Facebook Lead Ads\n\nZapier adds that individual to a specified list in MailChimp\n\nApps involved\n\nFacebook Lead Ads\n\nMailChimp",
    "steps": [
      {
        "description": "Facebook lead ads make signing up for business information easy for people and more valuable for businesses. The Facebook lead ad app is useful for marketers who want to automate actions on their leads.",
        "title": "Facebook Lead Ads",
        "url": "https://zapier.com/apps/facebook-lead-ads/integrations",
        "image": "https://cdn.zapier.com/storage/services/fd9fef95169fd589d6cda992c0057cf8.png",
        "api": "FacebookLeadsAPI",
        "slug": "facebook-lead-ads",
        "hex_color": "3b5998",
        "images": {
          "url_128x128": "https://cdn.zapier.com/storage/services/fd9fef95169fd589d6cda992c0057cf8.128x128.png",
          "url_64x64": "https://cdn.zapier.com/storage/services/fd9fef95169fd589d6cda992c0057cf8.64x64.png",
          "url_16x16": "https://cdn.zapier.com/storage/services/fd9fef95169fd589d6cda992c0057cf8.16x16.png",
          "url_32x32": "https://cdn.zapier.com/storage/services/fd9fef95169fd589d6cda992c0057cf8.32x32.png"
        },
        "id": 3535
      },
      {
        "description": "MailChimp is an email marketing service provider, founded in 2001. It has 6 million users that collectively send over 10 billion emails through the service each month.",
        "title": "MailChimp",
        "url": "https://zapier.com/apps/mailchimp/integrations",
        "image": "https://cdn.zapier.com/storage/services/5c727288d9c2f69a9eee136c5f5a0f72.png",
        "api": "MailChimpAPI",
        "slug": "mailchimp",
        "hex_color": "239AB9",
        "images": {
          "url_128x128": "https://cdn.zapier.com/storage/services/5c727288d9c2f69a9eee136c5f5a0f72.128x128.png",
          "url_64x64": "https://cdn.zapier.com/storage/services/5c727288d9c2f69a9eee136c5f5a0f72.64x64.png",
          "url_16x16": "https://cdn.zapier.com/storage/services/5c727288d9c2f69a9eee136c5f5a0f72.16x16.png",
          "url_32x32": "https://cdn.zapier.com/storage/services/5c727288d9c2f69a9eee136c5f5a0f72.32x32.png"
        },
        "id": 6
      }
    ],
    "create_url": "https://zapier.com/app/editor/template/10127?utm_campaign=Zap%20Templates%20Partners%20API&embedded=true&referrer=FacebookLeadsAPI&utm_source=partners&utm_medium=api&selected_apis=FacebookLeadsAPI,MailchimpCLIAPI@1.0.10",
    "id": 10127
  }
]
```

**Paging through results using limit and offset**

By default, this API returns the first 5 Zap templates. To get a different set of items,
you can use the `offset` and `limit` parameters in the query string.

For example, to get 20 Zap templates, skipping the first 20 results:

```bash
curl -H "Authorization: Bearer {token}" -L "https://api.zapier.com/v1/zap-templates/me?client_id=${client_id}&limit=20&offset=20"
```

## GET /v1/zaps

|            URL             | Protected By | Required Scopes |
| :------------------------: | :----------: | :-------------: |
| **api.zapier.com/v1/zaps** | Access Token |      `zap`      |

> **Note**
>
> 1. The zaps returned are narrowed/filtered by your Zapier app. For example, if you are Trello you'll only be returned a user's Zap that contain Trello in one of the steps of the Zap.
>
> 2. If your app is built with the [Zapier CLI](https://github.com/zapier/zapier-platform-cli) the Zaps returned are for **any** version of your app.

**Arguments**

Available parameters to the Zaps resource:

| parameter                   | requirement | notes                                                                                                                                      |
| --------------------------- | ----------- | ------------------------------------------------------------------------------------------------------------------------------------------ |
| **params\_\_{KEY}={VALUE}** | Optional    | Return Zaps that have a specific key/value set in the params (settings) of the Zap. **Note the `app` parameter must be included as well.** |

**Example Requests**

Get all Zaps in the user's account (note this will only include the OAuth app that is associated with the Zapier app).

```bash
curl -H "Authorization: Bearer {token}" -L "https://api.zapier.com/v1/zaps"
```

Get all Zaps in the user's account that have a particular Trello board (assuming the OAuth app is Trello).

```bash
curl -H "Authorization: Bearer {token}" -L "https://api.zapier.com/v1/zaps?&params__board=BOARD_ID"
```

**Example Response**

> Refer to the [Zap](#zap) reference for all the available fields.

```json
{
  "objects": [
    {
      "id": 125,
      "modified_at": "2017-03-22T09:38:11-05:00",
      "state": "on",
      "steps": [
        {
          "app": {
            "description": "Typeform helps you ask awesomely online! If you ever need to run a survey, questionnaire, form, contest etc... Typeform will help you achieve it beautifully across all devices, every time, using its next generation platform.",
            "hex_color": "8bcbca",
            "id": 4259,
            "image": "https://cdn.zapier.com/storage/developer/5e21b4c1e0a2a3346a801dbc0a2a5a6d_2.png",
            "images": {
              "url_128x128": "https://cdn.zapier.com/storage/developer/5e21b4c1e0a2a3346a801dbc0a2a5a6d_2.128x128.png",
              "url_16x16": "https://cdn.zapier.com/storage/developer/5e21b4c1e0a2a3346a801dbc0a2a5a6d_2.16x16.png",
              "url_32x32": "https://cdn.zapier.com/storage/developer/5e21b4c1e0a2a3346a801dbc0a2a5a6d_2.32x32.png",
              "url_64x64": "https://cdn.zapier.com/storage/developer/5e21b4c1e0a2a3346a801dbc0a2a5a6d_2.64x64.png"
            },
            "api": "TypeformDevAPI",
            "slug": "typeform",
            "title": "Typeform",
            "url": "https://zapier.com/apps/typeform/integrations"
          },
          "type_of": "read"
        },
        {
          "app": {
            "description": "Trello is team collaboration tool that lets you organize anything and everything to keep your projects on task.",
            "hex_color": "0079bf",
            "id": 4192,
            "image": "https://cdn.zapier.com/storage/services/da3ff465abd3a3e1b687c52ff803af74.png",
            "images": {
              "url_128x128": "https://cdn.zapier.com/storage/services/da3ff465abd3a3e1b687c52ff803af74.128x128.png",
              "url_16x16": "https://cdn.zapier.com/storage/services/da3ff465abd3a3e1b687c52ff803af74.16x16.png",
              "url_32x32": "https://cdn.zapier.com/storage/services/da3ff465abd3a3e1b687c52ff803af74.32x32.png",
              "url_64x64": "https://cdn.zapier.com/storage/services/da3ff465abd3a3e1b687c52ff803af74.64x64.png"
            },
            "api": "TrelloAPI",
            "slug": "trello",
            "title": "Trello",
            "url": "https://zapier.com/apps/trello/integrations"
          },
          "type_of": "write"
        }
      ],
      "title": "Create Trello cards from new Typeform entries",
      "url": "https://zapier.com/app/editor/125"
    },
    {
      "id": 123,
      "modified_at": "2017-03-21T22:04:05-05:00",
      "state": "off",
      "steps": [
        {
          "app": {
            "description": "Typeform helps you ask awesomely online! If you ever need to run a survey, questionnaire, form, contest etc... Typeform will help you achieve it beautifully across all devices, every time, using its next generation platform.",
            "hex_color": "8bcbca",
            "id": 4259,
            "image": "https://cdn.zapier.com/storage/developer/5e21b4c1e0a2a3346a801dbc0a2a5a6d_2.png",
            "images": {
              "url_128x128": "https://cdn.zapier.com/storage/developer/5e21b4c1e0a2a3346a801dbc0a2a5a6d_2.128x128.png",
              "url_16x16": "https://cdn.zapier.com/storage/developer/5e21b4c1e0a2a3346a801dbc0a2a5a6d_2.16x16.png",
              "url_32x32": "https://cdn.zapier.com/storage/developer/5e21b4c1e0a2a3346a801dbc0a2a5a6d_2.32x32.png",
              "url_64x64": "https://cdn.zapier.com/storage/developer/5e21b4c1e0a2a3346a801dbc0a2a5a6d_2.64x64.png"
            },
            "api": "TypeformDevAPI",
            "slug": "typeform",
            "title": "Typeform",
            "url": "https://zapier.com/apps/typeform/integrations"
          },
          "type_of": "read"
        },
        {
          "app": {
            "description": "Trello is team collaboration tool that lets you organize anything and everything to keep your projects on task.",
            "hex_color": "0079bf",
            "id": 4192,
            "image": "https://cdn.zapier.com/storage/services/da3ff465abd3a3e1b687c52ff803af74.png",
            "images": {
              "url_128x128": "https://cdn.zapier.com/storage/services/da3ff465abd3a3e1b687c52ff803af74.128x128.png",
              "url_16x16": "https://cdn.zapier.com/storage/services/da3ff465abd3a3e1b687c52ff803af74.16x16.png",
              "url_32x32": "https://cdn.zapier.com/storage/services/da3ff465abd3a3e1b687c52ff803af74.32x32.png",
              "url_64x64": "https://cdn.zapier.com/storage/services/da3ff465abd3a3e1b687c52ff803af74.64x64.png"
            },
            "api": "TrelloAPI",
            "slug": "trello",
            "title": "Trello",
            "url": "https://zapier.com/apps/trello/integrations"
          },
          "type_of": "write"
        }
      ],
      "title": "Create Trello cards from new Typeform entries",
      "url": "https://zapier.com/app/editor/123"
    }
  ]
}
```

# Data Objects

## App

| attribute       | type   | notes                                                                                                                                                 |
| --------------- | ------ | ----------------------------------------------------------------------------------------------------------------------------------------------------- |
| **description** | String | Plain text description of the app.                                                                                                                    |
| **links**       | Object | Link to get mutual Zap templates from Zapier's Partner API                                                                                            |
| **title**       | String | The name of the app.                                                                                                                                  |
| **url**         | String | An absolute url to the Zapbook Apps page.                                                                                                             |
| **image**       | String | The app's logo in large format.                                                                                                                       |
| **images**      | Object | Thumbnails for the app image. <br><small>Available sizes (and respective keys):<br> `url_128x128`, `url_64x64`, `url_32x32`, and `url_16x16`.</small> |
| **slug**        | String | A URL/SEO friendly ID for the app.                                                                                                                    |
| **categories**  | Object | A list of categories this app belongs to.                                                                                                             |

```json
{
  "description": "Slack is a platform for team communication: everything in one place, instantly searchable, available wherever you go. Offering instant messaging, document sharing and knowledge search for modern teams.",
  "links": {
    "mutual:zap_templates": "https://api.zapier.com/v1/zap-templates?apps=slack"
  },
  "title": "Slack",
  "url": "https://zapier.com/partner/embed/apps/trello/integrations/slack",
  "image": "https://cdn.zapier.com/storage/developer/57b336375384ab62cc06e7e83d5c3622_2.png",
  "images": {
    "url_16x16": "https://cdn.zapier.com/storage/developer/57b336375384ab62cc06e7e83d5c3622_2.16x16.png",
    "url_32x32": "https://cdn.zapier.com/storage/developer/57b336375384ab62cc06e7e83d5c3622_2.32x32.png",
    "url_128x128": "https://cdn.zapier.com/storage/developer/57b336375384ab62cc06e7e83d5c3622_2.128x128.png",
    "url_64x64": "https://cdn.zapier.com/storage/developer/57b336375384ab62cc06e7e83d5c3622_2.64x64.png"
  },
  "slug": "slack",
  "categories": [
    {
      "slug": "team-chat"
    },
    {
      "slug": "top-100"
    }
  ]
}
```

## Zap

| attribute       | type            | notes                                                 |
| --------------- | --------------- | ----------------------------------------------------- |
| **id**          | Number          | The ID of the Zap.                                    |
| **modified_at** | Date            | The last modified date time.                          |
| **state**       | String          | One of `'on'`, `'off'`, or `'draft'`                  |
| **steps**       | Array<Zap Step> | An array steps in the Zap. See [Zap Step](#zap-step). |
| **title**       | String          | The name of the Zap, if any, otherwise `null`.        |
| **url**         | String          | An absolute url to the Zap (to edit).                 |

```json
{
  "id": 125,
  "modified_at": "2017-03-22T09:38:11-05:00",
  "state": "on",
  "steps": [{ "See Step object definition ..." }],
  "title": "Create Trello cards from new Typeform entries",
  "url": "https://zapier.com/app/editor/125"
}

```

## Zap Step

| attribute   | type   | notes                                                                      |
| ----------- | ------ | -------------------------------------------------------------------------- |
| **type_of** | String | One of `'read'`, `'write'`, `'filter'`, `'search'`, or `'search_or_write'` |
| **app**     | App    | The app for the step. See [App object](#app).                              |

```json
{
  "app": {
    /* See the App object definition ... */
  },
  "type_of": "read"
}
```

## Zap Template

| attribute             | type       | notes                                                                                                                         |
| --------------------- | ---------- | ----------------------------------------------------------------------------------------------------------------------------- |
| **create_url**        | String     | An absolute URL used to create the Zap.                                                                                       |
| **description**       | String     | The HTML-rendered description provided when the Zap template was created.                                                     |
| **description_plain** | String     | Plain text (HTML tags stripped) description. **Note: `\r` and `\n` replaced with space character. Artifacts may be present.** |
| **description_raw**   | String     | The [Markdown][markdown] description provided when the Zap template was created.                                              |
| **slug**              | String     | A URL/SEO friendly ID for the Zap template.                                                                                   |
| **steps**             | Array<App> | An array of two or more steps in the Zap template. See [Zap step object](#zap-step).                                          |
| **title**             | String     | The name of the Zap template.                                                                                                 |
| **status**            | String     | The status of the Zap template (choices: `draft`, `published`).                                                               |
| **url**               | String     | An absolute url to the Zapbook Zap template Page.                                                                             |

```json
{
  "create_url": "https://zapier.com/app/editor/template/10127?utm_campaign=Zap%20Templates%20Partners%20API&embedded=true&referrer=FacebookLeadsAPI&utm_source=partners&utm_medium=api&selected_apis=FacebookLeadsAPI,MailchimpCLIAPI@1.0.10",
  "description": "<p>Facebook Lead Ads are an...",
  "description_plain": "Facebook Lead Ads ... ",
  "description_raw": "**Facebook Lead Ads** are an ...",
  "slug": "subscribe-new-facebook-lead-ads-mailchimp-list",
  "status": "published",
  "steps": [
    {
      /* ... see App object definition ... */
    }
  ],
  "title": "Subscribe new Facebook Lead Ad leads to a MailChimp list",
  "url": "https://zapier.com/apps/inside-sales-box/integrations/zoho-crm/12084/add-new-leads-created-in-inside-sales-box-to-zoho-crm"
}
```
