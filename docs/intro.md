# Welcome to expeditejs

expeditejs is an Open-Source Full-Stack solution that helps you to build fast and maintainable web applications using tools like Vue.js, Firebase, Progressive Web Apps support, dynamic offline support... The goal of this project is to provide a powerful and well configured stack (with CI/CD, hosting...) so you can focus on writing your web application very quickly.

As this project is a generator project and CLI is separate which adds support for vue components and/or changing the frontend base to react. Right now you have access to the entire CLI and generator app configuration so you can change it according to your needs. A single config is in works, but it often breaks, depending on what ou use.

<b>Lighthouse score :</b>

![Lighthouse score](https://raw.githubusercontent.com/expeditejs/expedite/master/resources/lighthouse-score-report.jpg)

<b>Optional CircleCI preconfigured workflow :</b>

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

> Pre-requisites
>
> `node@9.3.0+`
> `npm@5.5.0+`
> `TIP`
>
> We highly recommend to use VSCode with the following plugins to get a better development experience :
>
> Prettier
> Eslint
> Vetur
> expeditejs comes with a default code editor config that will automatically be used by vscode. This config is available in .vscode/settings.json.