---
title: Changelog
order: 3
layout: post
redirect_from: /partner_api/
---

# Changelog

## 2021-06-01
[DEPRECATION] After July 5, 2021, the endpoint `v1/zap-template/me` will no longer exist.

## 2021-05-13

### Added attributes to existing endpoint payloads

The endpoint `/v1/apps` exposes the `uuid` attribute for each app that is returned. This attribute is a UUID v4 string.

The endpoint `/v1/zap-templates` exposes the `label` attribute to each step. A `null` placeholder value is used if the label is unable to be resolved.

### Updated example endpoint payloads

The example payloads for endpoints `/v1/apps` and `/v1/zap-templates` have been updated to reflect these new attributes.

## 2021-01-14

### Introducing rate limiting

The endpoints are now rate limit protected. The limit is set to 9,000 requests per hour for an individual endpoint.

## 2018-05-31

### New `/apps` endpoint

This is a new endpoint that returns a list of apps in Zapier's App Directory.

## 2018-03-19

### Updated `/zap-templates` and `/zap-templates/me`

These endpoints now accept an `offset` parameter to support pagination through results.

## 2018-02-12

### Faster `/zap-templates` lookup.

Sub-second responses to the `/v1/zap-templates` even when requesting up to 100 Zap templates.

## 2017-11-01

### Access tokens never expire.

After security review, the access tokens granted **will no longer expire**. This may change in the future, however, based on endpoints provided by the API. In that event, we expect API consumers to provide the user with the authorize endpoint to get a fresh access token.

## 2017-10-16

###  `/zaps`

The endpoint will now return **all** Zaps regardless of the [Zapier CLI App's version](https://github.com/zapier/zapier-platform-cli) that was used when creating the Zap.
