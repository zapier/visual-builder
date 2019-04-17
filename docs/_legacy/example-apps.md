---
title: Legacy Web Builder Example Integrations
order: 5
layout: post-toc
redirect_from: /legacy/
---

# Legacy Web Builder Example Integrations

> **Note**: These guides are for Zapier's legacy web builder. For new integrations, use our [Zapier Platform UI Quick Start guide](https://platform.zapier.com/quickstart/introduction) to learn how to build Zapier integrations.

To help you become acquainted with the Developer Platform, we provide a number of examples that walk you through the process of adding a new App. Each example is step-by-step instructions that, once completed, will give you a working App to experiment with.

***

## Bitbucket

  * Using Basic Auth.
  * Setting up a polling trigger, which is reused as the test trigger.

This example will walk you through creating a developer app that uses Basic Authentication and a has a single trigger that polls a web service for data. To make the example real, we'll be implementing the actual Bitbucket API.

### Quick Preparation Checklist

* You must have a [Zapier account](https://zapier.com/sign-up/).
* You must have a [Bitbucket account](https://bitbucket.org/).
* Read the [Zapier Legacy Web Builder Documentation](https://platform.zapier.com/legacy/docs/) to familiarize yourself with some of the terminology and basic components of an App.
* Read the [Bitbucket API Documentation](https://confluence.atlassian.com/bitbucket/use-the-bitbucket-cloud-rest-apis-222724129.html) to familiarize yourself with Bitbucket.

### Create an App

To get started, go to the [Developer Platform](https://zapier.com/developer/builder/) and click the "Create App" button. You'll be asked to give a title and a brief description.

![Create App screen](https://cdn.zapier.com/storage/photos/d01c839734c22673df0073d3612637a6.png)

After you submit, you should find yourself with a fresh App like this:

![Screenshot of empty dev app](https://cdn.zapier.com/storage/photos/3e53bb94f6062a409b9b8f2decb07931.png)

### Setting up authentication

We'll start by defining how Zapier should authenticate with Bitbucket. From the above screen, click the "Get Started" button in the authentication section.

![Get Started button](https://cdn.zapier.com/storage/photos/b33516a2c469757a0240f82fd68edc6b.png)

On Step 1 you will want to choose Basic Auth since that is what Bitbucket uses. You should then find yourself on Step 2 with some pre-generated authentication fields. These are the fields that users will be presented with when they add a Bitbucket account in Zapier.

![Screenshot of pre-generated authenticationfields](https://cdn.zapier.com/storage/photos/be965c015d9553cd7375359a6c6edf14.png)

The default fields are all that is needed for Bitbucket, so  click next to go to the final step. Here, we define how the fields we collect from users should map to parameters used in the actual API call. Since this is Basic Auth, we will define username and password keys in the auth mapping. Our fields are conveniently called username and password as well, so all we need is this:

![Screenshot of auth mapping](https://cdn.zapier.com/storage/photos/06c76198c34a45010f2397bbf8b88ae6.png)

*Note: the &#123;&#123;username&#125;&#125; is our [variable syntax](https://platform.zapier.com/legacy/docs#variable-syntax), which says take whatever value the user put in the username authentication field and make it be the username in the Basic Auth call.*

At this point, we have the authentication setup and are ready to make our first trigger.

### Fetching data from Bitbucket using polling

The trigger we are going to build will watch Bitbucket for new repositories being added to a user's account. Generally, the first trigger you add to an App should be for an API endpoint that requires authentication and is guaranteed to always return some data. This allows Zapier to verify that the authentication credentials a user provides are valid (we make an actual API call to check).

From your App, click the "Add your first test trigger" button.

![Create trigger button](https://cdn.zapier.com/storage/photos/e63bd6a12406ef571f227e3af4c8030b.png)

The first form you see allows you to define some of the user-facing details of the trigger.

![Step 1 of adding a trigger](https://cdn.zapier.com/storage/photos/f2b8b851fc0dc931d1d5370f074f15ae.png)

Click next to proceed to Step 2, Trigger Fields. Trigger fields add extra information for the trigger which you can use in the URL or in Scripting. We're actually going to skip over this step because our New Repository trigger does not require any additional info. Hit next to get to Step 3, where we define how our trigger will fetch data from Bitbucket.

Bitbucket provides an API endpoint that lists the repositories in a user's account. For Zapier to keep up-to-date, we are going to poll this endpoint at a regular interval to check for new repositories. Here is what we will fill out:

![Step 3 of trigger editor](https://cdn.zapier.com/storage/photos/1bb12c951e8e2870c8b14140e75b1dd3.png)

Click save to proceed to Step 4. In this step, we will copy and paste an example of what the Bitbucket API returns. This is not strictly necessary, but it helps users setup their Zaps when they do not have any repositories available to sample. The data can be found by making a raw request with your favorite HTTP client, or using Bitbucket's [API Browser](http://restbrowser.bitbucket.org/).

![Step 4 sample data](https://cdn.zapier.com/storage/photos/b86355cddc5f9da041e4c6287cdf4d21.png)

When you click "Parse" you will be presented with a slew of form fields, one for each JSON key in the sample. These forms allow you to override the default name Zapier will give each key. For instance, Zapier will automatically turn the key "utc_last_updated" into "Utc Last Updated", but you might want to rename it to just "Last Updated". For now, we will skip this step and click "Save".

At this point, we have defined our first trigger and are ready to test it out!

### Testing what we have built

Now that we have built out the basics of our app, it is time to try it out and see if it works. Go to your [dashboard](https://zapier.com/app/dashboard) and click the create a zap button. On Step 1 of the Zap Editor, you should now have our Bitbucket Example app. The app should have a single trigger, New Repository.

![Your Dev App on Step 1 of Zap Editor](https://cdn.zapier.com/storage/photos/e94e92d34c5c6a7f9ba60aa1184635b7.png)

After you select the trigger and any action (the Zapier Delay is a good one to test with), Step 2 will ask you to add your Bitbucket account.

![Step 2 of Zap Editor](https://cdn.zapier.com/storage/photos/259d54122e3e235b48abee139aa258ba.png)

When you click the button, you will get this form:

![Screenshot of authentication fields from Zap Editor](https://cdn.zapier.com/storage/photos/76c614ad7c1cb76e35b8b6168dcc28d7.png)

As you can see, the form contains the two authentication fields we set up, plus another one that Zapier adds so the user can name the account. Fill out the form and click continue. At this point, Zapier will make an API call the repositories endpoint. If everything is setup correctly (and you have at least one repository in your Bitbucket account), you should get a success message and the account should be added:

![Example of successfully adding a Bitbucket account](https://cdn.zapier.com/storage/photos/9afc4f6b280fae1203eec710b86ce284.png)

If you like, you can continue to fill out the Zap. Down at Step 6, when you click the test button, you should see some samples load up that match repositories in your account. At this point, we know our trigger is working.

**Congratulations!** You have a working Bitbucket application that:

* Uses Basic Auth.
* One polling trigger (reused for testing).

Be sure to check out our other examples for more details on doing other interesting things with Zapier's developer platform!

***

## Pivotal Tracker

  * Using API Key authentication, where the token goes in an HTTP header.
  * Setting up a dedicated test trigger (one that is not shown to Zapier users).
  * Setting up an action.

This example will walk you through creating a Developer App that uses an API Key and has a single action that adds a record to a web service. To make the example real, we'll be implementing the Pivotal Tracker API.

### Quick Preparation Checklist

If you plan to follow along, it is recommended you set up everything beforehand and keep these resources open and ready for quick access.

* You must have a [Zapier account](https://zapier.com/sign-up/).
* You must have a [Pivotal Tracker account](http://www.pivotaltracker.com/).
* Read the [Zapier Legacy Web Builder Documentation](https://platform.zapier.com/legacy/docs/) to familiarize yourself with some of the terminology and basic components of an App.
* Read the [Pivotal Tracker API Documentation](https://www.pivotaltracker.com/help/api/rest/v5) to familiarize yourself with Pivotal Tracker.

### Create the App

To get started, go to the [Developer Platform](https://zapier.com/developer/builder/) and click the "Create App" button. You'll be asked to give a title and a brief description.

![Create App screen](https://cdn.zapier.com/storage/photos/acdf94babb83ea522e0fce6517be969a.png)

After you submit, you should find yourself with a fresh App like this:

![Screenshot of empty dev app](https://cdn.zapier.com/storage/photos/9da91be7ada9d51e64485261a020c906.png)

### Setting up authentication

We'll start by defining how Zapier should authenticate with Pivotal Tracker. From the above screen, click the "Get Started" button in the authentication section.

![Get Started button](https://cdn.zapier.com/storage/photos/b33516a2c469757a0240f82fd68edc6b.png)

On Step 1 you will want to choose API Key since that is what Pivotal Tracker uses. You also need to specify where Pivotal Tracker expects the API key to be included in the requests. Their docs tell us the HTTP headers, so select that. Later on, we'll discover the significance of this choice.

![Selecting API Key with Headers](https://cdn.zapier.com/storage/photos/d0af43a797c8c255a067df19d4cebf94.png)

You should then find yourself on Step 2 with a pre-generated authentication field. This is the field that users will be presented with when they add a Pivotal Tracker account to Zapier.

![Screenshot of generated authentication field](https://cdn.zapier.com/storage/photos/9b1ed3cd26f9f6e76a01d7f34fb4242e.png)

The default field is all that is needed for Pivotal Tracker, so click next to go to the final step. Here, we define how the key we collect from users should be used in the actual API calls. Pivotal Tracker's docs say the key needs to be provided as an HTTP header called "X-TrackerToken." We will define our auth mapping like this:

![Example of auth mapping](https://cdn.zapier.com/storage/photos/2a653262320b7342993fdb7d0d2b65fc.png)

This mapping, combined with our choice of headers in Step 1, tells Zapier to take whatever value a user provides in the api_key authentication field and include it as the X-TrackerToken HTTP header. Requests we make will automatically have the header included!

*Note: To find out more about the &#123;&#123;api_key&#125;&#125;, check out our [variable syntax docs](https://platform.zapier.com/legacy/docs#variable-syntax/).*

At this point, we have the authentication setup and are ready to make our test trigger.

### Setting up a test trigger

In order to verify the API keys users provide, we need to build a test trigger. The test trigger is simply an API call to an endpoint that requires authentication and is guaranteed to always return some data. This allows Zapier to verify that an API key a user provides is valid. For Pivotal Tracker, we'll use the /me endpoint as the test call.

From your App, click the "Add your first test trigger" button.

![Create trigger button](https://cdn.zapier.com/storage/photos/e63bd6a12406ef571f227e3af4c8030b.png)

The first form you see allows you to define some of the meta information about the trigger. Since this is a test trigger that will not be useful beyond verifying API tokens, we can put something short and leave the "Hide" checkbox checked.

![Step 1 of adding a trigger](https://cdn.zapier.com/storage/photos/628fecaff192b1886902faa0b75c51d0.png)

Click next to proceed to Step 2, Trigger Fields. Trigger fields add extra information for the trigger which you can use in the URL or in Scripting. We're actually going to skip over this step because our trigger does not require any additional info. Hit next to get to Step 3, where we define how our trigger will fetch data from Pivotal Tracker.

As mentioned before, Pivotal Tracker provides an API endpoint that returns basic information on a user's account. To configure Zapier to hit this endpoint, here is what we will fill out:

![Step 3 of adding a trigger](https://cdn.zapier.com/storage/photos/83871544cddd40a28e9aaaec43ca0ef3.png)

Click save to proceed to Step 4. Typically in this step you would copy and paste an example JSON representation of an account into the text area. Since this test trigger will be hidden from actual use in the Zapier UI, we'll skip this step, so just click save.

At this point, we have defined our test trigger and are ready to try it out!

### Testing what we have built so far (authentication)

Now is a good time to go and see if we have the authentication field and test trigger setup properly. To test them, you can go to your [connected accounts](https://zapier.com/app/settings/authorizations) and click the connect account dropdown.

![Connect account dropdown](https://cdn.zapier.com/storage/photos/f237f99ce91ed61535221b6fd31a2985.png)

After you select the Pivotal Tracker Example App, you will get this form:

![Screenshot of authentication field](https://cdn.zapier.com/storage/photos/b9131ec8fe1f7a8163ad718c44bc62c8.png)

As you can see, the form contains the authentication field we set up, plus another one that Zapier adds so the user can name the account. Fill out the form and click continue. At this point, Zapier will make an API call the /me endpoint. If everything is setup correctly, you should get a success message and the account should be added:

![Example of successfully adding a Pivotal Tracker account](https://cdn.zapier.com/storage/photos/722007a79fb5fe36f9e3fe0454169acd.png)

Now that we have working authentication, we are ready to create our first action.

### Creating an action

The action we are going to build will allow users to create new projects. From your App, click the "Add your first Action" button.
![Add action button](https://cdn.zapier.com/storage/photos/dfda776c25009d6b859e1d1200e6d720.png)

The first screen allows us to provide the user-facing details of the action.

![Step 1 of action editor](https://cdn.zapier.com/storage/photos/884f1ba53fa374682d0f1410b899c3a3.png)

After filling it out, click next to proceed to Step 2. Here, we define action fields. These are the fields that make up a project in Pivotal Tracker. Users fill these out to say what data should go into their new projects.

A project in Pivotal Tracker has many available fields. We are going to use three: name, description, and public. To start, click the add action Field button.

![Add action field button](https://cdn.zapier.com/storage/photos/cae07084b33dd6c8e3562f1e6d2e7124.png)

Fill it out like so:

![Adding Name Action Field](https://cdn.zapier.com/storage/photos/1f31768211369b4698edd8c6aac4a68c.png)

You should now see your action field.

![Action Field](https://cdn.zapier.com/storage/photos/f2718463f5c3af26be767e13d83d9328.png)

Use the same process for description, except do not mark it as required. For public, the setup is a little different because it is a boolean field in Pivotal Tracker. You can set it up like this:

![Adding Public Action Field](https://cdn.zapier.com/storage/photos/7bcc0fb481b6c9d76a39cc8b7c708c9b.png)

When you are all done, you should have three action fields:

![Action fields](https://cdn.zapier.com/storage/photos/887e2c61dd499bb6b534ccde2de0b8ee.png)

Click next to move on to the final step. The last piece to complete our action is to tell Zapier where to POST the data.

![Step 3 of action editor](https://cdn.zapier.com/storage/photos/8db0b6bb4b66480aca62e516725c1d26.png)

Click save and we are done. At this point, we have an action that we are ready to test.

### Testing the action

Now that we have built out the basics of our App, it is time to try it out and see if it works. Go to your dashboard and click the create a zap button. On Step 1 of the Zap Editor, you should now have the Pivotal Tracker Example App. The App should have a single action, Create Project.

![Step 1 Zap Editor](https://cdn.zapier.com/storage/photos/0f0926bb3ddbd564204d74db64a3dd85.png)

For the trigger, you could try anything you like. An easy one to test with is the Zapier New Service trigger.

Step 2 will ask you to add your Zapier account. Step 3 should pre-populate with your Pivotal Tracker account that you added during earlier when we tested our authentication. If it is not there, you can add your Pivotal Tracker account now. You can click through on Step 4.

Now in Step 5 we get to see our handy-work. You will see that there are three form fields, one for each of the action fields we made. Fill them out and continue.

![Step 5 of Zap Editor](https://cdn.zapier.com/storage/photos/91ff0a44dec38911cb723c57f92f2355.png)

In Step 6, we get a chance to send some requests and see if our action works. Load some samples and click Test on one of them.

![Step 6 Zap Editor](https://cdn.zapier.com/storage/photos/cf7c0bf199298b972dc0ce11dcb9297c.png)

You should now be able to login to Pivotal Tracker and see the new project.

![Project in Pivotal Tracker](https://cdn.zapier.com/storage/photos/35c1ef9ebc2eb286d60602d1a97920aa.png)

**Congratulations!** You have a working Pivotal Tracker application that:

* Uses an API key to authenticate.
* One polling trigger to test authentication credentials.
* One action.

Be sure to check out our other examples for more details on doing other interesting things with Zapier's developer platform!

***

## Formstack

  * Using OAuth V2.
  * Setting up a REST Hook trigger.
  * Using [Scripting](https://platform.zapier.com/legacy/scripting) to customize subscription process.

This example will walk you through creating a developer app that uses [REST Hooks](http://resthooks.org/) for a trigger that subscribes and unsubscribes a callback and waits for the data to come in. To make the example real, we'll be implementing the actual **Formstack** API. Let's get started!

### Quick Preparation Checklist

If you plan to follow along, it is recommended you set up everything beforehand and keep these resources open and ready for quick access.

* You must have a [Zapier account](https://zapier.com/sign-up/).
* You must have a [Formstack account](https://www.formstack.com/) and are ready to create a [Formstack Developer App](http://developers.formstack.com/).
* Read the [Zapier Legacy Web Builder Documentation](https://platform.zapier.com/legacy/docs/) to familiarize yourself with some of the terminology and basic components of an App.
* Learn a bit about what [REST Hooks](http://resthooks.org/) are and how they are different from polling.
* Read the [Formstack API Documentation](https://developers.formstack.com/v2.0/) to familiarize yourself with Formstack.
* Read our [OAuth Documentation](https://platform.zapier.com/legacy/docs#oauth-v2) for more details.

### Getting Started

To get started, go to the [Developer Platform](https://zapier.com/developer/builder/) and click the "Create App" button. You'll be asked to give a title and a brief description. After you submit, you should find yourself with a fresh app:

![https://cdn.zapier.com/storage/photos/dd43208410e0ffe3f4edc2b316bdb4a4.png](https://cdn.zapier.com/storage/photos/dd43208410e0ffe3f4edc2b316bdb4a4.png)

Next, you'll need to complete all the required steps to authenticate with OAuthV2! You can read a more [detailed OAuth V2 guide here](https://zapier.com/developer/documentation/v2/oauth-v2/), but we'll cover the basics here. First, you'll need to create your [developer app in Formstack](https://www.formstack.com/admin/applications/add):

![https://cdn.zapier.com/storage/photos/57ac50c03e310c2daa5a4aae0cbd0006.png](https://cdn.zapier.com/storage/photos/57ac50c03e310c2daa5a4aae0cbd0006.png)

To get your redirect URI, don't forget to set up your authentication settings, if you click the below button you can start an automated walkthrough that will help you get the basics set up:

![https://cdn.zapier.com/storage/photos/b33516a2c469757a0240f82fd68edc6b.png](https://cdn.zapier.com/storage/photos/b33516a2c469757a0240f82fd68edc6b.png)

And at the very end of that walkthrough, you will be able to input the information given to you from Formstack for your specific developer app:

![https://cdn.zapier.com/storage/photos/cb2f685b45250306c6ea1884f50a5251.png](https://cdn.zapier.com/storage/photos/cb2f685b45250306c6ea1884f50a5251.png)

### First Trigger and Test Trigger

Next up we'll want to **create our triggers**.  For this Formstack example, we're going to create two triggers which will be closely intertwined!

* **New Form**, will poll a JSON API to return a list of forms. We'll reuse this as the test trigger as well.
* **New Entry**, will subscribe/unsubscribe a webhook to get notifications of new entries for a form.

The first trigger will test our authentication mechanism. The first trigger you create will be a test by default, we have a handy button to get started:

![https://cdn.zapier.com/storage/photos/e63bd6a12406ef571f227e3af4c8030b.png](https://cdn.zapier.com/storage/photos/e63bd6a12406ef571f227e3af4c8030b.png)

Which will bring you to the basic details form about the trigger you are creating. Let's create the Form trigger, it is worth reviewing the [Formstack Developer Documentation on the GET /forms endpoint](https://developers.formstack.com/docs/form-get) which we'll be using to power the trigger.

![https://cdn.zapier.com/storage/photos/f5198e46d4edbb2d3b9e1179b98f8037.png](https://cdn.zapier.com/storage/photos/f5198e46d4edbb2d3b9e1179b98f8037.png)

Since we don't need any other information to make this trigger tick, we can skip trigger fields. Trigger fields just add extra information for the trigger which you can use in the URL or in scripting. Our next trigger will use Trigger fields, so just skip for now!

![https://cdn.zapier.com/storage/photos/7259817ddda8c022e98b0dca7fbe3ac3.png](https://cdn.zapier.com/storage/photos/7259817ddda8c022e98b0dca7fbe3ac3.png)

Since we know the URL to retrieve the list of Forms from the [Formstack Documentation](https://developers.formstack.com/docs/form-get), it is as simple as pasting `https://www.formstack.com/api/v2/form.json` directly into the Polling URL. You can skip the custom fields here, they are very rare for triggers!

![https://cdn.zapier.com/storage/photos/bf2bed43c66d1ce9c9bb6b3e65e92cff.png](https://cdn.zapier.com/storage/photos/bf2bed43c66d1ce9c9bb6b3e65e92cff.png)

> You have everything you need to actually use your app, so now is a great time to test your app! Since all developer apps are available immediately on your account you can just visit your [editor](https://zapier.com/app/editor) and use your app just like any other app Zapier supports!

### REST Hook Trigger

Now it's time for the main attraction! This is what this example is building up to, but first we need to collect a little information about the REST Hook or webhook subscription we can create. For that we'll turn to the [general Formstack documentation for webhooks](https://developers.formstack.com/docs/webhook-setup) and [Formstack's documented webhook endpoints](https://developers.formstack.com/docs/webhooks).

Here are the pieces we'll need in this step:

* The subscribe URL which looks something like `{% raw %}https://www.formstack.com/api/v2/form/{% templatetag openvariable %}form_id{% templatetag closevariable %}/webhook.json{% endraw %}`
* The **un**subscribe URL which looks something like `{% raw %}https://www.formstack.com/api/v2/webhook/{% templatetag openvariable %}webhook_id{% templatetag closevariable %}.json{% endraw %}`

First thing is first, we'll we'll need to set those subscription URLs up at the app level, you should see a button to manage your trigger settings.

![https://cdn.zapier.com/storage/photos/05cf36ab31fe5fd8639d12045ade3681.png](https://cdn.zapier.com/storage/photos/05cf36ab31fe5fd8639d12045ade3681.png)

Go ahead and paste the above URLs into the form and save the settings:

![https://cdn.zapier.com/storage/photos/79c5156f041d75e23805bf83eea6a1dc.png](https://cdn.zapier.com/storage/photos/79c5156f041d75e23805bf83eea6a1dc.png)

Next up is the big event: let's create the trigger that will use those subscription URLs! Click your add trigger button and fill out the basic information like so:

![https://cdn.zapier.com/storage/photos/75d6597a700ca86889104c60be35e518.png](https://cdn.zapier.com/storage/photos/75d6597a700ca86889104c60be35e518.png)

Now comes trigger fields, as you recall, in order to make set up the webhook subscription we need a `form_id`, luckily Zapier has some tools that makes it easy to make dynamic dropdown's that are powered by other triggers. It just so happens we've already made a trigger for this called "New Form". Let's just show you and recap after!

![https://cdn.zapier.com/storage/photos/646c14a2bd081273c84f14a2d96b2e35.png](https://cdn.zapier.com/storage/photos/646c14a2bd081273c84f14a2d96b2e35.png)

![https://cdn.zapier.com/storage/photos/1b3d49f33560cd96b98437c0db9f626f.png](https://cdn.zapier.com/storage/photos/1b3d49f33560cd96b98437c0db9f626f.png)

There are a few things going on, but the two most important are "Key" and "Dynamic Dropdown"

* Make sure to reuse the Key `form_id` from the subscribe URL when making the trigger field. This pattern is fairly common and Zapier will stitch them together for you.
* For the Dynamic Dropdown, there are three parts separated by a `.`:
  * `trigger_key` which references which trigger by key you'd like to us.
  * `field_id` which key from each object is the one we're interested (in this case it is the form_**id** we want).
  * `field_name` which key from object is the nice human readable version (in this case it is just **name**).

Both `field_id` and `field_name` are plucked from the JSON response that we get, for example, in this screenshot for the editor:

![https://cdn.zapier.com/storage/photos/04a15f4e2145d492f15124ba4adcf6a0.png](https://cdn.zapier.com/storage/photos/04a15f4e2145d492f15124ba4adcf6a0.png)

The left values are the `name` and the right values are the `id`. When a user selects an item, we'll display the `name` but store the `id` as well for use later in URLs!

Next up is actually telling this trigger to use REST Hooks and our subscription URLs as the way it grabs data, you can do this on the next step after saving your Trigger Field:

![https://cdn.zapier.com/storage/photos/21a4386bbfbfbeae76553a1c8f4175c6.png](https://cdn.zapier.com/storage/photos/21a4386bbfbfbeae76553a1c8f4175c6.png)

You *can* provide an optional polling URL or sample data with REST Hooks, but Zapier will handle the subscription process for you when the user needs some sample data. If either of those two options are available, we'll try and use them.

Next up is making sure that the request we send to Formstack for subscribe and unsubscribe are correct. That means we'll need to use our scripting feature to write some custom code to modify the requests before we send them. Just use the "Edit Code" button to start!

![https://cdn.zapier.com/storage/photos/ce5b8e75871cc50e8cb9d00f395b9c39.png](https://cdn.zapier.com/storage/photos/ce5b8e75871cc50e8cb9d00f395b9c39.png)

The three methods we'll need to use are:

* `pre_subscribe` - ensure the request to subscribe matches what Formstack expects.
* `post_subscribe` - ensure Zapier can store the data to identify the webhook.
* `pre_unsubscribe` - ensure Zapier can unsubscribe from the identified webhook.

Again, we are going to reference the Formstack documentation for [creating](https://developers.formstack.com/docs/form-id-webhook-post) and [removing](https://developers.formstack.com/docs/webhook-id-delete) webhooks to understand the format needed for both `pre_` calls. Check out the code snippet below for a better understanding:

{% highlight javascript %}
{% raw %}
var Zap = {
    pre_subscribe: function(bundle) {
        bundle.request.method = 'POST';
        bundle.request.headers['Content-Type'] = 'application/x-www-form-urlencoded';
        bundle.request.data = $.param({
            url: bundle.subscription_url,
            append_data: 1
        });
        return bundle.request;
    },
    post_subscribe: function(bundle) {
        // must return a json serializable object for use in pre_unsubscribe
        data = z.JSON.parse(bundle.response.content);
        // we need this in order to build the {% templatetag openvariable %}webhook_id{% templatetag closevariable %}
        // in the rest hook unsubscribe url
        return {webhook_id: data.id};
    },
    pre_unsubscribe: function(bundle) {
        bundle.request.method = 'DELETE';
        bundle.request.data = null;
        return bundle.request;
    },
};
{% endraw %}
{% endhighlight %}

Now, you are ready to hop back to the [Editor](https://zapier.com/app/dashboard) and test the trigger properly! If you check out the "Test this Step" section and click the continue button, you should see a spinner that appears as we perform the **subscribe** step:

![subscribing a webhook](https://cdn.zapier.com/storage/photos/8238c73634dfb64e8b077befc57c306a.png)

If you click out of the "Test this Step" section (say on "Edit Options"), we'll perform the **unsubscribe** step for you. Now you can go back to your developer app, check out the request logs and see the `POST` and `DELETE` requests corresponding to the popup.

![https://cdn.zapier.com/storage/photos/715bdc12d4ae72b0af14636923037d16.png](https://cdn.zapier.com/storage/photos/715bdc12d4ae72b0af14636923037d16.png)

*Note! This is the exact same process that will happen when a zap is turned on or off!*

Now that you've gotten the subscription process down, we need to actually **catch some data from the webhook**! The process is very simple:

1. Go back to the Editor.
2. Get the spinner going again on Test this Step.
3. Submit the chosen form in Formstack.
4. Wait. Don't click away

You should see something like this once we catch the data:

![successfully catching webhook](https://cdn.zapier.com/storage/photos/61bd201caa979808f0d37efac70aa019.png)

And if you click the resulting example you should see the data that we caught!

![example data](https://cdn.zapier.com/storage/photos/36d674c4a9d7dcc9bebb423a4b2c1966.png)

You can use the `catch_hook` scripting method to further cleanup data (like the name and address fields that are lumped together), but that is outside the scope of this tutorial. Also, you can view your HTTP logs in your developer app for more logs on hooks in addition to normal HTTP.

**Congratulations!** You have a working Formstack application that:

* Uses OAuth V2.
* One polling trigger (reused for testing).
* One REST Hooks trigger.
* Scripting or custom code around subscribe/unsubscribe calls.

Be sure to check out our other examples for more details on doing other interesting things with Zapier's developer platform!

***

## Mad Mimi

  * Using API key authentication, where the token is part of the query string.
  * Setting up a trigger that has a dynamic dropdown.
  * Setting up an action.
  * Using [Scripting](https://platform.zapier.com/legacy/scripting) to interact with an API that speaks XML.

This example app with showcase a simple usage of scripting to parse XML. The rest of the example is pretty straightforward and might be applicable to other APIs even if they don't use XML. To make this example even more real world, we'll be implementing a real API for a real service called **Mad Mimi**!

### Quick Preparation Checklist

If you plan to follow along, it is recommended you set up everything beforehand and keep these resources open and ready for quick access.

* You must have a [Zapier account](https://zapier.com/sign-up/).
* You must have a [Mad Mimi account](https://madmimi.com/).
* Read the the [Mad Mimi developer platform](https://madmimi.com/developer).
* Learn a bit about our [Scripting](https://platform.zapier.com/legacy/scripting/) facilities, we'll need that to parse XML.

### Getting Started

The first thing you'll want to do is create the app you'll be working on, this is probably the simplest thing of all! Just go to your developer apps and click the "Create App" button and enter the information.

![https://cdn.zapier.com/storage/photos/5be654bc411ab0fcd7905faeb8e51d14.png](https://cdn.zapier.com/storage/photos/5be654bc411ab0fcd7905faeb8e51d14.png)

### Authentication

The first thing to do is describe how the API authenticates, you can click the **Get Started** button after you create your app to do that.

![https://cdn.zapier.com/storage/photos/b33516a2c469757a0240f82fd68edc6b.png](https://cdn.zapier.com/storage/photos/b33516a2c469757a0240f82fd68edc6b.png)

If your browse the [Mad Mimi developer docs](https://madmimi.com/developer) you'll notice they place their authentication bits in the querystring of a URL like so: `{% raw %}?username={% templatetag openvariable %}username{% templatetag closevariable %}&api_key={% templatetag openvariable %}api_key{% templatetag closevariable %}{% endraw %}`. Luckily Zapier supports **API Key Querystring** authentication natively!

![https://cdn.zapier.com/storage/photos/344629ea9b18ae7c6b347ad5b6d6abe2.png](https://cdn.zapier.com/storage/photos/344629ea9b18ae7c6b347ad5b6d6abe2.png)

After you choose **API Key** and **Querystring**, you'll have the option to add more Authentication fields in addition the the most basic version which is just a field for `api_key` which we'll add for you by default:

![https://cdn.zapier.com/storage/photos/50a0a8b6711b6752bcb4f45075e63ee2.png](https://cdn.zapier.com/storage/photos/50a0a8b6711b6752bcb4f45075e63ee2.png)

Since Mad Mimi requires the `username` in addition to `api_key` we can very easily **Add Authentication Field** for the username portion as will (which Mad Mimi sometimes refers to as email as well). You'll need to fill it out similar to this:

![https://cdn.zapier.com/storage/photos/9a58e9e300ac492f919834ad5fb4c74d.png](https://cdn.zapier.com/storage/photos/9a58e9e300ac492f919834ad5fb4c74d.png)

After you save, we'll show you both fields that we'll present to the user to fill out: both `username` and `api_key`.

![https://cdn.zapier.com/storage/photos/47ff914863f02d7bcdaf32c95d467220.png](https://cdn.zapier.com/storage/photos/47ff914863f02d7bcdaf32c95d467220.png)

Finally, you'll need to define the mapping: that is where we take the user provided authentication values and place them into the querystring using a simple JSON mapping:

![https://cdn.zapier.com/storage/photos/5d3f10ad0b1711d74769896c90cd51f1.png](https://cdn.zapier.com/storage/photos/5d3f10ad0b1711d74769896c90cd51f1.png)

In case it the above screenshot is hard to read or you need some copy pasta, here are the values in the raw for the auth mapping:

{% highlight javascript %}
{% raw %}

    "username": "{% templatetag openvariable %}username{% templatetag closevariable %}",
    "api_key": "{% templatetag openvariable %}api_key{% templatetag closevariable %}"
}
{% endraw %}
{% endhighlight %}

### Your First Trigger

Now, authentication should be finished! The next piece is to create a test trigger that uses that authentication to confirm that it all works. It isn't uncommon to repurpose a normal trigger as a test trigger, so let's do that! The trigger we'll add is one that enumerates a new *Audience List* and you can read about in the [Mad Mimi Audience List API documentation](https://madmimi.com/developer/lists), let's get hopping, just click to create your first trigger:

![https://cdn.zapier.com/storage/photos/e64b8bb61974202d21dbbadcbc230dba.png](https://cdn.zapier.com/storage/photos/e64b8bb61974202d21dbbadcbc230dba.png)

After you input the trigger basics (be sure to uncheck "hide" since you are making a normal trigger at the same time), you'll have the option to create trigger fields. Since the endpoint in question doesn't need anything in addition to the standard username and api_key which Zapier will place for you automatically, so you can just skip this step:

![https://cdn.zapier.com/storage/photos/4b37703b8fb3efd4027bc99fb576fc4f.png](https://cdn.zapier.com/storage/photos/4b37703b8fb3efd4027bc99fb576fc4f.png)

The last bit for this trigger is placing the API URL we need to hit to get an array of audience lists, again, you can get that from [Mad Mimi Audience List API documentation](https://madmimi.com/developer/lists), it looks something like `http://api.madmimi.com/audience_lists/lists.xml`, just paste it in the right spot!

![https://cdn.zapier.com/storage/photos/8a015e11ffb7d0ddf2fafc05b748dd28.png](https://cdn.zapier.com/storage/photos/8a015e11ffb7d0ddf2fafc05b748dd28.png)

The only piece we're missing is the XML parsing via our javascript scripting feature, but before we attempt to write that it's time to go test the app on the [editor](https://zapier.com/app/editor).

> All developer apps are available immediately on your account, you can just visit your [editor](https://zapier.com/app/editor) and use your app just like any other app Zapier supports!

Just select your app, and continue through the editor:

![https://cdn.zapier.com/storage/photos/ed0e33fca1a04c9672ce0103bad5156a.png](https://cdn.zapier.com/storage/photos/ed0e33fca1a04c9672ce0103bad5156a.png)

And add your authentication in the second step:

![https://cdn.zapier.com/storage/photos/9188d7f6ad72f808c4d90b1535eed5f3.png](https://cdn.zapier.com/storage/photos/9188d7f6ad72f808c4d90b1535eed5f3.png)

Since all we care about is the `200` response, the test passes fine! However, we're still getting XML that we can't quite understand, you can view the HTTP logs back in the developer app overview to get an idea of what it looks like:

![https://cdn.zapier.com/storage/photos/d79c8adbe50a747b260e6038461d0d67.png](https://cdn.zapier.com/storage/photos/d79c8adbe50a747b260e6038461d0d67.png)

And if you view the details you should see the content we got back in the response:

![https://cdn.zapier.com/storage/photos/6b9e341f9bb0c5b68df0295df2dcc16b.png](https://cdn.zapier.com/storage/photos/6b9e341f9bb0c5b68df0295df2dcc16b.png)

### Scripting Your First Trigger

Now its time to load up the code editor! Since we called the trigger `audience_list`, we can write a `audience_list_post_poll` method to handle the otherwise successful response and convert the XML to JSON. To get started, just open up the code editor:

![https://cdn.zapier.com/storage/photos/047cef3c846cda5c46e6056cb7d10fca.png](https://cdn.zapier.com/storage/photos/047cef3c846cda5c46e6056cb7d10fca.png)

The input, code and output that works for this example is this:

#### Input

{% highlight xml %}
{% raw %}
<?xml version="1.0" encoding="UTF-8"?>
<lists>
  <list subscriber_count="0" display_name="" name="My Test List" id="933748"/>
</lists>
{% endraw %}
{% endhighlight %}

#### Code

{% highlight javascript %}
{% raw %}
Zap = {
	audience_list_post_poll: function(bundle) {
        // use the provided dom methods with a familiar jquery interface
        var xmlElements = $($.parseXML(bundle.response.content)).find('list');
        // return a list of objects that are json serializable
        return _.map(xmlElements, function(listElement) {
            listElement = $(listElement);
            // pull off each attribute manually, place into object
            return {
                id: 				listElement.attr('id'),
                subscriber_count: 	listElement.attr('subscriber_count'),
                display_name: 		listElement.attr('display_name'),
                name: 				listElement.attr('name'),
            };
        });
	},
};
{% endraw %}
{% endhighlight %}

#### Output

{% highlight json %}
{% raw %}
[
    {
        "name": "My Test List",
        "display_name": "",
        "id": "933748",
        "subscriber_count": "0"
    }
]
{% endraw %}
{% endhighlight %}

If you want to check out more examples for `post_poll` methods check out our [scripting documentation](https://platform.zapier.com/legacy/scripting/#trigger-post-poll-examples).

That's it for your first trigger that lives a double life as a test trigger (and will power a dynamic dropdown very shortly!). Keep reading, let's wrap up this app!

### Your First Action

The primary action we'll want to create is one that can add an audience member to a list. Of course, we'll need to provide the `list` and `email` address at minimum (which an option to expand to more fields if you like). Take a quick look at the [Add audience member list in the Mad Mimi docs](https://madmimi.com/developer/lists/add-membership) to get your bearings, and let's jump straight in!

![https://cdn.zapier.com/storage/photos/71f185dce57d59d530246db8d0ab0dd4.png](https://cdn.zapier.com/storage/photos/71f185dce57d59d530246db8d0ab0dd4.png)

This first thing is to define a bit of the basic information about the action, like below:

![https://cdn.zapier.com/storage/photos/0f04990ac536b310571ff9e6cc5a20b6.png](https://cdn.zapier.com/storage/photos/0f04990ac536b310571ff9e6cc5a20b6.png)

Next is time for action fields! You should see a screen like this:

![https://cdn.zapier.com/storage/photos/6033537bed7856447d47625362ac357f.png](https://cdn.zapier.com/storage/photos/6033537bed7856447d47625362ac357f.png)

Your goal is to get it looking more like:

![https://cdn.zapier.com/storage/photos/7ed43b565a4281a860ecb65a36a23602.png](https://cdn.zapier.com/storage/photos/7ed43b565a4281a860ecb65a36a23602.png)

You can do that by adding new action fields, be sure to define the dynamic dropdown source as `audience_list.id.name` to reference the trigger we made earlier. That will create a dropdown that a user can easily use to power their apps. For example:

![https://cdn.zapier.com/storage/photos/ffb2c892bebff26a588a84e7fd563b24.png](https://cdn.zapier.com/storage/photos/ffb2c892bebff26a588a84e7fd563b24.png)

When you create the email action field, be sure to check the "Send In JSON" option, you'll see why when we revisit your scripts in just a moment.

Now your action fields should look something like this:

![https://cdn.zapier.com/storage/photos/7ed43b565a4281a860ecb65a36a23602.png](https://cdn.zapier.com/storage/photos/7ed43b565a4281a860ecb65a36a23602.png)

The last step is letting us know where we should `POST` the data to! The URL should look something like `{% raw %} http://api.madmimi.com/audience_lists/{% templatetag openvariable %}audience_list{% templatetag closevariable %}/add{% endraw %}`. Note, the `audience_list` variable in the URL: that is referencing the dynamic dropdown action field. In the interface, the URL should be be placed in this location:

![https://cdn.zapier.com/storage/photos/cee53c671f37b6c9dd4dfb5c7282f78a.png](https://cdn.zapier.com/storage/photos/cee53c671f37b6c9dd4dfb5c7282f78a.png)

And that's it for the action definition, next up we need to convert our default `application/json` encoding into `application/x-www-form-urlencoded`, the "Send In JSON" option decides what we serialize by default, but you can always build even more complex structures from the `bundle.action_fields` object if you need to. We're just keeping it simple!

#### Default Input

{% highlight text %}
{% raw %}
{"email":"hello@world.com"}
{% endraw %}
{% endhighlight %}

#### Code

{% highlight javascript %}
{% raw %}
Zap = {
    // place other methods from earlier code here!

    audience_member_pre_write: function(bundle) {
        bundle.request.data = $.param(z.JSON.parse(bundle.request.data));
        bundle.request.headers['Content-Type'] = 'application/x-www-form-urlencoded';
        return bundle.request;
    }
};
{% endraw %}
{% endhighlight %}

#### Corrected Output

{% highlight text %}
{% raw %}
email=hello%40world.com
{% endraw %}
{% endhighlight %}

Alrighty, that wraps up all the work we need to do to make this action work. You are welcome to expand action fields out past `email` by including `first_name`, `last_name`, `country`, `state`, etc. However, we're going to leave this example as simple as possible!

### Test it out!

If you go back to your [editor](https://zapier.com/app/dashboard) and do a full page refresh, you should be able to select Mad Mimi and Add Audience Member as the action. As you scroll down to the mapping step, you should see something like:

![https://cdn.zapier.com/storage/photos/9f4fff60410c8f2f13d0490c10afba9e.png](https://cdn.zapier.com/storage/photos/9f4fff60410c8f2f13d0490c10afba9e.png)

Depending on what you use as the trigger, in the test step you can load some samples and send the sample across the wire to Mad Mimi and the action you just created:

![https://cdn.zapier.com/storage/photos/4c9cdcf00084bcfd66b051edac671f42.png](https://cdn.zapier.com/storage/photos/4c9cdcf00084bcfd66b051edac671f42.png)

After you complete that, go back to your developer app and view the HTTP requests to ensure that the request got sent:

![https://cdn.zapier.com/storage/photos/914e43ecde53831d2ab83e4bef7f720c.png](https://cdn.zapier.com/storage/photos/914e43ecde53831d2ab83e4bef7f720c.png)

And its also a good idea to login to Mad Mimi and ensure you see the email there too!

![https://cdn.zapier.com/storage/photos/b8201e364ce60bf211930a0a84271e24.png](https://cdn.zapier.com/storage/photos/b8201e364ce60bf211930a0a84271e24.png)

With that, I give you a well-earned **congratulations!** You've created an example application with a mix of XML and form encoded payloads that uses API keys, scripting, and dynamic dropdowns!

***

## HubSpot

  * Setting up a static webhook trigger.
  * Providing a good sample result and user-friendly field names.

This example will walk you through creating a developer app that uses a static webhook to receive data from a web app. To make the example real, we'll be implementing the actual Hubspot API.

### Quick Preparation Checklist

* You must have a [Zapier account](https://zapier.com/sign-up/).
* You must have a [Hubspot](http://www.hubspot.com/) account.
* Read the [Zapier Legacy Web Builder Documentation](https://platform.zapier.com/legacy/docs/) to familiarize yourself with some of the terminology and basic components of an App.
* Glance at the [Hubspot API Documentation](http://developers.hubspot.com/docs/endpoints) to familiarize yourself with Hubspot.

### Create an App

To get started, go to the [Developer Platform](https://zapier.com/developer/builder/) and click the "Create App" button. You'll be asked to give a title and a brief description.

![Create App screen](https://cdn.zapier.com/storage/photos/c8e36bb6e2f0d3ec6ab5f7ddfc01a8fb.png)

After you submit, you should find yourself with a fresh App like this:

![Screenshot of empty dev app](https://cdn.zapier.com/storage/photos/22fe17ddc140f73f223adcf580e63b83.png)

### Setting up authentication

Normally, the first step in building an app is to define how Zapier will authenticate with your app. For static webhooks, however, the data exchange is one-way, your app making requests to Zapier. As a result, credentials are not needed from the users.

For this example, we will skip this step. If we later wanted to add actions or triggeres that were not static webhooks, we would need to come back and complete this section.

### Setting up a trigger

The trigger we are going to add for Hubspot will use webhooks to listen for new contacts. From your App, click the "Add your first test trigger" button.

![Create trigger button](https://cdn.zapier.com/storage/photos/e63bd6a12406ef571f227e3af4c8030b.png)

The first form you see allows you to define some of the user-facing details of the trigger.

![Step 1 of adding a trigger](https://cdn.zapier.com/storage/photos/544399ec30b373866b829a514ca5aa8c.png)

Click next to proceed to Step 2, Trigger Fields. Trigger fields add extra information for the trigger which you can use in the URL or in Scripting. We're actually going to skip over this step because our trigger does not require any additional info. Hit next to get to Step 3, where we define how our trigger will receive data from Hubspot.

With a static webhook, the user gives your app a URL that you can send notifications to. Zapier automatically generates the URL for the user. All you need to do is  write clear instructions on where to use this URL inside of your app.

It is very important to replaced the default "Log into your app..." directions with ones specific to your app. Guiding the user to exactly the right place makes the setup process much easier for the user. Here is what we will say for Hubspot:

![Step 3 of trigger editor](https://cdn.zapier.com/storage/photos/8255ae3ea6a5fc2307e5aaa498716dcd.png)

Click save to proceed to Step 4. In this step, we will copy and paste an example of what Hubspot sends in a webhook. This is *critical* for static webhook triggers. If you do not do this step, Zapier won't know what fields to show users when they are trying to make Zaps.

The data can be found by copying and pasting out of examples in documentation, or by using a app like [RequestBin](http://requestb.in/) to catch a hook.

![Step 4 sample data](https://cdn.zapier.com/storage/photos/c1589c601c3c6216e7a8fa8735068953.png)

When you click "Parse" you will be presented with a slew of form fields, one for each JSON key in the sample. These forms allow you to override the default name Zapier will give each key. For instance, Zapier will automatically turn the key "is-contact" into "Is Contact", but you might want to rename it to "Is a Contact". For now, we will skip this step and click "Save".

At this point, we have defined our first trigger and are ready to test it out!

### Testing what we have built

Now that we have built out the basics of our app, it is time to try it out and see if it works. Go to your [dashboard](https://zapier.com/app/dashboard) and click the create a zap button. On Step 1 of the Zap Editor, you should now have our Hubspot Example app. The app should have a single trigger, New Contact.

![Your Dev App on Step 1 of Zap Editor](https://cdn.zapier.com/storage/photos/5771351d2b16a7e1532a79a1ab5ca45b.png)

After you select the trigger and any action (the Email Send Outbound Email is a good one to test with), Step 2 will show you the directions on how to use the static webhook URL.

![Step 2 of Zap Editor](https://cdn.zapier.com/storage/photos/b3d791f7537059150c85f39404b6c44d.png)

Continue down to Step 5 and click the "Insert Fields" button. You will get a dropdown list that has a bunch of fields. Note that the field names match up with what we put in our sample result.

![Step 5 of Zap Editor](https://cdn.zapier.com/storage/photos/75bf01664f562862d470f7cde489a840.png)

Now is also a good time to point out the value in renaming the fields when we pasted in the sample while building our trigger. Zapier turned the nested key `{properties: {firstname: {value: "joe@example.com"}}}` into "Properties Firstname Value". We can go back and edit our trigger to rename that field to just be "Contact First Name".

If you like, you can continue to fill out the Zap. On Step 6, when you click the test button, you will likely get a popup that says Zapier could not find any samples. All you need to do make Hubspot send a webhook by enrolling a contact into the workflow you setup. We'll catch the webhook and display it as a sample result. Once you get that, you can be sure your trigger is configured properly.

**Congratulations!** You have a working Hubspot application that uses static webhooks to receive data.

Be sure to check out our other examples for more details on doing other interesting things with Zapier's developer platform!

***

## SimplyBook

  * Setting up Session Auth.

This example will walk you through creating a Developer App that uses Session Auth and has a single visible trigger that looks for new data. To make the example real, we'll be implementing the SimplyBook API.

##This example will walk you through creating a Developer App that uses Session Auth and has a single visible trigger that looks for new data. To make the example real, we'll be implementing the SimplyBook API.

### Quick Preparation Checklist

If you plan to follow along, it is recommended you set up everything beforehand and keep these resources open and ready for quick access.

* You must have a [Zapier account](https://zapier.com/sign-up/).
* You must have a [SimplyBook account](https://simplybook.me/).
* Read the [Zapier Legacy Web Builder Documentation](https://platform.zapier.com/legacy/docs/) to familiarize yourself with some of the terminology and basic components of an App.
* Read the [SimplyBook API Documentation](https://simplybook.me/api/doc) to familiarize yourself with SimplyBook.

### Create the App

To get started, go to the [Developer Platform](https://zapier.com/developer/builder/) and click the "Create App" button. You'll be asked to provide a title and a brief description.

![Create App screen](https://cdn.zapier.com/storage/photos/1fae214ea4a25fc86394f476eb86038d.png)

After you submit, you should find yourself with a fresh App like this:

![Screenshot of empty dev app](https://cdn.zapier.com/storage/photos/55b0f01c617ca6431109f9a36a92e112.png)

### Setting up authentication

We'll start by defining how Zapier should authenticate with SimplyBook. From the above screen, click the "Get Started" button in the authentication section.

![Get Started button](https://cdn.zapier.com/storage/photos/eaaed229232e83b4ccf42f479df50fd8.png)

On Step 1 you will want to choose Session Auth since that is what SimplyBook uses.

![Selecting Session Auth](https://cdn.zapier.com/storage/photos/5e2cab2c4374f1f4d6fc8a080a758643.png)

You should then find yourself on Step 2 with a couple of pre-generated authentication fields. These are the fields that users will be presented with when they add a SimplyBook account to Zapier.

![Screenshot of generated authentication fields](https://cdn.zapier.com/storage/photos/55dd04e78f82df7ba2786c730b9bf8f2.png)

Looking at the documentation, there’s a `companyLogin` we’ll need, so let’s add that by clicking on “Add Another Authentication Field” on the top left of the list of fields.

![Screenshot of adding Company Login](https://cdn.zapier.com/storage/photos/8c9910269122dd0f27da2061ba0675f6.png)

After adding that, we have all fields we need. Sorting them (clicking the arrow buttons to the right) is a good idea, for an improved UX.

![Screenshot of all authentication fields](https://cdn.zapier.com/storage/photos/bf36cb34ca154ecc62f7586129119110.png)

After clicking Next, we’re at the final step for setting up the authentication schema plainly. Here we’ll want to define how authentication goes through, which, according to the documentation, is in the header.

![Screenshot of auth mapping](https://cdn.zapier.com/storage/photos/00bfb38e22c73d3ad24098a18183d3ba.png)

The [Auth Mapping](https://platform.zapier.com/legacy/docs#authentication-mappings) maps the variables provided by the user and returned by the `get_sesion_info()` we're going to define. In this case we define two headers.

At this point, we have the authentication setup and are ready to make our test trigger.

### Setting up a test trigger

In order to verify the authentication users provide, we need to build a test trigger. The test trigger is simply an API call to an endpoint that requires authentication and is guaranteed to always return some data. This allows Zapier to verify that the authentication information a user provides is valid. For SimplyBook, we'll use the `/admin` endpoint as the test call (using the `getCompanyInfo()` method).

**NOTE:** Usually there’s a `/me` or `/user` endpoint you can use, in most APIs.

From your App, click the "Add Your First Test Trigger" button.

![Create trigger button](https://cdn.zapier.com/storage/photos/a66e947b1745ae4b850fe6c9bcd9c0ad.png)

The first form you see allows you to define some of the meta information about the trigger. Since this is a test trigger that will not be useful beyond verifying authentication, we can put something short and leave the "Hide" checkbox checked.

![Step 1 of adding a trigger](https://cdn.zapier.com/storage/photos/4da216793545618af409164d76edabb5.png)

Click next to proceed to Step 2, Trigger Fields. Trigger fields add extra information for the trigger which you can use in the URL or in Scripting. We're actually going to skip over this step because our trigger does not require any additional info. Hit next to get to Step 3, where we define how our trigger will fetch data from SimplyBook.

Here, according to the documentation,, here is what we will need to fill out:

![Step 3 of adding a trigger](https://cdn.zapier.com/storage/photos/1f20df426626f9ae66e1d2481e475bbc.png)

Click save to proceed to Step 4. Typically in this step you would copy and paste an example JSON representation of a response in the text area. Since this test trigger will be hidden from actual use in the Zapier UI, we'll skip this step, so just click save.

At this point, we have defined our test trigger and are almost ready to try it out!

### Defining how authentication really works

Now we need to jump into Scripting and create our own `get_session_info` method.

Also a “generic” `add_custom_headers` method to inject in all `TRIGGER_KEY_pre_poll` (and similarly for any other actions or searches we could have) our custom headers.

Click the “Edit Code” button.

![Edit Code button](https://cdn.zapier.com/storage/photos/02d7f83e18580d701276b90c26566093.png)

According to SimplyBook’s documentation, the authentication needs to be a `POST` request to `https://user-api.simplybook.me/login`, with a JSON body, like:

{% highlight json %}
{% raw %}
{
  "jsonrpc": "2.0",
  "method": "getUserToken",
  "params": [
    "companyLogin",
    "username",
    "password"
  ],
  "id": 1
}
{% endraw %}
{% endhighlight %}

That means we should make Scripting look like:

{% highlight javascript %}
{% raw %}
'use strict';

var Zap = {
    get_session_info: function(bundle) {
        var user_token,
            request_data,
            token_request_payload,
            token_response,
            parsed_response;

        // Build Request Body
        request_data = {
            jsonrpc: '2.0',
            method: 'getUserToken',
            params: [
                bundle.auth_fields.company,
                bundle.auth_fields.username,
                bundle.auth_fields.password
            ],
            id: 1
        };

        // Assemble the meta data for our key swap request
        token_request_payload = {
            method: 'POST',
            url: 'https://user-api.simplybook.me/login',
            headers: {
                'Content-Type': 'application/json',
                'Accept': 'application/json'
            },
            data: z.JSON.stringify(request_data)
        };

        // Fire off the key exchange request.
        token_response = z.request(token_request_payload);
        parsed_response = z.JSON.parse(token_response.content);

        // Handle errors (ideally we'd look in the response status_code)
        if (parsed_response.error) {
            throw new HaltedException('Error: ' + parsed_response.error.message);
        }

        // Extract the `user_token` from the returned JSON.
        if (parsed_response.result) {
            user_token = parsed_response.result;
        } else {
            throw new HaltedException('Invalid Login Credentials!');
        }

        // Now we get the user_token!
        return { 'user_token': user_token };
    },

    // Modify the request details before checking auth
    auth_test_pre_poll: function(bundle) {

        // Build Request Body
        var request_data = {
            jsonrpc: '2.0',
            method: 'getCompanyInfo',
            params: [],
            id: 1
        };

        bundle.request.data = z.JSON.stringify(request_data);

        return bundle.request;
    },

    // Check if there's an invalid session
    auth_test_post_poll: function(bundle) {
        var parsed_response = z.JSON.parse(bundle.response.content);

        // Handle errors (ideally we'd look in the response status_code)
        if (parsed_response.error) {
            throw new InvalidSessionException();
        }

        return parsed_response.result;
    }
};
{% endraw %}
{% endhighlight %}

Don’t forget to Save (top right button)!

### Testing what we have built so far (authentication)

Now is a good time to go and see if we have the authentication field and test trigger setup properly. To test them, you can go to your [connected accounts](https://zapier.com/app/settings/authorizations) and click the connect account dropdown.

![Connect account dropdown](https://cdn.zapier.com/storage/photos/8a41637e84ea91251060f0b9986fff3a.png)

After you select the SimplyBook Example App, you will get this form:

![Screenshot of authentication field](https://cdn.zapier.com/storage/photos/142ca709d3ff7aa3e58ae938aceb0c36.png)

As you can see, the form contains the authentication fields we set up. Fill out the form and click continue. At this point, Zapier will make an API call to the auth trigger. If everything is setup correctly, you should get a success message and the account should be added:

![Example of successfully adding a SimplyBook account](https://cdn.zapier.com/storage/photos/7b2c71d767de84a4154ee09cc47fd429.png)

You can check the requests and what they have in your app’s Monitoring tab.

![App’s Monitoring Tab](https://cdn.zapier.com/storage/photos/ade8b71f4edda7971d6778d47dca6270.png)

Now that we have working authentication, we are ready to create our first visible trigger!

### Creating a visible trigger

A useful trigger would be to get all existing bookings.

Looking through the documentation we can find a `getBookingsZaper()` method in the `/admin` endpoint. Let’s use that.

We’ll start by clicking to add a new trigger.

![Add New Trigger button](https://cdn.zapier.com/storage/photos/fb5e28b091938d48405d9adf99f953ed.png)

Here’s what we’d fill in for the first step:

![Add New Trigger: Step 1](https://cdn.zapier.com/storage/photos/650bfab89c4f29d73aae6005b083e7fe.png)

Click “Save & Next”. Since there are no fields/params for this trigger, we can skip step 2 as well. Click “Next”

Here’s what we’ll need in Step 3:

![Add New Trigger: Step 3](https://cdn.zapier.com/storage/photos/5e0037bfd9ebd14bfdabb0e18ed85ffc.png)

Click “Save & Next”. In this last step we’ll add a sample object. This won’t usually be shown to the user in the UI, unless they skip the test step:

{% highlight json %}
{% raw %}
{
    "id": "1",
    "record_date": "2016-05-10 20:25:01",
    "start_date": "20160511T090000",
    "end_date": "20160511T100000",
    "unit_id": "1",
    "text": "Test Text",
    "client": "Test Client",
    "unit": "Test Unit",
    "event": "Test Event",
    "event_id": "1",
    "is_confirm": "1",
    "client_id": "1",
    "client_phone": "1111111111",
    "client_email": "test@example.com",
    "offset": "0",
    "comment": "",
    "code": "test"
}
{% endraw %}
{% endhighlight %}

Feel free to mark special fields as important and create better labels (we’ll automatically figure that out if you don’t set anything)

![Add New Trigger: Step 4](https://cdn.zapier.com/storage/photos/79e3625e1bf58a079c09da4bfc48f8e4.png)

Click save and we are done here.

Now we just need to use Scripting to customise (add `pre_poll` and `post_poll` for this new trigger).

Basically Scripting should become this:

{% highlight javascript %}
{% raw %}
'use strict';

var Zap = {
    get_session_info: function(bundle) {
        var user_token,
            request_data,
            token_request_payload,
            token_response,
            parsed_response;

        // Build Request Body
        request_data = {
            jsonrpc: '2.0',
            method: 'getUserToken',
            params: [
                bundle.auth_fields.company,
                bundle.auth_fields.username,
                bundle.auth_fields.password
            ],
            id: 1
        };

        // Assemble the meta data for our key swap request
        token_request_payload = {
            method: 'POST',
            url: 'https://user-api.simplybook.me/login',
            headers: {
                'Content-Type': 'application/json',
                'Accept': 'application/json'
            },
            data: z.JSON.stringify(request_data)
        };

        // Fire off the key exchange request.
        token_response = z.request(token_request_payload);
        parsed_response = z.JSON.parse(token_response.content);

        // Handle errors (ideally we'd look in the response status_code)
        if (parsed_response.error) {
            throw new HaltedException('Error: ' + parsed_response.error.message);
        }

        // Extract the `user_token` from the returned JSON.
        if (parsed_response.result) {
            user_token = parsed_response.result;
        } else {
            throw new HaltedException('Invalid Login Credentials!');
        }

        // Now we get the user_token!
        return { 'user_token': user_token };
    },

    // Add custom headers to a bundle
    add_custom_headers: function(bundle) {
        bundle.request.method = 'POST';
        bundle.request.headers['X-Company-Login'] = bundle.auth_fields.company;
        bundle.request.headers['X-User-Token'] = bundle.auth_fields.user_token;

        // Delete unnecessary auto-added fields
        delete bundle.request.headers.company;
        delete bundle.request.headers.username;
        delete bundle.request.headers.password;

        return bundle;
    },

    // Modify the request details before checking auth
    auth_test_pre_poll: function(bundle) {
        bundle = this.add_custom_headers(bundle);

        // Build Request Body
        var request_data = {
            jsonrpc: '2.0',
            method: 'getCompanyInfo',
            params: [],
            id: 1
        };

        bundle.request.data = z.JSON.stringify(request_data);

        return bundle.request;
    },

    // Check if there's an invalid session
    auth_test_post_poll: function(bundle) {
        var parsed_response = z.JSON.parse(bundle.response.content);

        // Handle errors (ideally we'd look in the response status_code)
        if (parsed_response.error) {
            throw new InvalidSessionException();
        }

        return parsed_response.result;
    },

    // Modify the request details before getting bookings
    new_booking_pre_poll: function(bundle) {
        bundle = this.add_custom_headers(bundle);

        // Build Request Body
        var request_data = {
            jsonrpc: '2.0',
            method: 'getBookingsZapier',
            params: [],
            id: 1
        };

        bundle.request.data = z.JSON.stringify(request_data);

        return bundle.request;
    },

    // Check if there's an invalid session
    new_booking_post_poll: function(bundle) {
        var parsed_response = z.JSON.parse(bundle.response.content);

        // Handle errors (ideally we'd look in the response status_code)
        if (parsed_response.error) {
            throw new InvalidSessionException();
        }

        return parsed_response.result;
    }
};
{% endraw %}
{% endhighlight %}

At this point, we have a visible trigger that we are ready to test.

### Testing the trigger

Now that we have built out the basics of our App, it is time to try it out and see if it works. Go to your dashboard and click the “Make a Zap!” button.

On the first step of the Zap Editor you should be able to see the SimplyBook app and select it’s single visible trigger

![Step 1 Zap Editor](https://cdn.zapier.com/storage/photos/14a42a6d8ac3360d6e245c66aa2b956f.png)

Now log into SimplyBook and create a new booking, if you don’t have any yet.

After that, you should be able to see it in your Zap.

![Step 2 Zap Editor](https://cdn.zapier.com/storage/photos/df7be48eb766ef54808e7c5b8c259d20.png)

As an action, you can use anything we like. Sending a direct message to slack tends to work really well.

![Step 3 Zap Editor](https://cdn.zapier.com/storage/photos/5b99ffe04afc83fa58387066841ed757.png)

You should now be able to login to Slack and see the new booking.

![New Booking in Slack](https://cdn.zapier.com/storage/photos/e561319c0c01b7fddd048b5de4634b9a.png)

**Congratulations!** You have a working SimplyBook application that:

* Uses Session Auth to authenticate.
* Has a polling trigger to test authentication credentials.
* Has a visible polling trigger.

Be sure to check out our other examples for more details on doing other interesting things with Zapier's developer platform!Testing the trigger

Now that we have built out the basics of our App, it is time to try it out and see if it works. Go to your dashboard and click the “Make a Zap!” button.

On the first step of the Zap Editor you should be able to see the SimplyBook app and select it’s single visible trigger

![Step 1 Zap Editor](https://cdn.zapier.com/storage/photos/14a42a6d8ac3360d6e245c66aa2b956f.png)

Now log into SimplyBook and create a new booking, if you don’t have any yet.

After that, you should be able to see it in your Zap.

![Step 2 Zap Editor](https://cdn.zapier.com/storage/photos/df7be48eb766ef54808e7c5b8c259d20.png)

As an action, you can use anything we like. Sending a direct message to slack tends to work really well.

![Step 3 Zap Editor](https://cdn.zapier.com/storage/photos/5b99ffe04afc83fa58387066841ed757.png)

You should now be able to login to Slack and see the new booking.

![New Booking in Slack](https://cdn.zapier.com/storage/photos/e561319c0c01b7fddd048b5de4634b9a.png)

**Congratulations!** You have a working SimplyBook application that:

* Uses Session Auth to authenticate.
* Has a polling trigger to test authentication credentials.
* Has a visible polling trigger.

Be sure to check out our other examples for more details on doing other interesting things with Zapier's developer platform!

***

## SimplyBook With Search or Create Action

  * Setting up a Write action.
  * Setting up a Search action.
  * Upgrading the Search to a Search or Create action.

This example will walk you through creating a write action and a search action, which will then be “upgraded” to create a “Search or Create” action. To make the example real, we'll be implementing the SimplyBook API.

### Quick Preparation Checklist

We’ll assume having started with the SimplyBook app from the Session Auth example above. Make sure you get all the links and code from there (or understand it to grasp how we’re extending it).

### Add Create Client Action

First, we need to create an action to Create a Client.

![Add Your First Action button](https://cdn.zapier.com/storage/photos/d6fce4f9d76a03cd670910de470a052e.png)

#### Step 1

We fill the first step like this:

![Step 1 of Create Client action](https://cdn.zapier.com/storage/photos/7a943c7ca94fb1d58339427b884a5aa8.png)

#### Step 2

To not overcomplicate this example, we’ll only add 3 fields:
- Name (required)
- Email
- Phone

For that we’ll need to use the “Add New Action Field” button.

![Add New Action Field button](https://cdn.zapier.com/storage/photos/dc179e54b9af8a4fa4fb8c0cd6cf39d5.png)

And here’s how each field would look:

![Name Action Field](https://cdn.zapier.com/storage/photos/63bec52e7911394c8c3db0ad08e84389.png)

![Email Action Field](https://cdn.zapier.com/storage/photos/abc82f27d487a6e7aeb5aadc2d9581a6.png)

![Phone Action Field](https://cdn.zapier.com/storage/photos/4657174f1f1013bdd107d069b89992a0.png)

All of them should have checked the “Send to Action Endpoint URL in JSON body” checkbox

![Send to Action Endpoint URL in JSON body](https://cdn.zapier.com/storage/photos/4a73994cbd7147e1efc24519c629c3ca.png)

This is how they look in the end for the action’s step 2:

![Step 2 of Create Client action](https://cdn.zapier.com/storage/photos/aa2d4b56d08b844dad3d3de6229b607c.png)

#### Step 3

For Step 3 we only need to set the `https://user-api.simplybook.me/admin` as the Action Endpoint URL

![Step 3 of Create Client action](https://cdn.zapier.com/storage/photos/e30545a23793b5655557c68e8a1421c1.png)

#### Step 4

In the last step, the API only returns the client ID, so that’s what we’ll add:

{% highlight json %}
{% raw %}
{
    "id": 1
}
{% endraw %}
{% endhighlight %}

![Step 4 of Create Client action](https://cdn.zapier.com/storage/photos/ef67befa4d96adf6acea08c9eb419fd1.png)

This API requires us to do some changes in the Scripting (your API might not), so we’ll add the following methods:

{% highlight javascript %}
{% raw %}
var Zap = {
    // other methods...

    // Modify the request details before creating a client
    create_client_pre_write: function(bundle) {
        bundle = this.add_custom_headers(bundle);

        // Build Request Body
        var request_data = {
            jsonrpc: '2.0',
            method: 'addClient',
            params: [bundle.action_fields],
            id: 1
        };

        bundle.request.data = z.JSON.stringify(request_data);

        return bundle.request;
    },

    // Check if there's an invalid session
    create_client_post_write: function(bundle) {
        var parsed_response = z.JSON.parse(bundle.response.content);

        // Handle errors (ideally we'd look in the response status_code)
        if (parsed_response && parsed_response.error) {
            throw new InvalidSessionException();
        }

        var result = {
            id: parsed_response.result.message
        };

        return result;
    }
};
{% endraw %}
{% endhighlight %}

We’re now ready to test the action! Zap away!

### Add Search Client Action

Now, we need to create a Search for Clients.

![Add Your First Search button](https://cdn.zapier.com/storage/photos/17ee493459e2674183e7f9500fd8fff7.png)

#### Step 1

We fill the first step like this:

![Step 1 of Find Client search](https://cdn.zapier.com/storage/photos/1ca0328d1e363f1360a9437415c099f1.png)

#### Step 2

The API allows us to send a `string` which searches in `name`, `email`, and `phone`, so we only need 1 field:

![Query Search Field](https://cdn.zapier.com/storage/photos/ed6e3f76315f665f69e058363c4585c9.png)

It should look like this:

![Step 2 of Find Client search](https://cdn.zapier.com/storage/photos/28c9286374c9338387aeaf0daae52070.png)

#### Step 3

We’ll leave this step empty for now, and will come back to it later. Just click “Save & Next”.

#### Step 4

Here’s how Step 4 should look. We’re using the same `https://user-api.simplybook.me/admin` URL because this API changes “what’s called” in the request body.

![Step 4 of Find Client search](https://cdn.zapier.com/storage/photos/c935d854f93ca4f205ad8567bac1f5e5.png)

#### Step 5

For the final step, we add the sample JSON for a single object:

{% highlight json %}
{% raw %}
{
    "name": "Test Client",
    "phone": "+1111-111-1111",
    "email": "test@example.com"
}
{% endraw %}
{% endhighlight %}

![Step 5 of Find Client search](https://cdn.zapier.com/storage/photos/112b114fae7a9d4d178ee7b4200ff293.png)

This API requires us to do some changes in the Scripting (your API might not), so we’ll add the following methods:

{% highlight javascript %}
{% raw %}
var Zap = {
    // other methods...

    // Modify the request details before finding a client
    find_client_pre_search: function(bundle) {
        bundle = this.add_custom_headers(bundle);

        // Build Request Body
        var request_data = {
            jsonrpc: '2.0',
            method: 'getClientList',
            params: [bundle.search_fields.query],
            id: 1
        };

        bundle.request.data = z.JSON.stringify(request_data);

        return bundle.request;
    },

    // Check if there's an invalid session
    find_client_post_search: function(bundle) {
        var parsed_response = z.JSON.parse(bundle.response.content);

        // Handle errors (ideally we'd look in the response status_code)
        if (parsed_response && parsed_response.error) {
            throw new InvalidSessionException();
        }

        return parsed_response.result;
    },

    // Modify the request details before fetching a client
    find_client_pre_read_resource: function(bundle) {
        bundle = this.add_custom_headers(bundle);

        // NOTE: This API doesn't really have a "GET" endpoint,
        // so we search for email and hope for the best.

        // Build Request Body
        var request_data = {
            jsonrpc: '2.0',
            method: 'getClientList',
            params: [bundle.read_fields.email],
            id: 1
        };

        bundle.request.data = z.JSON.stringify(request_data);

        return bundle.request;
    },

    // Check if there's an invalid session
    find_client_post_read_resource: function(bundle) {
        var parsed_response = z.JSON.parse(bundle.response.content);

        // Handle errors (ideally we'd look in the response status_code)
        if (parsed_response && parsed_response.error) {
            throw new InvalidSessionException();
        }

        var result = [];

        // Only return the object
        if (parsed_response.result && parsed_response.result.length > 0) {
            result = parsed_response.result[0];
        }

        return result;
    }
};
{% endraw %}
{% endhighlight %}

Now we have a working Create Client action and Find Client search!

### Upgrading to Search or Create

Our app allows us to create clients and search for them, but you can upgrade the search to automatically create a client if it’s not found. This is incredibly powerful, and easy to implement.

We just need to edit our search and go to step “3. Search or Action”.

In our case, we just need to link these to the create action we already have:

![Step 3 of Find Client search](https://cdn.zapier.com/storage/photos/f7f34592cec4ebdbe2db7abe68eb3a9d.png)

Now we can see it in action!

![Editor with Find or Create Client](https://cdn.zapier.com/storage/photos/5255005ae9c4eb8e97752b59b291f8e7.png)

**Congratulations!** You have a working SimplyBook application that:

* Has a visible write action.
* Has a visible search or create action.

Be sure to check out our other examples for more details on doing other interesting things with Zapier's developer platform!
