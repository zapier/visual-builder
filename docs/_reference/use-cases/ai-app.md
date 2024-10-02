---
title: Zapier integration structure for an AI app
order: 4
layout: post-toc
redirect_from: 

---

# Zapier integration structure for an AI app

AI app integrations built on Zapier allow users to automate tasks using AI capabilities. Here are some common pain points and recommendations when building AI apps on Zapier.

## Pain Points
### 1. Long-Running Actions  

**Pain Point:** Actions that take a long time to process can cause issues, especially with Zapier's execution time limits. Test steps in the Zapier editor are limited to 50 seconds, and live Zap executions default to 30 seconds.

**Recommendations:**

* Use `z.generateCallbackUrl()` and `performResume`
  * `z.generateCallbackUrl()`: This method generates a callback URL that your service can call once the long-running task is complete.  
  * `performResume`: This function allows the action to pause until the callback URL is called, resuming once the task is complete.  
  * **Why:** These tools help handle tasks that exceed Zapier's execution time limits by offloading the wait to an external service and resuming only when the task is done.
  * [Documentation](https://platform.zapier.com/reference/cli-docs#zgeneratecallbackurl)

### 2. Handling Samples for Long-Running Tasks  

**Pain Point:** Generating accurate samples for long-running tasks can be tricky, especially during the initial setup.

**Recommendation:**

* Use `bundle.meta.isLoadingSample`:  
  * When `bundle.meta.isLoadingSample` is true, return a simplified or cached version of the data that represents a typical response.  
  * **Why:** This approach ensures that users get a quick response during setup, avoiding delays caused by the actual long-running task.
  * [Documentation](https://platform.zapier.com/reference/cli-docs#bundlemeta)

### 3. Hiding Complex Fields in Actions  

**Pain Point:** Complex configuration fields can overwhelm users, making the setup process cumbersome.

**Recommendation:**

* Use Custom Input Fields:  
  * You can create an input field that depends on another. For example, you could create an “Advanced Features” input field at the bottom of all of your other ones that has the property `altersDynamicFields: true` so when it’s updated, all of the other fields refresh. Then any additional input fields could be dependent on whether that “Advanced Features” input field is true, then display the more advanced ones that are not necessarily required for all users. (ie. `if (bundle.inputData.advanced === true)`)
  * These custom input fields can hide complex fields behind simpler user interfaces.  
  * **Why:** Simplifying the user interface makes it more user-friendly, leading to a better experience and fewer setup errors.
  * [Documentation](https://platform.zapier.com/reference/cli-docs#customdynamic-fields)

### 4. Use-Case Specific Actions  

**Pain Point:** Users may struggle with setting up generalized actions that require specific configurations.

**Recommendations:**

* Create Use-Case Specific Actions:  
  * For example, a “ChatGPT Summarize Text" action can hide the configuration and prompt details behind the scenes. This can be accomplished by hardcoding a prompt into the action configuration itself and then just have the user input the text that needs to be summarized.
  * Why: Pre-configured actions tailored to specific use cases streamline the user experience, making it easier for users to set up and use your app effectively.
* Create Use-Case Specific Dropdown:  
  * For example, a “Send Prompt" action could have a dropdown of available “use-cases” that when selected, pre-fill input fields for the user. This can be accomplished by having a mapping of sorts for your use-cases and some complex logic using `altersDynamicFields: true` to then have all of your input fields as custom ones which are loaded in via functions based on the the use-case selected and the default of them pre-filled.
  * **Why:** Pre-configured AI prompts tailored to specific use cases streamline the user experience, making it easier for users to set up and use your app effectively and for them to understand how the AI is working where they could then tweak the prompt/other input fields themselves if need be.
  * [Documentation](https://github.com/zapier/zapier-platform/blob/main/packages/schema/docs/build/schema.md#fieldschema)

### 5. Value of Zap Templates  

**Pain Point:** Users often need help figuring out how to set up Zaps for common use cases.

**Recommendation:**

* Provide [Zap Templates](https://platform.zapier.com/publish/zap-templates):  
  * Create templates for common use cases with pre-mapped variables and good starter prompts.  
  * **Why:** Templates serve as a starting point, helping users quickly set up their Zaps without having to configure everything from scratch.

By addressing these pain points with the recommended strategies, you can significantly improve the user experience and functionality of AI apps on the Zapier platform. For detailed guidance and support, always refer to the [Zapier Developer Documentation](https://platform.zapier.com/docs) or contact the [Zapier support team](https://developer.zapier.com/contact).
