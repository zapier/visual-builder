---
title: How to Use Hydration in Zapier CLI
order: 5
layout: post-toc
redirect_from: /cli-tutorials/
---

# How to Use Hydration in Zapier Platform CLI

## What is Dehydration & Hydration?

The best answer to this lives on our [CLI docs](https://platform.zapier.com/cli_docs/docs#dehydration):

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

Check out our example files app (https://github.com/zapier/zapier-platform-example-app-files) for an example of file dehydration in action with a working Zapier demo integration. You can even initialize a Zapier app based on that repo by entering ``zapier init . --template=files`` in Terminal.

Your code can use [z.dehydrate](https://platform.zapier.com/cli_docs/docs#zdehydratefunc-inputdata) and [z.dehydrateFile](https://platform.zapier.com/cli_docs/docs#zdehydratefilefunc-inputdata) to create a "pointer string" that will be "hydrated" during a Zap Run. More on [Dehydration](https://platform.zapier.com/cli_docs/docs#dehydration) and [File Dehydration](https://platform.zapier.com/cli_docs/docs#file-dehydration) can be found in our CLI Docs.
