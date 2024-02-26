---
title: Use hydration in Platform CLI
order: 5
layout: post-toc
redirect_from: 
    - /cli_tutorials/hydration
    - /build/hydration
---

# Use hydration in Platform CLI

## What is dehydration & hydration?

The best answer to this lives in our [CLI docs](https://github.com/zapier/zapier-platform/blob/main/packages/cli/README.md#dehydration):

>  Dehydration, and its counterpart hydration, is a tool that can lazily load data that might be otherwise expensive to retrieve aggressively.

From a developer's perspective, you only need to worry about dehydration—Zapier will cover the hydration side of things.

## When to use dehydration?

The two most common times you should use dehydration in a Zapier integration are when:

1. You need to retrieve extra information from an API (e.g. a resource's list endpoint only returns IDs, but content must be retrieved per ID)
2. You need to provide access to a file (or files)

## Why use dehydration?

The core reason is reducing load to your API in case #1 above, where Zapier could fetch a list of known IDs of resources every 1-15 minutes per Zap, instead of the full definition of each of those resources. Putting any secondary requests behind a dehydration pointer means the request is made only once, although a Zap might see the same records again and again based on its polling cycle.

Dehydration saves even more bandwidth with files. No polling trigger should return files without dehydration, because otherwise, your app will send that file to Zapier around 100-300 times per day. For file outputs, implementing dehydration means the file will only be accessed and downloaded when a later Zap step asks for it.

The second reason is time. Your integration gets [30 seconds to run its API calls and any additional code](https://platform.zapier.com/build/troubleshoot-trigger-timeouts#trigger-runs-in-a-zap) each time a Zap step runs before the step would time out. If you are running into that time limit, consider if work could be offloaded to dehydration and hydration.

## How to use dehydration?

Check out our [example "files" app](https://github.com/zapier/zapier-platform/tree/main/example-apps/files) for an example of file dehydration in action with a working Zapier demo integration. You can even initialize a Zapier app based on that repo by entering ``zapier init . --template=files`` in Terminal to see it in your local code editor.


## Hydration in action

Some key areas include `index.js`, `hydrators.js`, `triggers/newFile.js`, and `creates/uploadFile.js`.

When building your integration, you'll likely be retrieving file info from a remote server. Instead, this example integration hard codes file urls to demonstrate.

The `New File` Trigger returns those file urls. The method [`z.dehydrateFile`](https://github.com/zapier/zapier-platform/blob/master/packages/cli/README.md#zdehydratefilefunc-inputdata) is used to create a pointer to the `downloadFile` function.  In order to pass those files to other apps in actions, we reference `hydrators.downloadFile`, our hydrating function given a file url. 

If you look at the `hydrators.js` file, you can see the `downloadFile` function. `downloadFile` calls the method[`z.stashFile`](https://github.com/zapier/zapier-platform/blob/master/packages/cli/README.md#zstashfilebufferstringstream-knownlength-filename-contenttype) to return a URL file pointer. 

All of these will work together to lazily fetch the trigger data only when needed, avoiding API calls during polling or for reuse. 

The only Action for this app is to upload the file, given a `bundle.inputData.file`. 

### Setup

First, install the sample Zapier app `zapier init . --template=files` and `zapier push` it to Zapier. If you've not worked with the CLI before, start by checking out the [tutorial](https://platform.zapier.com/quickstart/cli-tutorial). 

![](https://cdn.zappy.app/c3e87ca1ba18ce915d23dedf055e61af.png)

![](https://cdn.zappy.app/914893706d089af76bb445b3d885908d.png)

Here's how the integration looks in [Zapier's developer dashboard](https://developer.zapier.com/). Add an optional icon to it if you like. 

![](https://cdn.zappy.app/13df6356d05b5bb3e4533666bbfcc680.png)

Next, we'll want to add a Zap. Open the [Zap editor](https://zapier.com/editor), and select your integration's trigger.

![](https://cdn.zappy.app/50a4c0399eef2728b1f3e2b67f7fb916.png)

Select continue - you'll notice this app has no authentication, as the file urls are accessible without it. Select `Test trigger` to see the three sample urls pulled in and hydrated pointer for each. 

![](https://cdn.zappy.app/c68b2539d72c6c72da2ba3c35c9cef8d.png)


Now let's add the `Upload File` action to the Zap. Normally, we wouldn't want a setup like this (trigger off of new file / create a new file), because it would result in a [Zap loop](https://help.zapier.com/hc/en-us/articles/8496232045453-Zap-is-stuck-in-a-loop). But this is just a test—and be sure to turn the Zap off shortly after it's turned on.

![](https://cdn.zappy.app/28ed4762db06d0dd95563a4480a8dc36.png)

![](https://cdn.zappy.app/dd56ad225973829fbdc9fa1bcec5a2da.png)

Above, you'll see the string that prompts Zapier to hydrate a file. When the Zap runner encounters a string like this, Zapier will call the defined hydration function with the proper arguments. 

After selecting `Test step`, you will see three new requests show in the `Monitoring` [tab of your integration](https://platform.zapier.com/build/test-monitoring):

![](https://cdn.zappy.app/97152cd0012be0e7c35385a4f4b3f50a.png)

The POST at the top was from the upload itself. The GET requests retrieve the file from the pointer provided by the trigger. 

Now the Zap is ready to be turned on! 

![](https://cdn.zappy.app/81cac4d9b52b6a76194d5af91949bfef.png)

In this example app integration, the trigger will not run automatically due to the hard coded file urls used for illustrative purposes. Once you replace the `fileURLs` in the trigger `perform`, with a request to your API that returns the triggering file, you'll be able to test this out fully.   
