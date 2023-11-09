---
title: Compute a field from the data of the Test API call
order: 9
layout: post-toc
redirect_from: 
---

# Compute a field from the data of the Test API call

Zapier doesn’t store the responses from the test API call for OAuth v2 and session authentication. Using computed fields, you can use data from a test API call later in your Zapier integration.

## Prerequisites

- Knowledge of working with APIs
- Understanding of computed field concept
- Familiarity with JavaScript

## Steps

1. Log into the [Platform UI](https://zapier.com/app/developer).
2. Select your **integration**. 
3. In the _Build_ section in the left sidebar, click your **authentication**.
    -  For Session authentication: 
        -  Click **Configure a Token Exchange Request**
        - Click **Switch to Code Mode**.
    -  For OAuth v2 authentication: 
        -  Click **Add OAuth v2 Endpoint Configuration**. 
        - Click **Switch to Code Mode**.
4. Add **custom JavaScript code** to instruct Zapier to call both the URLs necessary for the authorization process and your test API call.
5. Click **Save & Continue**.
6. The *Test Request* section remains unchanged.
7. Return  [computed fields](https://github.com/zapier/zapier-platform/blob/main/packages/cli/README.md#computed-fields) for data returned from either API call so you can reference those fields in subsequent steps as `bundle.authData.field` where `field` is the field's name from your test API call response.

Upon completion, you will be able to use data from a test API call as a computed field in later stages of your Zapier integration. 