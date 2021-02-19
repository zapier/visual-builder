---
title: Maintaining your converted integration
order: 3
layout: post-toc
redirect_from: /conversion/
---

# Maintaining Your Integration on the New Platform

After you’ve completed the process, you’re ready to continue development on the new platform. If you’re coming from the legacy Web Builder tool, the new UI will be familiar, but with some important differences in how you manage your work.

Locating the current integration

On your [“My Integrations”](https://developer.zapier.com/) page, make sure you’re working on the copy of your integration in the “Integrations” section - _not_ the “Integrations Built with Legacy Web Builder” section.

![](https://cdn.zappy.app/50e1b6f3dfe56965ffce80cc7ad879cd.png)

## Versions

The most immediate and important difference you’ll notice is that the new platform introduces the concept of [versions](/docs/versions).  

In the legacy Web Builder, you’d make a clone of your project to make changes to your integration. In the new platform, the workflow is similar, but you can manage multiple versions of your app for a lot more control and flexibility.  

You might think of the top level of your integration as a thin container that describes your product and brand, including the title, logo, description of your app.  All partnership metrics and analytics will reference this "container".

Inside this container are versions.  Versions hold all the actual workings of your integration - triggers, actions, authentication configuration, etc.  You are free to make big changes from one version to another.  

## New management features: promotion, migration, deprecation

_To make a change to your integration._

- Create a new version by cloning an existing version in the versions section found in the left-hand navigation bar.
- Make your changes to the new version.  
- If you have invited testers they can create Zaps with this new version before anyone else has access to it.
- When you’re ready for the world to use your new version, promote it.  Promoting a version makes it the version new users will see when they make Zaps. 
- If you didn’t make breaking changes, migrate your users to the new version.  Unlike Web Builder, this doesn’t happen automatically. You can control when it happens.  A useful practice, when introducing non-trivial changes, is to migrate percentages of your users and watch for problems in your logs before migrating 100%.  
- If you made breaking changes, you can simply leave users using the older version, or deprecate the old version to force users to reconfigure their Zaps to accommodate your changes.

## About breaking changes

A breaking change happens when you need to change something that prevents us from being able to switch users' Zaps to the new version without their interaction.  Breaking changes include:

- Changing authentication
- Adding a new required field
- Removing a trigger/action/search
- Changing the key of a trigger/search/action or any inputField


## Deprecation

Deprecation is an extremely useful feature introduced in the new platform.  If you made a breaking change and can’t migrate users to your new version, you might choose, if necessary, to deprecate the older version.  This will automatically email users of the older version to let them know they need to revisit the Zap Editor and reconfigure their Zaps for your newer version.  On the deprecation date you set any remaining Zaps still using the deprecated version will be paused.  Zapier is a "set it and forget it" experience for users, so use this feature carefully weighing the impact to user experience.

> **To minimize user disruption, try to avoid too frequent breaking changes and deprecations.** 

![](https://cdn.zappy.app/567798b6c42e238d9d446763d5d9abbc.png)

![](https://cdn.zappy.app/673162702ac6f277b752624ee7dd8e88.png)



## Teams

In Web Builder, an integration had a single admin.  In the new platform, you can add your whole team as admins to collaborate on the development and maintenance of your integration.  No need to share logins.  It's helpful that each member of your team is added, so everyone can see the status of the integration and get notification emails when a user reports a bug or feature request for your integration through Zapier support.

You can also add 'subscribers'. Those folks will get emails about the integration's performance, but won't be allowed to edit the integration. 

![](https://cdn.zappy.app/a3f77d24190e718b6177efe3d7074736.png)

## Sharing

Have a set of users who will help you test your new integration versions prior to making them publicly available?  Go to the "Sharing" section of the UI and invite those users to give them access to versions of integration other than the public, "promoted" version. 

## Analytics

Check out how many Zaps are using each trigger & action, for each version of your integration.  We'll show you how many are enabled vs how many are paused.  

![](https://cdn.zappy.app/67ad08f295dde5fc914dd74fb7819c67.png)

We're looking to bring out lots more data and insights about your integration's performance and usage dynamics in the near future.

## Where’s my code?

Your converted project looks a little different than if you’d started it from scratch in the new platform, but should feel pretty familiar (apart from versioning).  One thing you may notice are sections where the configuration is a code block, and the code is simply calling `z.legacyScripting.run()`.  To make integrations written in the old environment run, without modification, in the new environment we 'wrapped' your custom code and API configuration, and created a runtime library that emulates the behavior of the old platform.  So each time you see this, you can recognize it as an artifact of this emulation - we're calling into the emulator to perform the operation we need using your original code and configuration.

Where you added custom code to override lifecycle methods in Web Builder, we've included that code in the "Advanced" section of the UI, in the "Legacy Web Builder" tab.  The `z.legacyScripting` will call these functions to drive your triggers, actions, and authentication transactions.  

![](https://cdn.zappy.app/79bb2a1ea31a301f286e07e209994dcd.png)




## Creating new triggers and actions

You'll be able to continue your development, creating new triggers and actions, in your converted Web Builder integration.  When you create a new trigger or action, the interface will look a little bit different than those triggers and actions that were converted over from the legacy platform.  It will look familiar to you.  The big difference is when configuring an HTTP API request, you'll have many more options to customize headers and parameters without having to write custom code.  And when you do need to use custom code, you'll do so in that trigger/actions's UI, rather than in a common script file.  We'll talk about differences in the scripting environment next.

## Differences when writing custom scripting code

The following applies when you're building _new_ triggers and actions, and working with custom scripting code.  These are the idioms of the way operations are executed on the new platform.  

_If you're making changes to the code in the Advanced > "Legacy Web Builder" section, the following statements do not apply.  That code is run in an "emulated" context and works just like the old environment._

**Code us scoped to the individual trigger or action**

When you're writing custom scripting code in the new platform the scope of that code is local to that trigger or action.  This makes it easier to understand when a request will be handled by custom code, or simply configuring a request for default request handling.  It also means you can't easily share code between different triggers and actions.  For that, have a look at moving to the Zapier CLI, which is geared toward teams, projects with custom code, projects that need 3rd party libraries, etc.  

![](https://cdn.zappy.app/27b0a08799b047fc9db1ed204d030377.gif)

>Pro Tip: A handy way to understand this is to have a look at the [schema](https://zapier.github.io/zapier-platform-schema/build/schema.html) of the integration definition you're building.  [Here](https://zapier.github.io/zapier-platform-schema/build/schema.html#basicpollingoperationschema) you'll see the structure of the definition of a polling trigger.  Notice that the `perform` field takes a request configuration object, or it simply takes a Javascript function.  The new builder UI reflects this.  When you configure an API interaction, you use the form UI to configure a request, or you use "Code Mode" to write a function to be called instead.

**No pre or post functions**

In Web Builder, you could write custom code that ran before the request was made, or after the request returned, or you could take over complete control of making the request and returning data to Zapier.  In the new platform, there is only the 'complete control' option.  Your request can implement a `perform` function that takes a bundle as input and is expected to return data when the request handling is completed.  

**Promise based API**

A big difference in the API of the new environment is that the request API is asynchronous, using promises rather than synchronous requests or callbacks.  For developers new to Javascript promises this can be a small stumbling block.  We recommend spending a few minutes getting familiar with how promises work in general.  The `z.request` library works very similarly to the promise-based Fetch API, so most articles and tutorials about that apply to working with custom code in Zapier's environment.  

- [Using promises (MDN)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Using_promises)
- [JavaScript Promises in Depth (Egghead.io)](https://egghead.io/courses/javascript-promises-in-depth)
- [Using Fetch (MDN)](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch)
- [A re-introduction to JavaScript (MDN)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/A_re-introduction_to_JavaScript)

**No libraries included**

The legacy Web Builder tool included several JavaScript libraries, such as Underscore and jQuery, in its context that you could use in your script code.  Those are no longer available when writing scripting code in the new platform's UI tool.  You'll be able to use any JavaScript feature of Node.js (version 12 at the time of this writing, possibly v14 by the time you're reading this), including its standard library with `z.require`.

If you need, or prefer to use, a 3rd party Javascript library you'll want to switch to the Zapier CLI where you can install modules from npm and reference them throughout your code.

**Structure and naming of the Bundle Object is different**

Field names and structure of the Bundle is slightly different between the legacy Web Builder and the new platform.  Please see the [Bundle docs](/cli_docs/docs#bundle-object) for details.

## The Zapier CLI

When we convert your Web Builder integration we make it available through our new web-based builder tool.  However, the new platform offers you two ways of developing and maintaining your Zapier integration.  In addition to the UI based tool, you may choose to use the Zapier Command Line Interface (CLI).  This is an SDK you install in your local development environments.  It allows you to build your integration solely in code.  This is the best option for professional developers, teams, projects with non-trivial amounts of custom code, and/or projects that require the use of 3rd party modules or advanced platform features.

It's easy to move your work to the CLI.  We provide a feature to "eject" your work to the CLI.  That code line will then need to be managed in the CLI from then on.  In other words, you can go from the UI to the CLI at any time, but not the other way around.  However, if you eject your project to the CLI and decide it's not for you, you can simply delete that integration version and go back to working in the UI, so there's no risk in trying it out.  You'll just lose any changes you made in the CLI version.

Some reasons to consider the Zapier CLI

- Access to all features of the Zapier Platform
- Ability to better optimize your code. Move shared logic into modules. Leverage middleware to centralize request & response processing.
- Easier team collaboration. You’ll manage your Zapier integration code in your own company's Git repo.
- Set up automated regression tests, to catch errors each time you push a change.
- If you wanted to fully remove references to the legacy environment the CLI gives you the power to do that.

More information on moving to the CLI [here](https://platform.zapier.com/docs/export)
