---
title: Use computed fields in OAuth or Session Authentication
order: 8
layout: post-toc
redirect_from: 
---

# Use computed fields in OAuth or Session Authentication

When adding a field in your integration's authentication configuration, Zapier offers two field type options; field and computed field. The field option allows users to enter account information needed for authentication.

The computed field option stores values returned by your integration's authentication response which you can then reference in subsequent API calls. You must maintain the same field key as your API uses for this field. 

The computed field option only supports session and OAuth v2 authentication. 

## Prerequisites

- Understanding of [Platform UI authentication configuration](https://platform.zapier.com/build/auth) 
- Familiarity with your API's authentication 

## Steps

1. Log into the [Platform UI](https://zapier.com/app/developer).
2. Select your **integration**. 
3. In the _Build_ section in the left sidebar, click your **authentication**.  
4. Click **Save**.
5. Click **Add Fields**.
6. Under *Field Type*, select **Computed Fields**.
7. Select the **Is this field required? Check if yes** checkbox. Zapier use your computed fields in the response data. This means that any omission of the fields marked as computed fields in the authentication response would cause Zapier to display an error.
8. Complete the rest of the relevant fields. Learn more in [Input Designer](https://platform.zapier.com/build/input-designer).
9. Click **Save**.
10. You can then reference the field in any subsequent API call from the input bundle. In [Code Mode](https://platform.zapier.com/build/code-mode), you replace `field` with your field key in this text {% raw %}`{{bundle.authData.field}}`{% endraw %}

![Code example shows how a computed field appears in the Zapier Platform](https://cdn.zappy.app/9ac5ede3a88928989a3f91590a611282.png)

