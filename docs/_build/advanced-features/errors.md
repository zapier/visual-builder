---
title: Add error response handling
order: 2
layout: post-toc
redirect_from: 
---

# Add error response handling

If your API returns responses with a status code above 400 that should not automatically throw an error then Zapier recommends enabling skipThrowForStatus. This feature allows you to create custom error handling script for status codes above 400. Note that 401 status codes will throw a `RefreshAuthError` [regardless](https://github.com/zapier/zapier-platform/blob/main/packages/cli/README.md#user-content-error-response-handling).

To enable `skipThrowForStatus`:


## 1. Enable skipThrowForStatus

- Log into the [Platform UI](https://zapier.com/app/developer).
- Select your **integration**. 
- In the _Build_ section in the left sidebar, click **Advanced**. 
- Click the **Settings** tab.
- Click the **On** toggle next to *Enable skipThrowForStatus*.
- Click **Save**.

## 2. Use Code Mode to add error handling script

You'll need to add error handling script to your authentication, triggers, actions that could encounter the error using [Code Mode](https://platform.zapier.com/build/code-mode). 

![code screenshot](https://cdn.zappy.app/9553266cb5a5ab7804d3f9ac1a9eed60.png)

```js
return z.request(options).then((response) => {
  if (response.status === 404) {
    throw new z.errors.Error(
      "Insert error message to user here",
      "InvalidData",
      404
    );
  }
  return response.json;
});
```

Learn more about [general error handling in Zapier](https://github.com/zapier/zapier-platform/blob/main/packages/cli/README.md#general-errors). 


