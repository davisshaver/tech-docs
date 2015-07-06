# Merge and Deploy Responsibilities

The end result of a [code review process](./code-review.md) is a merge (to
our master branch) and deploy (to WordPress VIP, in the case of our theme;
to Heroku or other production environment, or to a public tagged release
on Github and wordpress.org/plugins, in the case of WordPress plugins).

## Responsibilities of a code merger

At Fusion, we merge to our primary theme an average of 10-15 times a day.
Each of these pull requests represents a feature which is important to
some portion of our stakeholders or our audience. Each also represents
a potential breakage which can cause disruption, inconvenience, or
embarrassment. It is the responsibility of the merger to identify these
possibilities and be prepared to deal with them if they arise.

Merging a pull request is a way of saying "I've reviewed this, and I'm
confident that it will not break anything." It also implies taking
responsibility for fixing or directing fixes for any things which may be
broken.

While we do not currently have a automatic deployment process for merged
pull requests, we are working on automating this process, and 

Some basic guidelines apply to all code deploys:

- Deploy responsibly. Be around up to an hour or more after code is
  deployed to catch fallout. Keep big changes to the beginning of the day,
  and beginning of the week.
- Have an eye to whether it's great code. Refactors rarely happen, so make
  sure you're deploying code you want to live with in the future.
- Keep deploys as small and as atomic as possible. When things go wrong,
  it's much easier to track down and fix small changes. 
- Judge when to leave feedback for the engineer to clean up, and when to
  just take it over the finish line for them. Work through at least
  a couple rounds of feedback before diving in to clean up any remaining items.
- After merging and deploying a pull request with an associated issue,
  mark the issue with the "QA" label, so that product managers can follow
  up in production and verify that the code pushed actually fixed the
  issue.

Special attention should be given to working with Automattic's engineers
who perform the final review and deployment step for our production theme:

- Commits (to VIP) should be a descriptive subject and link to
  corresponding pull requests. This is really valuable context for other
  people watching your commits, and for yourself three months down the
  road.
- Address VIP feedback promptly. Prompt, courteous replies lead to
  a strong working relationship. When talking about code, include the SVN
  revision.


