# Code Review

A constant process of code review is a core part of our team's software development workflow. Code review and pairing on code are necessary to maintain quality output, as well as build cohesive styles in our work. Having a well-understood and cohesive style can make all our work easier to approach and maintain for new as well as established developers. If done right, code review can also be a learning process for all involved. Here's [a typical code review workflow at Fusion](#a-typical-code-review-workflow):

- [What code review is](#what-code-review-is)
- [How to review code](#how-to-review-code)
- [How to receive code review](#how-to-receive-code-review)

## A typical code review workflow

We're currently using Github for everything. Read up on [our Github workflow](../tools/github.md) for details of process, naming, usage of issues and pull requests. A moderately complex issue will typically be addressed across multiple pull requests, each tackling a distinct part of the issue. This makes review simpler, because each review stage wil be looking at a small code.

- On every commit pushed to a GH branch, our CI automated tests -- linting for all code, unit tests for functional code, and ideally, behavioral and automated acceptance testing -- are run on Travis. If the build passes, the PR can be reviewed. If not, the original developer will receive email notification that their pull needs to be fixed before it can be reviewed or merged.
- When the original developer is satisfied with their work, they can assign the pull request to another team member for review. 
- Simple pull requests can be merged by the developer who reviews them. More complex changesets will often require conversations back and forth between reviewer and developer.
- Github's "Files Changed" tab is a good place to leave inline comments on specific parts of the changeset. More general comments can be left on the pull request's "Conversation" tab.
- The reviewer may suggest changes in the form of a pull request off of the branch being reviewed, or in comments. - When the reviewer is done with their review, they will assign the PR back to the original developer to address any issues which were brought up.
- The developer will make changes suggested, discuss the issue for clarity, and may reassign it to the reviewer when they are satisfied with their work.
- If a pull request needs final cleanup before merging (for example, merging master back into the feature branch so that it can merge cleanly), the reviewer can commit directly to the branch. However, avoid rewriting code without consultation.
- When the reviewer is satisfied with changes, they can either merge or assign the pull request to a team lead to merge and push to production.

## What code review is

A good way to visualize the objectives of code review is [this analogy](http://blog.d3in.org/post/111338685456/maslows-pyramid-of-code-review) to Maslow's "Hierarchy of Needs" pyramid. From most basic to the highest level, a reviewer is checking that code is **Correct**, **Secure**, **Readable**, **Elegant**, and **Altruistic**. It's important to keep this sense of priorities: if a change introduces unhandled edge cases, bugs, or security vulnerabilities, those issues need to be addressed before coding style guidelines or beautification practices preferences will matter.

![code-review-pyramid](https://cloud.githubusercontent.com/assets/665992/7326019/1603bcd2-ea77-11e4-8510-4d7f76ca2ad1.png)

 ### How to review code

*As a reviewer*, your first job is to get an understanding of what the proposed change does and why it's essential. There's no point in critiquing anything until you understand what it does, why it's necessary, and what decisions went into the way this was built.

Next, look it over for correctness. Are all functions which take parameters and produce output covered by unit tests? Do they actually do what they're supposed to? Can you picture an edge case where a function would error unexpectedly or return something other than the expected result? If this has a UI component, does it render properly in all situations? Does it have sane fallbacks for uncommon situations? 

If it addresses the business and UX requirements, the next thing to check for is security. Does it follow basic sanitization and escaping practices for all untrusted input? If it interacts with other aspects of the codebase, is it liberal in the inputs it accepts and conservative in its output, making sure to only pass expected values? If it exposes data to authorized users though Ajax or post actions, does it use nonces properly to protect against CSRF attacks? Think like an attacker. If there's any way a malicious agent could exploit this code, or an unlucky user could trigger a bug that fatals or looks bad, it's your job to find it.

Next, check for readability. Functions, variables, and files should be named clearly according to their meaning. HTML elements, attributes, and CSS selectors should be named semantically and consistently with existing usage. Everything should adhere to the surrounding code style. 

> All code in any code-base should look like a single person typed it, no > matter how many people contributed. > > -- [Principles of writing Idiomatic Javascript](https://github.com/rwaldron/idiomatic.js/)

As readability is inherently subjective, this requires the ability to look back from the immediate code changes to the bigger picture. Think of someone months down the road trying to trace a given code path through the current changeset. Are there unnecessary steps that could be simplified? Are code comments and inline documentation robust enough to recreate the thought process behind the code?

Finally, check for elegance and overall quality. Code should follow existing and known patterns, so that others can understand it at a glance. If a change introduces a chance to refactor surrounding functionality, to abstract and standardize old code into new patterns, suggest those opportunities. 

 ### How to receive code review

*As the person receiving the code review*, your job is to learn from suggestions. Defensiveness, stubbornness, or impatience can prevent you from getting the most out of suggestions. It's OK to explain yourself if you feel the reviewer seemed to misunderstand your intent. Arguing semantics or insisting on the correctness of one approach is almost always a bad habit and distracts from the team process. If something isn't clear to someone familiar with the codebase who's reviewing your work today, it will definitely be unclear to a new developer being on-boarded six months from now.

It's best to respond to the issues addressed by the reviewer immediately if possible. Keep in mind that the review process requires context switching on the part of the reviewer as well as on your part, and the more immediate that process is, the less disruptive that context switch will be.

## Additional readings

* [Glen Sanford: On code review](http://glen.nu/ramblings/oncodereview.php) - "Pending code reviews represent blocked threads of execution[, code review should always be your top priority]"

* [The Ten Commandments of Egoless Programming](http://www.techrepublic.com/article/the-ten-commandments-of-egoless-programming/) - "Understand and accept that you will make mistakes. The point is to find them early, before they make it into production." 