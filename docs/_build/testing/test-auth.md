---
title: Test authentication
order: 1
layout: post-toc
redirect_from: 
    - /quickstart/test-complete
    - /docs/testing
    - /build/test-integration
---

# Test authentication

Testing a user's authentication is crucially important, as it is later used to test subsequent trigger and action steps when built.

## Prerequisites

- Completed authentication configuration with your app's authentication scheme
- Set of valid user credentials for your app - recommended to use a new account specifically for testing so you don't clutter your core app account with testing data. 

## Steps

1. In the final _Test your Authentication_ step, enter user credentials
2. Select _Test Authentication_ to make the test API call you configured 
3. Successful authentication shows a green check and a _Request Successful_ message at the top of the dialog.

![Add testing account in Zapier visual builder](https://cdn.zappy.app/60ebf09a1442345cc5d86b44440eb11c.png)

4. The _Response_ tab shows the JSON data response from your API, with each field and its data listed. 
5. The _Bundle_ tab shows the data Zapier stores about your authentication. 
6. The _HTTP_ tab shows the full request details for each API call Zapier made during the test. 
7. The _Console_ tab shows any additional data your API calls logged in Zapier if you use custom code for any part of your authentication.
8. Check each tab to ensure the expected data came through - it is possible to have an unsuccessful API call come through as successful if your API returns a message without an HTTP error code. Check the Response to make sure it includes the data expected from this API call, and if anything is incorrect, check the HTTP tab to help diagnose where things went wrong.

![Check response from authentication in Zapier visual builder](https://cdn.zappy.app/dacbdf7561aa6d2a78e599f12b80a325.png)

9. Clean up and remove older testing accounts from your core Zapier account. Open your [Zapier _Connected Accounts_](https://zapier.com/app/connections) page, and find your app's name (you may need to use the search box or `CMD`+`F` (Mac) or `Ctrl`+`F` (PC)). Click the app name. Once on the app's connections page, identify the connection to remove and click the three dots, then _Delete_, and confirm the deletion. Repeat for each subsequent testing account you added to clean up your authentication list.

Then refresh your integration page in the Platform UI, and you'll only see the authentications that were not deleted.

![Example account with multiple test accounts](https://cdn.zappy.app/943cd7b0ee2ada32492c834157a2eccb.png)

![Remove authed accounts](https://cdn.zappy.app/b31f5c7f712c1a585e727b729248615a.png)