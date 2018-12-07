# Website - Site Map

As we move to use a consolidated Ember app for the website, we intend for the URLs to appropriately reflect the data heirarchy. 
The routes in the website should reflect this heirarchy. The exceptions are the places where it makes sense to use a subdomain instead of a child route. 

```
├── INDEX (home)
├── DOCS
|   ├── Ember.js Guides  (sub-domain: guides.emberjs.com)
|   ├── ember-cli Guides (sub-domain: cli.emberjs.com)
|   ├── (ember-data guides) (sub-domain: data.emberjs.com)
|   ├── Ember.js API (sub-domain: api.emberjs.com)
|   ├── (ember-cli API) (sub-domain: cli-api.emberjs.com)
|   ├── (ember-data API) (sub-domain: data-api.emberjs.com)
|   └── Learn Ember
|       ├── Quick Start
|       └── Tutorials
|           ├── 101 (quick start)
|           ├── 201 (rolodex)
|           └── 301 (super rentals)
├── RELEASES
|   ├── Channels
|   |   ├── stable
|   |   ├── beta
|   |   └── canary
|   ├── Deprecations (sub-domain? deprecations.emberjs.com)
|   |   ├── ember/:version/:deprecation-id
|   |   ├── ember-cli/:version/:deprecation-id
|   |   └── ember-data/:version/:deprecation-id
|   └── Status Board
├── BLOG (sub-domain: blog.emberjs.com)
├── COMMUNITY
|   ├── The Ember.js Community
|   ├── Guidelines
|   ├── Contribute (GitHub) (external link)
|   ├── Help Wanted
|   ├── Meetups
|   |   ├── getting started
|   |   └── resources & assets
|   ├── Job Board (external link)
|   ├── EmberConf (external link)
|   └── Annual Community Survey
|       └── :year
├── ABOUT
|   ├── The Team
|   ├── Ember Doctrine
|   ├── Branding
|   ├── Mascots
|   |   ├── FAQ
|   |   └── Commission (workflow)
|   ├── Who Uses Ember
|   ├── Sponsors
|   ├── Legal
|   └── Security
└── 404
```

## Changes & Updates

Major changes to this site structure should require an RFC.
