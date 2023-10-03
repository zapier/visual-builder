---
title: Use environment variables in your API call
order: 1
layout: post-toc
redirect_from: 
    - /docs/advanced
    - /docs/knownissues
    - build/advanced-features
---

# Use environment variables in your API call 

Integrations can define environment variables that are available when the app's code executes. They are useful when you have data like an OAuth client ID and secret that you don't want to commit to source control. Environment variables can also be used as a way to toggle between a staging and production environment during app development and this would be recommended instead of the use of an independent integration for staging purposes.

Environment variables are defined on a per-version basis. Much like in local development environments such as the one in the [Platform CLI](https://github.com/zapier/zapier-platform/blob/main/packages/cli/README.md#environment), environment variables store key and value pairs outside of your app’s API calls. Instead of hardcoding critical, secret values into your API authentication, trigger, and action calls, it’s best to add them as environment variables in your integration, then reference the environment variable in your API calls.

If using OAuth v2 Authentication, the client ID and client secret fields are reserved environment variables. You'll need to use custom variable names for any other variables. 


## 1. Add environment variables
![Add Zapier environment variables](https://cdn.zappy.app/52c80699c321084eaaf7b387c47bd438.png)

To add environment variables:
- Log into the [Platform UI](https://zapier.com/app/developer).
- Select your **integration**. 
- In the _Build_ section in the left sidebar, click **Advanced** . There you can add your environment variables including a key and a value for each. 
- Click **Add** to include additional environment variables, or click the `x` icon to remove variables if needed.
- Once you've completed adding a key and value, click **Save**.

## 2. Reference environment variables
![Use Zapier environment variable](https://cdn.zappy.app/226591ede97cbcde75481b38fa0cd64f.png)
_Use environment variables in Zapier’s API call forms or in custom code_

Use environment variables in any Zapier integration API call through the form's _Show Options_ link, selecting _Request Body_, _URL Params_ or _HTTP Headers_ as your API expects. Reference the environment variable you've configured under _Advanced_, in the form with the following text, replacing `YOUR_KEY` with your actual key:
{% raw %}`{{process.env.YOUR_KEY}}`{% endraw %}
Zapier will then replace that variable with the value for that key from your _Advanced_ settings and will use the correct value every time if you change it in the future.
You can also reference environment variables in custom code if you switch your API call to code mode.

## 3. Change Environment Variables
![Edit Zapier Environment Variables](https://cdn.zappy.app/2bbe32e1bcfd77c62a75fce5be6eb03a.png)
_You can change environment variable values, but not the original keys_

It is possible to change your environment variables in a new version of your integration, or when switching from dev to production endpoints for the release of your integration to the public. 

To change an environment variable:
1. Log into the [Platform UI](https://zapier.com/app/developer).
2. Select your **integration**. 
3. In the _Build_ section in the left sidebar, click **Advanced**.
4. Edit the text in the **Values** column with the new variable values. You cannot edit the _Key_. If you need to change a key and its value, first delete the old key, then add a new one instead.


