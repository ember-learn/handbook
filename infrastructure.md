# Infrastructure

This document is a reference of all the apps maintained by the ember learning team. The main website https://emberjs.com uses the [heroku static buildpack][heroku-buildpack] to proxy to various different sites via the [static.json][static-json] configuration file.

## Overview

|   Repository                        | Purpose                              | Current tech                                  | Hosting Service                                       |
|-------------------------------------|--------------------------------------|-----------------------------------------------|-------------------------------------------------------|
| https://github.com/ember-learn/ember-website                | emberjs.com home page                | ember app with prember                        |netlify                   |
| https://github.com/ember-learn/ember-blog |    emberjs blog                     | ember app with prember                        | netlify
| https://github.com/emberjs/rfcs                   | RFC's page                           | static site generated from markdown by mdbook | github pages                         |
| https://github.com/ember-learn/ember-api-docs     | Ember API docs                       | ember app with fastboot running on express                                    | heroku  |
| https://github.com/ember-learn/deprecations-app   | List deprecations in ember           | ember app  with prember                                    | netlify          |
| https://github.com/ember-learn/upgrade-guide      | Display changes between versions     | ember app                                     | netlify |
| https://github.com/ember-learn/ember-octane-vs-classic-cheatsheet | octane syntax and patterns cheatsheet | ember app with ember intl | github pages |
| https://github.com/ember-learn/ember-help-wanted  | List issues across ember repos that need community help                                  | ember app                                     | netlify               |
| https://github.com/ember-learn/guides-app  | TBD                                  | ember app  with prember                                    | netlify               |
| https://github.com/ember-learn/cli-guides  | new ember-cli docs                                  | ember app  with prember                                    | netlify         |

## On hosting preferences

[Heroku][heroku] sponsors our hosting & [Fastly][fastly] sponsors our CDN :heart:. While heroku does have [a fastly addon][fastly-addon], for billing & maintenance reasons its easier to manage one fastly account with multiple service accounts configured in it. Heroku lets us have [pipelines][heroku-pipelines] that enables us to have different environments like staging & production. It also lets us have review apps explained in the following section. We have hosted few apps directly on GitHub pages. These are apps where only content of the app is changed by internal teams that they don't require the sophisticated setup that the other apps enjoy.

We've deployed apps prerendered with prember on [Netlify][netlify].

## Review apps

Heroku enables us to create [review apps][heroku-review-apps] which are same as regular apps but lets us review changes in pull requests. They're automatically created when members with write access of a repo raise a PR (also depends on whether the pipeline is configured to auto-deploy). To create a review app for a PR raised by non-members, go to the heroku pipeline and manually create the review app. Review apps get deleted after few days of inactivity on the PR. They also get deployed only on successful builds on Travis.

Creation & maintenance of review apps on netlify is automated & doesn't require manual intervention.

## Heroku deployment

Heroku deployment doesn't require special deploy section on `.travis.yml` configuration file since we always setup github integration via the [heroku dashboard][heroku-dashboard]. The deployment on heroku still checks to ensure that travis builds were successful before autodeploying the changes.

All our heroku apps are set to autodeploy `master` branch to their staging apps. The changes are usually elevated to production after a member manually deploys the production app. **DO NOT USE** the `promote to production` button to promote staging changes to production. This copies over the assets as is from staging container to production. This is problematic in our setup because we have variables that differ between staging and production that drive our ember app builds. e.g., `FASTLY_CDN_URL` is a typical environment variable we use across our ember apps. Promoting as is from staging would result in production pointing to staging's fastly url. This will start producing errors as soon as different changes are deployed to staging & those files are no longer available.

[heroku]:  https://heroku.com
[fastly]:  https://fastly.com
[fastly-addon]: https://elements.heroku.com/addons/fastly
[heroku-pipelines]: https://devcenter.heroku.com/articles/pipelines
[netlify]: https://www.netlify.com/
[heroku-review-apps]: https://devcenter.heroku.com/articles/github-integration-review-apps
[heroku-buildpack]: https://github.com/heroku/heroku-buildpack-static
[static-json]: https://github.com/emberjs/website/blob/master/static.json
[heroku-dashboard]: https://dashboard.heroku.com/teams/ember/apps