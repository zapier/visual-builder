---
title: Errors
order: 4
layout: post
redirect_from: /partner_api/
---

# Errors

Zapier uses HTTP response codes to indicate the success or failure of an API request.

| Code    | Status         | Explanation                                                     |
| ------- | -------------- | --------------------------------------------------------------- |
| **200** | OK             | Successful request.                                             |
| **400** | Bad Request    | Invalid request, or invalid parameters .                        |
| **403** | Authentication | Not authorized.                                                 |
| **404** | Not Found      | The resource requested was not found.                           |
| **5xx** | Server Error   | A fatal error occurred while processing the request. Try again. |

All errors will be JSON object with a String array of errors:

```json
{
  "errors": ["Malformed request"]
}
```
