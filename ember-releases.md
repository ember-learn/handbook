# Ember Releases

When a new version of Ember is released,
the learning team has to make sure some parts of our infrastructure are adequately updated to account for it.
**Please update the following in the listed order**:

## Preparation (ideally) before release day: 

1. [Merge Tutorial Updates](#merge-tutorial-updates)
1. [Create the release blog post](#create-the-release-blog-post)
1. [Deprecations](#deprecations)

### Merge Tutorial Updates

💁 manual process

🚨 This process is not well defined and needs to be streamlined ASAP 🚨

Check if there are any [`Tutorial Updates` PRs](https://github.com/ember-learn/guides-source/pulls?q=is%3Apr+%22Tutorial+Updates%22+is%3Aopen) that need to be merged **before ember-cli is released**. If we have missed our window then the `guides/release/tutorial/part-1/orientation.md` will show the **new ember-cli version** and when we snapshot the `release` folder (i.e. copy it to a folder with the previous release number) then the tutorial will be wrong.

### Create the release blog post

💁 manual process

**NOTE** ember-source, ember-data, and ember-cli must already be released.

1. Generate a new blog post for the release with `ember generate release-blog MAJOR.MINOR` where
MAJOR.MINOR is the version number, i.e `4.5`. There is a `--authors` option available which
defaults to the Ember Learning Team.
3. Open a PR with the template at [https://github.com/ember-learn/ember-blog/pulls](https://github.com/ember-learn/ember-blog/pulls).
4. Tag core teams in `core-meta` on discord to fill in details and approve for their respective teams.

### Deprecations

💁 manual process

1. Clone [deprecation-app](https://github.com/ember-learn/deprecation-app).
2. To see deprecations in `ember-source`, you can visit [https://deprecations.emberjs.com/v3.x/](https://deprecations.emberjs.com/v3.x/).
3. Check if there are deprecations listed under "Upcoming Features" that are a part of the new release (e.g. `v3.25`). If there are, proceed with this step, if there are not, you can skip to the Guides step.
4. Find the relevant Markdown file in `/content/ember/v3` folder.
5. Update the frontmatter `since: "Upcoming Features"` to `since: "v3.25"`.
6. Repeat steps 2-5 for deprecations in `ember-data`. ([https://deprecations.emberjs.com/ember-data/v3.x](https://deprecations.emberjs.com/ember-data/v3.x))
7. Open a pull request.

## On "release day":

### Prerequisites 

⚠️ WAIT! ⚠️ - Please ensure that Ember, Ember CLI and EmberData have each released before proceeding

We have a CLI tool called [`tool-new-release`](https://github.com/ember-learn/tool-new-release) that automates many of the below steps and is recommended. Each of those automated steps has a manual fallback process.

- install `tool-new-release` - this automates most of the things (deprecated and soon will not be needed)
- install 1Password and make sure you have access to the `Ember CLI` vault
- install `1password-cli`
- sign in to `1password-cli`
- sign in to 1password `Ember CLI` vault

### Follow these release steps in this specific order:

<!-- 1. run tool-new-release -->
1. [Guides PR](#guides)
1. [merge guides PR](merge-guides-pr)
1. [Guides search](#guides-search)   
1. [API documentation](#api-documentation)
1. [API docs search](#api-docs-search)
1. [merge blog PR](#merge-blog-pr)
1. [merge deprecations PR](#merge-deprecations-pr)
1. [Release pages](#release-pages)
1. [Upgrade Guide](#upgrade-guide)
1. [Glitch Ember starter](#glitch-ember-starter)
1. [Ember Wikipedia](#ember-wikipedia)
1. [Release bot](#release-bot)

### Guides

🤖 automated process

Run the following command with `ember-learn-release-tool`

```
pnpm dlx ember-learn-release-tool guides
```

Follow the prompts and open a PR for the new version

<details>
    <summary>Fallback 💁 Manual process</summary>

    Instructions are found in [MAINTAINERS.md](https://github.com/ember-learn/guides-source/blob/master/MAINTAINERS.md#deploying-a-new-version).

</details>

### Merge Guides PR

Merge the PR that you generated in the Guides step. Ensure that it is successfully deployed and manually spot-check the Guides before proceeding.

### Guides search

🤖 automated process

Run the following command with `ember-learn-release-tool`

```
npx ember-learn-release-tool guides-search
```

Follow the prompts and when it looks like it is done deploying you should test the search on https://guides.emberjs.com/

<details>
    <summary>Fallback 💁 manual process</summary>

    Instructions are found in [MAINTAINERS.md](https://github.com/ember-learn/guides-source/blob/master/MAINTAINERS.md#updating-the-guides-search).
</details>

### API documentation

💁 manual process

Instructions are found in the [README of ember-jsonapi-docs](https://github.com/ember-learn/ember-jsonapi-docs).

### API Docs Search

💁 manual process

Instructions are found in the [README of algolia-index-update-scripts](https://github.com/ember-learn/algolia-index-update-scripts).

### Merge Blog PR

Ensure the Blog post PR is ready to be released (final date checks, check no bug fixes, features or deprecations are missing from each package, double check grammar/spelling, general polish, etc.), and once it is ready merge the PR. Ensure the blog post is deployed.

### Merge Deprecations PR

Ensure the deprecations PR is ready to be merged (ensure no new deprecations have been added that need to be addressed if the PR has been open for some time). Ensure the deprecations PR is deployed.

### Release pages

💁 manual process

- Clone [ember-website](https://github.com/ember-learn/ember-website)
- Edit `data/project/ember/release.md`
  - update `lastRelease` to be the first patch version of the new `ember-source` release
  - update `date` to be the date of the first patch version of the new `ember-source` release
- Edit `data/project/emberData/release.md`
  - update `lastRelease` to be the first patch version of the new `ember-data` release
  - update `date` to be the date of the first patch version of the new `ember-data` release
- Edit `data/project/ember/beta.md`
  - update `lastRelease` to be the latest beta version of `ember-source`
  - update `date` to be the date of the latest beta version of `ember-source`
- Edit `data/project/emberData/beta.md`
  - update `lastRelease` to be the latest beta version of `ember-data`
  - update `date` to be the date of the latest beta version of `ember-data`

If there is a new LTS release then you should make the following changes too: 

- Edit `data/project/ember/lts.md`
  - update `lastRelease` to be the **latest patch** version of the new LTS release
  - update `date` to be the date of the **latest patch** version of the new LTS release
- Edit `app/controllers/releases/lts.js`
  - make sure the entries in the array are correct
  - if there is a LTS version that has been removed from support then remove it and add it to the html table on `app/templates/releases/lts.hbs`

Pro tip: if you're looking for the exact date that a project has released you can run `npm info ember-source time` and see the list of releases and dates.

Note: https://libraries.io/npm/<your package> may not contain all the versions so it may be best to check tags (not releases) in the GitHub project for dates.

### Upgrade Guide

💁 manual process

1. Clone [upgrade-guide](https://github.com/ember-learn/upgrade-guide) and run `npm install`. (You can run `ember serve` and visit [http://localhost:4200](http://localhost:4200) to see your changes take effect.)
2. Run `ember generate upgrade-notes <NEW_VERSION>` (e.g. `ember g upgrade-notes 3.25`) to create 3 Markdown files.
3. Edit the files by recording features and deprecations. You can find short descriptions for features and deprecations in the release blog post.
4. Edit the `app/utils/ember-versions.js` file. Append the release version to the end of the array.
5. Run `npm run lint` and `npm test`. (You will likely need to update 1 test assertion. It checks how many features and deprecations can be seen since Ember 3.15 release.)
6. Open a pull request, then merge it.

### Ember Wikipedia

💁 manual process

Note: The Wikipedia page may have already been updated automatically for the version you are releasing. If that is the case, you can skip this step.

1. Go to [https://en.wikipedia.org/wiki/Ember.js](https://en.wikipedia.org/wiki/Ember.js).
2. Click on the pencil icon next to the version. 
<img width="352" height="305" alt="Screenshot 2025-09-10 at 17 00 20" src="https://github.com/user-attachments/assets/c9b2728f-4798-4021-8bfb-b2017b518cea" />

3. Add the new version to the bottom of the `software version identifier` list
   1. Make sure to also add the reference, including the title. The title also needs to have a language, you can set this by clicking the keyboard icon that's popping up.
   2. After you have clicked published you need to update the ranks of the versions. Click the up-arrow above the circle to make it prefered and set the previous version back to normal by clicking on the circle. 
<img width="200" height="97" alt="Screenshot 2025-09-10 at 16 52 41" src="https://github.com/user-attachments/assets/07d600b4-dac9-4f16-bc36-43ab73ca4984" />

### Release bot

💁 manual process


1. Go to the core meta channel in Discord.
2. Mark current release as done with `/release-done blog`.
3. Schedule next release with the `/release-next <version M.mm> <date MM/DD/YYYY>` command. E.g. `/release-next 3.26 03/22/2021`. Note, the date should likely be 6 weeks from the Monday that the current release week started with (regardless of how late we might be). https://wolframalpha.com/ can help with accurately calculating this date.
