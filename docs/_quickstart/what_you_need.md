---
title: What You Need
order: 2
layout: post-toc
redirect_from: /quick-start/
---

# What You Need to Build a Zapier Integration

Ready to build your sample GitHub Zapier integration? Here’s what you need:

## A Zapier Account

If you haven’t used Zapier before, create a free [Zapier](https://zapier.com/){:target="_blank"} account. You could also set up this [example GitHub Zap](https://zapier.com/apps/github/integrations/email/10313/get-emails-with-new-github-issues){:target="_blank"} that will email you with new GitHub issues, to see how the new integration you’ll set up will work for end users.

## A GitHub Account

You also need a [GitHub](https://github.com/){:target="_blank"} account with at least one repo and issue. Since this tutorial will walk you through building an example GitHub integration, you need a GitHub account to test the integration. Have your GitHub username and password handy to set up your GitHub Zapier integration, along with the name of the repo you will use with the integration.

If you use GitHub two-factor authentication, you need a GitHub personal access token to authenticate with Zapier. To make one:

- Open [GitHub’s Tokens page](https://github.com/settings/tokens){:target="_blank"}
- Generate a new Token, add a name, and check the `repo` and `user` scopes
- Copy the token code to use instead of your GitHub password when testing your integration authentication.

If you don't already use GitHub two-factor authentication, now's a good time to enable it and create a personal access token. It's best security practice to never enter your password in another app's UI, and will help keep your GitHub account secure.

You may also want to keep the [GitHub API](https://developer.github.com/v3/){:target="_blank"} open in another tab for reference—though we’ll guide you through everything you need to build the integration.  

Now you’re ready to build a Zapier integration!