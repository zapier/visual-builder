## Zapier Visual Builder Docs

![Zapier Visual Builder](https://zapier.github.io/visual-builder/assets/images/visual-builder-header.svg)

Develop the best [Zapier](https://zapier.com/) integration for your app with Zapier's Platform UI and CLI

## Zapier Platform UI

Zapier Platform UI is the easiest way to build new Zapier integrations in an online visual builder without any coding.

- Try Zapier Platform UI: [zapier.com/app/developer](https://zapier.com/app/developer/)
- Build a basic integration with the [Platform UI Quick Start tutorial](https://zapier.github.io/visual-builder/updates/introduction)
- Learn more in [Zapier's Platform UI Documentation](https://zapier.github.io/visual-builder/docs/intro)

## Zapier Platform CLI

Zapier Platform CLI is the most advanced way to build integrations in your local development environment with your team's source code management and custom testing.

- Install Zapier Platform CLI and build a sample integration in the [CLI Quick Start guide](https://zapier.com/developer/start/introduction)
- Learn more in [Zapier's Platform CLI Documentation](https://zapier.github.io/zapier-platform/)
- Find detailed info on the Zapier Platform in the [Zapier Platform Schema](https://zapier.github.io/zapier-platform-schema/build/schema.html) from our built-in code docs
- Start quicker with our templates [Zapier Example Apps](https://github.com/zapier/zapier-platform/wiki/Example-Apps)

## Zapier Legacy Web Builder

Maintain existing Zapier integrations built with Zapier's original web builder:

- [Web Builder Documentation](https://zapier.com/developer/documentation/v2/reference/)
- [Web Builder Scripting](https://zapier.com/developer/documentation/v2/scripting/)
- [name Web Builder Apps](https://zapier.com/developer/documentation/v2/name-apps/)

***

# Running Locally

The Zapier Visual Builder Docs website is built on Ruby and Jekyll. You'll need to make sure to have a few things installed before moving forward:

1. [Ruby 2.2.5+](https://www.ruby-lang.org/en/documentation/installation/)
1. [Bundler](http://bundler.io/)
1. [Jekyll 3.7.0+](https://jekyllrb.com/docs/installation/)

**Note:** We recommend using [Ruby Version Manager (rvm)](https://rvm.io/rvm/install) to manage various versions of Ruby.

Once you've installed Ruby, Bundler and Jekyll you're ready to clone this repo.

```
git clone git@github.com:zapier/visual-builder.git
```

Now you'll want to install all of the dependencies to make this repo run.

```
bundle install
```

You should now have all of the packages installed and are ready to get up an running!

```
bundle exec jekyll serve
```

Go to <http://localhost:4000> in your browser and you'll be viewing a local instance of the Zapier Platform. Now you can make updates to the site and see them change instantly in your browser! :rocket:

:writing_hand: Ready to make some changes? Check out our [contributing guidelines](CONTRIBUTING.md).

* * *

## Adding a new collection (aka a new doc)
**Please feel free to ask a developer or post in #design for help.**

#### Step 1
Create a new folder in the `docs` folder with the format of `_name`. For example:

```
_updates
```

#### Step 2
Open up `_includes/side-nav.html` and add the following code but replacing `example` with your new collection name (e.g. `updates`). _Note: the order of the side bar retreat items reflects the order of the code._

```
  {% include side-nav-item.html title="example" items=site.example section_id="example" current_section=current_section %}
```

#### Step 3
Open up `_config.yml`. Add the following code to collections section (replacing `example` with your collection name), respecting the order that you used in `side-nav`:

```
example:
  output: true
  permalink: /:collection/:name
```

Next, add this code to the `defaults` section (replacing `example` with your collection name):

```
- scope:
    path: ""
    type: "example"
  values:
    layout: default
```

## Adding new posts


#### Step 1
Open up the `_drafts` folder and duplicate the `name.md` file  (which has names of headings, sub-headings, table of contents, etc) and place it inside your new collection (e.g. `_updates`). So it would look like this:

```
_updates/name.md
```

#### Step 2
This part of the file is called Front Matter:

```
---
title: name
order: 1
layout: post
redirect_from: /name/
---
```

Here's what this information means:
- The `title: name` is what appears on the side bar and top of the browser window.
- The `order: (number)` determines placement in the left navigation.
- The `layout: post` is default, but you can add `layout: post-toc` which will add the table of contents on the right based on the `h2` you use.
- The `redirect_from:` just put the name of the collection (e.g. _updates).

#### Step 3
Repeat to add more posts.

***

## Code snippet highlighting
If you are using a language that contains curly braces, you will likely need to place {% raw %} and  {% endraw %} tags around your code. [Learn more](https://jekyllrb.com/docs/liquid/tags/#code-snippet-highlighting).

```
The subscribe URL which looks something like `{% raw %}https://www.formstack.com/api/v2/form/{% templatetag openvariable %}form_id{% templatetag closevariable %}/webhook.json{% endraw %}`
```

```
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
```

* * *

## Deploying changes to production

Changes merged to master go directly to production.

* * *

## Need help?

Please feel free to ask a developer or post in #design for help.
