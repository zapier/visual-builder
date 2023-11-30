---
title: Use hydration in Platform CLI
order: 5
layout: post-toc
redirect_from: /cli_tutorials/hydration
---

# Use hydration in Platform CLI

## What is Dehydration & Hydration?

The best answer to this lives on our [CLI docs](https://platform.zapier.com/reference/cli-docs#dehydration):

>  Dehydration, and its counterpart Hydration, is a tool that can lazily load data that might be otherwise expensive to retrieve aggressively.

From a developer's perspective, you only need to worry about dehydration—Zapier will cover the hydration side of things.

## When Should I Use Dehydration?

The two most common times you should use dehydration in a Zapier integration are when:

1. You need to retrieve extra information from an API (e.g. a resource's list endpoint only returns IDs, but content must be retrieved per ID)
2. You need to provide access to a file (or files)

## _Why_ Should I Use Dehydration?

Fair question! The core reason is that dehydration could save you bandwidth in case #1 above, where Zapier could fetch a list of known IDs of resources every 5-15 minutes, instead of the full definition of each of those resources. Dehydration saves even more bandwidth with files. In general, no polling trigger should return files without dehydration, because otherwise, your app will send that file to Zapier around 100-300 times per day.

The second reason is time. Your app's integration gets 30 seconds to run its API calls and any additional code each time a Zap step runs before Zapier pulls the plug. If you are running into that time limit, consider if work could be offloaded to dehydration and hydration.

## How Do I use Dehydration?

Check out our [example "files" app](https://github.com/zapier/zapier-platform/tree/master/example-apps/files) for an example of file dehydration in action with a working Zapier demo integration. You can even initialize a Zapier app based on that repo by entering ``zapier init . --template=files`` in Terminal.

***

# Example Setup (optional)

## The Server

We've got a very simple file server set up with Express in this [Github repository](https://github.com/codebycaleb/express-files-example). The whole thing fits in one (hopefully) easy-to-read file, `index.js`. Let's take a quick look at what the API offers:

* GET `/files` - list filenames for the directory (only filenames!)
* GET `/files/:name` - download the file with the given filename or return a 404 if it's not found
* GET `/files/:name/meta` - return file meta info (size, creation date, etc.)
* POST `/files` - upload a file 

The README in that repo offers installation instructions (the server can be up and running in 4 commands).

## The App

What would an example be without an example app? Check out [https://github.com/codebycaleb/zapier-hydration-example/](https://github.com/codebycaleb/zapier-hydration-example/) to see what is available to get started with. Some key areas include `index.js`, `hydrators.js`, `triggers/newFile.js`, and `creates/uploadFile.js`.

The sole Trigger for this app will check our server's `/files` endpoint every time the Zap runs. As you may recall, the `/files` endpoint only returns filenames, but we want to offer the extra meta info (and the file itself!) to Zaps so that they can be passed to other apps in Actions. To achieve this, we reference `hydrators.fileMeta`, our function for hydrating metadata given a filename.

The only Action for this app is to upload the file. This is nearly identical to the Action in the example files app, with the one difference being that we dehydrate the file in the response so it is available to future actions via `hydrators.downloadFile`. This wouldn't normally be necessary in a file upload action (after all, the file was already available to be uploaded initially, so it could be used again in a later step as well), but it's been added in for illustrative reasons.

One final area to look at in this app is the hydrators defined in `hydrators.js`. If you look at this file, you can see our two methods (`downloadFile` and `fileMeta`). One thing that might not be necessarily common is that `fileMeta` also calls `downloadFile` - this is for illustrative purposes too, to show it's possible. Whenever `fileMeta` is called (in the Trigger), it will create a pointer to the meta data and call `downloadFile`, which will create a pointer to the file itself. 

`downloadFile` calls the method[`z.stashFile`](https://github.com/zapier/zapier-platform/blob/master/packages/cli/README.md#zstashfilebufferstringstream-knownlength-filename-contenttype) to return a URL file pointer. `fileMeta` calls the method `[z.dehydrateFile](https://github.com/zapier/zapier-platform/blob/master/packages/cli/README.md#zdehydratefilefunc-inputdata)` to create a pointer to the `downloadFile` function. The `New File` Trigger calls the method `[z.dehydrate](https://github.com/zapier/zapier-platform/blob/master/packages/cli/README.md#zdehydratefunc-inputdata)`  to create a pointer to the `fileMeta` function. All of these will work together to lazily fetch data when needed!

# Hydration in Action

## Getting Started

First, install the sample Zapier app and push it to Zapier.

![](https://zappy.zapier.com/D1FDB653-A9B3-4C78-9739-B36E263FC396.png)

Here's how the integration looks in [Zapier's developer dashboard](https://zapier.com/app/developer/) after adding your app icon to it:

![](https://zappy.zapier.com/E834B7C3-46ED-48A8-B70C-D7AEA45BC432.png)

Back in Terminal, you also need to install and start up the Express app.

![](https://zappy.zapier.com/E494B908-65CE-4E54-B296-D745BAE5B983.png)

Finally, I've started up ngrok to forward traffic to my computer on the port the Express app is running on (`ngrok http 3000`). You could actually host the Express server if you want, but I'm going with ngrok for ease of use:

![](https://zappy.zapier.com/ABCEB99C-E530-454E-9C7E-4EB6BBF943EB.png)

I'm also going to take a tip from the output above and open the Web Interface ([http://127.0.0.1:4040](http://127.0.0.1:4040/)):

![](https://zappy.zapier.com/B7CB465F-EA89-4EFB-B175-CAA252D852CD.png)

Finally, I'm ready to add a Zap. Open the [Zap creator](https://zapier.com/app/editor/), and select your integration's trigger.

![](https://zappy.zapier.com/C0EC57F8-2011-4897-8DB4-2EE1745DF66D.png)

Then add your ngrok URL to the authentication screen.

![](https://zappy.zapier.com/B04C5076-40E6-4827-BFDF-826CD40E500F.png)

After connecting an account, you'll see the first requests come in via ngrok:

![](https://zappy.zapier.com/F9D1245F-901D-4341-94F3-3CA2BF8765A5.png)

Now, add a file to your `/files` directory. I'll do a small image (<1MB). Then go back to Zapier, and have it pull in sample data for the Zap:

![](https://zappy.zapier.com/C9834ECA-BED4-4487-B4A2-38AED0FF0FB0.png)

And now we've got more requests! There's two new ones: the `/files` endpoint was hit, as was the meta endpoint for the one file in there:

![](https://zappy.zapier.com/3CF58AEC-C7FD-4458-AB4E-88F6A2D462EA.png)

![](https://zappy.zapier.com/0E456BE7-16FC-4C66-8019-156AB909FFD0.png)

Exciting! Let's add the Upload File Action to the Zap. Normally, we wouldn't want a setup like this (trigger off of new file / create a new file), because it would result in a Zap loop! But this is just a test—and be sure to turn the Zap off shortly after it's turned on.

![](https://zappy.zapier.com/0D6B2551-EAFA-4124-B148-66545B2C9DF3.png)

![](https://zappy.zapier.com/042E4AC8-D00E-4821-AC0A-BDDF96327478.png)

Above, you'll see the string that prompts Zapier to hydrate a file. When the Zap runner encounters a string like this, Zapier will call the defined hydration function with the proper arguments. 

After pressing the “Send Test” button, three new requests will show in ngrok:

![](https://zappy.zapier.com/2A33D13E-D405-4034-B938-2AEC88148743.png)

The POST at the top was from the upload itself. The GET `/files` under it was an authentication check that actually came in before the GET to download the file itself (ngrok isn't great at sorting same-second events; it doesn't keep track of milliseconds, so same-second requests aren't really sorted). Whenever performing hydration, Zapier will *always* run an authentication test.

Now the Zap is ready to be turned on! 

![](https://zappy.zapier.com/C1C88FF3-4D66-4099-BC6D-CE16FCB8671B.png)

(one minor note from above - I've added a “Delay For” step to introduce a delay between the Zap Triggering and the Action taking place; you'll see why in the near future!)

After turning the Zap on, a new request to `/files` will come in to set up the deduplication baseline (i.e. anything returned in here shouldn't trigger the Zap if it's seen on a future poll). At this point, I'm going to clear my ngrok requests log for a clear view of what happens during Zap execution. I'm also going to add a new photo to the `/files` directory. And now... we wait!

## A Zap at Work

My Zap has fired! Here's a look:

![](https://zappy.zapier.com/3EDC0260-0465-42D3-99D2-95674C4CA388.png)

When the Trigger runs, it detects a new file, prompting the `fileMeta` function to be executed. This is a key difference between `z.dehydrate` and `z.dehydrateFile` – as soon as the Trigger ran, we hydrated the request for `fileMeta`; however, we won't hydrate the stored `downloadFile` until the moment it is needed. This is why I added the "Delay For" step previously - to highlight that we won't hydrate dehydrated information until needed.

A short while later, ngrok receives three new requests:

![](https://zappy.zapier.com/28C6F8FD-677C-4EA0-837B-E4FBBD36C776.png)

![](https://zappy.zapier.com/0F46EF11-B50F-4EE1-A8C7-FDC82A743407.png)

Now is the time that the `downloadFile` function was evaluated, and the file was downloaded (in order to be uploaded again!). One final point that you may notice is that `downloadFile` was only called once; we did not call it again after the upload, despite adding a dehydrated call to it. That's what's great about `z.dehydrateFile`, we only use it when necessary!
