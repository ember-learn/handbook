# Ember Guides - Processes and Policies

This page is intended to document the processes and high-level decisions around developing the [Ember Guides](https://guides.emberjs.com/). This is not intended to be a contributing guide, all contributing information should be available in the [guides-source CONTRIBUTING.md](https://github.com/ember-learn/guides-source/blob/master/CONTRIBUTING.md).

## Backporting Changes
As a general rule we only ever update the documentation for the latest version of the guides. This used to be a technical restriction in the past due to the technical difficulty of updating older guides, but now this policy is primarily to minimise the maintenance burden of the Guides.

The rule to not backport changes has not come out of a lack of resources or time, it is more of an indication of priorities. For example: if it would take 5 hours to backport a large change to the Guides which would be valid for the previous 3 versions of the Guides, it is accepted that those 5 hours would be better spent improving the current Guides instead.

There have been some exceptions to this rule in the past:

- Minor changes that don't cause conflicts
- Documentation that is missing and is not documented anywhere else
  - a good example for both of these points was the [PR adding Optional Features documentation](https://github.com/ember-learn/guides-source/pull/64)
- Fixes to broken links
- Fixes to typos
- Fixes to 404s or anything that would affect SEO

All planned exceptions to this rule **must** be agreed to by the Learning Team and **should** be agreed in a weekly meeting before any work commences

## Table of Contents for Guides

The following rules of thumb help us organize content. They apply to all Guides (CLI, Ember.js, Ember Data, etc).

1. The Guides should show how pieces fit together, not repeat content from the API docs. If a lot of description is given for one single feature, as it works in isolation, it's a sign that it belongs in API docs and should just have a link to it from the Guides.
2. We do our best to give new pages names that match their general web development concept, rather than Ember-specific implementation names.
3. We aim to help our existing users find and understand Editions. As syntax changes across the board, it's important to give people easy access to materials that help them get up to speed quickly, as well as give newcomers a clue of how to translate older code samples from articles and Q&A into the latest and greatest approach. For Ember.js, these conversion guides will be kept in `Upgrading/Editions`, which contains content that will change as Ember grows and new features land. This guide can be linked to from throughout the rest of the Guides, rather than including much conversion content inline. This means that the new user experience is not cluttered with older syntax, but all users can still follow the trail when they need to.
3. The Guides should be able to be read like a book, providing a thoughtful order that builds upon previous knowledge. Topics that are foundational for understanding other sections should go earlier in the list.
4. We follow [RFC 431](https://github.com/emberjs/rfcs/pull/431) in order to improve the Guides learning experience. We aim to keep working to improve the learning flow after reaching MVP, and the RFC should not be considered "feature complete." After MVP is close to being reached, more RFCs should be proposed.


The goal of this document is to describe how nested topics in the Ember Guides could improve UX and content navigation.

## Nesting levels

The Ember Guides support nested topics in the sidebar, which we will use sparingly to organize in-depth content, to a maximum of 3 levels deep.

There have been multiple projects where people asked if there was an opportunity to have one
more grouping level, such as for the contributing Guides, A11y Guides, or a Cookbook. With Octane, it became clear that
we would need resources like a migration guide, and user feedback indicated that having these migration guides be
one page was too overwhelming. Yet, it seemed bad to have "Octane migration" as a top level topic.
This is where nesting can help:

```
Upgrading
    How to upgrade
    Ember Editions
    Octane migration
       Intro
       Components
       ...
```

In this way, we can logically group in-depth content under the right top-level topic, and create
digestible articles, but without cluttering the main message.

### Rules of thumb for using nesting

Having a structure with too many levels can lead to worse navigation, without some guidelines in place.
A third level of nesting is only appropriate when there are:

- There are more than 4 possible sub-pages to group together
- The content has already been written, and user feedback indicates that it is too much for one article
- The information is something that every Ember developer should be aware of (i.e. it belongs in the Guides)
