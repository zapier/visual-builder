---
title: Manage a legacy web builder integration in Platform UI
order: 10
layout: post-toc
redirect_from: 
    - /legacy/import
    - /legacy/docs
    - /legacy/dedupe
    - /legacy/example-apps
    - /legacy/app-checks-reference

---

# Manage a legacy web builder integration in Platform UI

Zapier's new Platform UI is the best way to build Zapier integrations online—and the only way to build new Zapier integrations from your browser. It's based on the same Zapier Platform as Zapier's CLI, so integrations can use the same features and are equally easy to maintain.

If you have existing integrations built with Zapier's legacy web builder, for now you can continue to maintain them using the same tools as before. Or, you can convert your integration to the new Zapier Platform UI to use our new input form editor and integration testing features to maintain your integration more efficiently.

## How to Maintain Converted Integrations in Zapier Platform UI

Once your Zapier Legacy Web Builder integration is converted to Zapier Platform UI, it will look nearly the same as a new integration built in Zapier Platform UI's visual builder. It will include every feature in new Zapier integrations, along with a few extra features to manage parts of your integration that were different in the Legacy Web Builder.

Many things in Zapier Platform UI are similar to the tools you've used in Zapier's Legacy Web Builder, only with a more modern design. You can build full integrations from our form-based editor, often without touching code. If you do need to use code for a custom API call, fetch custom fields, or to parse non-standard response data, you can add JavaScript code for each trigger or action in your app.

Here are some of the main things you'll notice in Zapier Platform UI:

### App Details

![Manage App Details](https://cdn.zappy.app/1dcf126db0ff36ee4182b42b07f2ee1c.png)

You can manage your app's branding in Zapier Platform UI from the gear icon beside your app's icon and name. There, you can add a new logo or Markdown-formatted description for your app, or change your app's name and capitalization if needed. You can also add a category for your app.

Some of the details may have not been entered in your original Zapier integration. If you change anything in your app branding, you will also need to fill in any additional required fields before clicking _Update_ to save the changes.

_→ Learn more about [Managing Your App Branding in Zapier Platform UI](https://platform.zapier.com/build/add)_

### Trigger and Action Details

![Zapier trigger and action details](https://cdn.zappy.app/2ae53853086711ad11436736bb5d007f.png)

The core details of your triggers and actions are easy to edit in an online form, much like a redesigned version of the editor you used in Zapier's legacy Web Builder. You will manage the core details in the first tab, add input fields in the second tab, then manage the API call and test it in the final tab.

Searches are now combined with Creates in our _Actions_ editor to simplify your Zapier integration, with _Create_ and _Search_ action types. You cannot change a create action to be a search action, or vise versa, but when you add a new action you can choose which type to add.

You can edit existing triggers and actions, or can add new ones to your integration as needed.

_→ Learn more in our [Trigger](https://platform.zapier.com/build/trigger), [Action](https://platform.zapier.com/build/actions), and [Search versus Create](https://platform.zapier.com/build/search-create-action) docs—though note that the API Configuration will be somewhat different for imported triggers._

### Input Designer

![Zapier Input Designer](https://cdn.zappy.app/4aafe32a9f88127b59a5cdfa3dea80c6.png)

One of the best new features in Zapier Platform UI is the Input Designer. Here, you can design the input fields of your Zapier triggers and actions in an online form builder, and preview how they will look inside Zapier. Imported integrations work the same as new integrations in the Input Designer, so you can update existing input fields, reorder them, or add new fields to your triggers and actions any time.

_→ Learn more about [how to use the new Zapier Input Designer](https://platform.zapier.com/build/input-designer)._

### Testing

![Testing in Zapier Platform UI](https://cdn.zappy.app/ccc6bacc29d43787beac2872096a339f.png)

Another Zapier Platform UI feature that will speed up your integration development is built-in testing. Inside the _API Configuration_ settings of your authentication, triggers, and actions, you can add an app account and test each option, then view the data Zapier sent to your app and received in the API call response. If something's wrong, you can then make changes and re-test without ever leaving the page.

_→ Learn more in our [Testing docs](https://platform.zapier.com/build/test-integration)._

### Integration Versions

![Versions in Zapier Platform UI](https://cdn.zappy.app/51c6524e9b5d731777fc2e35af2329e3.png)

The new Platform UI also includes versioning to build and test new versions of your integration without breaking the integration for existing users. That's a great way to rework older triggers and actions, or replace your authentication scheme if it changes. You can then slowly roll out the new version to test it with a subset of your users before making it the new default.

_→ Learn more in our [Versions docs](https://platform.zapier.com/manage/versions-ui)._

### Legacy API Configuration Settings

![Legacy API Configuration Settings](https://cdn.zappy.app/69285c90f9e37fc2803a06beb1395946.png)

Imported integrations' _API Configuration_ tab on authentication, triggers, and actions will appear slightly different from integrations (and new triggers or actions) built in Zapier Platform UI. In new integrations, each API field will let you set the API call settings in a form, or switch to [Code Mode](https://platform.zapier.com/build/code-mode) to add custom JavaScript code for that call and its response parsing.

In converted integrations, however, you will see static text fields for each API call URL. If you need to customize the API call or response bundle parsing, you will need to do so from the Legacy Scripting settings.


### Legacy Scripting

![Zapier Legacy Scripting](https://cdn.zappy.app/ff4188111f5b9c267d983aba6e636c77.png)

Zapier Legacy Web Builder let you customize your integration's authentication API calls, trigger and action setup, response data parsing, and more with our Scripting API. That tool is no longer available for new Zapier Platform UI integrations, replaced by [Code Mode](https://platform.zapier.com/build/code-mode) to customize each API call directly if needed. For imported integrations, though, you can continue to maintain your legacy code using the same Scripting API in Zapier Platform UI.

To edit code in an imported integration, open your integration's _Advanced_ settings, then click the _Legacy Web Builder_ tab. There you can edit code as before, this time in a redesigned editor that does not take up your full screen. Be sure to click _Save_ after editing your integration code, as Zapier does not auto-save changes.

_→ Find detailed documentation on how to edit your integration's code in [Zapier's Legacy Scripting docs](https://platform.zapier.com/legacy/scripting)._

## What is Not Included in Zapier Platform UI?

Zapier Platform UI includes most of the features you would expect from the Legacy Web Builder, along with new features to help better manage your integration. In converted integrations, you will see some additional features to manage existing authentication, triggers, and actions. If you add new triggers or actions to your integration, though, these features will not be available in the new items, including:

- **Scripting**: The Legacy Web Builder combined all code into one Scripting page that let you add custom code for authentication, triggers, actions, and response data parsing. You may continue to manage any existing code from your converted integration in the _Advanced → Legacy Web Builder_ settings. If you add new triggers or actions to your integration, though, use [Code Mode](https://platform.zapier.com/build/code-mode) to customize your API call or response bundle parsing.
- **Static Web Hooks**: Zapier Platform UI supports only REST hooks and Polling for Triggers. If your converted integration includes static rest hooks in a trigger, you may continue to maintain them in the new Platform UI. If you add new triggers, though, you will not be able to add them with static web hooks.
- **Custom Results Fields**: The Legacy Web Builder included an option in triggers and actions to make an API call that would fetch custom result field names. Zapier Platform UI does not include this option for new triggers and actions, though it does let you continue to use this option in converted, existing triggers and actions. If you add new triggers or actions to your integration and need to fetch custom results fields, you will need to add that to the trigger or action's API call in the code mode.
- **OAuth v1**: Zapier Platform UI does not support OAuth v1 for new integrations, and instead requires new integrations to use OAuth v2 authentication. You may continue to maintain existing OAuth v1 authentication in converted integrations, but if you make a new version of your integration or re-build it in Zapier Platform UI, you will need to use a newer authentication scheme.
- **Advanced Editor**: The Legacy Web Builder included an _Advanced Editor_ option to edit your integration in JSON text instead of the web UI editor. That feature is no longer available in Zapier Platform UI, for new or converted integrations. If you would prefer to manage your integration in JSON text and code, the better option would be to export your integration to Zapier Platform CLI to manage it from your local development environment. Once your app has been converted to the Platform UI, you will have the option of [exporting your app to the CLI](https://platform.zapier.com/manage/export-integration).
- **Files**: The Legacy Web Builder included some support for [file handling](https://platform.zapier.com/manage/legacy-scripting#files). The Platform UI does not include capabilities for working with files. To work with files in the new platform, [export your app to the CLI](https://platform.zapier.com/manage/export-integration) after it is converted.



