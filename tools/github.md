# Github

We use Github for all of our development projects. Here's a quick summary:

* Github Issues are often used in conjunction with [Trello cards](tools/trello.md) to break a project into multiple implementation steps.
* We follow a feature branch pull request workflow. Developers are encourage to commit often and keep their commit history clean — no squashing, please.
* An issue can comprise multiple pull requests. Issues should only be closed after final product owner signoff.
* Pull requests are great for code conversations. Issues are great for product conversations.

Read on for more detail on how we use Github: [Issues](#issues), [Labels](#labels), [Pull Requests](#pull-requests), [Milestones](#milestones).

If you'd like to get a five minute orientation to Github, their [help documentation](https://help.github.com/) is a great place to start.

### Notifications

A small note about email notifications. When you are first added to a project, you'll be subscribed by email to all updates from the repository. If you aren't actively involved with the project, can easily be overwhelming. You can control your notification frequency using this UI in the top right:

![image](https://cloud.githubusercontent.com/assets/36432/7704146/8b0cdb3e-fdf1-11e4-96eb-220c0832ea9b.png)

## Issues

* Clear titles make everything much more manageable. For instance, "Twitter optimization" is better as "Incorporate Twitter Card meta tags into header".
* Use in-description task lists to itemize components of the issue: `* [ ] Specific thing needing to be done`
* Be descriptive in your issue description. Feel free to rewrite/modify as needed to clarify.
* Issues should only be filed once they can be specific and actionable. Ideas and concepts should go in the Fusion for the Future repo.

## Labels

We're rolling with 4 priority levels:

**Blocker:** Items that NEED to be addressed within the next few hours. These are things that will make or break large business decisions or prohibit a major project from launching on time. Rule of thumb: If there's an alternate way of accomplishing an item, it's not a blocker. 

**High:** Items that should be addressed within the next 3 business days. There's no magic number of high priority issues that need to be in the queue at any given time, but they should all be immediately actionable and assigned to a developer for work. 

**Medium:** Items that can be put off until the next full work week. Some of these may soon be designated as high based on developer bandwidth, but if they can't be, your feelings won't get hurt. 

**Low:** Items that we definitely want to get to, but if it takes 2+ weeks to get to them, that's ok. The key is to keep these concise - anything too vague needs to go to <i>for-the-future</i>, developed as a Trello card, or published in 02. These low priority issues should still be actionable, in case a developer wants to grab as part of a relatable higher-ranked ticket. 

## Pull Requests

Code is developed on feature branches. Pull requests are where we discuss the development in progress, and determine whether a given feature branch is ready for merging to master.

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

Milestones are sometimes used alongside our Huboard-based status workflow. They are:

* Created on a product scope by product scope basis. For instance, our first milestone was improvements to the editorial experience.
* Assigned a deadline, although this will serve more as a guide than a hard and fast rule. We don’t want to cut corners just because we have a deadline.
* All enhancement issues will be created in advance of the milestone starting. Designs will be added as applicable, and implementation vetted from a technology perspective.

## Code Reviews

We conduct in depth code reviews with paired engineer teammates and ultimately through the team lead. 

1. Be satisfied with your work
1. Create a pull request and add the issue number to the comments
1. Assign the issue to your partner
1. Have your review partner check the code
1. The partner needs to sign off in the pull request
1. The partner will reassign the issue back to you
1. Move the issue card to ready for launch in huboard
1. Comment on the pull request for the team lead gate keeper to merge to master
1. Once merged mark the issue as completed
