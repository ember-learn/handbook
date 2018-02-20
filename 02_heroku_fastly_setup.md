# Heroku + Fastly setup for ember apps

This is a reference on how to setup a new ember app in our infrastructure.

## Important consideration & Website repo configuration

If the ember app is going to exist in a subpath of https://emberjs.com, e.g., https://emberjs.com/api then the term `api` is going to be important for us in multiple aspects. Let us use this subpath in this guide to understand more,

- Ensure there are no files/folders in the [emberjs website source][1] named `api`. If it does exist, delete them in the branch that introduces the proxy changes for the new app. This is required since [heroku static buildpack][2] will serve the local files if they exist before considering the proxy routes.

- In the [static.json][3] add an entry under the `proxies` section as shown below. Its important not to hardcode the value here. This enables us to use staging urls of this app with the staging app of website on heroku. This variable is configured via [`settings`][4] tab of the website app by clicking on the `Reveal Config Vars` button. The key in this case would be `EMBER_API_DOCS_URL` and the value would be the fastly url of the ember app. You also need to configure this variable in the [`app.json`][10] (see the link for reference).

```json
//static.json
{
    "proxies": {
        "/api": {
          "origin": "${EMBER_API_DOCS_URL}"
        },
    }
}
```

## Ember app requirements

- Create a file with the name `Procfile` with the content below. This enables heroku to execute its [release phase][6] purge our fastly cache on deployments. In this script `FASTLY_PURGE_KEY` is the api token of any of the admins of our fastly account. If you're one of our fastly admin, you can create one under the [personal API tokens][7] page. `FASTLY_SERVICE_ID` is the service id of our app on fastly. You can find it by following [these instructions][8]

```Procfile
release: npm i -g fastly-cli && fastly purge-all -k $FASTLY_PURGE_KEY -s $FASTLY_SERVICE_ID
```

- In the `config/environment.js` file, after `rootURL` add two new fields `routerRootUrl` with value `/` and `apiHost` with value `''`. Override their values for production as shown in this [reference][14].
- In `router.js` change `rootURL: config.rootURL` to `rootURL: config.routerRootURL`. This ensures internal links & redirection works as expected.
- If your app fetches any static content from within the app then make sure you set the `host` of your ember data adapter with the `apiHost` from config. Follow the same if you have fetch/ajax calls with relative urls. In case the app uses prember then configure the host as shown in [deprecation app's application adapter][12].
- In your `ember-cli-build.js` set the `fingerprint` `prepend` value with the cdn url. See [`deprecation-app/ember-cli-build.js`][11] for reference.
- Configure your `config/deploy.js` file's production target as shown in [this reference][13]

## Fastly configuration

- Go to `https://manage.fastly.com/services/all`, click on `CREATE SERVICE`. Fill in details as shown in the screenshot below. Note that there's a naming convention to follow depending on the app name in heroku. The url we enter in the domain field will be the `FASTLY_DOMAIN` variable's value in heroku.
![service creation][screen1]

- Once created, you'll see the following page.
![service created][screen2]

- Click on `CONFIGURATION` dropdown and click on `clone active`. On the left nav, click `Content`. Under `Headers` section click on `CREATE YOUR FIRST HEADER`. Set the exact content from the screenshot below & save it.
![header setup][screen3]

- On the same page click on `SET UP GZIP` and click `CREATE`.
- Once these are done, click on the `ACTIVATE` button to activate the new changes.

[1]:  https://github.com/emberjs/website/tree/master/source
[2]:  https://github.com/heroku/heroku-buildpack-static
[3]:  https://github.com/emberjs/website/blob/99a390760968cd775cafefed5e904d14b2e54933/static.json#L5
[4]:  https://dashboard.heroku.com/apps/ember-website-staging/settings
[5]:  https://devcenter.heroku.com/articles/procfile
[6]:  https://devcenter.heroku.com/articles/release-phase
[7]:  https://manage.fastly.com/account/personal/tokens
[8]:  https://docs.fastly.com/guides/account-management-and-security/finding-and-managing-your-account-info#finding-your-service-id
[9]: https://github.com/ember-learn/deprecation-app/blob/4c058c65e0ab43c03b062beb4164544d7a515600/config/environment.js#L52
[10]: https://github.com/emberjs/website/blob/99a390760968cd775cafefed5e904d14b2e54933/app.json#L6
[11]: https://github.com/ember-learn/deprecation-app/blob/master/ember-cli-build.js
[12]: https://github.com/ember-learn/deprecation-app/blob/master/app/adapters/application.js#L15
[13]: https://github.com/ember-learn/deprecation-app/blob/4c058c65e0ab43c03b062beb4164544d7a515600/config/deploy.js#L11
[14]: https://github.com/ember-learn/deprecation-app/blob/4c058c65e0ab43c03b062beb4164544d7a515600/config/environment.js#L52


[screen1]: https://raw.githubusercontent.com/ember-learn/handbook/master/images/fastly/01_create-service-page.png
[screen2]: https://raw.githubusercontent.com/ember-learn/handbook/master/images/fastly/02_service_created.png
[screen3]: https://raw.githubusercontent.com/ember-learn/handbook/master/images/fastly/03_cors_setup.png