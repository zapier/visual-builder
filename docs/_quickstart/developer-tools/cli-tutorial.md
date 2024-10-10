---
title: Platform CLI tutorial
order: 3
layout: post-toc
redirect_from: 
    - /quickstart/platform-cli-tutorial
---

# Platform CLI tutorial

This tutorial walks you through the process of building, testing, and pushing an example app to Zapier using Platform CLI. We'll use a mock API for recipes in this tutorial, but for production Zapier apps, you'd want to connect to a real API. 

## Prerequisites

- You'll need a [Zapier account](https://zapier.com/sign-up).
- Your dev environment meets the [requirements for running Platform CLI](https://github.com/zapier/zapier-platform/blob/main/packages/cli/README.md#requirements) with the proper version of Node.js installed. 

- Install the Platform CLI tool
```bash
# Install the CLI globally
npm install -g zapier-platform-cli
```
To see a list of all the available commands in Platform CLI, try `zapier help`.

- Next you'll need to identify yourself via the CLI.
```bash
# Setup auth to Zapier's platform with a deploy key
zapier login
```
Zapier writes your deploy key to `~/.zapierrc`. You'll want to keep that file safe and not check it into source control.

## 1. Start an integration

Use the `init` command to setup the [needed structure](https://github.com/zapier/zapier-platform/tree/main/example-apps). You'll be presented with a list of available templates to start with.

```bash
# Create a directory with the minimum required files and choose a template
zapier init example-app --template minimal

# Move into the new directory
cd example-app
```

Inside the directory, you'll see a few files. `package.json` is a typical requirements file of any Node.js application. It's pre-populated with a few dependencies, most notably the `zapier-platform-core`, which is what makes your app work with the Zapier Platform. There is also an `index.js` file and a test directory (more on those later).
Before we go any further, we need to install the dependencies for our app:

```bash
npm install
```

### `index.js`

`index.js` is the entry point to your app. This is where the Platform will look to understand how your app will interact with Zapier. Open the app directory you created in your code editor of choice.

You may see the following in `index.js`:

- a single `module.exports` definition which will be interpreted by Zapier
- `triggers` will describe ways to trigger off of data in your app
- `searches` will describe ways to find data in your app
- `creates` will describe ways to create data in your app
- `resources` are purely optional but convenient ways to describe CRUD-like objects in your app (see [an example resources app](https://github.com/zapier/zapier-platform/tree/main/example-apps/resource))
- `beforeRequest` & `afterResponse` are hooks into the HTTP client to manipulate the request/response on every call

## 2. Add a trigger

Add a [**trigger**](https://github.com/zapier/zapier-platform/blob/master/packages/cli/README.md#triggerssearchescreates) configured to read data from a mock API:

```bash
zapier scaffold trigger recipe
```

The [scaffold](https://github.com/zapier/zapier-platform/blob/main/packages/cli/docs/cli.md#scaffold) creates a new file `recipe.js` in the `triggers` folder. When building your own integration, you'll likely name your JS files with nouns like `contact.js`, `lead.js` or `order.js`.

Open `triggers/recipe.js` (file created by `zapier scaffold trigger recipe`) and **replace** it with:

```javascript
const listRecipes = async (z, bundle) => {
  const response = await z.request('http://57b20fb546b57d1100a3c405.mockapi.io/api/recipes');
  return response.data;
};

module.exports = {
  key: 'recipe',
  noun: 'Recipe',
  display: {
    label: 'New Recipe',
    description: 'Triggers when a new recipe is created.'
  },
  operation: {
    perform: listRecipes,
    sample: {
      id: 1,
      createdAt: 1472069465,
      name: 'Best Spaghetti Ever',
      authorId: 1,
      directions: '1. Boil Noodles\n2.Serve with sauce',
      style: 'italian'
    },
  },
};
```

To try out the trigger locally, try running `zapier invoke`. The command will ask you which action you'd like to invoke. Now we only have one trigger `recipe`, so you can choose that one.

```
$ zapier invoke
? Which action type would you like to invoke? trigger
? Which "trigger" key would you like to invoke? recipe
✔ Invoking triggers.recipe.operation.inputFields
✔ Invoking triggers.recipe.operation.perform
[
  {
    "id": "1",
    "createdAt": 1471984289,
    "name": "name 1",
    "authorId": 63,
    "directions": "directions 1",
    "style": "style 1"
  },
  <omitted...>
]
```

Let's review the code. The function definition for `listRecipes` handles the API work, making the HTTP request and returning the parsed response data.

In JavaScript, `async/await` are syntactic sugar built on top of [Promises](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise). Be sure to use `await` or `.then()` when you call asynchronous functions.

The `listRecipes` function receives two arguments, a `z` object and a `bundle` object.

- The [Z Object](https://github.com/zapier/zapier-platform/blob/master/packages/cli/README.md#z-object) is a collection of utilities needed when working with APIs. In our snippet, we use `z.request` to make the HTTP call.
- The [Bundle Object](https://github.com/zapier/zapier-platform/blob/master/packages/cli/README.md#bundle-object) contains any data needed to make API calls, like authentication credentials or data for a POST body. In our snippet the Bundle is not used, since we don't require any of those to make our simple GET request.

It is possible to accomplish the same tasks using alternate Node.js libraries, but it is preferable to use the `z` object as there are features built into these utilities that augment the Zapier experience like logging of HTTP calls and error handling. 

In `module.exports`, we export some metadata plus our `listRecipes` function and a sample. We'll explain later how Zapier uses this metadata and exposes it to the end user. For now, know that it satisfies the minimum info required to define a trigger.

As well as defining the trigger, the `scaffold` command has done the following:

`index.js` file now includes:

```javascript
const getRecipe = require('./triggers/recipe')
```

```javascript
module.exports = {
  // ...
  triggers: {
    [getRecipe.key]: getRecipe 
  },
  // ...
};
```

In test/triggers folder, the `recipe.test.js` file was created:

```javascript
const App = require('../../index');
const appTester = zapier.createAppTester(App);
// read the `.env` file into the environment, if available
zapier.tools.env.inject();

describe('triggers.recipe', () => {
  it('should run', async () => {
    const bundle = { inputData: {} };

    const results = await appTester(App.triggers.recipe.operation.perform, bundle);
    expect(results).toBeDefined();
    // TODO: add more assertions
  });
});
```

You should be able to run the test with `zapier test` and see it pass:

```
$ zapier test
Validating project locally
No structural errors found during validation routine.
This project is structurally sound!

✔ Running integration checks ... 23 checks passed

Integration checks passed, no issues found.

Adding /Users/marinahand/.zapierrc to environment as ZAPIER_DEPLOY_KEY...
Running test suite with the following command:

 npm run --silent test --

PASS  test/triggers/recipe.test.js
PASS  test/triggers.test.js (7.52 s)

Test Suites: 2 passed, 2 total
Tests:       3 passed, 3 total
Snapshots:   0 total
Time:        9.429 s
Ran all test suites.
```

For this example, we'll stick to a single test, but you can see what multiple tests look like in [another of the example apps](https://github.com/zapier/zapier-platform/blob/main/example-apps/trigger/test/triggers.js).

## 3. Modify a trigger

To let users tweak the cuisine style of recipes they are triggering on, you can provide an input field a user can fill out.

In `triggers/recipe.js`, **replace** the file with:

```javascript
const listRecipes = async (z, bundle) => {
  const params = {};
  if (bundle.inputData.style) {
    params.style = bundle.inputData.style;
  }

  const requestOptions = {
    url: 'http://57b20fb546b57d1100a3c405.mockapi.io/api/recipes',
    params: params,
  };

  const response = await z.request(requestOptions);
  return response.data;
};

module.exports = {
  key: 'recipe',
  noun: 'Recipe',
  display: {
    label: 'New Recipe',
    description: 'Triggers when a new recipe is created.',
  },
  operation: {
    inputFields: [
      {
        key: 'style',
        type: 'string',
        helpText: 'Which styles of cuisine this should trigger on.',
        required: false
      },
    ],

    perform: listRecipes,
    sample: {
      id: 1,
      createdAt: 1472069465,
      name: 'Best Spagetti Ever',
      authorId: 1,
      directions: '1. Boil Noodles\n2.Serve with sauce',
      style: 'italian',
    },
    outputFields: [
      { key: 'id', label: 'ID' },
      { key: 'createdAt', label: 'Created At' },
      { key: 'name', label: 'Name' },
      { key: 'directions', label: 'Directions' },
      { key: 'authorId', label: 'Author ID' },
      { key: 'style', label: 'Style' },
    ],
  },
};
```

See how the input field key `"style"` was added in the following places:

- In the `inputFields` on `operation` - this defines the field as exposed in the Zap Editor for the user to see. The field is not required, so it could be null.
- In the `listRecipes` function - we use the provided style via the bundle `bundle.inputData.style`. 

Since you are developing locally, rerun `zapier invoke` to verify everything still works. This time, let's skip those interactive prompts. Specify the action type (`trigger`), the key (`recipe`), and the input data in the command, and you'll see:

```
$ zapier invoke trigger recipe --inputData '{"style":"style 20"}'
✔ Invoking triggers.recipe.operation.inputFields
✔ Invoking triggers.recipe.operation.perform
[
  {
    "id": "20",
    "createdAt": 1578590011,
    "name": "name 20",
    "authorId": 90,
    "directions": "directions 20",
    "style": "style 20"
  }
]
```

Let's also tweak the test. In test/trigger, replace the `recipe.test.js` file with:

```javascript
const zapier = require('zapier-platform-core');
const App = require('../../index'); 

const appTester = zapier.createAppTester(App);

describe('triggers', () => {
  describe('new recipe trigger', () => {
    it('should load recipes', async () => {
      const bundle = {
        inputData: {
          style: 'style 2',
        },
      };

      const results = await appTester(
        App.triggers.recipe.operation.perform,
        bundle,
      );

      expect(results.length).toBeGreaterThan(1);

      const firstRecipe = results[0];
      expect(firstRecipe.name).toEqual('name 2');
      expect(firstRecipe.directions).toEqual('directions 2');
    });

    it('should load recipes without filters', async () => {
      const bundle = {};

      const results = await appTester(
        App.triggers.recipe.operation.perform,
        bundle,
      );

      expect(results.length).toBeGreaterThan(1);

      const firstRecipe = results[0];
      expect(firstRecipe.name).toEqual('name 1');
      expect(firstRecipe.directions).toEqual('directions 1');
    });
  });
});
```

You can run your test again and make sure everything still works:

```bash
zapier test
```

## 4. Deploy an integration

To take your local app integration and make it available to use in a Zap, you'll need to push it to Zapier.

You can have many versions of an app, which simplifies making breaking changes and testing in the future. For now, you will push a single version.

Since this is your first time pushing your app version, you'll need to register your app with Zapier. Run the `zapier register` command and Zapier will ask you to provide a name and some details about your app. Follow the prompt and then you can push your app using `zapier push`:

Zapier will ask you to provide a name and some details about your app with the `zapier register` command. Follow the prompts and then push your app again.

```
$ zapier push
✔ Copying project to temp directory
✔ Installing project dependencies
✔ Applying entry point file
✔ Building app definition.json
✔ Validating project schema and style
✔ Zipping project and dependencies
✔ Testing build
✔ Cleaning up temp directory
✔ Uploading version 1.0.0

Push complete! Built build/build.zip and build/source.zip and uploaded them to Zapier.
```

Log in and visit the [Zap editor](https://zapier.com/app/editor) to create a Zap with your new integration. 

For the trigger step, choose your app and the "New Recipe" trigger, where you can see the label and description that were defined in `triggers/recipe.js`.

In the Zap editor, see the input field `"style"` and fill it out. Run the trigger test and the `listRecipes` function associated with the trigger runs, making the API request and returning the result to Zapier. 

Go back to your terminal. Use the `zapier logs --type http` command to see the HTTP requests Zapier made. 

```
$ zapier logs --type http

The logs of your app "Example App" listed below.

┌────────┬────────┬────────────────────────────────────────────────────────┬───────────────┬─────────┬──────────────────────────────────────┬───────────────────────────┐
│ Status │ Method │ URL                                                    │ Querystring   │ Version │ Step                                 │ Timestamp                 │
├────────┼────────┼────────────────────────────────────────────────────────┼───────────────┼─────────┼──────────────────────────────────────┼───────────────────────────┤
│ 200    │ GET    │ http://57b20fb546b57d1100a3c405.mockapi.io/api/recipes │ style=italian │ 1.0.0   │ a9055e16-fc0d-4fb2-a3e6-9d442d1f70e8 │ 2016-09-13T15:11:30-05:00 │
└────────┴────────┴────────────────────────────────────────────────────────┴───────────────┴─────────┴──────────────────────────────────────┴───────────────────────────┘
  Most recent logs near the bottom.
```

## 5. Add authentication

Authentication is crucial to interacting with most APIs. Zapier supports a number of different [authentication schemes](https://github.com/zapier/zapier-platform/blob/main/packages/cli/README.md#authentication). In this example, you are going to set it up to include an API Key in a header.

For different types of authentication, see these example apps:

- [OAuth 2](https://github.com/zapier/zapier-platform/tree/master/example-apps/oauth2)
- [Basic Auth](https://github.com/zapier/zapier-platform/tree/master/example-apps/basic-auth)
- [Session Auth](https://github.com/zapier/zapier-platform/tree/master/example-apps/session-auth)
- [API Key](https://github.com/zapier/zapier-platform/tree/master/example-apps/custom-auth)

Define the `authentication` section for the example app you've built. In `index.js`, **add** the following to `module.exports`:

```javascript
  authentication: {
    type: 'custom',
    fields: [{ key: 'apiKey', type: 'string' }],
    test: async (z, bundle) => {
      const response = await z.request('http://57b20fb546b57d1100a3c405.mockapi.io/api/me');
      return response.data;
    },
  },
```

The above snippet defines the two required properties of `authentication`:

- `fields` is where we define our auth fields. This works similar to the `inputFields` of triggers. When users connect their account to Zapier, they'll be prompted to fill in this field, and the value they enter becomes available in the `bundle.authData`. Not every authentication type will include `inputFields`.
- `test` is a function used during the account connection process to verify that the user entered valid credentials. The goal of the function is to make an authenticated API request whose response indicates if the credentials are correct. A profile in the connected app, such as a `/me` endpoint, is a common choice. If valid, the test function can return anything. On invalid credentials, the test needs to raise an error. Since `z.request()` already throws an error for non-2xx responses, we don't need to throw an error explicitly in this case.

Next, make sure the API key is included in all the requests your app makes.

In `index.js`, **edit** the file to include:

```javascript
// Add this helper function above `module.exports`: 
const addApiKeyToHeader = (request, z, bundle) => {
  request.headers['My-Auth-Header'] = bundle.authData.apiKey;
  return request;
};

// module.exports = ...
```

The helper function `addApiKeyToHeader`, adds the user-provided API key as a request header called `My-Auth-Header`. The name chosen is illustrative, the header would be whatever the API you are integrating with requires. Sometimes, an API would require it in a query parameter instead of a header, and/or encoded first. You'll want to reference the API documentation for the expected format. 

Finally, to ensure the helper function takes effect, it needs to be registered in the app. 

In `index.js`, **edit** `module.exports` to also include:

```javascript
  beforeRequest: [
    addApiKeyToHeader, // new line of code
  ],
```

`beforeRequest` is a list of functions that are called before every HTTP request that uses `z.request`. It's where you add headers, query params, or whatever is needed to be within _all outbound requests_. With this addition, every outgoing HTTP request made by `z.request` will now have the API key added in a header.

The `zapier invoke` command has `auth test` subcommand that essentially calls the `authentication.test` function for you to verify the credentials locally. But first, you need to initialize the auth credentials with the `auth start` subcommand:

```
$ zapier invoke auth start
The .env file does not exist or is empty. You may need to set some environment variables in there if your code uses process.env.
? apiKey | string: mock-api-key
Auth data appended to .env file. Run `zapier invoke auth test` to test it.
```

Next, run the `auth test` subcommand to verify the credentials. You'll know you have the right API key if you can see the response data from the `/me` endpoint:

```
$ zapier invoke auth test 
✔ Invoking authentication.test
[
  {
    "id": "1",
    "createdAt": 1473801403,
    "userName": "userName 1"
  }
]
```

Re-push the app to Zapier to deploy the changes:

```bash
zapier push
```

Go back to your Zap at https://zapier.com/app/zaps. It will now have a new ["Account" item](https://cdn.zappy.app/9096a3bc1d6cd8147fb695bb460692b2.png) in your "New Recipe" trigger. 

Add an account by entering any value you like for the API key, the mock API does not care.

As soon as you add the account, Zapier will run your app's `authentication.test` function to confirm the credentials are valid.

We can verify the header is present in the request by looking at the logs again.

```
$ zapier logs --type http --detailed --limit=1

The logs of your app "Example App" listed below.

┌─────────────────────┬────────────────────────────────────────────────────────────────────────────────────────┐
│ Status              │ 200                                                                                    │
│ Method              │ GET                                                                                    │
│ URL                 │ http://57b20fb546b57d1100a3c405.mockapi.io/api/me                                      │
│ Querystring         │                                                                                        │
│ Version             │ 1.0.0                                                                                  │
│ Step                │                                                                                        │
│ Timestamp           │ 2016-09-16T15:57:51-05:00                                                              │
│ Request Headers     │ user-agent: Zapier                                                                     │
│                     │ My-Auth-Header: :censored:6:b1af149262:                                                │
│ Request Body        │                                                                                        │
│ Response Headers    │ server: Cowboy                                                                         │
│                     │ connection: close                                                                      │
│                     │ x-powered-by: Express                                                                  │
│                     │ access-control-allow-origin: *                                                         │
│                     │ access-control-allow-methods: GET,PUT,POST,DELETE,OPTIONS                              │
│                     │ access-control-allow-headers: X-Requested-With,Content-Type,Cache-Control,access_token │
│                     │ content-type: application/json                                                         │
│                     │ content-length: 59                                                                     │
│                     │ etag: "-80491811"                                                                      │
│                     │ vary: Accept-Encoding                                                                  │
│                     │ date: Fri, 16 Sep 2016 20:57:51 GMT                                                    │
│                     │ via: 1.1 vegur                                                                         │
│ Response Body       │ [{"id":"1","createdAt":1473801403,"userName":"userName 1"}]                            │
└─────────────────────┴────────────────────────────────────────────────────────────────────────────────────────┘
```

You can see from the detailed log that the request included our auth header. The value appears as `:censored:6:b1af149262:`, which is intentional. Zapier does not log authentication credentials in plain text.

## 6. Invite team members to help manage your integration

Share your integration with your team of fellow developers so it shows up in their [developer dashboard](https://developer.zapier.com/).

From the Zapier CLI, run either of these:

- `zapier team:add user@example.com admin` to invite a team member [as an admin](https://platform.zapier.com/manage/add-team) for the app.
- `zapier team:add user@example.com collaborator` to invite a team member [as a collaborator](https://platform.zapier.com/manage/add-team) for the app.

Replace the example email address with the user you want to invite. 

## 7. Share users to your integration

Once you have at least one trigger or action, you'll want to share your integration with some of your users. Early feedback helps make sure you’re building functionality that will be used. 

From the Zapier CLI, run `zapier users:add user@example.com 1.0.0` to email this user to let them view and use the app version 1.0.0 in their Zaps.

Replace the example email address with the user you want to invite. You'll see a confirmation prompt, type `Y`. 

The alternative way to invite anyone to use your app in their Zaps is via a link to the app. Run `zapier users:links` to see a public sharing link per specific version or a link to all versions. The link looks something like `https://zapier.com/platform/public-invite/1/222dcd03aed943a8676dc80e2427a40d/`. You can put this in your help docs, post it to your website, add it to your email campaign, etc. Access shared via these links cannot be revoked once shared with your users. 

## 8. Modify your integration

If you need to make any changes to your integration in [a new version](https://github.com/zapier/zapier-platform/blob/main/packages/cli/README.md#deploying-an-app-version). Versions helps to track and manage changes to your integration over time.

Public integrations or private integrations with more than 5 users **require** a new version to make any edits. It is still recommended to make changes for private integrations with fewer than 5 users in a new version as well and [consider Zapier's best practices](https://platform.zapier.com/manage/making-changes) when doing so. 

Integrations created with the Platform CLI cannot be edited in the Platform UI. You can’t add triggers or actions, edit code or configurations - these options will be grayed out in the UI.

The following details of your CLI integration can be managed from the UI if preferred: 

- Invite team members
- Monitor integration usage
- Submit your integration to be made publicly available
- Promote a new integration version to public
- Migrate users between versions

## Learn more

- [Z object](https://github.com/zapier/zapier-platform/blob/master/packages/cli/README.md#z-object)
- [Bundle object](https://github.com/zapier/zapier-platform/blob/master/packages/cli/README.md#bundle-object) for functionalities available within the `perform` functions
- [Different authentication schemes and search/create implementations examples](https://github.com/zapier/zapier-platform/tree/main/example-apps)
- [Interactive tutorial](https://developer.zapier.com/cli-guide/introduction) that uses the GitHub API (a little outdated)
- About [different types of support](https://platform.zapier.com/quickstart/support) available to help you build your integration
