# Setup

## Step 1 - Installation

> 🕙Estimated time → 20 seconds

```shell
git clone
cp .env.example .env.local
npm i
```

## Step 2 - Firebase configuration

> 🕙Estimated time → 3 minutes

* Create a new firebase project with the firebase console
* Once your firebase project is created, add an application by clicking the web button Enter an app nickname but do not check "Also set up Firebase Hosting" and click `next`. Copy the `firebaseConfig` object and replace the config variable in `/src/firebase/init.js` in expeditejs project.
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

> 🕙Estimated time → 5 minutes

We've built a CircleCI configuration that will trigger the following actions when you're pushing to your github repository. The process is the following :

* Check that all project files matches the prettier format : `npm run prettier:check`
* Run the linter : `npm run lint`
* Run unit tests : `npm run test:unit`
* Run e2e tests : `npm run test:e2e:headless`
* Build the project : `npm run build`
* Check your js bundles sizes : `npm run bundlesize`
* Eventually deploy the built project to firebase hosting if the targeted branch is master : `npm run firebase:deploy:ci`

> ⚠️ For this step, we assume that you already have a github repository that hosts your expeditejs project with your source code pushed on the master branch ⚠️

### Steps

* Go to [CircleCI](https://circleci.com)
* Login with your github account
* Authorize CircleCI to look into your github projects
* Go to Side menu → Add projects and click the Set Up Project button corresponding to your expeditejs project
* You might be asked for choosing an OS and a language. If so, choose `Linux` and `Node`.
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