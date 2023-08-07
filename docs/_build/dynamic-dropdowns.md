---
title: Use dynamic dropdowns in Platform CLI
order: 18
layout: post-toc
redirect_from: /cli_tutorials/dynamic-dropdowns
---

# Use dynamic dropdowns in Platform CLI 

<script src="https://fast.wistia.com/embed/medias/q9u484vkoc.jsonp" async></script><script src="https://fast.wistia.com/assets/external/E-v1.js" async></script><div class="wistia_responsive_padding" style="padding:56.25% 0 0 0;position:relative;"><div class="wistia_responsive_wrapper" style="height:100%;left:0;position:absolute;top:0;width:100%;"><div class="wistia_embed wistia_async_q9u484vkoc seo=false videoFoam=true" style="height:100%;position:relative;width:100%"><div class="wistia_swatch" style="height:100%;left:0;opacity:0;overflow:hidden;position:absolute;top:0;transition:opacity 200ms;width:100%;"><img src="https://fast.wistia.com/embed/medias/q9u484vkoc/swatch" style="filter:blur(5px);height:100%;object-fit:contain;width:100%;" alt="" onload="this.parentNode.style.opacity=1;" /></div></div></div></div>

## What are Dynamic Dropdowns?

API endpoints sometimes require clients to specify a parent object in order to create or access the child resources, for instance, specifying a spreadsheet ID in order to retrieve its worksheets. Since people don't speak in auto-incremented ID's, Zapier offers a simple way for users to select that parent object using human readable handles.

Zapier does that with a dropdown that is populated by making a live API call to fetch a list of parent objects. We call these special dropdowns "dynamic dropdowns."

![screenshot of dynamic dropdown in Zap Editor](https://cdn.zapier.com/storage/photos/dd31fa761e0cf9d0abc9b50438f95210.png)  

More details about implementing dynamic dropdowns in your integration can be found in our [CLI Docs](https://github.com/zapier/zapier-platform/blob/master/packages/cli/README.md#dynamic-dropdowns).
