---
title: Canary Testing
order: 3
layout: post-toc
redirect_from: /build/test-integration#monitoring
---

# Canary Testing

Canary testing is a way to test new changes temporarily with real users in production with the goal of validating changes don’t cause bugs.
These users are not informed or aware of the changes, as this is usually done at random and in small subsets to obtain a sample. Builders should have careful monitoring in place to watch for errors and rollback when necessary.

## Prerequisites

- Completed build of your Zapier integration, built from the CLI
- A [Zapier account](https://zapier.com/sign-up)
- If you haven’t used Zapier before, you'll want to learn the basics in our [Zapier Getting Started Guide](https://zapier.com/learn/zapier-quick-start-guide/).

You may want to use the canary tool when adding a new feature, or fixing a bug. For example, if you’re planning to roll out a bug fix, and you want to test this out to see if the fix will work. Your usual steps may include unit tests, and _[setting up Zaps for validation](https://platform.zapier.com/build/test-monitoring). Unit tests will ensure your integration code functionality matches what you intended to do. Setting up Zaps will ensure the trigger or action works with the inputs you provide. The canary tool ensures your changes work for many existing live Zaps, with different inputs and outputs. 

Now you have another way to build confidence that the fix can work for all different types of Zap set ups.
`zapier canary` allows you to set the version you want to test with, the version you want to replace with, the percentage of traffic, and a duration before the versions are rolled back.
You can choose to delete the canary test before the duration is expired in case something catastrophic happens.



## Best Practices

- **Start Small**: Begin with a small percentage of traffic.
- **Monitor Closely**: Use monitoring tools to track performance and errors.
- **Communicate**: Inform your team about the canary test.

## Troubleshooting

- **Issue: High Error Rate**: Rollback immediately and investigate the logs.
- **Issue: Performance Degradation**: Reduce the traffic percentage or rollback.

## FAQ

**Q: What happens if I don't rollback in time?**
A: The system will automatically rollback to the previous version after the specified duration.

**Q: Can I extend the duration of a canary test?**
A: Yes, you can extend the duration by stopping the existing canary, and re-running the `zapier canary` command with a new duration.

**Q: How do I monitor the canary test?**
A: Use Zapier's monitoring tools and logs to keep track of the test performance.
