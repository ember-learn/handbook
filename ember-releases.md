# Ember Releases

When a new version of Ember is released,
the learning team has to make sure some parts of our infrastructure are adequately updated to account for it.
These are:

- Guides
- API documentation
- Release blog post
- Release page (index, stable, beta, LTS)
- [Glitch Ember starter](https://emberjs.glitch.me)

## Guides

Instructions are found in [MAINTAINERS.md](https://github.com/ember-learn/guides-source/blob/master/MAINTAINERS.md#deploying-a-new-version).

## API documentation

1. Clone the following repositories into a common folder. For example, `/releases/ember.js` and `/releases/data`:
    1. [ember-jsonapi-docs](https://github.com/ember-learn/ember-jsonapi-docs)
    2. [ember.js](https://github.com/emberjs/ember.js/)
    3. [data](https://github.com/emberjs/data/)
2. `cd ember-jsonapi-docs`
3. Go to the heroku instance, navigate to `Settings`, click `reveal config vars` and use the values seen there as values for the following variables in your local environment:
    1. `AWS_ACCESS_KEY`
    2. `AWS_ACCESS_KEY_ID`
    3. `AWS_SECRET_ACCESS_KEY`
    4. `AWS_SECRET_KEY`
    5. `AWS_SHOULD_PUBLISH`
4. Run `yarn run start --sync`
5. Wait and confirm there were no errors
6. Done!

## Release blog post

**NOTE** ember-source, ember-data, and ember-cli must already be released.

1. Go to [https://github.com/ember-learn/ember-blog/pulls](https://github.com/ember-learn/ember-blog/pulls)
2. Merge the relevant blog post once it is OK'ed by all the team representatives.

## Release pages

The next release date is not affected by "delays", and should always be calculated as original date + 6 weeks.

1. Clone [ember-website](https://github.com/ember-learn/ember-website)
2. Edit the following files:
    1. `data/project/ember/lts.md`
    2. `data/project/ember/release.md`
    3. `data/project/ember/beta.md`
    4. `data/project/emberData/release.md`
    5. `data/project/emberData/beta.md`

## Glitch Ember starter

1. Go to [https://glitch.com/edit/console.html?ember](https://glitch.com/edit/console.html?ember)
2. Update the local [ember-new-output](https://github.com/ember-cli/ember-new-output) repository
3. `git checkout` the relevant release version
4. Include the following snippet for the Glitch button in `app/index.html`
```
<!-- include the Glitch button to show what the webpage is about and
  to make it easier for folks to view source and remix -->
<div class="glitchButton" style="position:fixed;top:20px;right:20px;"></div>
<script src="https://button.glitch.me/button.js"></script>
```
5. Edit `package.json` to explicitly include port 4200: `"start": "ember serve -p 4200"`
