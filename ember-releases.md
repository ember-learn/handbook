# Ember Releases

NOTE: The steps below are manual deploy steps. We have a CLI tool called
[`tool-new-release`](https://github.com/ember-learn/tool-new-release)
that automates these steps.

When a new version of Ember is released,
the learning team has to make sure some parts of our infrastructure are adequately updated to account for it.
**Please update the following in the listed order**:

1. [Release blog post](#1-release-blog-post)
2. [Guides](#2-guides)
3. [API documentation](#3-api-documentation)
4. [Release pages](#4-release-pages) (index, stable, beta, LTS)
5. [Deprecations](#5-deprecations)
6. [Upgrade Guide](#6-upgrade-guide)
7. [Glitch Ember starter](#7-glitch-ember-starter)
8. [Ember Wikipedia](#8-ember-wikipedia)
9. [Release bot](#9-release-bot)

The Guides and API docs should be published first, followed by the Release blog post. This way, links to the Guides and API docs can be included in the Release blog post. All other steps come after the blog post.


## 1. Release blog post

**NOTE** ember-source, ember-data, and ember-cli must already be released.

1. Generate a new blog post for the release with `ember generate release-blog MAJOR.MINOR` where
MAJOR.MINOR is the version number, i.e `4.5`. There is a `--authors` option available which
defaults to the Ember Learning Team.
3. Open a PR with the template at [https://github.com/ember-learn/ember-blog/pulls](https://github.com/ember-learn/ember-blog/pulls)
4. Tag core teams to fill in details
5. Merge the relevant blog post once it is OK'ed by all the team representatives.

Once the release post is out, the website resources may be deployed.

## 2. Guides

Instructions are found in [MAINTAINERS.md](https://github.com/ember-learn/guides-source/blob/master/MAINTAINERS.md#deploying-a-new-version).

## 3. API documentation

1. Clone the `ember-jsonapi-docs` repository:
```bash
git clone https://github.com/ember-learn/ember-jsonapi-docs.git
cd ember-jsonapi-docs
```
2. Go to the heroku instance, navigate to `Settings`, click `reveal config vars` and use the values seen there as values for the following variables in your local environment:
    1. `AWS_ACCESS_KEY`
    2. `AWS_ACCESS_KEY_ID`
    3. `AWS_SECRET_ACCESS_KEY`
    4. `AWS_SECRET_KEY`
    5. `AWS_SHOULD_PUBLISH`
4. Run `yarn run start --sync`
5. Wait and confirm there were no errors
6. Done!

## 4. Release pages

The next release date is not affected by "delays", and should always be calculated as original date + 6 weeks.

1. Clone [ember-website](https://github.com/ember-learn/ember-website)
2. Edit the following files:
    1. `data/project/ember/lts.md`
    2. `data/project/ember/release.md`
    3. `data/project/ember/beta.md`
    4. `data/project/emberData/release.md`
    5. `data/project/emberData/beta.md`

## 5. Deprecations

1. Clone [deprecation-app](https://github.com/ember-learn/deprecation-app).
2. To see deprecations in `ember-source`, you can visit [https://deprecations.emberjs.com/v3.x/](https://deprecations.emberjs.com/v3.x/).
3. Check if there are deprecations listed under "Upcoming Features" that are a part of the new release (e.g. `v3.25`).
4. Find the relevant Markdown file in `/content/ember/v3` folder.
5. Update the frontmatter `since: "Upcoming Features"` to `since: "v3.25"`.
6. Repeat steps 2-5 for deprecations in `ember-data`. ([https://deprecations.emberjs.com/ember-data/v3.x](https://deprecations.emberjs.com/ember-data/v3.x))
7. Open a pull request.

## 6. Upgrade Guide

1. Clone [upgrade-guide](https://github.com/ember-learn/upgrade-guide) and run `npm install`. (You can run `ember serve` and visit [http://localhost:4200](http://localhost:4200) to see your changes take effect.)
2. Run `ember generate upgrade-notes <VERSION>` (e.g. `ember g upgrade-notes 3.25`) to create 3 Markdown files.
3. Edit the files by recording features and deprecations. You can find short descriptions for features and deprecations in the release blog post. (See [step 3](#3-release-blog-post))
4. Edit the `app/utils/ember-versions.js` file. Append the release version to the end of the array.
5. Run `yarn lint` and `yarn test`. (You will likely need to update 1 test assertion. It checks how many features and deprecations can be seen since Ember 3.15 release.)
6. Open a pull request, then merge it.

## 7. Glitch Ember starter

Since generating a new application using ember-cli made Glitch run out of memory,
the application is cloned from [ember-new-output](https://github.com/ember-cli/ember-new-output).

1. Log in to [https://glitch.com/](https://glitch.com/)
1. Go to [https://glitch.com/edit/console.html?emberjs](https://glitch.com/edit/console.html?emberjs)
1. Update the local repository with `git fetch`
1. Check out the release version with `git reset --hard <VERSION>`. Replace `<VERSION>` with the correct tag, e.g. `v.3.25.0`
1. Add the following snippet for the Glitch button in `app/index.html`:
```
<!-- include the Glitch button to show what the webpage is about and
  to make it easier for folks to view source and remix -->
<div class="glitchButton" style="position:fixed;top:20px;right:20px;"></div>
<script src="https://button.glitch.me/button.js"></script>
```
5. Edit `package.json` to explicitly include port 4200: `"start": "ember serve -p 4200"`.

## 8. Ember Wikipedia

1. Go to [https://en.wikipedia.org/wiki/Ember.js](https://en.wikipedia.org/wiki/Ember.js).
2. Click the `Edit source` tab (you will likely need to login).
3. Update the `latest release version`, `latest release date`, `latest preview version` & `latest preview date` in the Infobox if they need updating.
4. Be sure to update the accessdate for the citation url of the releases page referenced on the `latest release date` line.

## 9. Release bot

1. Go to the core meta channel in Discord.
2. Mark current release as done with `!release done blog`.
3. Schedule next release with the `!release next M.mm YYYY-MM-DD` command. E.g. `!release next 3.26 2021-03-22`.
