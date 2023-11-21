---
title: Add required authentication field
order: 3
layout: post-toc
redirect_from: /manage/making-changes#adding-a-required-auth-field
---

# Add required authentication field

## Change scenario

You'd like to add, remove, or change an optional input field to be required in your current authentication schema. 

## Impact to users

This will cause a breaking change which will have the following significant effects to users:
- Existing connected accounts will not work: All existing connected accounts will no longer be functional with your integration until users re-authenticate manually.
- Manual updates are required for all Zaps: Zaps cannot be migrated due to a breaking change, users will have to edit each Zap individually before they can start running tasks again. For example, if a user has 20 Zaps set up with your integration, they will need to manually update each one of those Zaps.

## Best practices

- **Add the field as optional:** Use field [help text](https://platform.zapier.com/build/build/basicauth#1-build-an-input-form) and [custom error handling](https://github.com/zapier/zapier-platform/blob/main/packages/cli/README.md#error-handling) (if you're using our Code Mode or the CLI platform) to validate that the newly required field is provided, while keeping it set to optional. Also, consider using custom code to set the field’s default value in your API call if left blank.
- **Set a default value:** If possible, provide a default value for the required field that can be overwritten if necessary. This ensures that users who do not provide explicit values for these fields can continue to use your integration without issues.

For example in the case of updated API endpoints for geographical region or site domain, it is possible to account for an added **required** inputField with scripting to ensure existing authentications are backward compatible, allowing existing users to be migrated to the new version.

In this example code, the default URL for US region is updated when the user selects AU or CA when authenticating.

```
let baseURL = "theUsApiBaseUrl";
switch (authData.region) {
  case "AU":
    baseURL = "theAuApiBaseUrl";
    break;
  case "CA":
    //other regions can be easily supported by adding cases like this
    baseURL = "theCaApiBaseUrl";
    break;
  default:
    console.log("Legacy credentials are in use, defaulting to US Base URL.");
}
```