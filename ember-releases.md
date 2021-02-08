# Ember Releases

When a new version of Ember is released,
the learning team has to make sure some parts of our infrastructure are adequately updated to account for it.
**Please update the following in the listed order**:

1. [Guides](#1-guides)
2. [API documentation](#2-api-documentation)
3. [Release blog post](#3-release-blog-post)
4. [Release pages](#4-release-pages) (index, stable, beta, LTS)
5. [Deprecations](#5-deprecations)
6. [Glitch Ember starter](#6-glitch-ember-starter)
7. [Ember Wikipedia](#7-ember-wikipedia)
8. [Release bot](#8-release-bot)

The Guides and API docs should be published first, followed by the Release blog post. This way, links to the Guides and API docs can be included in the Release blog post. All other steps come after the blog post.

## 1. Guides

Instructions are found in [MAINTAINERS.md](https://github.com/ember-learn/guides-source/blob/master/MAINTAINERS.md#deploying-a-new-version).

## 2. API documentation

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

## 3. Release blog post

**NOTE** ember-source, ember-data, and ember-cli must already be released.

1. Go to [https://github.com/ember-learn/ember-blog/pulls](https://github.com/ember-learn/ember-blog/pulls)
2. Merge the relevant blog post once it is OK'ed by all the team representatives.

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

1. Go to [https://deprecations.emberjs.com/v3.x/](https://deprecations.emberjs.com/v3.x/) and [https://deprecations.emberjs.com/v3.x/](https://deprecations.emberjs.com/v3.x/)
2. Check if any of the deprecations listed under "Upcoming Features" are part of the new release
3. Find the relevant deprecation in `https://github.com/ember-learn/deprecation-app/tree/master/content`
4. Update `since: "Upcoming Features"` in the frontmatter to the respective release in the `v3.12` format.
5. Merge and confirm changes on the live website 

## 6. Glitch Ember starter

Since generating a new application using ember-cli made Glitch run out of memory,
the application is cloned from [ember-new-output](https://github.com/ember-cli/ember-new-output).

1. Log in to [https://glitch.com/](https://glitch.com/)
1. Go to [https://glitch.com/edit/console.html?emberjs](https://glitch.com/edit/console.html?emberjs)
1. Update the local repository with `git fetch`
1. Check out the release version with `git reset --hard <VERSION>`. Replace `<VERSION>` with the correct tag, e.g. `v.3.22.0`
1. Add the following snippet for the Glitch button in `app/index.html`:
```
<!-- include the Glitch button to show what the webpage is about and
  to make it easier for folks to view source and remix -->
<div class="glitchButton" style="position:fixed;top:20px;right:20px;"></div>
<script src="https://button.glitch.me/button.js"></script>
```
5. Edit `package.json` to explicitly include port 4200: `"start": "ember serve -p 4200"`.

## 7. Ember Wikipedia

1. Go to [https://en.wikipedia.org/wiki/Ember.js](https://en.wikipedia.org/wiki/Ember.js).
2. Click the `Edit source` tab (you will likely need to login).
3. Update the `latest release version`, `latest release date`, `latest preview version` & `latest preview date` in the Infobox if they need updating.
4. Be sure to update the accessdate for the citation url of the releases page referenced on the `latest release date` line.

## 8. Release bot

1. Go to the core meta channel in Discord.
2. Mark current release as done with `!release done`.
3. Schedule next release with the `!release next M.mm YYYY-MM-DD` command. E.g. `!release next 3.25 2021-02-08`.
