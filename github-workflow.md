# GitHub workflow

This document describes the GitHub workflow process and permissions rules for our team. 
It does not apply to undeployed apps that are in greenfield development.

## Reviews

Our repositories require reviews by one or more people as a requirement to merge.

For very minor changes (typos, wording edits affecting one sentence, etc) a
community member's review is enough. Reviews are a great opportunity to
get more people involved in Ember!

For more significant changes, a core team member's review is required. 
Examples include restructuring a paragraph, adding a brand new paragraph or example,
confirming that a bugfix doesn't break something else, etc.
The review should be requested for at least one of the lead project maintainers.
For example, `ember-styleguide`'s needs, goals, and active team are very
different from the Guides, and reviews are a chance to make sure that
the project's goals are being met and varying standards are upheld.
In cases of conflicting reviews, the decision should be brought to the
team for consensus.

For major changes, such as rearranging the flow of an app, 
creating new views/subpages, changing many lines, substantive styling changes,
or architectural work, there should be consensus of the core team before
merging. Consensus can be gathered either by GitHub PR reviews, as
decided and recorded in the learning team meetings, as discussed in the
team chat, via RFC, or by approving comments on a Quest issue.


### RFCs

In some cases, an RFC may be required before a PR can be merged. For an example of
learning team RFCs, see [#431](https://github.com/emberjs/rfcs/pull/431).
For RFC guidelines, see the [rfcs README](https://github.com/emberjs/rfcs).

## Admin and maintainer privileges

At the core team's discretion, some number of members may receive permission
to review and merge. Some number may also have the ability to override
reviews, change settings, and change the permissions of other people.
This section outlines our norms for making the right use of these abilities.

All members should strive to provide meaningful feedback and seek reviews
from other people so that their work can be iterated upon and merged.
Anything that can wait for a review, should.

Admins should not use their ability to merge without reviews unless the
following circumstances arise:

1. It's an emergency hotfix: something is quite broken, like not rendering at all, 
and the person has high confidence in their fix. Hotfixes should be announced
in the core team channel.
2. It's part of normal, documented deployment process of code that has been
previously reviewed. An example is tagging and versioning. These should
also be announced in the core team channel.

If the GitHub permission rules must be edited to apply one of the above,
they should be put back when an Admin is finished.

### How to override reviews

When necessary, here's how to override reviews. Not all members will have
this ability.

1. Remember to announce in the team channel what you are doing,
and seek a review if possible one last time.
2. Go to the project's settings
3. Choose Branches
4. Choose to edit "master" under Branch protection
5. Uncheck "Include administrators"
6. Do your work
6. Reenable "Include administrators" and also confirm that
"Require reviews before merging" is still checked.

## When to follow these rules for new projects

Once a greenfield project has reached MVP, and is preparing for
deployment, it should have branch protection put in place and
begin following the rules outlined here.
