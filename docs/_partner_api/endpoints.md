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
  "total": 3649,
  "page": 2,
  "pages": 1825,
  "per_page": 2,
  "objects": [
    {
      "uuid": "ca83afc5-ee9a-470d-b577-e7f8fd555b67",
      "title": "Slack",
      "slug": "slack",
      "description": "Slack is a platform for team communication: everything in one place, instantly searchable, available wherever you go. Offering instant messaging, document sharing and knowledge search for modern teams.",
      "image": "https://zapier-images.imgix.net/storage/services/6cf3f5a461feadfba7abc93c4c395b33_2.png?auto=format%2Ccompress&ixlib=python-3.0.0&q=50",
      "url": "https://api.zapier.com/v1/embed/apps/google-ads/integrations/slack",
      "links": {
        "mutual:zap_templates": "https://api.zapier.com/v1/zap-templates?apps=slack"
      },
      "categories": [
        {
          "slug": "team-chat"
        }
      ],
      "images": {
        "url_16x16": "https://zapier-images.imgix.net/storage/services/6cf3f5a461feadfba7abc93c4c395b33_2.png?auto=format%2Ccompress&fit=crop&h=16&ixlib=python-3.0.0&q=50&w=16",
        "url_32x32": "https://zapier-images.imgix.net/storage/services/6cf3f5a461feadfba7abc93c4c395b33_2.png?auto=format%2Ccompress&fit=crop&h=32&ixlib=python-3.0.0&q=50&w=32",
        "url_64x64": "https://zapier-images.imgix.net/storage/services/6cf3f5a461feadfba7abc93c4c395b33_2.png?auto=format%2Ccompress&fit=crop&h=64&ixlib=python-3.0.0&q=50&w=64",
        "url_128x128": "https://zapier-images.imgix.net/storage/services/6cf3f5a461feadfba7abc93c4c395b33_2.png?auto=format%2Ccompress&fit=crop&h=128&ixlib=python-3.0.0&q=50&w=128"
      }
    },
    {
      "uuid": "d74234df-0045-436e-bd5b-ee577e74e6b8",
      "title": "Google Calendar",
      "slug": "google-calendar",
      "description": "Google Calendar lets you organize your schedule and share events with co-workers and friends. With Google's free online calendar, it's easy to keep track of your daily schedule.",
      "image": "https://zapier-images.imgix.net/storage/services/62c82a7958c6c29736f17d0495b6635c.png?auto=format%2Ccompress&ixlib=python-3.0.0&q=50",
      "url": "https://api.zapier.com/v1/embed/apps/google-ads/integrations/google-calendar",
      "links": {
        "mutual:zap_templates": "https://api.zapier.com/v1/zap-templates?apps=google-calendar"
      },
      "categories": [
        {
          "slug": "calendar"
        },
        {
          "slug": "google"
        }
      ],
      "images": {
        "url_16x16": "https://zapier-images.imgix.net/storage/services/62c82a7958c6c29736f17d0495b6635c.png?auto=format%2Ccompress&fit=crop&h=16&ixlib=python-3.0.0&q=50&w=16",
        "url_32x32": "https://zapier-images.imgix.net/storage/services/62c82a7958c6c29736f17d0495b6635c.png?auto=format%2Ccompress&fit=crop&h=32&ixlib=python-3.0.0&q=50&w=32",
        "url_64x64": "https://zapier-images.imgix.net/storage/services/62c82a7958c6c29736f17d0495b6635c.png?auto=format%2Ccompress&fit=crop&h=64&ixlib=python-3.0.0&q=50&w=64",
        "url_128x128": "https://zapier-images.imgix.net/storage/services/62c82a7958c6c29736f17d0495b6635c.png?auto=format%2Ccompress&fit=crop&h=128&ixlib=python-3.0.0&q=50&w=128"
      }
    }
  ],
  "prev_url": "https://api.zapier.com/v1/apps?per_page=2&page=1",
  "next_url": "https://api.zapier.com/v1/apps?per_page=2&page=3"
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
    "id": 51652,
    "steps": [
      {
        "id": 1,
        "title": "Google Ads",
        "slug": "google-ads",
        "description": "Google Ads (formerly Google AdWords) is an online advertising platform developed by Google, where advertisers pay to display brief advertisements, service offerings, product listings, video content, and generate mobile application installs within the Google ad network to web users.",
        "image": "https://zapier-images.imgix.net/storage/services/4058ec8b47ad751cbd39bd686cf4eab7.png?auto=format%2Ccompress&ixlib=python-3.0.0&q=50",
        "hex_color": "4285F4",
        "images": {
          "url_16x16": "https://zapier-images.imgix.net/storage/services/4058ec8b47ad751cbd39bd686cf4eab7.png?auto=format%2Ccompress&fit=crop&h=16&ixlib=python-3.0.0&q=50&w=16",
          "url_32x32": "https://zapier-images.imgix.net/storage/services/4058ec8b47ad751cbd39bd686cf4eab7.png?auto=format%2Ccompress&fit=crop&h=32&ixlib=python-3.0.0&q=50&w=32",
          "url_64x64": "https://zapier-images.imgix.net/storage/services/4058ec8b47ad751cbd39bd686cf4eab7.png?auto=format%2Ccompress&fit=crop&h=64&ixlib=python-3.0.0&q=50&w=64",
          "url_128x128": "https://zapier-images.imgix.net/storage/services/4058ec8b47ad751cbd39bd686cf4eab7.png?auto=format%2Ccompress&fit=crop&h=128&ixlib=python-3.0.0&q=50&w=128"
        },
        "api": "GoogleAdsCLIAPI@3.0.0",
        "url": "https://zapier.com/apps/google-ads/integrations?utm_medium=partner_api",
        "label": "New Campaign"
      },
      {
        "id": 2,
        "title": "Slack",
        "slug": "slack",
        "description": "Slack is a platform for team communication: everything in one place, instantly searchable, available wherever you go. Offering instant messaging, document sharing and knowledge search for modern teams.",
        "image": "https://zapier-images.imgix.net/storage/services/6cf3f5a461feadfba7abc93c4c395b33_2.png?auto=format%2Ccompress&ixlib=python-3.0.0&q=50",
        "hex_color": "510f4d",
        "images": {
          "url_16x16": "https://zapier-images.imgix.net/storage/services/6cf3f5a461feadfba7abc93c4c395b33_2.png?auto=format%2Ccompress&fit=crop&h=16&ixlib=python-3.0.0&q=50&w=16",
          "url_32x32": "https://zapier-images.imgix.net/storage/services/6cf3f5a461feadfba7abc93c4c395b33_2.png?auto=format%2Ccompress&fit=crop&h=32&ixlib=python-3.0.0&q=50&w=32",
          "url_64x64": "https://zapier-images.imgix.net/storage/services/6cf3f5a461feadfba7abc93c4c395b33_2.png?auto=format%2Ccompress&fit=crop&h=64&ixlib=python-3.0.0&q=50&w=64",
          "url_128x128": "https://zapier-images.imgix.net/storage/services/6cf3f5a461feadfba7abc93c4c395b33_2.png?auto=format%2Ccompress&fit=crop&h=128&ixlib=python-3.0.0&q=50&w=128"
        },
        "api": "SlackAPI",
        "url": "https://zapier.com/apps/slack/integrations?utm_medium=partner_api",
        "label": "Send Channel Message"
      }
    ],
    "title": "Send messages to Slack channels whenever new Google Ads campaigns launch",
    "slug": "send-messages-to-slack-channels-whenever-new-google-ads-campaigns-launch",
    "status": "published",
    "description_plain": "A new Google Ads campaign can mean the start of your next marketing push, but it can also mean the start of a ton of new sales and service workflows. Zapier gives you a head start on those projects by automatically posting a new message in Slack to a specific channel you choose. Give your teams the heads up they need before your new clients come rolling in!\n",
    "description_raw": "A new Google Ads campaign can mean the start of your next marketing push, but it can also mean the start of a ton of new sales and service workflows. Zapier gives you a head start on those projects by automatically posting a new message in Slack to a specific channel you choose. Give your teams the heads up they need before your new clients come rolling in!",
    "url": "https://zapier.com/apps/google-ads/integrations/slack/51652/send-messages-to-slack-channels-whenever-new-google-ads-campaigns-launch?utm_medium=partner_api",
    "description": "<p>A new Google Ads campaign can mean the start of your next marketing push, but it can also mean the start of a ton of new sales and service workflows. Zapier gives you a head start on those projects by automatically posting a new message in Slack to a specific channel you choose. Give your teams the heads up they need before your new clients come rolling in!</p>\n",
    "create_url": "https://api.zapier.com/v1/embed/google-ads/create/51652",
    "type": "guided_zap"
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
  "next": "https://api.zapier.com/v1/zaps?limit=2&offset=2",
  "previous": null,
  "count": 4,
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

## GET /v1/profiles/me

**Example Requests**

Get user information related to the given `access_token`

```bash
curl -H "Authorization: Bearer {token}" -L "https://api.zapier.com/v1/profiles/me"
```

**Example Response**

> Refer to the [Profile](#profile) reference for all the available fields.

```json
{
    "id": 88998899,
    "first_name": "Jacob",
    "last_name": "Corwin",
    "email": "jacob.corwin@gmail.com",
    "email_confirmed": true,
    "timezone": null,
    "full_name": "Jacob Corwin",
    "roles": [
        {
            "account_id": 998998998,
            "role": "owner"
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

## Profile

| attribute           | type            | notes                                                 |
| ------------------- | --------------- | ----------------------------------------------------- |
| **id**              | Number          | The ID of the User.                                   |
| **first_name**      | String          | User's first name.                                    |
| **last_name**       | String          | User's last name.                                     |
| **email**           | String          | User's email.                                         |
| **email_confirmed** | Boolean         | Says if the user confirmed the email to Zapier.       |
| **timezone**        | String          | User's timezone.                                      |
| **full_name**       | String          | User's full name                                      |
| **roles**           | List<Role>      | List of user's accounts with their respective roles   |

```json
{
    "id": 88998899,
    "first_name": "Jacob",
    "last_name": "Corwin",
    "email": "jacob.corwin@gmail.com",
    "email_confirmed": true,
    "timezone": null,
    "full_name": "Jacob Corwin",
    "roles": [{ "See Role object definition ..." }]
}
```

## Role

| attribute           | type            | notes                                                 |
| ------------------- | --------------- | ----------------------------------------------------- |
| **account_id**      | Number          | The ID of the User's account.                         |
| **role**            | String          | User's role (ex: owner, member)                               |

```json
{
    "account_id": 99998999,
    "role": "owner"
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
