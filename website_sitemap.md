# Website - Site Map

As we move to use a consolidated Ember app for the website, we intend for the URLs to appropriately reflect the data heirarchy. 
The routes in the website should reflect this heirarchy. The exceptions are the places where it makes sense to use a subdomain instead of a child route. 

Items in parenthesis () indicate that the item is planned but doesn't exist yet. 

```
├── INDEX (home)
├── DOCS
|   ├── Ember.js Guides  (sub-domain: guides.emberjs.com)
|   ├── ember-cli Guides (sub-domain: cli.emberjs.com)
|   ├── (ember-data guides) (sub-domain: data.emberjs.com)
|   ├── API (sub-domain: api.emberjs.com)
|   |   ├── Ember.js API
|   |   ├── Ember Data
|   |   └── (ember-cli API) (currently: https://ember-cli.com/api/)
|   └── Learn Ember
|       └── Tutorials
|           ├── 101 Quick Start
|           ├── 201 Contact Book
|           └── 201 Super Rentals
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
