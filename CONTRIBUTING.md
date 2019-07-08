# Contribution Guidelines

So you want to contribute to the Zapier Visual Identity website? Great! In this section, you'll learn more about our best practices and how to submit an issue.

## Reporting an Issue

Did you find a bug or think of a great suggestion for us? First, check out our [existing list of issues](https://github.com/zapier/visual-identity/issues) to see if that issue already exists. If not, you can [open a new issue](https://github.com/zapier/visual-identity/issues/new) with your suggestion or bug.

## Requesting a Change to Our Content Style Guide

The Zapier Visual Identity website also contains our company's style guide for written content. Everyone at Zapier writes and creates content. Likewise, we want everyone on the team to contribute their knowledge to our brand style.

Before you request or add changes, though, please follow these ground rules:

- **Don't duplicate content.** This guide is the bedrock for our brand style, and keeping it in sync helps us tell a consistent story. Before you add new content, make sure it doesn't exist elsewhere. Multiple sources of truth means no source of truth.
- **Check in with experts.** Trust your teammates—they're here cuz they're smart! If you're changing something that impacts the way a team at Zapier works, get their feedback first. Head on over to the #content-club Slack channel for guidance.
- **Get a review.** Ask for a second set of eyes—at least—before merging your changes into the style guide.
- **Be vocal about big changes.** If something monumental changes—like we rename "Zaps" to "Sprinkles"—be proactive and spread the word.

## Submitting a Pull Request

Want to submit a fix? Great! We're thrilled that you are interested in helping out with the website and contributing your talents to our code base. In this section, you'll learn more about how to go about actually contributing and how to get your local development environment setup.

### How to submit a pull request

1. Fork the repo by clicking on the little fork icon on the the top right. That will make a copy of the repo into your account under the same name.
1. Clone the project from your account, not from Zapier's.
1. In your repo, make a new local branch for your feature based off  the default branch, `master` (e.g. `git branch update-homepage`).
1. Switch to that new branch (e.g. `git checkout update-homepage`)
1. Make any changes on your branch.
1. Test it out locally by running `bundle exec jekyll serve` and visiting [http://127.0.0.1:4000](http://127.0.0.1:4000) in your favorite browser.
1. Push your branch to your repo (e.g. `git push origin update-homepage`)
1. Open github and go to Zapier's repository. It will prompt a message asking if you want to make a Pull Request
1. Submit a pull request against `master` branch. Be sure to include information around what you are solving, include any relevant screenshots and reference any issues this resolves.


The team will get a notification that you submitted a pull request, but feel free to ping us in #design in Slack to take a look!

## Deploying

Once your PR is merged into `staging`, https://zapier.ninja/brand will be automatically updated with your changes.

To update the real deal (https://zapier.com/brand), create a PR to merge `staging` into `master`.
