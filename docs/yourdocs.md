# Welcome to expeditejs

<br />

**expeditejs** is an Open-Source Full-Stack solution that helps you to build fast and maintainable web applications using tools like Vue.js, Firebase, Progressive Web Apps support, dynamic offline support... The goal of this project is to provide a powerful and well configured stack (with CI/CD, hosting...) so you can focus on writing your web application very quickly.

As this project is a generator project and CLI is separate which adds support for vue components and/or changing the frontend base to react. Right now you have access to the entire CLI and generator app configuration so you can change it according to your needs. A single config is in works, but it often breaks, depending on what ou use.

**Lighthouse score :**

![Lighthouse score](https://raw.githubusercontent.com/expeditejs/expedite/master/resources/lighthouse-score-report.jpg)

**Optional CircleCI preconfigured workflow :**

![CI Workflow](https://raw.githubusercontent.com/expeditejs/expedite/master/resources/ci-workflow.jpg)

## The stack is made up of

* Vue.js : front-end framework
* Vue-cli : standard tooling for vue.js development
* Vuex : state management
* Firestore : cloud NoSQL Database
* Firebase hosting : fast and secure web hosting
* Firebase authentication : for easy authentication
* PWA : progressive web app support
* Prettier : code formatting rules
* Eslint : control code quality
* Jest : unit testing
* Cypress : e2e testing
* Vue head : meta description per page
* [Optional] prerender spa plugin : pages prerendering
* [Optional] circleci : continuous integration/deployment
* [Optional] bundlesize : control your javascript bundles sizes

## App embedded features

* Google authentication
* Offline support (dynamic & static caching)
* New version available prompt on new app deployments
* Add to home screen prompt for ios & android
* Smart redirection for auth protected routes
* Products page example to demonstrate app data management with firestore and vuex
* Better PWA support for all browsers with PWACompat

    Pre-requisites

    `node@9.3.0+`
    `npm@5.5.0+`
    `TIP`

    We highly recommend to use VSCode with the following plugins to get a better development experience :

    Prettier
    Eslint
    Vetur
    expeditejs comes with a default code editor config that will automatically be used by vscode. This config is available in .vscode/settings.json.

## Step 1 - Installation

🕙Estimated time → 20 seconds

```
git clone
cp .env.example .env.local
npm i
```

## Step 2 - Firebase configuration

🕙Estimated time → 3 minutes

* Create a new firebase project with the firebase console
* Once your firebase project is created, add an application by clicking the web button 👉 Firebase web app button and copy the config object and replace the config variable in `/src/firebase/init.js` in expeditejs project.
* Go to Side menu → Database → Create database and select Start in test mode. Now your firestore database is up.
* Go to Side menu → Authentication click Set up sign-in method.
* Click on Google provider, enable it by clicking the switch button, select a project support email and click save button. You will be able to change or add new auth providers later if you need to.
* Back to your expeditejs project, open a console and run :
`npm i -g npx`

## login with the account you used to create the firebase project

`npx firebase login`

## select the project you've just created and use "default" as alias

`npx firebase use --add`

## Build the app and deploy

* `npm run build`
* `npx firebase deploy`
* You're done ! 🎉
* Your project is now available on firebase hosting.
* You can also run npm run serve and start your app development !

However we recommend you to go through optional steps to get a better developer experience 😎

## Step 3 (Optional) - Continuous integration/deployment

🕙Estimated time → 5 minutes

We've built a CircleCI configuration that will trigger the following actions when you're pushing to your github repository. The process is the following :

* Check that all project files matches the prettier format : `npm run prettier:check`
* Run the linter : `npm run lint`
* Run unit tests : `npm run test:unit`
* Run e2e tests : `npm run test:e2e:headless`
* Build the project : `npm run build`
* Check your js bundles sizes : `npm run bundlesize`
* Eventually deploy the built project to firebase hosting if the targeted branch is master : `npm run firebase:deploy:ci`

⚠️ For this step, we assume that you already have a github repository that hosts your expeditejs project with your source code pushed on the master branch ⚠️

Steps :

* Go to https://circleci.com
* Login with your github account
* Authorize CircleCI to look into your github projects
* Go to Side menu → Add projects and click the Set Up Project button corresponding to your expeditejs project
* Choose Linux for operating system and Node for the language
* You can directly start your first CircleCI build by clicking Start building button.
* Go to Side menu → Jobs and you should see your first CircleCI job running
* Now wait for all the jobs to finish
* The last job (deploy) will fail and this is normal 😅 It's because of the deployment step (npm run firebase:deploy:ci). We need to authorize circle ci to deploy on our firebase hosting project. For this we just need to add a firebase token to circle ci :

* Back to a terminal run the following command :
* `npx firebase login:ci`
* Login with you google account and authorize firebase-cli. The command will print out a token that looks like this :
* `1/PXcLCJ5BXAZ7ciFwkrrpikUbnMAMX8xRFmt16pLYudg9`
* Copy this token and in your CircleCI project interface, go to Your CircleCI project settings → Environment Variables and click Add Variable button.
* For the env variable name, use `FIREBASE_TOKEN` and for the value, use the token you got from the firebase login:ci command.
* Go to Side menu → Jobs click the job that fails and click the Rerun workflow button.
* Wait again for all the jobs to finish.
* Now the deploy step has completed with success and your project has automatically been deployed to firebase hosting


## Commands

### Compiles and hot-reloads for development

npm run serve

### Compiles and minifies for production

npm run build

### Run your tests

npm run test

### Lints and fixes files

npm run lint

### Run your end-to-end tests

npm run test:e2e

### Run your unit tests

npm run test:unit

### Run prettier check format

npm run prettier:check

### Format all files with prettier

npm run prettier:format-all


## Guide

### Tooling

<br />

**expeditejs** uses [Vue CLI](https://cli.vuejs.org/) which is the default standard tooling for Vue.js development.

<br />

_ tip
📘 Refer to [the official documentation](https://cli.vuejs.org/) for more details.
_

## Environments

<br />

### Configurations files

**Vue-cli** configuration may be different depending on the mode you are running the app. You can find all config files per mode on the `/vue-config` folder. `/vue-config/config.default.js` will be merged with either `/vue-config/config.development.js` or `/vue-config/config.production.js` depending on the mode you are using.

<br />

_ tip
📘 Refer to [the official documentation](https://cli.vuejs.org/guide/mode-and-env.html#modes) for more details.
_

### Environments variables & Modes

<br />

_ tip
📘 Refer to [the official documentation](https://cli.vuejs.org/guide/mode-and-env.html#modes) for more details.
_

## PWA

<br />

### Service worker

**expeditejs** uses [vue-cli-plugin-pwa](https://github.com/vuejs/vue-cli/tree/dev/packages/%40vue/cli-plugin-pwa) to configure **service worker** and PWA stuff.

The **service worker** configuration is available in `public/service-worker.js`.

**Service worker registration** is done from this file `src/misc/register-service-worker.js`. **By default, service workers are on registered on `production` environment**.

<br />

_ tip
📘 Refer to [the official documentation](https://github.com/vuejs/vue-cli/tree/dev/packages/%40vue/cli-plugin-pwa) for more details.
_

### App new version available

When you release a version of your app, your user will be informed with a toastr that a new version of you app is available so he can refresh :

![New version available](/assets/img/new-version-available.jpg)

This logic is located in `src/misc/register-service-worker.js` in the `updated` hook function.

### Manifest

The **web app manifest** is available here `public/manifest.json`.

<br />

_ tip
📘 Refer to [the google documentation](https://developers.google.com/web/fundamentals/web-app-manifest/) for more details.
_

### Offline

With **expeditejs** your app is fully available online.
The project comes with a cache for static files (handle by the service worker) and a dynamic cache for firestore database requests (firestore offline mode is enabled in `/src/firebase/async-firestore.js`).

Offline status event listener is located in `src/misc/handle-network-status.js`.

### Add to home screen

If you are using chrome on an android device, the browser will automatically prompt the user to install your PWA.
<br />

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

<br />

**expeditejs** uses [prerender-spa-plugin](https://github.com/chrisvfritz/prerender-spa-plugin) for prerendering.
If you don't know what prerendering is, you should read [this](https://github.com/chrisvfritz/prerender-spa-plugin#what-is-prerendering).

The prerendering configuration is available in `vue-config/config.default.js` :

```
new PrerenderSPAPlugin({
  // Required - The path to the webpack-outputted app to prerender.
  staticDir: path.join(__rootDirname),
  // Required - Routes to prerender.
  routes: prerenderedRoutesList // => prerenderedRoutesList is the array of routes to prerender
})
```

If you want to configure the list of routes to prerender, you need to update the `prerenderedRoutesList` variable in `vue-config/config.default.js` :

```
const prerenderedRoutesList = ['/login', '/home', '/']
```

<br />

_ tip
📘 Refer to [the official documentation](https://github.com/chrisvfritz/prerender-spa-plugin) for more details.
_

## Authentication

<br />

**expeditejs** uses [firebase auth](https://firebase.google.com/docs/auth/) to handle user authentication. By default, Google Authentication is the only provider enabled in the **expeditejs** stack. You can easily add other providers like **Twitter** or **Facebook** by going to the [firebase console](https://console.firebase.google.com), on the `Authentication` page.

* Login component is located in `src/views/Login.vue`.
* Authentication management code is located in `src/misc/handle-authentication.js` and in `src/store/authentication` folder.

<br />

_ tip
📘 Refer to [the official documentation](https://firebase.google.com/docs/auth/) for more details.
_

## Cloud database

<br />

**expeditejs** uses [firestore](https://firebase.google.com/docs/firestore/) to store and sync data.
You can find firestore related code in `src/firebase` folder.

**expeditejs** provides a "CRUD" feature that might help you to manage firestore entities in `src/firebase/generic-db.js`.
You can extend this behavior for your different firestore entities as it is done in `src/firebase/users-db.js` and `src/firebase/user-products-db.js`.

With firestore, you need to secure your data with [security rules](https://firebase.google.com/docs/firestore/security/overview).
You can find find these rules in `src/firebase/firestore.rules`.

To manually deploy firestore rules, run :

```
npx firebase deploy --only rules
```

<br />

_ tip
📘 Refer to [the official documentation](https://firebase.google.com/docs/firestore/) for more details.
_

## Data management

<br />

Front-end data management is done with [vuex](https://vuex.vuejs.org/).

**Vuex** code is located in the `src/store` folder.

<br />

_ tip
📘 Refer to [the official documentation](https://vuex.vuejs.org/) for more details.
_

## Hosting

<br />

**expeditejs** uses [firebase-hosting](https://firebase.google.com/docs/hosting/) for app deployment.

To manually deploy your app, run :

```
npx firebase deploy --only hosting
```

:warning: To deploy, you must have build your app before :

```
npm run build
```

Deployment configuration can be found in `/firebase.json`.

<br />

_ tip
📘 Refer to [the official documentation](https://firebase.google.com/docs/hosting/) for more details.
_

## Continuous integration/deployment

<br />

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

<br />

_ tip
📘 Refer to [the CircleCI documentation](https://circleci.com/docs/) for more details.
_

## Tests

<br />

All tests and related configuration can be found in `tests` folder.<br />
[Cypress](https://www.cypress.io/) is use for E2E tests and [Jest](https://jestjs.io/) for unit tests.

**Run E2E tests :**

```
npm run test:e2e
```

**Run unit tests :**

```
npm run test:unit
```

You can easily change these testing frameworks with [vue-cli](https://cli.vuejs.org/) if you want.

<br />

_ tip
📘 Refer to the [Jest documentation](https://jestjs.io/) or [Cypress documentation](https://www.cypress.io/) for more details.
_

## BundleSize

<br />

BundleSize helps you control your javascript bundle sizes for better performances.<br />
BundleSize rules are located in the `package.json`, in the `bundlesize` property. You can add as many rules as you want. It is recommended to add as many rules as javascript bundles you have.

**Run BundleSize check command :**

```
npm run bundlesize
```

If you did [**step 3** in the setup](/setup/#step-3-optional-continuous-integration-deployment) section, `bundlesize` command will be run during the CI process.

<br />

_ tip
📘 Refer to [the official documentation](https://github.com/siddharthkp/bundlesize) for more details.
_

## Code format

<br />

**expeditejs** uses [prettier](https://prettier.io/) to keep you code formatted.

**Check all files code format command :**

```
npm run prettier:check
```

**Fix all files code format command :**

```
npm run prettier:format-all
```

<br />

_ tip
📘 Refer to [the official documentation](https://prettier.io/) for more details.
_

## Code quality

<br />

**expeditejs** uses [eslint](https://eslint.org/) to control the quality of your code.

**Run linter command :**

```
npm run lint
```

<br />

_ tip
📘 Refer to [the official documentation](https://eslint.org/) for more details.
_

## Pages meta infos

<br />

Manipulating the meta information of the head tag is done with [vue-head](https://github.com/ktquez/vue-head).

<br />

_ tip
📘 Refer to [the official documentation](https://github.com/ktquez/vue-head) for more details.
_