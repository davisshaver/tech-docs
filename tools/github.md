# Github

We use Github for all of our development projects. Here's a quick summary:

* Github Issues are often used in conjunction with [Trello cards](tools/trello.md) to break a project into multiple implementation steps.
* We follow a feature branch pull request workflow. Developers are encourage to commit often and keep their commit history clean — no squashing, please. Our pull request workflow enables copious [code review](../team-culture/code-review.md).
* An issue can comprise multiple pull requests. Issues should only be closed after final product owner signoff.
* Pull requests are great for code conversations. Issues are great for product conversations.

Read on for more detail on how we use Github: [Issues](#issues), [Labels](#labels), [Pull Requests](#pull-requests), [Milestones](#milestones).

If you'd like to get a five minute orientation to Github, their [help documentation](https://help.github.com/) is a great place to start.

### Notifications

A small note about email notifications. When you are first added to a project, you'll be subscribed by email to all updates from the repository. If you aren't actively involved with the project, can easily be overwhelming. You can control your notification frequency using this UI in the top right:

![image](https://cloud.githubusercontent.com/assets/36432/7704146/8b0cdb3e-fdf1-11e4-96eb-220c0832ea9b.png)

## Issues

* Issues should only be filed once they can be specific and actionable by development. Github issues are a useful filter for distinguishing what's actually actionable. They're also a useful history for technical conversation that lives close to the codebase.
* Clear titles make everything much more manageable. For instance, "Twitter optimization" is better as "Incorporate Twitter Card meta tags into header".
* Use in-description task lists to itemize components of the issue: `* [ ] Specific thing needing to be done`
* Be descriptive in your issue description. Feel free to rewrite/modify as needed to clarify. If your issue is related to a Trello Card, link them explicitly.

## Labels

Across our internal, private repositories, we have a consistent set of labels to make our issues understandable across repos.

* [bug](https://github.com/issues?utf8=%E2%9C%93&q=label%3Abug+user%3Afusioneng+sort%3Aupdated-desc+is%3Aopen+is%3Aprivate+) - An issue for an already launched feature that needs to be fixed. How quickly it should be fixed will be denoted by a priority label.
* [priority:blocker](https://github.com/issues?q=label%3Apriority%3Ablocker+user%3Afusioneng+sort%3Aupdated-desc+is%3Aopen+is%3Aprivate) - Issues that need to be addressed as soon as technically possible. These are things that will make or break large business decisions or prohibit a major project from launching on time. When addressing a blocker, engineering may want to consider hacky workarounds to address the immediate business need.
* [priority:high](https://github.com/issues?q=label%3Apriority%3Ahigh+user%3Afusioneng+sort%3Aupdated-desc+is%3Aopen+is%3Aprivate) - Issues that would ideally be addressed within the next few business days. They should be immediately actionable by engineering, and assigned.
* [priority:medium](https://github.com/issues?q=label%3Apriority%3Amedium+user%3Afusioneng+sort%3Aupdated-desc+is%3Aopen+is%3Aprivate) - Issues that would ideally be addressed within two to three weeks of creation.
* [priority:low](https://github.com/issues?q=label%3Apriority%3Alow+user%3Afusioneng+sort%3Aupdated-desc+is%3Aopen+is%3Aprivate) - Actionable issues we want to get to when we have time. The key is to keep these concise - anything too vague needs to go to _for-the-future_, developed as a Trello card, or published in 02.
* [review:design](https://github.com/issues?utf8=%E2%9C%93&q=label%3Areview%3Adesign+user%3Afusioneng+sort%3Aupdated-desc+is%3Aopen+is%3Aprivate+) - This unit of work currently needs to be reviewed in some way by design.
* [review:engineering](https://github.com/issues?utf8=%E2%9C%93&q=label%3Areview%3Aengineering+user%3Afusioneng+sort%3Aupdated-desc+is%3Aopen+is%3Aprivate+) - This unit of work currently needs to be reviewed in some way by design.
* [review:product](https://github.com/issues?utf8=%E2%9C%93&q=label%3Areview%3Aproduct+user%3Afusioneng+sort%3Aupdated-desc+is%3Aopen+is%3Aprivate+) - This unit of work currently needs to be reviewed in some way by product.

## Pull Requests

Code is developed on feature branches. Pull requests are where we [discuss the development in progress](../team-culture/code-review.md), and determine whether a given feature branch is ready for merging to master.

Please create your pull request as soon as you start work on a branch. If you are working on the pull request, assign it to yourself. If you're want feedback or a #reviewmerge from someone else, assign the pull request to them.

Remember to check your diff regularly to make sure you're only changing code you expect to be.

When creating a branch, please use the following naming structure: <code>(number of original Github issue)-followed-by-keywords-describing-the-project</code>.

When creating a pull request, please use a clear title and reference the issue in the pull request description:

![image](https://cloud.githubusercontent.com/assets/36432/4772116/4444b6da-5b95-11e4-89cc-2106064a977a.png)

This makes it easy to see the history of pull requests for an issue:

![image](https://cloud.githubusercontent.com/assets/36432/4772139/58f18cca-5b95-11e4-8895-6f8dc5b42cbc.png)

When a pull request touches anything visual or on the frontend, include a screenshot so it's easier to confirm expected results.

Issues should exist for pull requests as much as possible. Issues are how we track a feature question from creation to closing.

## Milestones

Milestones are sometimes used alongside our Trello-based status workflow. They are:

* Created on a product scope by product scope basis. For instance, our first milestone was improvements to the editorial experience.
* Assigned a deadline, although this will serve more as a guide than a hard and fast rule. We don’t want to cut corners just because we have a deadline.
* All enhancement issues will be created in advance of the milestone starting. Designs will be added as applicable, and implementation vetted from a technology perspective.
