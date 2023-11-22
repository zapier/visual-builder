---
title: Zapier integration structure for a project management app
order: 3
layout: post-toc
redirect_from: 

---

# Zapier integration structure for a project management app

While you can't automate project work, you can automatically add tasks, create new projects, and keep track of progress via an app integration on Zapier.

To add a project management app integration in the Platform UI:

## Prerequisites 

- A [Zapier account](https://zapier.com/sign-up).
- If you haven’t used Zapier before, you'll want to learn the basics in our [Zapier Getting Started Guide](https://zapier.com/learn/zapier-quick-start-guide/).
- Familiarity with your app's API documentation and available endpoints.
- Review the [Platform UI Tutorial](https://platform.zapier.com/quickstart/ui-tutorial). 

## 1. Add triggers for common record types in each project

- Check out the [common record types](https://platform.zapier.com/build/recommended-integration-features#project-management) used as triggers by other project management apps. 

- For apps with many record types, consider including a _New Activity_ trigger, with options to let users choose which type of activity should trigger the Zap.

![new activity trigger](https://cdn.zappy.app/b34f31e26be51d5581f2a669c62c8d14.png)

- Build separate triggers for new and updated records. _Updated_ triggers for project management apps are most useful as these updates affect work to be done. Users want to know if the task deadline changed, if details were added or the scope was redefined, or if someone completed something.

- It is strongly recommended to ensure that any trigger behavior encompasses all updates that are visible to a logged-in user in your app's user interface, independent of admin/creator permissions for a record type. Users expect to be able to automate off any record that is shared with them, regardless if they’re an admin/creator or not. If this is not possible with your API, make this clear in the Trigger description. For example, for a _New Note_ trigger, add help text such as "Triggers when the **connected** user account adds a note to a project."

- Allow users to filter which records they want to trigger on. For example, a _New Task_ trigger could trigger when tasks are added to any project _or_ to one specific project. Include [dynamic dropdowns](https://platform.zapier.com/build/input-designer#dynamic-dropdown) ordered by the most recently added to fetch accounts, projects, lists, and other items users would want to filter.

![Trigger Filter Options](https://cdn.zappy.app/fe08bdcbf666e8f2961f0c2b3932b460.png)

- Project management records are linked to other records in your app. If the data is visible for that record in your app, users expect to see it in their Zap as well. For example, a "New Task" trigger should include details about the task's project too. 

- Include both IDs for linked data in the response output so they can be mapped to your app’s action steps, as well as human-readable data such as individual fields for project name and description.

- If your record API endpoint does not automatically return additional linked data beyond the ID or name of the record, add custom code to your trigger API call to fetch relevant data linked to the record as well.

![Linked Data in Trello](https://cdn.zappy.app/3f2f5450c1c7981b41a4d2234047bfaa.png)

## 2. Include common search actions

- Users expect to have searches for top-level records available for project management integrations so they can add child-level details. For example, a Project can have many Tasks, and some projects may have the same or similar tasks. Users are more likely to want a _Find Project_ search so they can add tasks to projects, rather than a Find Task search which may not return the precise item they need.

- Configure the search to find an existing record, returning it in the same format the trigger returns records to give a consistent experience and allow the data to be used in the same manner in later actions.

- Offer multiple search key and value options where applicable. For example, a _Find Project_ search should let users search by project ID and name. The former is useful for searching based on data in previous steps, where the latter is useful to find projects with human input. Return exact matches first and provide help text to communicate to users how the search matches records to search terms.

![Project Management Search Options](https://cdn.zappy.app/542be79e48ccbd6d12e43646690dcebb.png)

## 3. Include common create actions

- Check out the [common record types](https://platform.zapier.com/build/recommended-integration-features#project-management) other project management apps have create actions for.  

- Add corresponding _Update_ actions with available _Search_ actions to make it easier for users to update the correct project record. 

- Account for linked records in action input fields, so when your app’s UI allows users to create a task and link it to existing projects, the same action is available via a Zap, via a [dynamic dropdown](https://platform.zapier.com/build/input-designer#dynamic-dropdown) to fetch linked record options and let users select them. 

- Do not have a single action create multiple records. When a user creates a new task through Zapier, this should only create new tasks, and should not also create other linked records at the same time. Rather include a separate action to create the other linked record, along with a task update action to link the task after the other record is created. This reduces the chance for errors and record redundancy.

- Optionally link a [search connector](https://cdn.zappy.app/99829074f857d0938c0ba7b3c5e97e84.png) to linked record input fields if users need to have the Zap find the correct related record, and map the found ID to the input field. To add that user prompt you'll need to work in the [Platform CLI](https://github.com/zapier/zapier-platform/blob/main/packages/cli/README.md#search-powered-fields). 

## 4. Test your triggers and actions

Make Zaps with the following criteria to ensure your app integration works as expected:

- Connect your integration with [other project management apps](https://zapier.com/apps/categories/project-management), to see if the data your integration returns blends well with our common apps. Companies frequently use integrations to copy tasks and projects across a blend of project management apps to keep track of work between teams.
- If your integration supports events or tasks with due dates, connect a Zap to popular [calendar or scheduling apps](https://zapier.com/apps/categories/calendar) to verify those dates can be added to other apps. 
- If your integration has many nested items (such as projects containing sub-projects with tasks and sub-tasks), try setting up a few Zaps to see if the behavior across nested objects is the same as parent objects. Data returned should always be the same format; if your API doesn’t enable access to nested objects, note that in the help text for that trigger/search/action.