# Infrastructure

This document is a reference of all the apps maintained by the ember learning team. The main website [https://emberjs.com][15] uses the [heroku static buildpack][14] to proxy to various different sites via the [static.json][16] configuration file.

## Overview

|   Repository                        | Purpose                              | Current tech                                  | Direct URL                                            |
|-------------------------------------|--------------------------------------|-----------------------------------------------|-------------------------------------------------------|
| [emberjs/website][1]                | emberjs.com home page                | static site built on Middleman                |https://ember-website.herokuapp.com/                   |
| [emberjs/rfcs][2]                   | RFC's page                           | static site generated from markdown by mdbook |https://emberjs.github.io/rfcs                         |
| [ember-learn/ember-api-docs][3]     | Ember API docs                       | ember app                                     |https://ember-api-docs-frontend.global.ssl.fastly.net  |
| [ember-learn/statusboard][4]        | Status of ember milestone projects   | ember app                                     |https://ember-learn.github.io/statusboard/             |
| [ember-learn/deprecations-app][5]   | List deprecations in ember           | ember app                                     |https://deprecations-app-prod.herokuapp.com/           |
| [ember-learn/builds][6]             | Shows ember releases                 | ember app                                     |                                                       |
| [ember-learn/ember-help-wanted][7]  | TBD                                  | ember app                                     |https://ember-help-wanted.herokuapp.com/               |

## On hosting preferences

[Heroku][8] sponsors our hosting & [Fastly][9] sponsors our CDN :heart:. While heroku does have [a fastly addon][10], for billing & maintenance reasons its easier to manage one fastly account with multiple service accounts configured in it. Heroku lets us have [pipelines][11] that enables us to have different environments like staging & production. It also lets us have review apps explained in the following section. We have hosted few apps directly on GitHub pages. These are apps where only content of the app is changed by internal teams that they don't require the sophisticated setup that the other apps enjoy.

## Heroku review apps

Heroku enables us to create [review apps][12] which are same as regular apps but lets us review changes in pull requests. They're automatically created when members with write access of a repo raise a PR (also depends on whether the pipeline is configured to auto-deploy). To create a review app for a PR raised by non-members, go to the heroku pipeline and manually create the review app. Review apps get deleted after few days of inactivity on the PR. They also get deployed only on successful builds on Travis.

## Heroku deployment

Heroku deployment doesn't require special deploy section on `.travis.yml` configuration file since we always setup github integration via the [heroku dashboard][13]. The deployment on heroku still checks to ensure that travis builds were successful before autodeploying the changes.

All our heroku apps are set to autodeploy `master` branch to their staging apps. The changes are usually elevated to production after a member manually deploys the production app. **DO NOT USE** the `promote to production` button to promote staging changes to production. This copies over the assets as is from staging container to production. This is problematic in our setup because we have variables that differ between staging and production that drive our ember app builds. e.g., `FASTLY_CDN_URL` is a typical environment variable we use across our ember apps. Promoting as is from staging would result in production pointing to staging's fastly url. This will start producing errors as soon as different changes are deployed to staging & those files are no longer available.

[1]:  https://github.com/emberjs/website
[2]:  https://github.com/emberjs/rfcs
[3]:  https://github.com/ember-learn/ember-api-docs
[4]:  https://github.com/ember-learn/statusboard
[5]:  https://github.com/ember-learn/deprecation-app
[6]:  https://github.com/ember-learn/builds
[7]:  https://github.com/ember-learn/ember-help-wanted
[8]:  https://heroku.com
[9]:  https://fastly.com
[10]: https://elements.heroku.com/addons/fastly
[11]: https://devcenter.heroku.com/articles/pipelines
[12]: https://devcenter.heroku.com/articles/github-integration-review-apps
[13]: https://dashboard.heroku.com/teams/ember/apps
[14]: https://github.com/heroku/heroku-buildpack-static
[15]: https://emberjs.com
[16]: https://github.com/emberjs/website/blob/master/static.json