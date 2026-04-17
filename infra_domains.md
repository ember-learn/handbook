# Domains

The domains are managed as part of the Ember brand by Tilde.

## Sub-domains

We will employ the use of sub-domains for official Ember projects. Right now we have the following apps deployed on subdomains:

- https://emberjs.com (apex domain)
  - the main website
  - source: https://github.com/ember-learn/ember-website
- https://www.emberjs.com
  - redirects to https://emberjs.com
- https://guides.emberjs.com
  - documentation source: https://github.com/ember-learn/guides-source
  - template source: https://github.com/ember-learn/guidemaker-ember-template
- https://cli.emberjs.com (will soon be deprecated)
  - https://github.com/ember-learn/cli-guides
- https://deprecations.emberjs.com
  - documentation and frontend app source: https://github.com/ember-learn/deprecation-app
- https://api.emberjs.com
  - documentation source (extracted from ember.js source code): https://github.com/ember-learn/ember-api-docs-data
  - frontend app source: https://github.com/ember-learn/ember-api-docs
- https://blog.emberjs.com
  - content source: https://github.com/ember-learn/ember-blog
  - template source: https://github.com/ember-learn/empress-blog-ember-template
- https://help-wanted.emberjs.com
  - frontend app source: https://github.com/ember-learn/ember-help-wanted
  - backend app source: https://github.com/ember-learn/ember-help-wanted-server
- https://upgrade.emberjs.com
  - content and frontend app source: https://github.com/ember-learn/upgrade-guide
- http://new.emberjs.com/
  - redirects to Stackblitz to start a new Ember app in the browser

Sub-domains are strongly preferred in cases where parts of our sites work best as standalone, separately maintained apps.

- It is the best fit for the way that Netlify hosting works and will allow us to maintain service workers independently on separate apps when the time comes.
- It’s better for us to use sub-domains because it allows for us to use service workers (via @Todd J )

## Implementation Process

- The source of a website being configured as an official sub-domain must be in the `emberjs`, `ember-learn` or `glimmer` orgs on GitHub.
- Anyone with access to the website must use 2FA and have appropriate access rights. This includes 2FA on GitHub, Heroku, Netlify and Fastly.  
- Our DNS management provider DNSimple provides free SSL certificates via Lets Encrypt. But in cases of providers like Heroku, certs can be created and managed by Heroku. Either way ensure that the new site has SSL setup and that http to https redirects are setup. Netlify manages certs without user intervention. All our sites must run on https and the http to https redirects are setup.
- Sites are Ember apps and should endeavour to still work with no JS (with prember/fastboot etc)
- We use `pnpm` as our package manager unless there’s a technical barrier
