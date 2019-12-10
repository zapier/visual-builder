---
title: Changelog
order: 2
layout: post
redirect_from: /partner_api/
---


|    Date    |                  Resource                  | Change                                                                                                                                                                                                                                                                          |
| :--------: | :----------------------------------------: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 2018-05-31 |                  `/apps`                   | This is a new endpoint that returns a list of apps in Zapier's App Directory.                                                                                                                                                                                                   |
| 2018-03-19 |  `/zap-templates` and `/zap-templates/me`  | These endpoints now accept an `offset` parameter to support pagination through results.                                                                                                                                                                                         |
| 2018-02-12 |        Faster Zap templates lookup.        | Sub-second responses to the `/v1/zap-templates` even when requesting up to 100 Zap templates.                                                                                                                                                                                   |
| 2017-11-01 | All endpoints with access token protection | After security review, the access tokens granted **will no longer expire**. This may change in the future, however, based on endpoints provided by the API. In that event, we expect API consumers to provide the user with the authorize endpoint to get a fresh access token. |
| 2017-10-16 |                  `/zaps`                   | The endpoint will now return **all** Zaps regardless of the [Zapier CLI App's version](https://github.com/zapier/zapier-platform-cli) that was used when creating the Zap.                                                                                                      |
