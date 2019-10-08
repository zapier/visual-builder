---
title: Getting Started With Zapier Platform CLI
order: 1
layout: post-toc
redirect_from: /cli/
---

# Getting Started With Zapier Platform CLI

Welcome to the Zapier Platform! In this tutorial, we'll walk you through the process of building, testing, and pushing an example app to Zapier. We'll use a fake/mock API for recipes in this example, but for production Zapier apps, you'd want to connect to a real API.

## Installing the CLI

To get started, first make sure that your dev environment meets the [requirements](https://github.com/zapier/zapier-platform-cli#requirements) for running the the platform. Once you have the proper version of Node.js, install the Zapier CLI tool.

```bash
# install the CLI globally
npm install -g zapier-platform-cli
```

The CLI is the primary tool for managing your apps. With it, you can validate and test apps locally, push apps so they are available on Zapier, and view logs for debugging. To see a list of all the available commands, try `zapier help`.

Now that your CLI is installed - you'll need to identify yourself via the CLI.

```bash
# setup auth to Zapier's platform with a deploy key
zapier login
```

Now your CLI is installed and ready to go! Zapier writes your deploy key to `~/.zapierrc`. You'll want to keep that file safe and not check it into source control.

## Starting an App

To begin building an app, use the `init` command to setup the [needed structure](https://github.com/zapier/zapier-platform-example-app-minimal).

```bash
# create a directory with the minimum required files
zapier init example-app
# move into the new directory
cd example-app
```

Inside the directory, you'll see a few files. `package.json` is a typical requirements file of any Node.js application. It's pre-populated with a few dependencies, most notably the `zapier-platform-core`, which is what makes your app work with the Zapier Platform. There is also an `index.js` file and a test directory (more on those later).

Before we go any further, we need to install the dependencies for our app:

```bash
npm install
```

## Your `index.js`

Right next to `package.json` should be `index.js`, which is the entry point to your app. This is where the Platform will look to understand how your app will interact with Zapier. Open it up in your editor of choice and let's take a look!

You'll see a few things in `index.js`:

- we export a single `App` definition which will be interpreted by Zapier
- in `App` definition, `beforeRequest` & `afterResponse` are hooks into the HTTP client to manipulate the request/response on every call
- in `App` definition, `triggers` will describe ways to trigger off of data in your app
- in `App` definition, `searches` will describe ways to find data in your app
- in `App` definition, `creates` will describe ways to create data in your app
- in `App` definition, `resources` are purely optional but convenient ways to describe CRUD-like objects in your app (see [example resources app](https://github.com/zapier/zapier-platform-example-app-resource))

## Adding a Trigger

Let's start by adding a [**trigger**](https://zapier.com/developer/documentation/v2/triggers/). We will configure it to read data from a mocked API (in the future - your real app will use a real API, of course :-):

```bash
mkdir triggers
touch triggers/recipe.js
```

> Note: The `triggers` folder is simply a convention - we recommend it. Also, `recipe.js` is just an example name of a model - maybe you'll eventually make a `contact.js`, `lead.js` or `order.js`.

Open `triggers/recipe.js` (file created by `zapier init`) and **replace** it with:

```javascript
const listRecipes = (z, bundle) => {
  z.console.log('hello from a console log!')
  const promise = z.request(
    'http://57b20fb546b57d1100a3c405.mockapi.io/api/recipes'
  )
  return promise.then(response => response.json)
}

module.exports = {
  key: 'recipe',
  noun: 'Recipe',
  display: {
    label: 'New Recipe',
    description: 'Trigger when a new recipe is added.'
  },
  operation: {
    perform: listRecipes,
    sample: {
      id: 1,
      createdAt: 1472069465,
      name: 'Best Spagetti Ever',
      authorId: 1,
      directions: '1. Boil Noodles\n2.Serve with sauce',
      style: 'italian'
    }
  }
}
```

Let's break down what is happening in this snippet!

First, look first at the function definition for `listRecipes`. You see that it handles the API work, making the HTTP request and returning a promise that will eventually yield a result.

> _Note_: If you're new to promises, they are essentially synchronous callbacks. The equivalent content of a callback should go inside the `.then()` portion of a promise.

The `listReceipes` function receives two arguments, a `z` object and a `bundle` object.

- The [Z Object](https://github.com/zapier/zapier-platform-cli#z-object) is a collection of utilities needed when working with APIs. In our snippet, we use `z.request` to make the HTTP call and `z.JSON` to parse the response.
- The [Bundle Object](https://github.com/zapier/zapier-platform-cli#bundle-object) contains any data needed to make API calls, like authentication credentials or data for a POST body. In our snippet the Bundle is not used, since we don't require any of those to make our simple GET request.

> Note about Z Object: While it is possible to accomplish the same tasks using alternate Node.js libraries, it's preferable to use the `z` object as there are features built into these utilities that augment the Zapier experience. For example, logging of HTTP calls and better handling of JSON parsing failures. [Read the docs](https://github.com/zapier/zapier-platform-cli#z-object) for more info.

Second, look at the second part of our snippet; the export. Essentially, we export some metadata plus our `listRecipes` function and a sample. We'll explain later how Zapier uses this metadata and exposes it to the end user. For now, know that it satisfies the minimum info required to define a trigger.

With our trigger defined, we need to incorporate it into our app.

In `index.js`, **edit** the file to include:

```javascript
// Place this at the top of index.js
const recipe = require('./triggers/recipe')
```

With the trigger imported, we need to register it on our app by editing the existing `triggers` property.

In `index.js`, **edit** the `App`'s `triggers` section to include:

```javascript
// Edit the App definition to register our trigger
const App = {
  // ...
  triggers: {
    [recipe.key]: recipe // new line of code
  }
  // ...
}
```

Now, let's add a test to make sure our code is working properly.

In `test/index.js`, **replace** the file with:

```javascript
const should = require('should')

const zapier = require('zapier-platform-core')

const App = require('../index')
const appTester = zapier.createAppTester(App)

describe('My App', () => {
  it('should load recipes', done => {
    const bundle = {}

    appTester(App.triggers.recipe.operation.perform, bundle)
      .then(results => {
        should(results.length).above(1)

        const firstResult = results[0]
        console.log('test result: ', firstResult)
        should(firstResult.name).eql('name 1')
        should(firstResult.directions).eql('directions 1')

        done()
      })
      .catch(done)
  })
})
```

You should be able to run the test with `zapier test` and see it pass:

```bash
zapier test
#
#   triggers
# 200 GET http://57b20fb546b57d1100a3c405.mockapi.io/api/recipes
#     ✓ should load recipes (312ms)
#
#   1 passing (312ms)
#
```

For this example, we'll stick to a single test, but you can see what multiple tests look like in our [this example](https://github.com/zapier/zapier-platform-example-app-rest-hooks/blob/master/test/triggers.js).

## Modifying a Trigger

Let's say we want to let our users tweak the cuisine style of recipes they are triggering on. A classic way to do that with Zapier is to provide an input field a user can fill out.

In `triggers/recipe.js`, **replace** the file with:

```javascript
const listRecipes = (z, bundle) => {
  z.console.log('hello from a console log!')
  const promise = z.request(
    'http://57b20fb546b57d1100a3c405.mockapi.io/api/recipes',
    {
      // NEW CODE
      params: {
        style: bundle.inputData.style
      }
    }
  )
  return promise.then(response => JSON.parse(response.content))
}

module.exports = {
  key: 'recipe',
  noun: 'Recipe',
  display: {
    label: 'New Recipe',
    description: 'Trigger when a new recipe is added.'
  },
  operation: {
    // NEW CODE
    inputFields: [{ key: 'style', type: 'string', required: false }],
    perform: listRecipes,
    sample: {
      id: 1,
      createdAt: 1472069465,
      name: 'Best Spagetti Ever',
      authorId: 1,
      directions: '1. Boil Noodles\n2.Serve with sauce',
      style: 'italian'
    }
  }
}
```

Notice that we now include and use an input field keyed `"style"`. We have to add it in two places:

- In the `inputFields` on `operation` - this defines the field as exposed in the Zapier UI.
- In the `listRecipes` function - we use the provided style via the bundle `bundle.inputData.style`. Since the field is not required - it could be null!

Since we are developing locally, let's tweak the test to verify everything still works.

In `test/index.js`, **replace** the file with:

```javascript
const should = require('should')

const zapier = require('zapier-platform-core')

const App = require('../index')
const appTester = zapier.createAppTester(App)

describe('My App', () => {
  it('should load recipes', done => {
    const triggerPointer = 'triggers.recipe'
    const bundle = {
      // NEW CODE
      inputData: {
        style: 'mediterranean'
      }
    }

    appTester(App.triggers.recipe.operation.perform, bundle)
      .then(results => {
        should(results.length).above(1)

        const firstResult = results[0]
        console.log('test result: ', firstResult)
        should(firstResult.name).eql('name 1')
        should(firstResult.directions).eql('directions 1')

        done()
      })
      .catch(done)
  })
})
```

You can run your test again and make sure everything still works:

```bash
zapier test
#
#   triggers
# 200 GET http://57b20fb546b57d1100a3c405.mockapi.io/api/recipes
#     ✓ should load recipes (312ms)
#
#   1 passing (312ms)
#
```

Looking good locally! Let's move on.

## Deploying an App

So far, everything we have done has been local, on your machine. It's been fun, but we want our app on Zapier.com so we can use it with the thousands of other integrations! To do so, we need to take our working local app and push it to Zapier.

Let's push a version of your app! You can have many versions of an app, which simplifies making breaking changes and testing in the future. For now, we just need a single version pushed.

> If this is your first time pushing your app version - we will ask you to provide a name so we can register your app - this is a one time thing!

```bash
zapier push
# Preparing to build and upload your app.
#
#   Copying project to temp directory - done!
#   Installing project dependencies - done!
#   Applying entry point file - done!
#   Validating project - done!
#   Building app definition.json - done!
#   Zipping project and dependencies - done!
#   Cleaning up temp directory - done!
#   Uploading version 1.0.0 - done!
#
# Build and upload complete! You should see it in your Zapier editor at https://zapier.com/app/editor now!
```

Now that your app version is properly pushed, log in and visit [https://zapier.com/app/editor](https://zapier.com/app/editor) to create a Zap and check our progress.

You'll see the app listed as an available option for the first step. Selecting it, you'll see the "New Recipe" trigger. At this point, we've come full circle on the trigger definition from earlier. Remember that, as part of the metadata, we defined a `display` property with a label and help text. Those properties control the info you see inside the Zapier UI.

As you click through, you'll see our input field "style" appear, which you can fill out. Once you finish setting up the step and test it, Zapier will run the `listRecipes` function associated with the trigger, which will make the API request and return the result to Zapier. If you are curious to see what HTTP requests Zapier makes at any point, you can use the `zapier logs` command to find out.

```bash
zapier logs --type=http

# The logs of your app "Example App" listed below.
#
# ┌────────┬────────┬────────────────────────────────────────────────────────┬───────────────┬─────────┬──────────────────────────────────────┬───────────────────────────┐
# │ Status │ Method │ URL                                                    │ Querystring   │ Version │ Step                                 │ Timestamp                 │
# ├────────┼────────┼────────────────────────────────────────────────────────┼───────────────┼─────────┼──────────────────────────────────────┼───────────────────────────┤
# │ 200    │ GET    │ http://57b20fb546b57d1100a3c405.mockapi.io/api/recipes │ style=italian │ 1.0.0   │ a9055e16-fc0d-4fb2-a3e6-9d442d1f70e8 │ 2016-09-13T15:11:30-05:00 │
# └────────┴────────┴────────────────────────────────────────────────────────┴───────────────┴─────────┴──────────────────────────────────────┴───────────────────────────┘
#   Most recent logs near the bottom.
```

Good work, we've built a trigger locally and pushed it to Zapier.

## Adding Authentication

Up to this point we've ignored something that is usually crucial to APIs: authentication. Zapier supports a number of different [authentication schemes](https://github.com/zapier/zapier-platform-cli#authentication). For our app, we are going to set it up to include an API Key in a header.

For different types of authentication, see these example apps:

- [OAuth 2](https://github.com/zapier/zapier-platform-example-app-oauth2)
- [Basic Auth](https://github.com/zapier/zapier-platform-example-app-basic-auth)
- [Session Auth](https://github.com/zapier/zapier-platform-example-app-session-auth)
- [API Key in query string](https://github.com/zapier/zapier-platform-example-app-custom-auth)

For this app, our API Key will go in the header. The first thing we need to do is define the `authentication` section on the app.

In `index.js`, **edit** `App` to include:

```javascript
const App = {
  // ...
  authentication: {
    type: 'custom',
    fields: [{ key: 'apiKey', type: 'string' }],
    test: (z, bundle) => {
      const promise = z.request(
        'http://57b20fb546b57d1100a3c405.mockapi.io/api/me'
      )
      return promise.then(response => {
        if (response.status !== 200) {
          throw new Error('Invalid API Key')
        }
      })
    }
  }
  // ...
}
```

In the above snippet, we define the two required properties of `authentication`:

- `fields` is where we define our auth fields. This works similar to the `inputFields` of triggers. When users connect their account to Zapier, they'll be prompted to fill in this field, and the value they enter becomes available in the `bundle`. Not every authentication type will include `inputFields`.
- `test` is a function used during the account connection process to verify that the user entered valid credentials. The goal of the function is to make an authenticated API request whose response indicates if the credentials are correct. A profile for the user, such as a `/me` endpoint, is a common choice. If valid, the test function can return anything. On invalid credentials, the test needs to raise an error.

With that setup, we now need to make sure that our API key is included in all the requests our app makes.

In `index.js`, **edit** the file to include:

```javascript
// Add this helper function above the App definition
const addApiKeyToHeader = (request, z, bundle) => {
  request.headers['MY-AUTH-HEADER'] = bundle.authData.apiKey
  return request
}

// const App = ...
```

Above we define a helper function, `addApiKeyToHeader`, that puts the user-provided API key in a request header called `MY-AUTH-HEADER`. The name chosen is illustrative, it can be whatever the API you are integrating with requires. Alternatively, you could put it in a query parameter instead of a header, and/or encode it first.

To make our helper function take effect, we need to register it on our app.

In `index.js`, **edit** `App` to include:

```javascript
const App = {
  // ...
  beforeRequest: [
    addApiKeyToHeader // new line of code
  ]
  // ...
}
```

`beforeRequest` is a list of functions that are called before every HTTP request that uses `z.request` or the default `perform` function. This lets you add headers, query params, or whatever is needed to be within _all outbound requests_. In our case, every HTTP request will now have the API key added in a header.

To check our progress, we need to re-push our app.

```bash
zapier push
```

Go back to your Zap at `https://zapier.com`. You'll see a new 'Connect Account' item in your 'New Recipe' trigger. Add an account for our app (enter any value you like for the API key, the mock API does not care).

As soon as you add the account, Zapier will run our app's `authentication.test` function to confirm the credentials are valid.

We can verify the header is present in the request by looking at the logs again.

```bash
zapier logs --type=http --detailed --limit=1

# The logs of your app "Example App" listed below.
#
# ┌─────────────────────┬────────────────────────────────────────────────────────────────────────────────────────┐
# │ Status              │ 200                                                                                    │
# │ Method              │ GET                                                                                    │
# │ URL                 │ http://57b20fb546b57d1100a3c405.mockapi.io/api/me                                      │
# │ Querystring         │                                                                                        │
# │ Version             │ 1.0.0                                                                                  │
# │ Step                │                                                                                        │
# │ Timestamp           │ 2016-09-16T15:57:51-05:00                                                              │
# │ Request Headers     │ user-agent: Zapier                                                                     │
# │                     │ MY-AUTH-HEADER: :censored:6:b1af149262:                                                │
# │ Request Body        │                                                                                        │
# │ Response Headers    │ server: Cowboy                                                                         │
# │                     │ connection: close                                                                      │
# │                     │ x-powered-by: Express                                                                  │
# │                     │ access-control-allow-origin: *                                                         │
# │                     │ access-control-allow-methods: GET,PUT,POST,DELETE,OPTIONS                              │
# │                     │ access-control-allow-headers: X-Requested-With,Content-Type,Cache-Control,access_token │
# │                     │ content-type: application/json                                                         │
# │                     │ content-length: 59                                                                     │
# │                     │ etag: "-80491811"                                                                      │
# │                     │ vary: Accept-Encoding                                                                  │
# │                     │ date: Fri, 16 Sep 2016 20:57:51 GMT                                                    │
# │                     │ via: 1.1 vegur                                                                         │
# │ Response Body       │ [{"id":"1","createdAt":1473801403,"userName":"userName 1"}]                            │
# └─────────────────────┴────────────────────────────────────────────────────────────────────────────────────────┘
```

You can see from the detailed log that the request included our auth header. The value appears as `:censored:6:b1af149262:`, which is intentional. Zapier does not log authentication credentials in plain text.

With that, we've successfully added authentication to our app!

## Invite Users to Your App

If you have at least one trigger or action, now would be a fine time to share your app with some of your users. Early feedback can help you make sure you’re building something they’ll use!

From the Zapier CLI, run:
`zapier invite email@example.com`

Replace the example email address with the user you want to invite. Or run the command without an email address to get a URL you can put in your help pages or other messages to your users.

You can also invite users from the visibility tab of your [developer dashboard](https://zapier.com/developer/builder/):
![Invite users to your app](https://cdn.zapier.com/storage/photos/6055c15a160d905e726e66e1ab24e389.png)

For more on inviting users, see our [detailed documentation](https://zapier.github.io/zapier-platform-cli/#sharing-an-app-version)

## Tutorial Next Steps

Congrats, you've completed the tutorial! At this point we recommend reading up on the [Z Object](https://github.com/zapier/zapier-platform-cli#z-object) and [Bundle Object](https://github.com/zapier/zapier-platform-cli#bundle-object) to get a better idea of what is possible within the `perform` functions. You can also check out the other [example apps](https://github.com/zapier/zapier-platform-cli/wiki/Example-Apps) to see how to incorporate different authentication schemes into your app and how to implement things like searches and creates.
