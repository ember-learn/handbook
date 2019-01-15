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
- Fixes to 404s or anything that would affect SEO

All planned exceptions to this rule **must** be agreed to by the Learning Team and **should** be agreed in a weekly meeting before any work commences
