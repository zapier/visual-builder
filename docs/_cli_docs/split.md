---
title: Examples In Each
order: 3
layout: post-toc
redirect_from: /split/
---

<script>
  const storageKey = 'zapier.appType';
  const godzilla = 'godzilla';
  const cli = 'cli';

  const _iterate = (klass, display) => {
    for (const el of document.querySelectorAll(`.${klass}`)) {
      el.style.display = display;
    }
  };

  const showAll = klass => {
    _iterate(klass, 'block');
  };
  const hideAll = klass => {
    _iterate(klass, 'none');
  };

  const showCli = () => {
    window.localStorage.setItem(storageKey, cli);
    showAll(cli);
    hideAll(godzilla);
  };

  const showGodzilla = () => {
    window.localStorage.setItem(storageKey, godzilla);
    showAll(godzilla);
    hideAll(cli);
  };

  window.onload = () => {
    const appType = window.localStorage.getItem(storageKey) || cli; // default to CLI

    if (appType === cli) {
      showCli();
    } else {
      showGodzilla();
    }
  };
</script>

# Examples in Each

Here's how you do some things in both CLI and Godzilla

<a class="button blue" href="#" onclick="showCli()">CLI</a>
<a class="button blue" href="#" onclick="showGodzilla()">Godzilla</a>

## Lifecycle

The basic flow in which you do things

### Promotion

When it's time for an app to be seen by users, you need to do this:

<div class="cli">
  <div class="highlighter-rouge">
    <div class="highlight">
      <pre class="highlight"><code>$ zapier promote 1.2.3
</code></pre>
    </div>
  </div>
</div>

<div class="godzilla">
  <p>
    <img
      src="https://zappy.zapier.com/F7646205-9EEE-4892-B520-A8EAD616FFB1.png"
      alt=""
    />
  </p>
</div>

That's how you do it!
