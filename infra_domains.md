# Domains

The domains are managed as part of the Ember brand by Tilde.

## Sub-domains

We will employ the use of sub-domains for official Ember projects. Right now we have the following apps deployed on subdomains:

- https://emberjs.com (apex domain)
  - the main website
- https://www.emberjs.com
  - redirects to https://emberjs.com
- https://guides.emberjs.com
- https://cli.emberjs.com
- https://deprecations.emberjs.com
- https://api.emberjs.com
- https://blog.emberjs.com
- https://help-wanted.emberjs.com

Sub-domains are strongly preferred in cases where parts of our sites work best as standalone, separately maintained apps.

- It is the best fit for the way that Netlify hosting works and will allow us to maintain service workers independently on separate apps when the time comes.
- It’s better for us to use sub-domains because it allows for us to use service workers (via @Todd J )

### Planned new subdomains

We also have other subdomains planned for the future, in some cases it is just migrating external project websites to be subdomains (such as the recent ember-cli.com to cli.emberjs.com migration) and in other cases it will be creating entirely new sites.

#### engines.emberjs.com
this will replace ember-engines.com in a similar way that cli.emberjs.com replaces ember-cli.com               

#### data.emberjs.com
This will be a new site designed to document ember data as a standalone project. This project is not planned to start any time soon

## Implementation Process

- The source of a website being configured as an official sub-domain must be in the `emberjs`, `ember-learn` or `glimmer` orgs on GitHub.
- Anyone with access to the website must use 2FA and have appropriate access rights. This includes 2FA on GitHub, Heroku, Netlify and Fastly.  
- Our DNS management provider DNSimple provides free SSL certificates via Lets Encrypt. But in cases of providers like Heroku, certs can be created and managed by Heroku. Either way ensure that the new site has SSL setup and that http to https redirects are setup. Netlify manages certs without user intervention. All our sites must run on https and the http to https redirects are setup.
- Sites are Ember apps and should endeavour to still work with no JS (with prember/fastboot etc)
- We use `yarn` as our package manager unless there’s a technical barrier
