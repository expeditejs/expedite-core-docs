# Guide

## Tooling

**expeditejs** uses [Vue CLI](https://cli.vuejs.org/) which is the default standard tooling for Vue.js development.

📘 Refer to [the official documentation](https://cli.vuejs.org/) for more details.

## Environments

### Configurations files

**Vue-cli** configuration may be different depending on the mode you are running the app. You can find all config files per mode on the `/vue-config` folder. `/vue-config/config.default.js` will be merged with either `/vue-config/config.development.js` or `/vue-config/config.production.js` depending on the mode you are using.

📘 Refer to [the official documentation](https://cli.vuejs.org/guide/mode-and-env.html#modes) for more details.

### Environments variables & Modes

📘 Refer to [the official documentation](https://cli.vuejs.org/guide/mode-and-env.html#modes) for more details.

## PWA

### Service worker

**expeditejs** uses [vue-cli-plugin-pwa](https://github.com/vuejs/vue-cli/tree/dev/packages/%40vue/cli-plugin-pwa) to configure **service worker** and PWA stuff.

The **service worker** configuration is available in `public/service-worker.js`.

**Service worker registration** is done from this file `src/misc/register-service-worker.js`. **By default, service workers are on registered on `production` environment**.

📘 Refer to [the official documentation](https://github.com/vuejs/vue-cli/tree/dev/packages/%40vue/cli-plugin-pwa) for more details.

### App new version available

When you release a version of your app, your user will be informed with a toastr that a new version of you app is available so he can refresh :

![New version available](/assets/img/new-version-available.jpg)

This logic is located in `src/misc/register-service-worker.js` in the `updated` hook function.

### Manifest

The **web app manifest** is available here `public/manifest.json`.

📘 Refer to [the google documentation](https://developers.google.com/web/fundamentals/web-app-manifest/) for more details.

### Offline

With **expeditejs** your app is fully available online.
The project comes with a cache for static files (handle by the service worker) and a dynamic cache for firestore database requests (firestore offline mode is enabled in `/src/firebase/async-firestore.js`).

Offline status event listener is located in `src/misc/handle-network-status.js`.

### Add to home screen

If you are using chrome on an android device, the browser will automatically prompt the user to install your PWA.

**On safari IOS, this process is not automatic yet**. The user has to manually add the PWA to home screen.
For a better experience on IOS, **expeditejs** display a modal explaining the process to add the app to home screen.
This modal is shown only the first time the user visit your app. The app will show this modal again after 1 month (if the PWA is still not installed).

![Add to home screen](/assets/img/add-to-home-screen.jpg)

This logic is located in `src/misc/handle-apple-install-prompt.js`

### PWACompat

[PWACompat](https://github.com/GoogleChromeLabs/pwacompat) brings the Web App Manifest to non-compliant browsers for better Progressive Web Apps.

## Push notifications

You can easily add push notifications to your expeditejs project with [firebase cloud messaging](https://firebase.google.com/docs/cloud-messaging/)

## Prerendering

**expeditejs** uses [prerender-spa-plugin](https://github.com/chrisvfritz/prerender-spa-plugin) for prerendering.
If you don't know what prerendering is, you should read [this](https://github.com/chrisvfritz/prerender-spa-plugin#what-is-prerendering).

The prerendering configuration is available in `vue-config/config.default.js` :

```javascript
new PrerenderSPAPlugin({
  // Required - The path to the webpack-outputted app to prerender.
  staticDir: path.join(__rootDirname),
  // Required - Routes to prerender.
  routes: prerenderedRoutesList // => prerenderedRoutesList is the array of routes to prerender
})
```

If you want to configure the list of routes to prerender, you need to update the `prerenderedRoutesList` variable in `vue-config/config.default.js` :

```javascript
const prerenderedRoutesList = ['/login', '/home', '/']
```

📘 Refer to [the official documentation](https://github.com/chrisvfritz/prerender-spa-plugin) for more details.

## Authentication

**expeditejs** uses [firebase auth](https://firebase.google.com/docs/auth/) to handle user authentication. By default, Google Authentication is the only provider enabled in the **expeditejs** stack. You can easily add other providers like **Twitter** or **Facebook** by going to the [firebase console](https://console.firebase.google.com), on the `Authentication` page.

* Login component is located in `src/views/Login.vue`.
* Authentication management code is located in `src/misc/handle-authentication.js` and in `src/store/authentication` folder.

📘 Refer to [the official documentation](https://firebase.google.com/docs/auth/) for more details.

## Cloud database

**expeditejs** uses [firestore](https://firebase.google.com/docs/firestore/) to store and sync data.
You can find firestore related code in `src/firebase` folder.

**expeditejs** provides a "CRUD" feature that might help you to manage firestore entities in `src/firebase/generic-db.js`.
You can extend this behavior for your different firestore entities as it is done in `src/firebase/users-db.js` and `src/firebase/user-products-db.js`.

With firestore, you need to secure your data with [security rules](https://firebase.google.com/docs/firestore/security/overview).
You can find find these rules in `src/firebase/firestore.rules`.

To manually deploy firestore rules, run :

```shell
npx firebase deploy --only rules
```

📘 Refer to [the official documentation](https://firebase.google.com/docs/firestore/) for more details.

## Data management

Front-end data management is done with [vuex](https://vuex.vuejs.org/).

**Vuex** code is located in the `src/store` folder.

📘 Refer to [the official documentation](https://vuex.vuejs.org/) for more details.

## Hosting

**expeditejs** uses [firebase-hosting](https://firebase.google.com/docs/hosting/) for app deployment.

To manually deploy your app, run :

```shell
npx firebase deploy --only hosting
```

:warning: To deploy, you must have build your app before :

```shell
npm run build
```

Deployment configuration can be found in `/firebase.json`.

📘 Refer to [the official documentation](https://firebase.google.com/docs/hosting/) for more details.

## Continuous integration/deployment

Continuous integration/deployment is handled by [CircleCI](https://circleci.com/) (**[If you've enabled it](/setup/#step-3-optional-continuous-integration-deployment)**)

CircleCI will process the following :

* Check that all project files matches the prettier format : `npm run prettier:check`
* Run the linter : `npm run lint`
* Run unit tests : `npm run test:unit`
* Run e2e tests : `npm run test:e2e:headless`
* Build the project : `npm run build`
* Check your js bundles sizes : `npm run bundlesize`
* **Eventually** deploy the built project to firebase hosting if the targeted branch is **master** : `npm run firebase:deploy:ci`

![CircleCI workflow](/assets/img/ci-workflow.jpg)

**CircleCI** configuration is available in `.circleci/config.yml`.

📘 Refer to [the CircleCI documentation](https://circleci.com/docs/) for more details.

## Tests

All tests and related configuration can be found in `tests` folder.
[Cypress](https://www.cypress.io/) is use for E2E tests and [Jest](https://jestjs.io/) for unit tests.

**Run E2E tests :**

```shell
npm run test:e2e
```

**Run unit tests :**

```shell
npm run test:unit
```

You can easily change these testing frameworks with [vue-cli](https://cli.vuejs.org/) if you want.

📘 Refer to the [Jest documentation](https://jestjs.io/) or [Cypress documentation](https://www.cypress.io/) for more details.

## BundleSize

BundleSize helps you control your javascript bundle sizes for better performances.
BundleSize rules are located in the `package.json`, in the `bundlesize` property. You can add as many rules as you want. It is recommended to add as many rules as javascript bundles you have.

**Run BundleSize check command :**

```shell
npm run bundlesize
```

If you did [**step 3** in the setup](/setup/#step-3-optional-continuous-integration-deployment) section, `bundlesize` command will be run during the CI process.

📘 Refer to [the official documentation](https://github.com/siddharthkp/bundlesize) for more details.

## Code format

**expeditejs** uses [prettier](https://prettier.io/) to keep you code formatted.

**Check all files code format command :**

```shell
npm run prettier:check
```

**Fix all files code format command :**

```shell
npm run prettier:format-all
```

📘 Refer to [the official documentation](https://prettier.io/) for more details.

## Code quality

**expeditejs** uses [eslint](https://eslint.org/) to control the quality of your code.

**Run linter command :**

```shell
npm run lint
```

📘 Refer to [the official documentation](https://eslint.org/) for more details.

## Pages meta infos

Manipulating the meta information of the head tag is done with [vue-head](https://github.com/ktquez/vue-head).

📘 Refer to [the official documentation](https://github.com/ktquez/vue-head) for more details.