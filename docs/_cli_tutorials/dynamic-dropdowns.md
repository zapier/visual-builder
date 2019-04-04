---
title: How to Use Dynamic Dropdowns in Zapier CLI
order: 1
layout: post-toc
redirect_from: /cli-tutorials/
---

# How to Use Dynamic Dropdowns in Zapier CLI  

[![CLI Dynamic Dropdowns Walkthrough](https://zappy.zapier.com/B851677F-070F-4B11-8EA4-E305F04B90AA.png)](https://zapier.wistia.com/medias/q9u484vkoc\)

## What are Dynamic Dropdowns?
Sometimes, API endpoints require clients to specify a parent object in order to create or access the child resources. For instance, specifying a spreadsheet id in order to retrieve its worksheets. Since people don't speak in auto-incremented ID's, it is necessary that Zapier offer a simple way to select that parent using human readable handles.

Our solution is to present users a dropdown that is populated by making a live API call to fetch a list of parent objects. We call these special dropdowns "dynamic dropdowns."  

![screenshot of dynamic dropdown in Zap Editor](https://cdn.zapier.com/storage/photos/dd31fa761e0cf9d0abc9b50438f95210.png)  

A full guide on how to implement dynamic dropdowns in your app can be found in our [CLI Docs](https://github.com/zapier/zapier-platform-cli#dynamic-dropdowns).
