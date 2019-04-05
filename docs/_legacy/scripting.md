---
title: Zapier Legacy Web Builder Scripting
order: 4
layout: post-toc
redirect_from: /legacy/
---

# Zapier Legacy Web Builder Scripting

> **Caution**: Do not use this documentation with new integrations built in Zapier's Platform CLI or UI visual builder. For new integrations, use [Zapier's new visual builder](https://platform.zapier.com/docs/intro) or the [Zapier Command Line Interface](https://zapier.github.io/zapier-platform-cli/) to build an integration in code.
> 
> If you have an existing integration built with Zapier's legacy web builder, or have migrated a legacy web builder integration to the new Zapier Platform UI, use this doc to edit and maintain your existing scripts.

Zapier's Web Builder scripting functionality allows you to manipulate the requests and responses that are exchanged between your app's API and Zapier Legacy Web Builder Integrations.

You can modify HTTP requests just before they are sent and can parse responses before Zapier does anything with them. This enables you to do things like:

*   Set unique HTTP Headers
*   Modify the request URL based on user's input criteria.
*   Construct unique URL query strings like filters.
*   Turn XML or other serialization formats into properly formatted JSON primitives.
*   Create completely new keys on JSON objects for user consumption (like turning 1000 into $10.00).

Scripting works by giving you places to add your own code to the request-response cycle. To add a method, click the edit code button on your App's developer dashboard:

![Edit Code button](https://cdn.zapier.com/storage/photos/832a4038e1e1608158f0bcf383338598.png)

Inside the editor, you will create the root module `Zap`. By default it is a blank JavaScript object. You add to it by defining one or more of the [available methods](https://platform.zapier.com/legacy/scripting/#available-methods). Each method accepts a single variable called `bundle`, which is a JSON serializable object. The content of the bundle varies depending on the method you are implementing. The output of your method must alshttps://platform.zapier.com/legacy/o be a serializable object.

Below is an example of implementing a method to be a pass-through:

```javascript
var Zap = {
  my_trigger_pre_poll: function(bundle) {
    // your code to modify bundle.request before sent
    return bundle.request;
  }
}
```

**Note**: All code written in the Scripting API must adhere to [strict mode](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Strict_mode), which is a subset of Javascript. Any issues with your code that violate this will now be shown in the Scripting API editor with red X marks in the sidebar. The code will run in Node.js 4.3.2.

## Limits and Considerations

Scripting is powerful, but not unlimitedly so.

When writing your code, make it lean and run fast.

Some hard limits are that each method needs to run in under 30 seconds, and it won't process request/response payloads larger than ~5 MB.

## Available Methods

There are a variety of methods for manipulating requests Zapier makes to your API. Below is the complete list of methods you can use in scripting. You may provide any, all, or none of these methods.

### Trigger Methods

Many of the trigger methods follow a naming pattern of key + method name, where key is the key given to the trigger when you created it. Below, we use the convention of `KEY` as the placeholder for the trigger's  actual key. For example, if you define a trigger with the key "my_trigger" and you want to implement the pre_poll method, you would write a method called `my_trigger_pre_poll`.

### Polling

#### `KEY_pre_poll`
Runs before the request to the polling URL, can modify the request before it is sent.

```javascript
var Zap = {
  KEY_pre_poll: function(bundle) {
    /* 
    Argument:
      bundle.request.method: <string> # "GET"
      bundle.request.url: <string>
      bundle.request.auth: <array>
      bundle.request.headers: <object>
      bundle.request.params: <object>

      bundle.url_raw: <string>
      bundle.auth_fields: <object>
      bundle.trigger_fields: <object> # the fields provided by the user during setup
      bundle.zap: <object> # info about the zap
      bundle.meta: <object> # extra runtime information you can use

    The response should be bundle.request or a similar object
    */
    return {
      url: bundle.request.url,
      method: bundle.request.method,
      auth: bundle.request.auth,
      headers: bundle.request.headers,
      params: bundle.request.params,
      data: bundle.request.data
    }; // or return bundle.request;
  }
}
```

See [bundle.request](https://platform.zapier.com/legacy/scripting#prepared-request-via-bundlerequest).

> **Note**: This code is only valid for Zapier's legacy web builder, and is mostly incompatible with Zapier [CLI](https://zapier.com/developer/documentation/v2/getting-started-cli/) and [visual builder](https://zapier.com/developer/documentation/v2/visual-builder-getting-started/).

#### `KEY_post_poll`
Runs after we receive a response from the polling URL. Can parse the response to format the data that enters Zapier or throw an [exception](https://platform.zapier.com/legacy/scripting/#available-exceptions). We will throw for status codes 4xx and 5xx after the method runs automatically.

```javascript
var Zap = {
  KEY_post_poll: function(bundle) {
    /* 
    Argument:
      bundle.response.status_code: <integer>
      bundle.response.headers: <object>
      bundle.response.content: <str>

      bundle.request: <original object from KEY_pre_poll bundle>

      bundle.auth_fields: <object>
      bundle.trigger_fields: <object> # the fields provided by the user during setup
      bundle.zap: <object> # info about the zap
      bundle.meta: <object> # extra runtime information you can use

    The response should be JSON serializable:
      [
        <object>, # with unique 'id' key
        <object> # with unique 'id' key
      ]
    */
    return [];
  }
}
```
> **Note**: This code is only valid for Zapier's legacy web builder, and is mostly incompatible with Zapier [CLI](https://zapier.com/developer/documentation/v2/getting-started-cli/) and [visual builder](https://zapier.com/developer/documentation/v2/visual-builder-getting-started/).

#### `KEY_poll`
Runs in place of pre_poll and post_poll. You get a bundle and are expected to make the request and return a list of results or throw an [exception](https://platform.zapier.com/legacy/scripting/#available-exceptions). We will **not** throw for status codes like 4xx and 5xx automatically!

```javascript
var Zap = {
  KEY_poll: function(bundle) {
    /* 
    Arguments:
      bundle.request.method: <string> # "GET"
      bundle.request.url: <string>
      bundle.request.auth: <array>
      bundle.request.headers: <object>
      bundle.request.params: <object>

      bundle.url_raw: <string>
      bundle.auth_fields: <object>
      bundle.trigger_fields: <object> # the fields provided by the user during setup
      bundle.zap: <object> # info about the zap
      bundle.meta: <object> # extra runtime information you can use

      If you include a callback in the arguments, you can also perform async:
        callback(err, response)

    You are expected to make the request yourself. The response should be JSON serializable:
      [
        <object>, # with unique 'id' key
        <object> # with unique 'id' key
      ]
    */
    return []; // or callback(null, [])
  }
}
```

See [bundle.request](https://platform.zapier.com/legacy/scripting#prepared-request-via-bundlerequest).

> **Note**: This code is only valid for Zapier's legacy web builder, and is mostly incompatible with Zapier [CLI](https://zapier.com/developer/documentation/v2/getting-started-cli/) and [visual builder](https://zapier.com/developer/documentation/v2/visual-builder-getting-started/).

### Static and REST Hooks

#### `KEY_catch_hook`
Runs when we receive a static or subscription hook from your API. Can parse the response to format the data that enters Zapier.

```javascript
var Zap = {
  KEY_catch_hook: function(bundle) {
    /*
    Argument:
      bundle.request.method: <str> # 'GET', 'POST', 'PATCH', 'PUT', 'DELETE'
      bundle.request.headers: <object>
      bundle.request.querystring: <str> # parse with $.param(bundle.request.querystring)
      bundle.request.content: <str>

      bundle.cleaned_request: <object> or <array> # our best guess at parsing
                                                  # and combining the request
                                                  # (including handling JSON & XML).
      bundle.auth_fields: <object>
      bundle.trigger_fields: <object> # the fields provided by the user during setup
      bundle.zap: <object> # info about the zap

    The response should be either a JSON serializable array...
      [
        <object>,
        <object>
      ]

    ...or a single object:
      <object>
    */
    return []; // or {}
  }
}
```
> **Note**: This code is only valid for Zapier's legacy web builder, and is mostly incompatible with Zapier [CLI](https://zapier.com/developer/documentation/v2/getting-started-cli/) and [visual builder](https://zapier.com/developer/documentation/v2/visual-builder-getting-started/).

### REST Hooks and Notification REST Hooks

#### `pre_subscribe`
Runs before we subscribe.

```javascript
var Zap = {
  pre_subscribe: function(bundle) {
    /*
    Argument:
      bundle.request.method: <string> # "POST"
      bundle.request.url: <string>
      bundle.request.auth: <array>
      bundle.request.headers: <object>
      bundle.request.params: <object>
      bundle.request.data: <string>

      bundle.auth_fields: <object>
      bundle.trigger_fields: <object> # the data from trigger fields
      bundle.target_url: <string> # our unique Zapier url for this subscription
      bundle.event: <string> # the event being subscribed to
      bundle.zap: <object> # info about the zap

    The response should be bundle.request or a similar object
    */
    return {
      url: bundle.request.url,
      method: bundle.request.method,
      auth: bundle.request.auth,
      headers: bundle.request.headers,
      params: bundle.request.params,
      data: bundle.request.data
    }; // or return bundle.request;
  }
}
```

See [bundle.request](https://platform.zapier.com/legacy/scripting#prepared-request-via-bundlerequest).

> **Note**: This code is only valid for Zapier's legacy web builder, and is mostly incompatible with Zapier [CLI](https://zapier.com/developer/documentation/v2/getting-started-cli/) and [visual builder](https://zapier.com/developer/documentation/v2/visual-builder-getting-started/).

#### `post_subscribe`
Runs after we subscribe. It is exclusively for storing results that are needed later for pre_unsubscribe.

```javascript
var Zap = {
  post_subscribe: function(bundle) {
    /*
    Argument:
      bundle.response.status_code: <integer>
      bundle.response.headers: <object>
      bundle.response.content: <str>

      bundle.request: <original object from pre_subscribe bundle>

      bundle.target_url: <string> # our unique Zapier url for this subscription
      bundle.event: <string> # the event (if any) that was subscribed to
      bundle.auth_fields: <object>
      bundle.trigger_fields: <object> # the data from trigger fields
      bundle.zap: <object> # info about the zap

    The response should be JSON serializable, you'll have access to it as
    subscribe_data in the unsubscribe call. Normally you'd store some state
    about the hook resource you created, for example, some apps need
    an ID to locate and unsubscribe from a hook.

    */
    return ""; // or {}, or [] 
  }
}
```
> **Note**: This code is only valid for Zapier's legacy web builder, and is mostly incompatible with Zapier [CLI](https://zapier.com/developer/documentation/v2/getting-started-cli/) and [visual builder](https://zapier.com/developer/documentation/v2/visual-builder-getting-started/).

#### `pre_unsubscribe`
Runs before we unsubscribe.

```javascript
var Zap = {
  pre_unsubscribe: function(bundle) {
    /*
    Argument:
      bundle.request.method: <string> # "POST"
      bundle.request.url: <string>
      bundle.request.auth: <array>
      bundle.request.headers: <object>
      bundle.request.params: <object>
      bundle.request.data: <string>

      bundle.target_url: <string> # our unique Zapier url for this subscription
      bundle.subscribe_data <json> # any data you returned from post_subscribe
      bundle.event: <string> # the event (if any) being unsubscribed from
      bundle.auth_fields: <object>
      bundle.trigger_fields: <object> # the data from trigger fields
      bundle.zap: <object> # info about the zap

    The response should be bundle.request or a similar object
    */
    return {
      url: bundle.request.url,
      method: bundle.request.method,
      auth: bundle.request.auth,
      headers: bundle.request.headers,
      params: bundle.request.params,
      data: bundle.request.data
    }; // or return bundle.request;
  }
}
```

See [bundle.request](https://platform.zapier.com/legacy/scripting#prepared-request-via-bundlerequest).

> **Note**: This code is only valid for Zapier's legacy web builder, and is mostly incompatible with Zapier [CLI](https://zapier.com/developer/documentation/v2/getting-started-cli/) and [visual builder](https://zapier.com/developer/documentation/v2/visual-builder-getting-started/).

### Notification REST Hooks

#### `KEY_pre_hook`
Runs before the consuming call.

```javascript
var Zap = {
  KEY_pre_hook: function(bundle) {
    /*
    Argument:
      bundle.request.method: <string>
      bundle.request.headers: <object>
      bundle.request.querystring: <string> # parse using $.param(bundle.request.querystring)
      bundle.request.content: <string>

      bundle.auth_fields: <object>
      bundle.trigger_fields: <object> # the fields provided by the user during setup
      bundle.zap: <object> # info about the zap

    The response should be bundle.request or a similar object
    */
    return {
      url: bundle.request.url,
      method: bundle.request.method,
      auth: bundle.request.auth,
      headers: bundle.request.headers,
      params: bundle.request.params,
      data: bundle.request.data
    }; // or return bundle.request;
  }
}
```

See [bundle.request](https://platform.zapier.com/legacy/scripting#prepared-request-via-bundlerequest).

> **Note**: This code is only valid for Zapier's legacy web builder, and is mostly incompatible with Zapier [CLI](https://zapier.com/developer/documentation/v2/getting-started-cli/) and [visual builder](https://zapier.com/developer/documentation/v2/visual-builder-getting-started/).

#### `KEY_post_hook`
Runs after we receive a response from the consuming call. Can parse the response to format the data that enters Zapier or throw an [exception](https://platform.zapier.com/legacy/scripting/#available-exceptions). We will throw for status codes 4xx and 5xx after the method runs automatically.

```javascript
var Zap = {
  KEY_post_hook: function(bundle) {
    /*
    Argument:
      bundle.response.status_code: <integer>
      bundle.response.headers: <object>
      bundle.response.content: <str>

      bundle.request: <original object from KEY_pre_hook bundle>

      bundle.auth_fields: <object>
      bundle.trigger_fields: <object> # the fields provided by the user during setup
      bundle.zap: <object> # info about the zap

    The response should be JSON serializable:
      [
        <object>,
        <object>
      ]
    */
    return [];
  }
}
```

> **Note**: This code is only valid for Zapier's legacy web builder, and is mostly incompatible with Zapier [CLI](https://zapier.com/developer/documentation/v2/getting-started-cli/) and [visual builder](https://zapier.com/developer/documentation/v2/visual-builder-getting-started/).

### Available to all triggers

#### `KEY_pre_custom_trigger_fields`
Runs before the request to the custom field URL (if provided).

> Note: Although this method does not end with `result_fields` like there are for [actions](#key_pre_custom_action_fields) and [searches](#key_pre_custom_search_fields) it does in fact define custom fields and labels for the **result** (sample) of the trigger and not for its **Edit Template** step in the Zap Editor. See [Trigger Result Fields (Custom)](https://platform.zapier.com/legacy/trigger-fields-custom/).

```javascript
var Zap = {
  KEY_pre_custom_trigger_fields: function(bundle) {
    /*
    Argument:
      bundle.request.method: <string> # "GET"
      bundle.request.url: <string>
      bundle.request.auth: <array>
      bundle.request.headers: <object>
      bundle.request.params: <object>

      bundle.url_raw: <string>
      bundle.auth_fields: <object>
      bundle.trigger_fields: <object> # the fields provided by the user during setup
      bundle.zap: <object> # info about the zap

    The response should be bundle.request or a similar object
    */
    return {
      url: bundle.request.url,
      method: bundle.request.method,
      auth: bundle.request.auth,
      headers: bundle.request.headers,
      params: bundle.request.params,
      data: bundle.request.data
    }; // or return bundle.request;
  }
}
```

See [bundle.request](https://platform.zapier.com/legacy/scripting#prepared-request-via-bundlerequest).

> **Note**: This code is only valid for Zapier's legacy web builder, and is mostly incompatible with Zapier [CLI](https://zapier.com/developer/documentation/v2/getting-started-cli/) and [visual builder](https://zapier.com/developer/documentation/v2/visual-builder-getting-started/).

#### `KEY_post_custom_trigger_fields`
Runs after the response for custom fields is received. Can parse the response to format the data that enters Zapier or throw an [exception](https://platform.zapier.com/legacy/scripting/#available-exceptions). We will throw for status codes 4xx and 5xx after the method runs automatically.

> Note: Although this method does not end with `result_fields` like there are for [actions](#key_pre_custom_action_fields) and [searches](#key_pre_custom_search_fields) it does in fact define custom fields and labels for the **result** (sample) of the trigger and not for its **Edit Template** step in the Zap Editor. See [Trigger Result Fields (Custom)](https://platform.zapier.com/legacy/trigger-fields-custom/).

```javascript
var Zap = {
  KEY_post_custom_trigger_fields: function(bundle) {
    /*
    Argument:
      bundle.response.status_code: <integer>
      bundle.response.headers: <object>
      bundle.response.content: <str>

      bundle.request: <original object from KEY_pre_hook bundle>

      bundle.url_raw: <string>
      bundle.auth_fields: <object>
      bundle.trigger_fields: <object> # the fields provided by the user during setup
      bundle.zap: <object> # info about the zap

    The response should be JSON serializable:
      [
        # `type` can be unicode, int, bool
        # `key` should be unique and match a key found in the JSON representation we receive from your API
        # `label` is a human-readable name we can give this field in the UI
        {'type': <str>, 'key': <str>, 'label': <str>}
      ]
    */
    return [];
  }
}
```
> **Note**: This code is only valid for Zapier's legacy web builder, and is mostly incompatible with Zapier [CLI](https://zapier.com/developer/documentation/v2/getting-started-cli/) and [visual builder](https://zapier.com/developer/documentation/v2/visual-builder-getting-started/).

## Action Methods

Action methods follow a naming pattern of key + method name, where key is the key given to the action when you created it. Below, we use the convention of `KEY` as the placeholder for the action's actual key. For example, if you define an action with the key "my_action" and you want to implement the pre_write method, you would write a method called `my_action_pre_write`.

### `KEY_pre_write`
Runs before the request to the action URL, can modify the request before it is sent.

```javascript
var Zap = {
  KEY_pre_write: function(bundle) {
    /*
    Argument:
      bundle.request.method: <string> # "POST"
      bundle.request.url: <string>
      bundle.request.auth: <array>
      bundle.request.headers: <object>
      bundle.request.params: <object>
      bundle.request.data: <string>
      bundle.request.files: <object>

      bundle.url_raw: <string>
      bundle.auth_fields: <object>
      bundle.action_fields: <object> # pruned and replaced users' fields
      bundle.action_fields_full: <object> # all replaced users' fields
      bundle.action_fields_raw: <object> # before we replace users' variables
      bundle.zap: <object> # info about the zap

    The response should be bundle.request or a similar object
    */
    return {
      url: bundle.request.url,
      method: bundle.request.method,
      auth: bundle.request.auth,
      headers: bundle.request.headers,
      params: bundle.request.params,
      data: bundle.request.data
    }; // or return bundle.request;
  }
}
```

See [bundle.request](https://platform.zapier.com/legacy/scripting#prepared-request-via-bundlerequest).

> **Note**: This code is only valid for Zapier's legacy web builder, and is mostly incompatible with Zapier [CLI](https://zapier.com/developer/documentation/v2/getting-started-cli/) and [visual builder](https://zapier.com/developer/documentation/v2/visual-builder-getting-started/).


### `KEY_post_write`
Runs after we receive a response from the action endpoint, can modify the response or throw an [exception](https://platform.zapier.com/legacy/scripting/#available-exceptions). We will throw for status codes 4xx and 5xx after the method runs automatically. *Note:* If the action occurs as part of a search-or-create Zap, the output of this method is *not* exactly what the user sees. In that case, the action will be followed up with a request to fetch the written record, and we will present the user with the output from that follow-up request. If you need to modify the returned data in that scenario, use `_post_read_resource`.

```javascript
var Zap = {
  KEY_post_write: function(bundle) {
    /*
    Argument:
      bundle.response.status_code: <integer>
      bundle.response.headers: <object>
      bundle.response.content: <str>

      bundle.request: <original object from KEY_pre_write bundle>

      bundle.auth_fields: <object>
      bundle.action_fields: <object> # pruned and replaced users' fields
      bundle.action_fields_full: <object> # all replaced users' fields
      bundle.action_fields_raw: <object> # before we replace users' variables
      bundle.zap: <object> # info about the zap

    The response will be used to give the user more fields to use 
    in the next step of the Zap.  Please return a JSON serializable object.

    return <object>;
    */
  }
}
```
> **Note**: This code is only valid for Zapier's legacy web builder, and is mostly incompatible with Zapier [CLI](https://zapier.com/developer/documentation/v2/getting-started-cli/) and [visual builder](https://zapier.com/developer/documentation/v2/visual-builder-getting-started/).

### `KEY_write`
Runs in place of pre_write and post_write. You get a bundle and are expected to make the request and return the appropriate response or throw an [exception](https://platform.zapier.com/legacy/scripting/#available-exceptions). We will **not** throw for status codes like 4xx and 5xx automatically! *Note:* If the action occurs as part of a search-or-create Zap, the output of this method is *not* exactly what the user sees. In that case, the action will be followed up with a request to fetch the written record, and we will present the user with the output from that follow-up request. If you need to modify the returned data in that scenario, use `_post_read_resource`.

```javascript
var Zap = {
  KEY_write: function(bundle, [callback]) {
    /*
    Arguments:

      bundle.request.method: <string> # "POST"
      bundle.request.url: <string>
      bundle.request.auth: <array>
      bundle.request.headers: <object>
      bundle.request.params: <object>
      bundle.request.data: <string>
      bundle.request.files: <object>

      bundle.url_raw: <string>
      bundle.auth_fields: <object>
      bundle.action_fields: <object> # pruned and replaced users' fields
      bundle.action_fields_full: <object> # all replaced users' fields
      bundle.action_fields_raw: <object> # before we replace users' variables
      bundle.zap: <object> # info about the zap

    If you include a callback in the arguments, you can also perform async:
      callback(err, response)

    The response will be used to give the user more fields to use 
    in the next step of the Zap.  Please return a JSON serializable object.

    return <object>;
    */
    // your code to modify bundle.request before sent
    var response = z.request(bundle.request);
    return z.JSON.parse(response.content);
  }
}
```

See [bundle.request](https://platform.zapier.com/legacy/scripting#prepared-request-via-bundlerequest).

> **Note**: This code is only valid for Zapier's legacy web builder, and is mostly incompatible with Zapier [CLI](https://zapier.com/developer/documentation/v2/getting-started-cli/) and [visual builder](https://zapier.com/developer/documentation/v2/visual-builder-getting-started/).

### `KEY_pre_custom_action_fields`
Runs before the request to the custom field URL (if provided).

```javascript
var Zap = {
  KEY_pre_custom_action_fields: function(bundle) {
    /*
    Argument:
      bundle.request.method: <string> # "GET"
      bundle.request.url: <string>
      bundle.request.auth: <array>
      bundle.request.headers: <object>
      bundle.request.params: <object>

      bundle.url_raw: <string>
      bundle.auth_fields: <object>
      bundle.action_fields: <object> # the raw action fields (if applicable)
      bundle.zap: <object> # info about the zap (details below)

    The response should be bundle.request or a similar object
    */
    return {
      url: bundle.request.url,
      method: bundle.request.method,
      auth: bundle.request.auth,
      headers: bundle.request.headers,
      params: bundle.request.params,
      data: bundle.request.data
    }; // or return bundle.request;
  }
}
```

See [bundle.request](https://platform.zapier.com/legacy/scripting#prepared-request-via-bundlerequest).

> **Note**: This code is only valid for Zapier's legacy web builder, and is mostly incompatible with Zapier [CLI](https://zapier.com/developer/documentation/v2/getting-started-cli/) and [visual builder](https://zapier.com/developer/documentation/v2/visual-builder-getting-started/).

### `KEY_post_custom_action_fields`
Runs after the response for custom fields is received. Can parse the response to format the data that enters Zapier or throw an [exception](https://platform.zapier.com/legacy/scripting/#available-exceptions). We will throw for status codes 4xx and 5xx after the method runs automatically.

```javascript
var Zap = {
  KEY_post_custom_action_fields: function(bundle) {
    /*
    Argument:
      bundle.response.status_code: <integer>
      bundle.response.headers: <object>
      bundle.response.content: <str>

      bundle.request: <original object from KEY_pre_custom_action_fields bundle>

      bundle.url_raw: <string>
      bundle.auth_fields: <object>
      bundle.action_fields: <object> # the fields provided by the user during setup
      bundle.zap: <object> # info about the zap

    The response should be JSON serializable:
      [
        # `type` can be unicode, int, bool
        # `key` should be unique, and will be the "key" in "key: value" in the POST
        # `help_text` and `label` are also available
        {'type': <str>, 'key': <str>}
      ]
    */
    return []; // return fields in the order you want them displayed in the UI. They'll be appended after the regular action fields
  }
}
```

> **Note**: This code is only valid for Zapier's legacy web builder, and is mostly incompatible with Zapier [CLI](https://zapier.com/developer/documentation/v2/getting-started-cli/) and [visual builder](https://zapier.com/developer/documentation/v2/visual-builder-getting-started/).

### `KEY_custom_action_fields`
Allows you to completely take over the handling of retrieving and processing field metadata for custom action fields.  Pre- and Post- methods will not be called if you've implemented this method.  This method will be passed a bundle and must return an array of custom field metadata.  If a request to an endpoint fails, you will need to throw an exception - the platform will not do it automatically.

```javascript
var Zap = {KEY_custom_action_fields: function(bundle) {
    /*    
    Argument:      
        bundle.request.method: <string> # GET
        bundle.request.url: <string> # ""
        bundle.request.auth: <array>
        bundle.request.headers: <object>
        bundle.request.params: <object>

        bundle.url_raw: <string> # ""
        bundle.auth_fields: <object>
        bundle.action_fields: <object> # the raw action fields (if applicable)
        bundle.zap: <object> # info about the zap    

    The response should be JSON serializable:      
        [

            # "type": "unicode",
            # "key": "json_key", // the field "name", will be used to construct a label if none is provided
            # "required": false, // whether this field must be filled out. defaults to true
            # "label": "Pretty Label", // optional
            # "help_text": "Helps to explain things to users.", // optional
            # "choices": { // optional
                "raw": "label"
            } // can also be a flat array if raw is the label
            {'type': <str>, 'key': <str>}

         ]   
       */
       return []; // return fields in the order you want them displayed in the UI. They'll be appended after the regular action fields
    }
}
```

See [bundle.request](https://platform.zapier.com/legacy/scripting#prepared-request-via-bundlerequest).

> **Note**: This code is only valid for Zapier's legacy web builder, and is mostly incompatible with Zapier [CLI](https://zapier.com/developer/documentation/v2/getting-started-cli/) and [visual builder](https://zapier.com/developer/documentation/v2/visual-builder-getting-started/).

### `KEY_custom_action_result_fields`
Allows you to completely take over the handling of retrieving and processing field metadata for custom fields when users are working with *results* of your action in the Zap editor.  Pre- and Post- methods will not be called if you've implemented this method.  This method will be passed a bundle and must return an array of custom field metadata.  If a request to an endpoint fails, you will need to throw an exception - the platform will not do it automatically.

```javascript
var Zap = {KEY_custom_action_result_fields: function(bundle) {
    /*    
    Argument:      
        bundle.response.status_code: <integer>      
        bundle.response.headers: <object>      
        bundle.response.content: <str>      

        bundle.request: <original object from KEY_pre_custom_action_fields bundle>      

        bundle.url_raw: <string>      
        bundle.auth_fields: <object>      
        bundle.action_fields: <object> # the raw action fields (if applicable)
        bundle.zap: <object> # info about the zap    

    The response should be JSON serializable:      
        [        
            # `type` can be unicode, int, bool        
            # `key` should be unique, and will be the "key" in "key: value" in the response content        
            # `label` is also available       
            {'type': <str>, 'key': <str>, 'label': <str>}      
        ]    
       */
       return []; // return fields in the order you want them displayed in the UI. They'll be appended after the regular action fields
    }
}
```

> **Note**: This code is only valid for Zapier's legacy web builder, and is mostly incompatible with Zapier [CLI](https://zapier.com/developer/documentation/v2/getting-started-cli/) and [visual builder](https://zapier.com/developer/documentation/v2/visual-builder-getting-started/).

### `KEY_pre_custom_action_result_fields`
Runs before the request to the custom response fields URL (if provided).

```javascript
var Zap = {
  KEY_pre_custom_action_result_fields: function(bundle) {
    /*    
    Argument:      
        bundle.request.method: <string> # "GET"
        bundle.request.url: <string>
        bundle.request.auth: <array>
        bundle.request.headers: <object>
        bundle.request.params: <object>

        bundle.url_raw: <string>      
        bundle.auth_fields: <object>      
        bundle.action_fields: <object> # the raw action fields (if applicable)      
        bundle.zap: <object> # info about the zap (details below)    

    The response should be bundle.request or a similar object
    */
    return {
        url: bundle.request.url,
        method: bundle.request.method,
        auth: bundle.request.auth,
        headers: bundle.request.headers,
        params: bundle.request.params,
        data: bundle.request.data
    }; // or return bundle.request;
  }
}
```

See [bundle.request](https://platform.zapier.com/legacy/scripting#prepared-request-via-bundlerequest).

> **Note**: This code is only valid for Zapier's legacy web builder, and is mostly incompatible with Zapier [CLI](https://zapier.com/developer/documentation/v2/getting-started-cli/) and [visual builder](https://zapier.com/developer/documentation/v2/visual-builder-getting-started/).

### `KEY_post_custom_action_result_fields`
Runs after the response for custom response fields is received. Can parse the response to format the data that enters Zapier or throw an exception [exception](https://platform.zapier.com/legacy/scripting/#available-exceptions). We will throw for status codes 4xx and 5xx after the method runs automatically.

```javascript
var Zap = {
    KEY_post_custom_action_result_fields: function(bundle) {
    /*    
    Argument:      
        bundle.response.status_code: <integer>      
        bundle.response.headers: <object>      
        bundle.response.content: <str>      

        bundle.request: <original object from KEY_pre_custom_action_fields bundle>      

        bundle.url_raw: <string>      
        bundle.auth_fields: <object>            
        bundle.action_fields: <object> # the raw action fields (if applicable)      
        bundle.zap: <object> # info about the zap    
    The response should be JSON serializable:      
        [        
            # `type` can be unicode, int, bool        
            # `key` should be unique, and will be the "key" in "key: value" in the response content        
            # `label` is also available        
            {'type': <str>, 'key': <str>, 'label': <str>}      
        ]    
    */
        return []; // return fields in the order you want them displayed in the UI. They'll be appended after the regular action fields
    }
}
```

## Search Methods

Search methods follow a naming pattern of key + method name, where key is the key given to the search when you created it. Below, we use the convention of `KEY` as the placeholder for the search's actual key. For example, if you define an search with the key "my_search" and you want to implement the pre_search method, you would write a method called `my_search_pre_search`.

### `KEY_pre_search`
Runs before the request to the search URL, can modify the request before it is sent.

```javascript
var Zap = {
  KEY_pre_search: function(bundle) {
    /*
    Argument:
      bundle.request.method: <string> # "GET"
      bundle.request.url: <string>
      bundle.request.auth: <array>
      bundle.request.headers: <object>
      bundle.request.params: <object>

      bundle.url_raw: <string>
      bundle.auth_fields: <object>
      bundle.search_fields: <object> # pruned and replaced users' fields
      bundle.zap: <object> # info about the zap

    The response should be bundle.request or a similar object
    */
    return {
      url: bundle.request.url,
      method: bundle.request.method,
      auth: bundle.request.auth,
      headers: bundle.request.headers,
      params: bundle.request.params,
      data: bundle.request.data
    }; // or return bundle.request;
  }
}
```

See [bundle.request](https://platform.zapier.com/legacy/scripting#prepared-request-via-bundlerequest).

> **Note**: This code is only valid for Zapier's legacy web builder, and is mostly incompatible with Zapier [CLI](https://zapier.com/developer/documentation/v2/getting-started-cli/) and [visual builder](https://zapier.com/developer/documentation/v2/visual-builder-getting-started/).

### `KEY_post_search`
Runs after we receive a response from the search endpoint, can modify the response or throw an [exception](https://platform.zapier.com/legacy/scripting/#available-exceptions). We will throw for status codes 4xx and 5xx after the method runs automatically. *Note:* The output of the method is *not* exactly what the user sees. We follow searches up with requests for the individual resources and present the user with the output from those follow-up requests. If you wish to modify the number (or ordering) of the search results, use `_post_search`. If you wish to modify the data the user sees, use `_post_read_resource`. One other thing to be aware of is that searches must return an *array* of objects, so if your search endpoint returns a single object, you can use this method to wrap your object in an array.

> Note we'll only use the first object in the array for now, so if you can add optional fields to help narrow the search down, it's a great idea.

```javascript
var Zap = {
  KEY_post_search: function(bundle) {
    /*
    Argument:
      bundle.response.status_code: <integer>
      bundle.response.headers: <object>
      bundle.response.content: <str>

      bundle.request: <original object from KEY_pre_search bundle>

      bundle.auth_fields: <object>
      bundle.search_fields: <object> # pruned and replaced users' fields
      bundle.zap: <object> # info about the zap

    The response is an array, which may contain zero or more matches.

    If multiple matches are found, sort the array with the "best match" first.

    Use the available exceptions to vary errors.
    */
    return [ ]; // no matches
    /* --- or --- */
    return [ { ... } ];  // return a single match
    /* --- or --- */
    return [ { ... }, { ... }, ... ]; // several matches, with "best match" first
  }
}
```

> **Note**: This code is only valid for Zapier's legacy web builder, and is mostly incompatible with Zapier [CLI](https://zapier.com/developer/documentation/v2/getting-started-cli/) and [visual builder](https://zapier.com/developer/documentation/v2/visual-builder-getting-started/).

### `KEY_search`
Runs in place of pre_search and post_search. You get a bundle and are expected to make the request and return the appropriate response or throw an [exception](https://platform.zapier.com/legacy/scripting/#available-exceptions). We will **not** throw for status codes like 4xx and 5xx automatically! Note: The output of the method is not exactly what the user sees. We follow searches up with requests for the individual resources and present the user with the output from those follow-up requests. If you wish to modify the number (or ordering) of the search results, you can do that inside `_search`. If you wish to modify the data the user sees, use `_post_read_resource`.

> Note we'll only use the first object in the array for now, so if you can add optional fields to help narrow the search down, it's a great idea.

```javascript
var Zap = {
  KEY_search: function(bundle, [callback]) {
    /*
    Arguments:

      bundle.request.method: <string> # "GET"
      bundle.request.url: <string>
      bundle.request.auth: <array>
      bundle.request.headers: <object>
      bundle.request.params: <object>

      bundle.url_raw: <string>
      bundle.auth_fields: <object>
      bundle.search_fields: <object> # pruned and replaced users' fields

      bundle.zap: <object> # info about the zap

    If you include a callback in the arguments, you can also perform async:
      callback(err, response)

    The response will be used to give the user more fields to use 
    in the next step of the Zap.  Please return a JSON serializable object.
    */

    return {...}; // or callback(null, {...})
  }
}
```

See [bundle.request](https://platform.zapier.com/legacy/scripting#prepared-request-via-bundlerequest).

> **Note**: This code is only valid for Zapier's legacy web builder, and is mostly incompatible with Zapier [CLI](https://zapier.com/developer/documentation/v2/getting-started-cli/) and [visual builder](https://zapier.com/developer/documentation/v2/visual-builder-getting-started/).

### `KEY_pre_custom_search_fields`
Runs before the request to the custom field URL (if provided).

```javascript
var Zap = {
  KEY_pre_custom_search_fields: function(bundle) {
    /*
    Argument:
      bundle.request.method: <string> # "GET"
      bundle.request.url: <string>
      bundle.request.auth: <array>
      bundle.request.headers: <object>
      bundle.request.params: <object>

      bundle.url_raw: <string>
      bundle.auth_fields: <object>
      bundle.search_fields: <object> # the raw search fields (if applicable)

      bundle.zap: <object> # info about the zap (details below)

    The response should be bundle.request or a similar object
    */
    return {
      url: bundle.request.url,
      method: bundle.request.method,
      auth: bundle.request.auth,
      headers: bundle.request.headers,
      params: bundle.request.params,
      data: bundle.request.data
    }; // or return bundle.request;
  }
}
```

See [bundle.request](https://platform.zapier.com/legacy/scripting#prepared-request-via-bundlerequest).

> **Note**: This code is only valid for Zapier's legacy web builder, and is mostly incompatible with Zapier [CLI](https://zapier.com/developer/documentation/v2/getting-started-cli/) and [visual builder](https://zapier.com/developer/documentation/v2/visual-builder-getting-started/).

### `KEY_post_custom_search_fields`
Runs after the response for custom fields is received. Can parse the response to format the data that enters Zapier or throw an [exception](https://platform.zapier.com/legacy/scripting/#available-exceptions). We will throw for status codes 4xx and 5xx after the method runs automatically.

```javascript
var Zap = {
  KEY_post_custom_search_fields: function(bundle) {
    /*
    Argument:
      bundle.response.status_code: <integer>
      bundle.response.headers: <object>
      bundle.response.content: <str>

      bundle.request: <original object from KEY_pre_custom_search_fields bundle>

      bundle.url_raw: <string>
      bundle.auth_fields: <object>
      bundle.zap: <object> # info about the zap

    The response should be JSON serializable:
      [
        # `type` can be unicode, int, bool
        # `key` should be unique, and will be the "key" in "key: value" in the POST
        # `help_text` and `label` are also available
        {'type': <str>, 'key': <str>}
      ]
    */
    return []; // return fields in the order you want them displayed in the UI. They'll be appended after the regular search fields
  }
}
```

> **Note**: This code is only valid for Zapier's legacy web builder, and is mostly incompatible with Zapier [CLI](https://zapier.com/developer/documentation/v2/getting-started-cli/) and [visual builder](https://zapier.com/developer/documentation/v2/visual-builder-getting-started/).

### `KEY_custom_search_fields`
Allows you to completely take over the handling of retrieving and processing field metadata for custom search action fields.  Pre- and Post- methods will not be called if you've implemented this method.  This method will be passed a bundle and must return an array of custom field metadata.  If a request to an endpoint fails, you will need to throw an exception - the platform will not do it automatically.

```javascript
var Zap = {KEY_custom_search_fields: function(bundle)
  {
    /*    
    Argument:      
      bundle.request.method: <string> # "GET"
      bundle.request.url: <string>
      bundle.request.auth: <array>
      bundle.request.headers: <object>
      bundle.request.params: <object>

      bundle.auth_fields: <object>      
      bundle.zap: <object> # info about the zap    
    The response should be JSON serializable:      
    [        
      # `type` can be unicode, int, bool        
      # `key` should be unique, and will be the "key" in "key: value" in the POST        
      # `help_text` and `label` are also available        
      {'type': <str>, 'key': <str>}      
    ]    
    */
  return []; // return fields in the order you want them displayed in the UI. They'll be appended after the regular search fields
}
}
```

See [bundle.request](https://platform.zapier.com/legacy/scripting#prepared-request-via-bundlerequest).

> **Note**: This code is only valid for Zapier's legacy web builder, and is mostly incompatible with Zapier [CLI](https://zapier.com/developer/documentation/v2/getting-started-cli/) and [visual builder](https://zapier.com/developer/documentation/v2/visual-builder-getting-started/).

### `KEY_custom_search_result_fields`
Allows you to completely take over the handling of retrieving and processing field metadata for custom fields when users are working with *results* of your search action in the Zap editor.  Pre- and Post- methods will not be called if you've implemented this method.  This method will be passed a bundle and must return an array of custom field metadata.  If a request to an endpoint fails, you will need to throw an exception - the platform will not do it automatically.

```javascript
var Zap = {
    KEY_custom_search_result_fields: function(bundle) {
        /*
        Argument:
            bundle.response.status_code: <integer>
            bundle.response.headers: <object>
            bundle.response.content: <str>

            bundle.request: <original object from KEY_pre_custom_search_fields bundle>

            bundle.url_raw: <string>
            bundle.auth_fields: <object>
            bundle.zap: <object> # info about the zap
       The response should be JSON serializable:
           [
               # `type` can be unicode, int, bool
               # `key` should be unique, and will be the "key" in "key: value" in the response content
               # `label` should be provided
               # `important` is optional
               {'type': <str>, 'key': <str>, 'label': <str>, 'important': <str>}
           ]
        */
        return []; // return fields in the order you want them displayed in the UI. They'll be appended after the regular search fields
    }
}
```

> **Note**: This code is only valid for Zapier's legacy web builder, and is mostly incompatible with Zapier [CLI](https://zapier.com/developer/documentation/v2/getting-started-cli/) and [visual builder](https://zapier.com/developer/documentation/v2/visual-builder-getting-started/).

### `KEY_pre_custom_search_result_fields`
Runs before the request to the custom search result field URL (if provided)

```javascript
var Zap = {
    KEY_pre_custom_search_result_fields: function(bundle) {
    /*    
    Argument:      
        bundle.request.method: <string> # "GET"
        bundle.request.url: <string>
        bundle.request.auth: <array>
        bundle.request.headers: <object>
        bundle.request.params: <object>

        bundle.url_raw: <string>      
        bundle.auth_fields: <object>      
        bundle.search_fields: <object> # the raw search fields (if applicable)      
        bundle.zap: <object> # info about the zap (details below)    

    The response should be bundle.request or a similar object
    */
        return {
            url: bundle.request.url,
            method: bundle.request.method,
            auth: bundle.request.auth,
            headers: bundle.request.headers,
            params: bundle.request.params,
            data: bundle.request.data
        }; // or return bundle.request;
    }
}
```

See [bundle.request](https://platform.zapier.com/legacy/scripting#prepared-request-via-bundlerequest).

> **Note**: This code is only valid for Zapier's legacy web builder, and is mostly incompatible with Zapier [CLI](https://zapier.com/developer/documentation/v2/getting-started-cli/) and [visual builder](https://zapier.com/developer/documentation/v2/visual-builder-getting-started/).

### `KEY_post_custom_result_search_fields`
Runs after the response for custom search result fields is received. Can parse the response to format the data that enters Zapier or throw an [exception](https://platform.zapier.com/legacy/scripting/#available-exceptions). We will throw for status codes 4xx and 5xx after the method runs automatically.

```javascript
var Zap = {
    KEY_post_custom_search_result_fields: function(bundle) {
    /*    
    Argument:      
        bundle.response.status_code: <integer>      
        bundle.response.headers: <object>      
        bundle.response.content: <str>      

        bundle.request: <original object from KEY_pre_custom_search_fields bundle>      

        bundle.url_raw: <string>      
        bundle.auth_fields: <object>      
        bundle.zap: <object> # info about the zap    
    The response should be JSON serializable:      
           [        
               # `type` can be unicode, int, bool        
               # `key` should be unique, and will be the "key" in "key: value" in the response content        
               # `label` should be provided
               # `important` is optional
               {'type': <str>, 'key': <str>, 'label': <str>, 'important': <str>}
           ]     
    */
        return []; // return fields in the order you want them displayed in the UI. They'll be appended after the regular search fields
    }
}
```

> **Note**: This code is only valid for Zapier's legacy web builder, and is mostly incompatible with Zapier [CLI](https://zapier.com/developer/documentation/v2/getting-started-cli/) and [visual builder](https://zapier.com/developer/documentation/v2/visual-builder-getting-started/).

### `KEY_pre_read_resource`
Runs before we do the request to read an individual resource. Use to modify the request before it is sent.

```javascript
var Zap = {
  KEY_pre_read_resource: function(bundle) {
    /*
    Argument:
      bundle.request.method: <string> # "GET"
      bundle.request.url: <string>
      bundle.request.auth: <array>
      bundle.request.headers: <object>
      bundle.request.params: <object>

      bundle.url_raw: <string>
      bundle.auth_fields: <object>
      bundle.read_fields: <object> # the response data from the search (or the write in case of search-or-create)
      bundle.read_context: <object> # the original params passed into the search (or the write in case of search-or-write)
      bundle.zap: <object> # info about the zap (details below)

    The response should be bundle.request or a similar object
    */
    return {
      url: bundle.request.url,
      method: bundle.request.method,
      auth: bundle.request.auth,
      headers: bundle.request.headers,
      params: bundle.request.params,
      data: bundle.request.data
    }; // or return bundle.request;
  }
}
```

See [bundle.request](https://platform.zapier.com/legacy/scripting#prepared-request-via-bundlerequest).

> **Note**: This code is only valid for Zapier's legacy web builder, and is mostly incompatible with Zapier [CLI](https://zapier.com/developer/documentation/v2/getting-started-cli/) and [visual builder](https://zapier.com/developer/documentation/v2/visual-builder-getting-started/).

### `KEY_post_read_resource`
Runs after we do the request to read an individual resource. Use to modify the data returned or throw an [exception](https://platform.zapier.com/legacy/scripting/#available-exceptions). We will throw for status codes 4xx and 5xx after the method runs automatically.

```javascript
var Zap = {
  KEY_post_read_resource: function(bundle) {
    /*
    Argument:
      bundle.response.status_code: <integer>
      bundle.response.headers: <object>
      bundle.response.content: <str>

      bundle.request: <original object from KEY_pre_read_resource bundle>

      bundle.url_raw: <string>
      bundle.auth_fields: <object>
      bundle.read_fields: <object> # the response data from the search (or the write in case of search-or-create)
      bundle.read_context: <object> # the original params passed into the search (or the write in case of search-or-write)

      bundle.zap: <object> # info about the zap

    The response will be used to give the user more fields to use 
    in the next step of the Zap.  Please return a JSON serializable object.

    return <object>;
    */
    return {...};
  }
}
```

> **Note**: This code is only valid for Zapier's legacy web builder, and is mostly incompatible with Zapier [CLI](https://zapier.com/developer/documentation/v2/getting-started-cli/) and [visual builder](https://zapier.com/developer/documentation/v2/visual-builder-getting-started/).

### `KEY_read_resource`
Runs in place of pre_read_resource and post_read_resource. You get a bundle and are expected to make the request and return the appropriate response or throw an [exception](https://platform.zapier.com/legacy/scripting/#available-exceptions). We will **not** throw for status codes like 4xx and 5xx automatically! 

```javascript
var Zap = {
  KEY_read_resource: function(bundle, [callback]) {
    /*
    Arguments:

      bundle.request.method: <string> # "GET"
      bundle.request.url: <string>
      bundle.request.auth: <array>
      bundle.request.headers: <object>
      bundle.request.params: <object>

      bundle.url_raw: <string>
      bundle.auth_fields: <object>
      bundle.read_fields: <object> # the response data from the search (or the write in case of search-or-create)
      bundle.read_context: <object> # the original params passed into the search (or the write in case of search-or-write)

      bundle.zap: <object> # info about the zap

    If you include a callback in the arguments, you can also perform async:
      callback(err, response)

      The response should be an object representing the resource. Can also use the available exceptions to vary errors.
    */
    return {...}; // or callback(null, {...})
  }
}
```

See [bundle.request](https://platform.zapier.com/legacy/scripting#prepared-request-via-bundlerequest).

> **Note**: This code is only valid for Zapier's legacy web builder, and is mostly incompatible with Zapier [CLI](https://zapier.com/developer/documentation/v2/getting-started-cli/) and [visual builder](https://zapier.com/developer/documentation/v2/visual-builder-getting-started/).

## Authentication Methods

### `pre_oauthv2_token`
Modify the request we'd send to the access token endpoint.

> Be aware that for legacy reasons the request does not follow [RFC6749](https://tools.ietf.org/html/rfc6749#section-4.1.3) and passes the parameters via the query string. If you define `pre_oauthv2_token` then it is up to you correct this if needed. Without the method, we will retry the request conform standards if the API returns an error on the first attempt.

```javascript
var Zap = {
  pre_oauthv2_token: function(bundle) {
    /*
    Argument:
      bundle.request.method: <string> # "POST"
      bundle.request.url: <string>
      bundle.request.auth: <array>
      bundle.request.headers: <object> # {"Accept": "application/json", "Content-Length": 0}
      bundle.request.params: <object> client_id, client_secret, redirect_uri, grant_type:authorization_code, code

      bundle.load: <object> # identical to bundle.request.params
      bundle.oauth_data: <object> # obj that contains your client_id, client_secret, etc...
      bundle.zap: <object> # info about the zap

    The response should be an object of:
      url: <string>
      method: <string> # 'GET', 'POST', 'PATCH', 'PUT', 'DELETE'
      headers: <object>
      params: <object> # this will be mapped into the query string
      data: <string> or null # request body: optional if POST, not needed if GET
    */
    return {
      url: bundle.request.url,
      method: bundle.request.method,
      headers: bundle.request.headers,
      params: bundle.request.params,
      data: bundle.request.data
    }; // or return bundle.request;
  }
}
```

See [bundle.request](https://platform.zapier.com/legacy/scripting#prepared-request-via-bundlerequest).

> **Note**: This code is only valid for Zapier's legacy web builder, and is mostly incompatible with Zapier [CLI](https://zapier.com/developer/documentation/v2/getting-started-cli/) and [visual builder](https://zapier.com/developer/documentation/v2/visual-builder-getting-started/).

### `post_oauthv2_token`
Modify the response from the access token endpoint or throw an [exception](https://platform.zapier.com/legacy/scripting/#available-exceptions). We will throw for status codes 4xx and 5xx **before** the method runs automatically.

```javascript
var Zap = {
  post_oauthv2_token: function(bundle) {
    /* 
    Argument:
      bundle.response.status_code: <integer>
      bundle.response.headers: <object>
      bundle.response.content: <str>

      bundle.oauth_data: <object> # client id/secret and oauth related URLs
      bundle.auth_fields: <object>
    */
    // If you have defined extra fields besides access_token 
    // and refresh_token in the Extra Requested Fields setup,
    // you may return them here as well.
    return z.JSON.parse(bundle.response.content);
  }
}
```

> **Note**: This code is only valid for Zapier's legacy web builder, and is mostly incompatible with Zapier [CLI](https://zapier.com/developer/documentation/v2/getting-started-cli/) and [visual builder](https://zapier.com/developer/documentation/v2/visual-builder-getting-started/).

### ` pre_oauthv2_refresh`
Modify the request we'd send to the refresh token endpoint. Only use if you have set the auth type for your App to be OAuth V2 with Refresh.

```javascript
var Zap = {
  pre_oauthv2_refresh: function(bundle) {
    /*
    Argument:
      bundle.request.method: <string> # "POST"
      bundle.request.url: <string>
      bundle.request.auth: <array>
      bundle.request.headers: <object>
      bundle.request.data: <object> # client_id, client_secret, refresh_token, grant_type

      bundle.load: <object> # same as bundle.request.data
      bundle.auth_fields: <object>
      bundle.oauth_data: <object> # obj that contains your client_id, client_secret, etc...
      bundle.zap: <object> # info about the zap

    The response should be an object of:
      url: <string>
      method: <string> # 'GET', 'POST', 'PATCH', 'PUT', 'DELETE'
      headers: <object>
      params: <object> # this will be mapped into the query string
      data: <string> or null # request body: optional if POST, not needed if GET
    */
    return {
      url: bundle.request.url,
      method: bundle.request.method,
      headers: bundle.request.headers,
      params: bundle.request.params,
      data: bundle.request.data
    }; // or return bundle.request;
  }
}
```

See [bundle.request](https://platform.zapier.com/legacy/scripting#prepared-request-via-bundlerequest).

> **Note**: This code is only valid for Zapier's legacy web builder, and is mostly incompatible with Zapier [CLI](https://zapier.com/developer/documentation/v2/getting-started-cli/) and [visual builder](https://zapier.com/developer/documentation/v2/visual-builder-getting-started/).

### `get_session_info`
Zapier exposes a `get_session_info()` function for APIs that require any form of session-based authorization. Feel free to use the following skeleton function to inspire your session authorization:

 > Zapier will only invoke this function on an as-needed basis. It will be called when your API returns a 401 or when you raise an `InvalidSessionException` in your `KEY_post_poll` or `KEY_post_write` functions. We will retry the request if the function returns new session info successfully.
  
```javascript
Zap = {
  get_session_info: function(bundle) {
    /*
    Argument:
      bundle.auth_fields: <object>      
      bundle.zap: <object> # info about the zap
    */

    // Make z.request calls as needed. 

    // Returned object will be mixed into bundle.auth_fields in future calls.
    return {'api_key': api_key};
  }
};
```

> **Note**: This code is only valid for Zapier's legacy web builder, and is mostly incompatible with Zapier [CLI](https://zapier.com/developer/documentation/v2/getting-started-cli/) and [visual builder](https://zapier.com/developer/documentation/v2/visual-builder-getting-started/).

### `get_connection_label`
Zapier exposes a `get_connection_label()` function for APIs that need customization on their Connection Label:

> Zapier will only invoke this function after the authentication is tested (when a new account is connected, and when the "test" button is pressed).
  
```javascript
Zap = {
  get_connection_label: function(bundle) {
    /*
    Argument:
      bundle.test_result: <object> # results from the test trigger, if it returned an object
      bundle.auth_fields: <object>
      bundle.zap: <object> # info about the zap
    */

   // Make z.request calls as needed. 

    // Returned string will be used as a Connection Label.
    // Please note it should be short and easily identifiable
    return 'contact@zapier.com';
  }
};
```

> **Note**: This code is only valid for Zapier's legacy web builder, and is mostly incompatible with Zapier [visual builder](https://platform.zapier.com/docs/intro) or the [Zapier CLI](https://zapier.github.io/zapier-platform-cli/).

## Built-in Functions and Tools

### Available Libraries

Our scripting engine uses JavaScript. As you'd expect, it provides the standard JavaScript interfaces (JSON, Math, Date and more) as well as `$` for jQuery (1.8.3),  `_` for Underscore (1.4.4), and `moment` for Moment.js (2.0.0 with timezone), `crypto`, and `async` (0.2.9). Plus, it has some handy Zapier specific tools on the `z` object!

> **Note:** Do not use Underscore's collection methods (`_.each()`, `_.map()`...) on objects. This [will break](https://github.com/jashkenas/underscore/issues/2407#issuecomment-169541016) if the object has a `length` property. Use `Object.keys(obj, fn)` instead.

### Unavailable Objects

Some "common" objects you might expect to find we don't provide access to include `root`, `child_process`, `Function`, `module`, `process`, `global`, and `setInterval` (they'll be `undefined` at runtime).

### Making Outbound Requests (z.request)

The `z.request` function allows you to make external calls. It performs in a synchronous manner for ease of use, but also provides standard asynchronous features as well if you pass an optional callback.

#### Usage

- Asynchronous: `z.request(request, [callback])`
- Synchronous: `var response = z.request()`

#### Options

- `request <Object>`: Takes all [options for the NPM request package](https://www.npmjs.com/package/request#requestoptions-callback) plus some that allow it to accept what most pre-scripting methods receive as `bundle.request`:
  - `request <Object>`: Means you can also pass `bundle` and we'll extract `bundle.request` to work with.
  - `auth <Array> | <Object>`: If `auth` is an `Array`, it will be transforrmed to `{'user':auth[0], 'pass':auth[1]}` to match the package's [HTTP Authentication](https://www.npmjs.com/package/request#http-authentication). If your Zapier app is configured to use Basic Auth then `bundle.request.auth` will be array with 2 elements for the username and password. If it uses Digest Auth then the third element will be `false`. In this case, when `auth[2]` is set, we will set `auth.sendImmediately` to `auth[2]` and also default `jar` to `true` since most digest servers require cookies.
  - `params <Object>`: Will become `qs` unless that already exists.
  - `data <string>` Will become `body` unless that already exists. While `bundle.request.data` will always be a `String`, be aware that `body` also accepts a `Buffer`, `ReadStream` or - if `json` is set to `true` - any JSON-serializable object.
- `callback Function ([error], response)`: Will be called on completion, with:
	- `error <Error>`: Any error, when applicable.
	- `response <Object>`: See *Response*.

#### Response

You will not receive the full response but a selection from [`http.IncomingMessage`](https://nodejs.org/api/http.html#http_class_http_incomingmessage) that matches what most post-scripting methods receive as `bundle.response`:

- `status_code <number>`: The 3-digit HTTP response status code. E.G. `404`.
- `headers <Array>`: Key-value pairs of header names (lower-cased) and values.
- `content <string>`: If `http.IncomingMessage.body` is a `string` or `Buffer` then we'll wrap it in `String()`.

### Errors

When you call `z.request()` without a callback and an error occurs, it will be thrown. Wrap your call in `try/catch` block to handle it.

### Example

Let's call [http://httpbin.org/get?hello=world](http://httpbin.org/get?hello=world) with a header to tell it we like JSON:

```javascript
var request = {
  'method': 'GET',
  'url': 'http://httpbin.org/get',
  'params': {
    'hello': 'world'
  },
  'headers': {
    'Accept': 'application/json'
  },
};

// Synchronous
var response = z.request(request);
console.log('Status: ' + response.status_code);
console.log('Headers: ' + JSON.stringify(response.headers));
console.log('Content: ' + response.content);

// Asynchronous
z.request(request, function(err, response){

  if (err) {
	 // you can always throw it, we'll catch it, but it
	 // is better to throw a user-friendly ErrorException
    throw err;
  }

  console.log('Status: ' + response.status_code);
  console.log('Headers: ' + JSON.stringify(response.headers));
  console.log('Content: ' + response.content);
});
```

> Please note that your scripts have 30 seconds, including waiting for and processing any requests. If you need to do lots of extra API calls, especially in a loop, you should look our hydration routine.

### Parsing JSON (z.JSON.parse)

The `z.JSON.parse` function acts a lot like the native `JSON.parse`, but adds some helpful logging and error handling. 

`z.JSON.parse(string)`, where `string` is the string representation of a valid JSON object. An error will be thrown if the structure is invalid. 

```javascript
var response = z.request({
  method: 'GET',
  url: 'https://api.someservice.com/me',
  auth: [bundle.auth_fields.api_key, '']
});
var str = response.content;
var obj = z.JSON.parse(str);
// return obj.fields.whatever[0];
```

### Hashing

We support both hashing and HMAC hashing. 

```javascript
// z.hash(algorithm, string, encoding="hex", input_encoding="binary")
var hash = z.hash('sha256', "my awesome string"); 

// z.hmac(algorithm, key, string, encoding="hex")
var hmac_hash = z.hmac('sha256', 'key', 'string');

// Node.js crypto's library does not officially document using input encodings with hmac, but you can do the following:
var crypto = require('crypto');
crypto.createHmac('sha256', 'key').update('string', 'input_encoding').digest('encoding');
```

For output encoding (the `encoding` parameter) we default to `hex` and also support `base64` as a parameter value. For input encoding (the `input_encoding` parameter) we default to `binary` and also support `utf8` as a parameter value. You should use `utf8` if you expect data to be hashed that may include UTF8 characters.

The following hash algorithms are supported:

`DSA-SHA1-old`, `dsa`, `dsa-sha`, `dsa-sha1`, `dsaEncryption`, `dsaWithSHA`, `dsaWithSHA1`, `dss1`, `ecdsa-with-SHA1`, `md4`, `md4WithRSAEncryption`, `md5`, `md5WithRSAEncryption`, `mdc2`, `mdc2WithRSA`, `ripemd`, `ripemd160`, `ripemd160WithRSA`, `rmd160`, `rsa-md4`, `rsa-md5`, `rsa-mdc2`, `rsa-ripemd160`, `rsa-sha`, `rsa-sha1`, `rsa-sha1-2`, `rsa-sha224`, `rsa-sha256`, `rsa-sha384`, `rsa-sha512`, `sha`, `sha1`, `sha224`, `sha256`, `sha384`, `sha512`, `ssl2-md5`, `ssl3-md5`, `ssl3-sha1`, `whirlpool`

### Base 64 Encoding

If you're looking to turn some text to base64 for something like Basic Auth or otherwise, use this simple function available from Node.js:

```javascript
var b64data = btoa("this is my string to turn into base64");
```

### Hydration & Dehydration

> Hydration & dehydration is an experimental feature! Contact us if you need a hand at [contact@zapier.com](contact@zapier.com).

Dehydration is what we call the creation of a pointer to some data, this is what you'll normally use to provide data that may not be needed now but could the future.

Hydration is the opposite of dehydration. It is the consumption of a pointer that returns data. Let's show an example!

```javascript
var Zap = {
    get_contact: function(bundle) {
        /* 
        Argument:
            bundle.auth_fields: <object>
            bundle.zap: <object> # info about the zap

            Anything else you might need, like bundle.request.headers, will need to be passed in when you call z.dehydrate()
        */
        var contact = z.JSON.parse(z.request({
            method: 'GET',
            url: 'https://api.fancycrm.com/v1/contacts/' + bundle.contact_id + '.json',
            auth: [bundle.auth_fields.api_key, ''] // you'll need to handle auth
        }).content) || {};
        return contact;
    },
    deal_post_poll: function(bundle) {
        var deals = z.JSON.parse(bundle.response.content);
        return _.map(deals, function(deal) {
            // this delays Zap.get_contact({contact_id: deal.contact_id, auth_fields: bundle_auth_fields})
            deal.contact = z.dehydrate('get_contact', {contact_id: deal.contact_id});
            return deal;
        });
    }
};
```

In the example above, `get_contact` will not be called when post_poll is called. Instead, a unique hash is created and stored in place of `deal.contact`.

There are two scenarios when `get_contact` will then be called and "hydrated".

1. When a user is first setting up their Zap in the UI and accessing fields (because `deal.contact` may have keys to choose from on itself).

2. When a user's Zap tries to send `deal.contact` out to another app.

### Files

> Files are an experimental feature! You can read more about files here: [files reference](https://platform.zapier.com/legacy/docs#files).

#### Dehydrating Files

Dehydration is what we call the creation of a pointer to data, this is what you'll normally use in triggers to provide binary data out of band to Zapier. The idea is simple: you don't want to download all the attachments from all 100 records in a poll - that would take way too long and would be wasteful! So we offer a handy way to create pointers that we can consume "on-demand".

```javascript
// you can pass along urls and extra request information

// important: dehydrateFile will not download the file immediately!
// it just creates a pointer that our system understands so it can
// get the file on demand if it is needed

// if you just provide the url, we'll include any standard api
// headers or querystrings you configure for oauth or similar
var url = 'https://example.com/test.txt';
var filePointer = z.dehydrateFile(url);

var filePointer = z.dehydrateFile(
  url,

  // you can configure the request using the same options
  // as z.request, but this makes you responsible for authorization
  // and we will not refresh tokens or sessions before hydrating
  {
    method: 'post',
    params: {
      custom: 'param'
    },
    headers: {
      'X-Download-Key': 'abcdef1234567890'
    }
   },

  // you can configure the content filename and length
  // if you leave it out we'll try to determine it for you
  {
    name: 'mytextfile.txt',
    length: 123
  }
);
```

> Please note that request will be done via the [requests library for Python](http://docs.python-requests.org/en/master/user/quickstart/#make-a-request) which is different from [z.request()](https://platform.zapier.com/legacy/scripting#making-outbound-requests-zrequest). You cannot set an `auth` property (e.g. for Basic Auth). Instead provide the exact `params` and `headers`.

#### Hydrating Files

The scripting portion of hydration in actions is incomplete - right now your API will need to adhere to our multipart pattern as described in our [files reference documentation](https://platform.zapier.com/legacy/files/#actions-via-multipart).


## Bundle Details

### Prepared request via `bundle.request`

All `pre` and methods like `KEY_write` receive a prepared request via `bundle.request`. This object has the same format as what the `pre` methods are expected. This means you can modify and return it. It is also the same format that `z.request()` accepts. This is what you'd do in most `KEY_TYPE` methods.

- `url <string>`: Configured Polling, Action or Search Endpoint URL. Any variables will be resolved.
- `method <string>`: Will be `GET` in most cases, but `POST` for actions (`_write`), `pre_subscribe` and `pre_unsubscribe`.
- `auth <Array>`: Will only be set if the app's Auth Type is *Basic* or *Digest Auth*. The first 2 elements are the username and password. *Digest Auth* has a third element which is always `false`.
- `headers <Object>`: If the Auth Type is *API Key (Headers)* or when it is *OAuth V2*, *OAuth V2 (w/refresh)* or *Session Auth* and you have selected *Header* or *Both* for *Access Token Placement*, then this object will have the required/mapped headers. In addition, we always set `Content-Type: application/json; charset=utf-8` and `Accept: application/json` since `data` defaults to JSON and we prefer to get that back as well.
- `params <Object>`: Will be mapped into the querystring. If the Auth Type is *API Key (Query String)* or when it is *OAuth V2*, *OAuth V2 (w/refresh)* or *Session Auth* and you have selected *Querystring* or *Both* for *Access Token Placement*, then this object will have the required/mapped parameters. If you need to convert this to an actual querystring, use `$.param(bundle.request.params)`. Be aware that we do not automatically set params for your *Trigger Fields*!
- `data <string>`: Will form the body of the request. This will be set to a JSON string for `pre_subscribe`, `pre_unsubscribe` and actions (`_write`) that have one or more fields with *Send to Action Endpoint URL in JSON body* enabled. To parse a JSON string back to an object use `z.JSON.parse(bundle.request.data)`. To stringify an object use `JSON.stringify(your_object)`.
- `files <Object>`: For actions (`_write`) that have file-type *Action Fields* this will be an object with the field keys as keys while the values are an `Array` of:
	- `[0] <string>` Filename or `null`.
	- `[1] <string>` URL to a zapier.com endpoint that will stream the file.
	- `[2] <string>` Mimetype or `null`.

For Static and REST Hooks, `KEY_catch_hook` also receives `bundle.request`, but as this is an incoming request it has a different structure. It does not have an `url` or `auth` property, `params <Object>` is `querstring <string>` and `data` is called `content`.

### Raw URL via `bundle.url_raw`

The `bundle.url_raw` is simply the unrendered version of the URL with `{% templatetag openvariable %}curlies{% templatetag closevariable %}` still intact.

### Auth Fields via `bundle.auth_fields`

The `bundle.auth_fields` is a javascript object that matches the authentication settings provided by the user when the API is connected. For example, if you have an [authentication field](https://platform.zapier.com/legacy/authentication-fields/) of `api_key` and `subdomain` you can expect:

```json
{
  "api_key": "fc5e038d38a57032085441e7fe7010b0",
  "subdomain": "example"
}
```

### Rendered Fields via `bundle.trigger_fields` or `bundle.action_fields`

Both `bundle.trigger_fields` and `bundle.action_fields` are javascript objects that surface the data given by a user to power a part of a zap. This is after rendering `{% templatetag openvariable %}curlies{% templatetag closevariable %}`. These follow the [trigger fields](https://platform.zapier.com/legacy/trigger-fields/) or [action fields](https://platform.zapier.com/legacy/action-fields/) you define. For example, maybe you have a field with a key `list_id` and `name`:

```json
{
  "list_id": "1234",
  "name": "Joe Blow"
}
```

For actions, this will prune out any fields you chose not to send in the JSON. Use `bundle.action_fields_full` if you want them included as well.

### Raw Fields via `bundle.trigger_fields_raw` or `bundle.action_fields_raw`

Both `bundle.trigger_fields_raw` or `bundle.action_fields_raw` are javascript objects that surface the data given by a user to power a part of a zap. This is before rendering `{% templatetag openvariable %}curlies{% templatetag closevariable %}`. These follow the [trigger fields](https://platform.zapier.com/legacy/trigger-fields/) or [action fields](https://platform.zapier.com/legacy/action-fields/) you define. For example, maybe you have a field with a key `list_id`:

```json
{
  "list_id": "1234",
  "name": "{% templatetag openvariable %}first_name{% templatetag closevariable %} {% templatetag openvariable %}last_name{% templatetag closevariable %}"
}
```

For actions, this will prune out any fields you chose not to send in the JSON.

### Trigger Details via `bundle.trigger_data`

This is deprecated and will be going away entirely soon. Instead, use standard [Action Fields](https://platform.zapier.com/legacy/reference/#action-fields) which the user maps, to access trigger data.

### Webhook Payload via `bundle.cleaned_request`

The `bundle.cleaned_request` is our best guess at the parsed payload. We do our best to parse JSON, XML and form-encoded data into respective javascript objects. If we cannot parse it correctly - look into `bundle.request.content` and parse it yourself.

### Zap Details via `bundle.zap`

The `bundle.zap` object contains extra information about the zap (FYI: you may not see this information in debug bundles until the `zap` is referenced at least once in your script):

```json
{
  "name": "My Fancy Zap Title",
  "live": false,
  "link": "https://zapier.com/app/editor/12345",
  "user": {
    "timezone": "America/Denver",
  },
}
```

You can access the information like this:

```javascript
var Zap = {
  any_old_pre_poll: function(bundle) {
    var zap = bundle.zap;
    var message = 'The Zap title is ' + zap.name'!';
    // message == "The Zap title is My Fancy Zap Title!"
    return bundle.request;
  }
}
```

### Extra Request Info via `bundle.meta`

The `bundle.meta` object contains some runtime information about the Zap which you can use.

```javascript
{ 
  "frontend": true, // if true, it's being done through the Zap editor/setup
  "prefill": false, // if true, this poll is running as a prefill (dynamic dropdown)
              // for another poll
  "filter": false, // if true, this poll will be filtered afterwards
  "hydrate": true, // if true, the results from this poll will be hydrated
  "limit": 5, // how many items you should limit the API call to for
              // performance reasons. a value of -1 means not limited
  "test_poll": false, // if true, means this API call came from the user
                      // testing their account in the UI
  "standard_poll": true, // opposite of bundle.meta.test_poll
  "first_poll": false, // if true, means this API call is our initial check for
                     // items in the API when the Zap is turned on
  "page": 0 // which page of API results you should return, useful for
            // paging backwards for dynamic dropdowns. It is 0-indexed
            // (add 1 via JS if your paging scheme is 1-indexed)
            // note this is only available for dynamic dropdowns,
            // when bundle.meta.frontend === true
}
```

> Use bundle.meta.page to implement pagination - this is especially important for triggers that power dropdowns.

You can access the information for limited pagination features like this:

```javascript
var Zap = {
  any_old_pre_poll: function(bundle) {
    // adds ?page=0 to URL querystring
    bundle.request.params.page = bundle.meta.page
    return bundle.request;
  }
}
```

## Available Exceptions

> **Note**: This guide is for Zapier's legacy web builder. For new integrations, use Zapier [Platform UI or CLI](https://platform.zapier.com/docs/intro), which expects [standard HTTP errors](https://zapier.github.io/visual-builder/docs/auth#common-authentication-error-messages) to be thrown.

In scripting, you have several exception classes at your disposal. Most are used for communicating errors to the user, but a couple do some more interesting bits. See the specifics of each class to find out more.

> Heads up: these exceptions are for custom scripting in a **Legacy Web Builder** app. If you're working on a CLI app, check out our CLI error handling docs [here](https://zapier.github.io/zapier-platform-cli/#error-handling).

### General Errors

The most rudimentary exception class is the `ErrorException`. Use it in situations where the user has something misconfigured with their Zap and will need to take action. Typically, this will be for prettifying `4xx` responses and API's that return errors as `200` with a payload that describes the error.

Example: `throw new ErrorException('Your error message.');`

Note that if a Zap raises too many error messages it will be automatically turned off, so only use these if the scenario is truly an error that needs to be fixed.

### Halting Execution

Any method can be interrupted or "halted" (not success, not error, but stopped for some specific reason) with a `HaltedException`. You might find yourself using this exception in cases where a required pre-condition is not met. For example, in an action to add notes to a contact where contacts are searched for by email address, you would want to throw a `HaltedException` if a contact was not found. Unlike the `ErrorException`, a Zap will never be turned off when this exception is raised (even if it is raised more often than not).

Example: `throw new HaltedException('Your reason.');`

Any pre_XXX call can be interrupted **silently** with `StopRequestException`. This will prevent the request from being made and will never cause a user's Zap to be turned off. 

Example: `throw new StopRequestException('Your reason.');`

### Stale Authentication Credentials

For apps that require manual refresh of authorization on a regular basis, we provide a mechanism to notify users of expired credentials. With the `ExpiredAuthException`, the current call is interrupted, the zap is turned off (to prevent more calls with expired credentials), and a predefined email is sent out informing the user to refresh the credentials.

Example: `throw new ExpiredAuthException('Your message.');`

For apps that use OAuth, but do not return a typical 401 when tokens expire, you can use the `RefreshTokenException` in a post_XXX. This will signal Zapier to attempt to refresh the access token and then repeat the failed call.

Example: `throw new RefreshTokenException();`

### Updating Session Credentials

For session-based APIs only, stale authorization credentials can be refreshed by throwing the `InvalidSessionException`. This will tell Zapier to invoke your provided `get_session_info()` function. Zapier will store these results for you and make them available to every `poll` and `write`. We will throw the exception for you if the API responds with a 401 status.

## Code Examples

### Trigger Pre-Poll Examples

> Heads up! This code is only valid for the v2 platform, and is incompatible with today's [Zapier Platform UI and CLI](https://platform.zapier.com/docs/vs).

{% raw %}
```javascript
"use strict"; 

var Zap = {
  // STRAIGHT PASS THROUGH
  // same as not providing the method at all
  // for illustration purposes only
  simple_pre_poll: function(bundle) {
    return bundle.request;
  },

  // CHANGE REQUEST METHOD
  // for endpoints that don't like the default GET
  simple_pre_poll: function(bundle) {
    bundle.request.method = 'POST';
    return bundle.request;
  },

  // PLACE A HEADER BASED ON USER INPUT
  // a trigger field that should be added as a header but
  // if there isn't one, default to "None"
  some_header_pre_poll: function(bundle) {
    var request = bundle.request;
    request.headers["X-Project-ID"] = bundle.trigger_fields.project_id || "None";
    return request;
  },

  // SUBSTITUTE HUMAN FRIENDLY CHOICES
  // if you add a trigger field with human friendly choices:
  //     Yesterday,Today,Tomorrow
  // but the querystring should be:
  //     &when=-1, &when=0, or &when=1
  event_pre_poll: function(bundle) {
    var request = bundle.request;
    switch (bundle.trigger_fields.when) {
      case "Yesterday":
        request.params.when = -1;
        break;
      case "Today":
        request.params.when = 0;
        break;
      default:
        request.params.when = 1;
    }
    return request;
  },

  // BUILD THE URL YOURSELF
  // this does exactly what we do when transforming the URL
  // from bundle.url_raw to bundle.request.url
  // utilizes underscores template system (preloaded with proper syntax)
  room_pre_poll: function(bundle) {
    var request = bundle.request;
    // bundle.url_raw is 'http://{{account_name}}.campfirenow.com/room/{{room_id}}/speak.json'
    // bundle.auth_fields is {account_name: 'myaccount', api_key: '1234567890'}
    request.url = _.template(bundle.url_raw)(bundle.auth_fields);
    // request.url is 'http://myaccount.campfirenow.com/room/{{room_id}}/speak.json'
    // bundle.auth_fields is {room_id: 12345, message: 'Hello world!'}
    request.url = _.template(request.url)(bundle.trigger_fields);
    // request.url is 'http://myaccount.campfirenow.com/room/12345/speak.json'
    return request;
  }
}
```
{% endraw %}

### Trigger Post-Poll Examples

> Heads up! This code is only valid for the v2 platform, and is incompatible with today's [Zapier Platform UI and CLI](https://platform.zapier.com/docs/vs).

```javascript
"use strict"; 

var Zap = {
  // STRAIGHT PASS THROUGH OF JSON
  // same as not providing the method at all
  // for illustration purposes only
  straight_post_poll: function(bundle) {
    // bundle.response.content is '[{"id":1234,"title":"Hello!"}, ... ]'
    return z.JSON.parse(bundle.response.content);
  },

  // WRAP IN ARRAY
  // for APIs that return a single object
  straight_post_poll: function(bundle) {
    // bundle.response.content is '{"id":1234,"title":"Hello!"}'
    return [z.JSON.parse(bundle.response.content)];
  },

  // CENTS INTO DOLLARS
  // take a key in cents and offer it up as a dollar formatted string
  sale_post_poll: function(bundle) {
    // bundle.response.content is '[{"id":1234,"cents":925}, ... ]'
    var results = z.JSON.parse(bundle.response.content);
    _.each(results, function(result) {
      result.dollars = "$" + (Math.floor(result.cents / 100)) + "." + (result.cents % 100);
    })
    // results is '[{"id":1234,"cents":925,"dollars":"$9.25"}, ... ]'
    return results;
  },

  // XML INTO JSON
  // given an string of xml data, turn that into JSON:
  //   <messages type="array">
  //     <message>
  //       <id type="integer">2</id>
  //       <title>Anyone home?</title>
  //       <body>I can't seem to see anything!</body>
  //     </message>
  //     <message>
  //       <id type="integer">1</id>
  //       <title>Hello there world!</title>
  //       <body>I am just tickled to see you!</body>
  //     </message>
  //   </messages>
  my_xml_doc_post_poll: function(bundle) {
    // bundle.response.content is xml string from API, $ is preloaded jQuery
    var xml = $($.parseXML(bundle.response.content)).find('message');
    // build javascript primitives: array of objects
    var results = _.map(xml, function(element){
      return {
        id: $(element).find('id').text(),
        title: $(element).find('title').text(),
        body: $(element).find('body').text()
      };
    });
    // results is '[{"id":"2","title":"Anyone home?","body":"I can't seem to see anything!"}, ... ]'
    return results;
  }
}
```

### Catching Webhooks Example

> Heads up! This code is only valid for the v2 platform, and is incompatible with today's [Zapier Platform UI and CLI](https://platform.zapier.com/docs/vs).

```javascript
"use strict";

var Zap = {
  // STRAIGHT PASS THROUGH OF CLEANED_REQUEST
  // same as not providing the method at all
  // for illustration purposes only
  straight_catch_hook: function(bundle) {
    // bundle.cleaned_request is usually an object or array
    return bundle.cleaned_request;
  },

  // PLACE QUERY STRING AS MAIN OBJECT
  // in this example our hook is just a GET with a query string
  // there is no request content or body, maybe a url like this:
  //   GET https://zapier.com//hooks/catch/123/n/456789/?name=bryan&age=27
  simple_get_catch_hook: function(bundle) {
    // bundle.cleaned_request includes the query string already parsed
    // but you could parse it yourself from bundle.request.querystring:
    var example = $.param(bundle.request.querystring);

    // but let's just return the cleaned_request version:
    return bundle.cleaned_request.querystring; // {"name":"bryan","age":27}
  },

  // MOVE LIST ON SUBKEY TO MAIN OBJECT
  // if a json POST contains a list on a root object's key "data" 
  // we can move the list to the parent to trigger for each item
  // the content/body might look like:
  //   {"data":[{"name":"bryan","age":27},{"name":"mike","age":23}]}
  myjson_catch_hook: function(bundle) {
    // bundle.cleaned_request includes the json already parsed
    // but you could parse it yourself from bundle.request.content:
    var example = z.JSON.parse(bundle.request.content).data;

    // but let's just return the cleaned_request version:
    return bundle.cleaned_request.data; // the array
  }

  // FILTER OUT CERTAIN STATIC WEBHOOKS
  // if your hooks are noisy, then you may want to filter based on
  // some static value, or even user provided trigger fields
  filter_out_catch_hook: function(bundle) {
    // manually create json from the posted string
    var json = z.JSON.parse(bundle.request.content);

    // filter out hooks that aren't the event type we care about
    if (json.event_type != 'new_comment') {
      return []; // return [] or {} to take no action
    }

    // filter out hooks that aren't the status that the user expected
    if (bundle.trigger_fields.status && json.status != bundle.trigger_fields.status) {
      return []; // return [] or {} to take no action
    }

    // else
    return json;
  },
}
```

### Action Pre-Write Examples

> Heads up! This code is only valid for the v2 platform, and is incompatible with today's [Zapier Platform UI and CLI](https://platform.zapier.com/docs/vs).

```javascript
"use strict"; 

var Zap = {
  // STRAIGHT PASS THROUGH
  // same as not providing the method at all
  // for illustration purposes only
  pass_through_pre_write: function(bundle) {
    return bundle.request;
  },

  // WRAP FIELDS IN TOP-LEVEL ARRAY UNDER DATA KEY
  wrap_in_array_pre_write: function(bundle) {
    bundle.request.data = JSON.stringify({data: [bundle.action_fields]})
    return bundle.request;
  },

  // DO NOT UNFLATTEN __
  // by default we will turn fields like {custom__c: 12}
  // into {custom: {c: 12}}, but this can avoid this by
  // using the "full" action fields, like this
  dont_unwrap_pre_write: function(bundle) {
    bundle.request.data = JSON.stringify(bundle.action_fields_full);
    return bundle.request;
  },

  // LIMIT STRING LENGTH
  // a field called message cannot be longer than 256 characters
  message_pre_write: function(bundle) {
    var outbound = z.JSON.parse(bundle.request.data);
    outbound.message = outbound.message.substring(0, 256);
    bundle.request.data = JSON.stringify(outbound);
    return bundle.request;
  },

  // GENERATE XML FOR POSTING
  // you'll have access to your action fields
  // we'd normally POST as JSON, but this shows how to do XML
  xml_doc_pre_write: function(bundle) {
    // root el is ignored in .html()
    var xml = $("<XMLDocument><message/></XMLDocument>");
    // bundle.action_fields is {title: "Anyone home?", body: "I can't seem to see anything!"}
    Object.keys(bundle.action_fields).forEach(function(key){
      $(xml.find("message")).append($("<" + key + " />").text(bundle.action_fields[key]));
    })
    // '<message><title>Anyone home?</title><body>I can't seem to see anything!</body></message>'
    bundle.request.data = xml.html();
    // set the headers
    bundle.request.headers['Content-Type'] = "application/xml; charset=utf-8";
    bundle.request.headers['Accept'] = "application/xml";
    return bundle.request;
  },

  // FORM ENCODE INSTEAD OF JSON
  // sometimes you don't want to JSON encode, so this example shows how
  // to form encode POST data instead (just like a form submission)
  my_form_pre_write: function(bundle) {
    // build a querystring from the object with all fields
    bundle.request.data = $.param(bundle.action_fields_full);
    // correct the content type header
    bundle.request.headers['Content-Type'] = 'application/x-www-form-urlencoded';
    return bundle.request;
  }
}
```

### Search Post-Write Examples

> Heads up! This code is only valid for the v2 platform, and is incompatible with today's [Zapier Platform UI and CLI](https://platform.zapier.com/docs/vs).

Sometimes, a search endpoint will return a successful response despite the search being unsuccessful. To account for this, you need to manipulate the response in a [`_post_search`](#key_post_search) method:

```javascript
// let's say the response content looks like this:
// {
//   "search_results": {},
//   "time": "2018-04-01T01:02:03.456-00:00"
// }
// by default, our system will interpret this as a successful search
// and return the "search_results" and "time" keys -- what we really
// want is the content nested under that search_results key (which in
// this example is an empty object, because there was no search match)

var Zap = {
  my_search_key_post_search: function(bundle) {
    var response = z.JSON.parse(bundle.response.content);
    return response.search_results;
  }
}
```

### REST Hook Subscription Examples

> Heads up! This code is only valid for the v2 platform, and is incompatible with today's [Zapier Platform UI and CLI](https://platform.zapier.com/docs/vs).

```javascript
var Zap = {
    pre_subscribe: function(bundle) {
        bundle.request.method = 'POST';
        bundle.request.headers['Content-Type'] = 'application/x-www-form-urlencoded';
        bundle.request.data = $.param({
            url: bundle.target_url,
            list_id: bundle.trigger_fields.list_id, // from trigger field
            append_data: 1
        });
        return bundle.request;
    },
    post_subscribe: function(bundle) {
        // must return a json serializable object for use in pre_unsubscribe
        var data = z.JSON.parse(bundle.response.content);
        // we need this in order to build the {% templatetag openvariable %}webhook_id{% templatetag closevariable %}
        // in the rest hook unsubscribe url
        return {webhook_id: data.id};
    },
    pre_unsubscribe: function(bundle) {
        bundle.request.method = 'DELETE';
        // bundle.subscribe_data is from return data in post_subscribe method
        bundle.request.url = 'https://example.com/x.php?id=' + bundle.subscribe_data.webhook_id;
        bundle.request.data = null;
        return bundle.request;
    },
};
```

**Adding Trigger Fields to Subscription Payload**

```javascript
var Zap = {
  
  pre_subscribe: function (bundle) { 
    if (Object.keys(bundle.trigger_fields).length) {
      var data = z.JSON.parse(bundle.request.data);
      var dataWithFields = Object.assign({}, data, bundle.trigger_fields);
      bundle.request.data = JSON.stringify(dataWithFields);
    }
    return bundle.request;
  }
  
};
```

### Session Auth Examples

> Heads up! This code is only valid for the v2 platform, and is incompatible with today's [Zapier Platform UI and CLI](https://platform.zapier.com/docs/vs).

```javascript
var Zap = {
  get_session_info: function(bundle) {
    var api_key,
        api_key_request_payload,
        api_key_response;

    // Assemble the meta data for our key swap request
    api_key_request_payload = {
        method: 'POST',
        url: 'https://api.domain-name.com/api/login',
        params: bundle.auth_fields,
        headers: {
            'Content-Type': 'application/json',  // Could be anything.
            Accept: 'application/json' 
        }
    };

    // Fire off the key exchange request.
    api_key_response = z.request(api_key_request_payload);

    // Extract the `api_key` from returned JSON.
    api_key = z.JSON.parse(api_key_response.content).api_key;

    // This structure is an example. You may need to add
    // a different key name, or multiple keys, depending
    // on your API's requirements.
    // This will be mixed into bundle.auth_fields in future calls.
    return {'api_key': api_key};
  },
  
  new_contact_post_poll: function(bundle) {

    // We will catch bundle.response.status_code === 401
    // If your API doesn't conform to this standard, you can handle it yourself:
    if (z.JSON.parse(bundle.response.content).code === 401) {
      throw new InvalidSessionException(); // Call get_session_info() and try the request again
    }
    
    return z.JSON.parse(bundle.response.content);
  }
};
```

## Debugging

_For CLI app debugging see [here](https://zapier.github.io/zapier-platform-cli/cli.html#logs)_.

By far the easiest way to debug is to use the [Monitor](https://platform.zapier.com/legacy/docs#monitoring/) to track requests (which includes a rudimentary JavaScript Exception catcher). We also have a Bundle Logs option. You can access both from the scripting platform:

![how to get to console/http logs](https://cdn.zapier.com/storage/photos/fb02eddd9a548b39501ab6f1aa64079f.png)

> **Bundle Logs** are only available for Private apps.

The ability to log to a console that you can view live. Similar to your browser, logging something is simple as:

```javascript
console.log('hello world!');
console.log({id: 1234, name: 'Bob Smith'});
```

And then, from the Code Editor you can open the bundle log console and watch logs come in live:

![console logging](https://cdn.zapier.com/storage/photos/ffeebe8543a1c886c183aad36f3875c3.png)

> _Warning: If you try to use `console.log()` with a large object, all logs before and including that one will be removed and only logs after it will show. You should avoid logging potentially large objects._

Unlike your browser, if your function generates an error after `console.log(...)`, it will not show up in the console.

To mitigate the possibility of an error after `console.log(...)`, you should return early. Keep in mind, you need to return an object of the expected format for that function type.

```javascript
Zap = {
  TRIGGERKEY_pre_poll: function(bundle) {
    console.log('my error');
    return bundle.request; // expected return format for pre poll functions
  }

  TRIGGERKEY_post_poll: function(bundle) {
    console.log('my error');
    return []; // expected return format for post poll functions
  }
}
```

### Common Issues

#### Error: Scripting payload too large

Your app runs on AWS Lambda, which has a throughput limit of 6MB. The total size of your scripting code and the data received and returned by a method cannot exceed that limit. If you're seeing this error, the most likely cause is the amount of data being returned from a `X_post_poll` method. To solve, try transforming the raw response to return only the relevant fields or return a subset of items (only the most recent 50, for instance). Some APIs also support asking for certain fields instead of everything, which can cut down bundle size. 

#### Python Artifacts

When doing a POST request in a write action, you may see Python unicode artifacts in your payload. For example: 

```
[{u'lastName': u'Wayne', u'firstName': u'Bruce'}]
```

This mean you're passing an object to bundle.request.data, which expects a string. Call `JSON.stringify` on your data object in the `ACTION_KEY_pre_write` method.

## Editor Keyboard Shortcuts

Below is a list of available keyboard shortcuts you can use while in the Scripting Editor:

**Select All** `Ctrl-A` (PC) `Cmd-A` (Mac)

Select the whole content of the editor.

**Save** `Ctrl-S` (PC) `Cmd-S` (Mac)

Saves the current content of the editor.

**Undo** `Ctrl-Z` (PC) `Cmd-Z` (Mac)

Undo the last change.

**Redo** `Ctrl-Y` (PC) `Cmd-Y` (Mac)

Redo the last undone change.

**Undo Selection** `Ctrl-U` (PC) `Cmd-U` (Mac)

Undo the last change to the selection, or if there are no selection-only changes at the top of the history, undo the last change.

**Redo Selection** `Alt-U` (PC) `Shift-Cmd-U` (Mac)

Redo the last change to the selection, or the last text change if no selection changes remain.

## Movement

**Jump to Doc Start** `Ctrl-Up` (PC), `Cmd-Up` (Mac)

Move the cursor to the start of the document.

**Jump to Doc End** `Ctrl-Down` (PC) `Cmd-Down` (Mac)

Move the cursor to the end of the document.

**Jump to Start of Line** `Alt-Left` (PC) `Cmd-Left` (Mac)

Move the cursor to the start of the line.

**Jump to Start of Line Smart** `Home`

Move to the start of the text on the line, or if we are already there, to the actual start of the line (including whitespace).

**Jump to Line End** `Alt-Right` (PC) `Cmd-Right` (Mac)

Move the cursor to the end of the line.

**Move Left a Group** `Ctrl-Left` (PC), `Alt-Left` (Mac)

Move to the left of the group before the cursor. A group is a stretch of word characters, a stretch of punctuation characters, a newline, or a stretch of more than one whitespace character.

**Move Right a Group** `Ctrl-Right` (PC) `Alt-Right` (Mac)

Move to the right of the group after the cursor (see above).

## Search

**Find** `Ctrl-F` (PC) `Cmd-F` (Mac)

Typical search, with the added bonus of being able to do regular expressions.

**Find Next** `Ctrl-G` (PC) `Cmd-G` (Mac)

After you perform a search, use to jump to the next match.

**Find Previous** `Shift-Ctrl-G` (PC) `Shift-Cmd-G` (Mac)

After you perform a search, use to jump to the previous match.

**Replace** `Shift-Ctrl-F` (PC) `Cmd-Alt-F` (Mac)

Perform a replace. Use the buttons to move through the matches.

**Replace All** `Shift-Ctrl-R` (PC) `Shift-Cmd-Alt-F` (Mac)

Perform a replace on every match (no confirmation). 

## Delete

**Kill Line** `Ctrl-K` (Mac only)

Emacs-style line killing. Deletes the part of the line after the cursor. If that consists only of whitespace, the newline at the end of the line is also deleted.

**Delete Line** `Ctrl-D` (PC) `Cmd-D` (Mac)

Deletes the whole line under the cursor, including newline at the end.

**Delete Group Before** `Ctrl-Backspace` (PC) `Alt-Backspace` (Mac)

Delete to the left of the group before the cursor.

**Delete Group After** `Ctrl-Delete` (PC) `Alt-Delete` (Mac)

Delete to the start of the group after the cursor.

## Indent

**Auto Indent** `Shift-Tab`

Auto-indent the current line or selection.

**Indent More** `Ctrl-]` (PC) `Cmd-]` (Mac)

Indent the current line or selection by one indent unit.

**Indent Less** `Ctrl-[` (PC) `Cmd-[` (Mac)

Dedent the current line or selection by one indent unit.