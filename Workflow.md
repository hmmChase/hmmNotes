# _Workflow_

---

# _Setup_

- https://medium.com/@adamramberg/setting-up-a-react-app-from-scratch-42521a118b10

## _Basic_

### repo first

1. Create repo on GitHub
   1. All lowercase
   2. Select readme and gitignore files
2. `git clone https://github.com/hmmChase/reponame.git`
3. `cd reponame`
4. `npm init -y`
   1. `"private": true`
5. Add to `/public/`
   1. `index.html`
   2. `scripts.js`
   3. `styles.css`

### project first

- Have project
- Create repo
- `git init`
- `git remote add origin https://github.com/hmmChase/reponame.git`
- `git add .`
- `git commit -m "first commit"`
- `git push -u origin master`

## _New Create-React-App_

1. If the client is not the root:
   1. Create repo on GitHub
      1. All lowercase
      2. Select readme and gitignore files
   2. `git clone https://github.com/hmmChase/reponame.git`
   3. `cd reponame`
   4. `npx create-react-app client`--use-npm``
   5. Delete `.git` folder in `./src` if present
   6. `npm init -y`
      1. Add `"private": true,`
   7. `cd`client``
   8. Move `.gitignore` to root folder
      1. Prepend folders with `**/`
      2. Add node ignores
2. If the client is the root:
   1. Create repo on GitHub
      1. All lowercase
      2. Don't select readme or gitignore files
   2. `npx create-react-app reponame`--use-npm``
   3. `cd reponame`
   4. `git init`
   5. `git remote add origin https://github.com/hmmChase/reponame.git`
3. Make initial commit to master branch
   1. `git checkout -b master`
   2. `git add .`
   3. `git commit -m "Add project files"`
   4. `git push origin master`

## _Add Redux_

- `npm i redux react-redux`
- `npm i -D redux-devtools-extension`
- Create `src/actions/` & `src/reducers/`
- Update `src/index.js`

## _Add Router_

- `npm i react-router-dom`
- Update `src/index.js`

## _Add middleware_

### Thunk

- `npm i redux-thunk`
- `npm i -D redux-devtools-extension`
- Create `src/thunks`
- Update `index.js`

### Add Saga

- `npm i redux-saga`
- If needed `npm i -D redux-devtools-extension`
- Create `src/sagas`
- Update `index.js`

## _Add Testing_

### Jest

- `npm i -D jest`

### Enzyme

- `npm i -`D `enzyme enzyme-adapter-react-16`
- Add `src/setupTests.js`

### Mocha/chai

- `npm i -`D``mocha `chai`chai-http``
- In `package.json`
  - `"test": "NODE_ENV=test mocha **/*.test.js --exit"`

## _Add concurrently_

- ?? Must have nodemon and concurrently installed globally
- In root `package.json`

```
"server": "cd server && nodemon server.js",
 "client": "cd client && npm start",
 "app": "concurrently --kill-others-on-fail \"npm run server\" \"npm run client\""
```

## _Add cross-env_

- `cd server`
- `npm i -D cross-env`
- Update `package.json`
  - `"test": "cross-env NODE_ENV=test mocha **/*.test.js --exit"`

## _Add TypeScript_

- https://www.carlrippon.com/creating-a-react-and-typescript-project/

## _Add Stylus_

- `npm i stylus`autoprefixer-stylus``
- Update `package.json` scripts

```
"watch": "concurrently --names \"webpack, stylus\" --prefix name \"npm run start\" \"npm run styles:watch\"",
"styles": "stylus -u autoprefixer-stylus ./src/css/style.styl -o ./src/css/style.css",
"styles:watch": "stylus -u autoprefixer-stylus -w ./src/css/style.styl -o ./src/css/style.css"
```

## _Add ESLint_

- `npm i -D eslint`
- `npm i -D babel-eslint`
- `npm i -D eslint-config-airbnb`
- `npm i -D eslint-plugin-react`
- ``npm i -D `eslint-plugin-jsx-a11y`
- `npm i -D eslint-plugin-import`
- Add `.eslintrc` and `.eslintignore` to root
- Add `package.json` script
  -

## _Add Proptypes_

- `npm install --save prop-types`

```
import PropTypes from 'prop-types';

MyComponent.propTypes = {
  SomeArray: PropTypes.array.isRequired
};
```

## _Connect to Firebase DB_

- Add project on firebase website
- `npm i firebase re-base`
- Create `src/base.js`

```
import firebase from 'firebase';
import Rebase from 're-base';

const firebaseApp = firebase.initializeApp({
  // get these from firebase dashboard
  apiKey: '',
  authDomain: '',
  databaseURL: ''
});

const base = Rebase.createClass(firebaseApp.database());

export { firebaseApp };

export default base;
```

- Setup a route that has a param to use a key in the database
  - `<Route path="/store/:storeID" component={App} />`
- Add to `App.js`

```
componentDidMount = () => {
  const { params } = this.props.match;
  this.ref = base.syncState(`${params.storeID}/fishes`, {
    context: this,
    state: 'fishes'
  });
};

componentWillUnmount = () => {
  base.removeBinding(this.ref);
};
```

## _Add Postgres database_

- psql `CREATE DATABASE database_name;`
- psql `CREATE DATABASE database_name_test;`
- `cd server`
- ` npm i knex ``pg `
- `knex init`
- Update `knexfile.js`
- `knex migrate:make initial`
  - Add migration code
- `knex migrate:latest`
- `knex seed:make table_name`
  - Add seed code
- `knex seed:run`

## _Add Express server_

- Create `/server`
- `cd server`
- `npm init -y`
  - `"private": true,`
- `npm i express ``body-parser```
- Create `server.js`
- If using C-R-A
  - Add proxy to `client/src/package.json`
    - `,"proxy": "http://localhost:3001/"`

## _Express backend w/ CRA frontend_

- `mkdir my-app`
- `cd my-app`
- `npm init -y`
  - `"private": true,`
  - `"main": "server.js"`
- `git init`
  - `git remote add origin https://github.com/hmmChase/reponame.git`
- `eslint`--init``
  - `"lint": "./node_modules/eslint/bin/eslint.js . --ignore-pattern node_modules/"`
  - `"lintWin": "eslint . --ignore-pattern node_modules/"`
- `npm i express ``body-parser```
- `npm i -D nodemon`concurrently``
- `npm i`-D``mocha `chai`chai-http``
  - `"test": "NODE_ENV=test mocha --exit"`
- Add `.gitignore`
- Add `README.md`
- Add `server.js`
- Add these npm scripts to be able to start the backend and frontend at the same time using `npm run app`

```
`"start": "node server.js",
` `"server": "nodemon server.js",
 "client": "cd client && npm start",
 "app": "concurrently --kill-others-on-fail \"npm run server\" \"npm run client\""`
```

- `create-react-app client`--use-npm``
- `cd client`
- Delete `README.md` & `.gitignore`
- `npm i normalize.css`
  - in `index.css`
    - `@import '../node_modules/normalize.css/normalize.css';`
- Add a `"proxy"` key in `client/package.json` so CRA will proxy API requests from the React app to the Express app
  - This tells the Webpack development server to proxy our API requests to our API server
  - `"proxy": "http://localhost:5000"`
- Add Router
  - `npm i react-router-dom`
- Add Redux
  - `npm i redux react-redux`
  - `npm install —save-dev redux-devtools-extension`
  - Add `src/actions/` & `src/reducers/`
  - Update `src/index.js`
- Add sagas/thunks
- Add Jest and Enzyme
  - `npm install —save-dev jest`
  - `npm i enzyme enzyme-adapter-react-16 —save-dev`
  - Add `src/setupTests.js`

## _Deploy to Heroku_

- https://daveceddia.com/deploy-react-express-app-heroku/
- Add a start script in `package.json`, so that Heroku knows how to start the app
  - Heroku will run the `start` script by default
  - `"start": "nodemon server.js"`
- Add these npm scripts to be able to start the backend and frontend at the same time using `npm run app`
  - `"server": "cd server && npm start", "client": "cd client && npm start", "app": "concurrently --kill-others-on-fail \"npm run server\" \"npm run client\""`
    - The `–kill-others-on-fail` flag will kill other processes if one exits with a non zero status code
- `create-react-app client`--use-npm``
- Add a “proxy” key in `client/package.json` so CRA will proxy API requests from the React app to the Express app
  - This tells the Webpack development server to proxy our API requests to our API server
  - `"proxy": "http://localhost:5000"`
- Heroku depends on the built client code in `client/build`, which we don’t have yet, and which we’d rather not check in to git
  - Tell Heroku to build the React app after we push up the code
  - Add to root `package.json`
  - `"heroku-postbuild": "cd client && npm install && npm run build"`
  - or
  - `"heroku-postbuild": "cd client && npm install && npm install --only=dev --no-shrinkwrap && npm run build"`

## _Deploy to Heroku using Travis CI_

- Create new app in dashboard
- If using a server
  - Add a `Procfile`
  - Install Postgres Addon
  - Configure Knex for Production
  - Update Your Server Environment
  - Migrate Your Production Database
- Add deploy config to `.travis.yml`
  - `travis setup heroku`
  - Must have the Travis and Heroku CLI tools install in order to generate an API key

## _Deploy to Now_

- Install Now globally if needed
  - `npm i -g now`
- `npm i serve`
- Update `package.json` script
  - `"dev": "react-scripts start",` `"start": "serve --single ./build",`
- `now`

## _Deploy to Netlify_

- Install Netlify globally if needed
  - `npm i -g netlify-cli`
- Create `\build\_redirects` file
  - Add `/* /index.html 200`
- `netlify deploy`
  - deploy path: `build`

## _Deploy to Apache web server_

- Copy `\build\` folder onto server using FTP client
- Add `.htacess` file

```
RewriteBase /
RewriteRule ^index\.html$ - [L]
RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME} !-d
RewriteRule . /index.html [L]
```

---

# _Next_

- `mkdir my-app`
- `cd my-app`
- `mkdir frontend`
- `mkdir backend`

---

## Frontend

- `cd frontend`
- `npm init -y`
- Update `package.json`
  - `"private": true`
- `npm i react react-dom next`
- `mkdir pages`
- `mkdir components`
- create `/pages/index.js`

```
export default () => <p>Hello World</p>;
```

- add scripts to `package.json`

```
"dev": "next -p 7777",
"build": "next build",
"start": "next start",
```

- start client with `npm run dev`

## Styled Components

- `npm i -D babel-plugin-styled-components`
- update `.babelrc`

```
{
  "presets": ["next/babel"],
  "plugins": ["styled-components"]
}
```

- update `_document.js`
- update `_app.js`

## Apollo client

- ` npm i graphql apollo-boost react-apollo ``isomorphic-unfetch `
- `mkdir graphql`
- `cd`graphql``
- Add `initApollo.js`
  - paste boilerplate
- Add `withApollo.js`
  - paste boilerplate
- Update `/pages/_app.js`

```
import { ApolloProvider } from 'react-apollo';
import withApollo from '../apollo/withApollo';

  render() {
    const { Component, pageProps, apolloClient } = this.props;

    return (
      <Container>
        <ApolloProvider client={apolloClient}>
          <ThemeProvider theme={theme}>
            <Layout>
              <Component {...pageProps} />
            </Layout>
          </ThemeProvider>
        </ApolloProvider>
      </Container>
    );
  }
}

export default withApollo(MyApp);
```

---

## _Backend_

- `cd backend`
- `npm init -y`
- Update `package.json`

```
`"private": true`

"dev": "nodemon src/index.js",
"start": "cross-env NODE_ENV=production node src/index.js",
"deploy": "prisma deploy -e .env",
```

### Apollo Server w/prisma

- `npm i graphql apollo-server dotenv graphql-import prisma-client-lib`
- `npm i -D nodemon prisma cross-env`
- `mkdir src`
- `mkdir prisma`
- `mkdir src/resolvers`
  - Create `src/resolvers/Query.js`

```
const Query = {};

module.exports = Query;
```

    * Create `src/resolvers/Mutation.js`

```
const Mutation = {};

module.exports = Mutation;
```

- Create `.env` & `.env.example`

```
PRISMA_ENDPOINT=
PRISMA_SECRET=
PRISMA_MANAGEMENT_API_SECRET=
PORT=
```

- Create `/src/index.js`

```
require('dotenv').config();
const createServer = require('./createServer');

const server = createServer();

server
  .listen({ port: process.env.PORT })
  .then(({ url }) => console.log(`Server ready at ${url}`));
```

- Create `/src/createServer.js`

```
const { ApolloServer } = require('apollo-server');
const { importSchema } = require('graphql-import');
const path = require('path');
const { prisma } = require('../prisma/generated/prisma-client');
const typeDefs = importSchema(path.resolve('src/schema.graphql'));
const Query = require('./resolvers/Query');
const Mutation = require('./resolvers/Mutation');

function createServer() {
  return new ApolloServer({
    typeDefs,
    resolvers: {
      Query,
      Mutation
    },
    context: req => ({
      ...req,
      prisma
    }),
    introspection: false,
    playground: false
  });
}

module.exports = createServer;
```

- Create `/src/schema.graphql`

```
# import * from '../prisma/generated/prisma.graphql'

type Query {}

type Mutation {}
```

### Create Prisma Server & Database

- Go to [https://app.prisma.io](https://app.prisma.io/)
- Click Add Server
- Input name/desc
- Click Create a new database
- Click Heroku
- Connect to Heroku
- Click Create Database
- Click Set up a server
- Click Heroku
- Click Create Server
- Click View the server
- Click your server name

* `prisma init`
  - Move Prisma files into `/prisma/`
* Update `prisma.yml`

```
endpoint: ${env:PRISMA_ENDPOINT}
datamodel: datamodel.prisma
secret: ${env:PRISMA_SECRET}
generate:
  - generator: javascript-client
    output: ./generated/prisma-client
  - generator: graphql-schema
    output: ./generated/
hooks:
  post-deploy:
    - prisma generate
```

- `npm run deploy -- -n`
  - Select server you created
  - Input a service name
  - Input `prod` for stage name
- Update `.env`

```
# Copy from the deploy output
PRISMA_ENDPOINT=
# Make up a secret
PRISMA_SECRET=
# On website, under Database section
# Click View on Heroku
# Click Settings
# Click Reveal Config Vars
# Copy from config => managementApiSecret
PRISMA_MANAGEMENT_API_SECRET=
# Choose a port to host the Apollo server on
PORT=
```

npm i

- `npm run deploy`
- Update `/prisma/prisma.yml`
  - `endpoint: ${env:PRISMA_ENDPOINT}`

### Deployment

- AWS Lambda
  - https://www.apollographql.com/docs/apollo-server/deployment/lambda.html

---

# _Versioning_

- SemVer
  - https://semver.org/
  - semantic versioning

---

# _License_

- Open source
  - https://choosealicense.com/
- Closed source
  - When you make a creative work (which includes code), the work is under exclusive copyright by default
  - Unless you include a license that specifies otherwise, nobody else can copy, distribute, or modify your work without being at risk of take-downs, shake-downs, or litigation
  - Once the work has other contributors (each a copyright holder), “nobody” starts including you

```
/*******************************************************
 * Copyright (C) 2010-2011 {name} <{email}>
 *
 * This file is part of {project}.
 *
 * {project} can not be copied and/or distributed without the express
 * permission of {name}
 *******************************************************/
```

---

# _Files_

- .gitignore
  - This is the standard file used by the source control tool git to determine which files and directories to ignore when committing code

* package.json
  - This file outlines all the settings
  - `name` is the name of your app
  - `version` is the current version
  - `"private": true` is a failsafe setting to avoid accidentally publishing your app as a public package within the npm ecosystem
  - `dependencies` contains all the required node modules and versions required for the application
  - `devDependencies` contains useful node modules and versions for using the app in a development environment
  - `scripts` specifies aliases that you can use to access scripts commands in a more efficient manner

- package-lock.json
  - This file contains the exact dependency tree installed in /node_modules/
  - This provides a way for teams working on private apps to ensure that they have the same version of dependencies and sub-dependencies
  - It also contains a history of changes to package.json, so you can quickly look back at dependency changes

* README.md
  - Explains what the project is, how to use it, and often times, how to contribute (though sometimes there is an extra file, 'CONTRIBUTING.md', for those details)

- LICENSE.md
  - Lists the type of license you put on your project
  - This lets others know how they can use it
  - choosealicense.com

* /public/manifest.json
  - Configures how your web app will behave if it is added to an Android user’s home screen (Android users can “shortcut” web apps and load them directly from the Android UI)
  - https://developers.google.com/web/fundamentals/web-app-manifest/

---

# _Folders_

- /node_modules/
  - Contains dependencies and sub-dependencies of packages used by the app, as specified by package.json

* /public/
  - Contains assets that will be served directly without additional processing by webpack
  - index.html provides the entry point for the web app

- /src/
  - This contains the JavaScript that will be processed by webpack and is the heart of the React app. Browsing this folder, you see the main App JavaScript component (**App.js**), its associated styles (**App.css**), and test suite (**App.test.js**). index.js and its styles (**index.css**) provide an entry into the App and also kicks off the **registerServiceWorker.js**. This service worker takes care of caching and updating files for the end-user. It allows for offline capability and faster page loads after the initial visit. More on this methodology is available here (https://goo.gl/KwvDNy).
  - As your React app grows, it is common to add a **components/** directory to organize components and component-related files and a views directory to organize React views and view-related files.

---

# _File structure_

## co-location

- Place files as close to where they’re relevant as possible
- datepicker/
  ├── day.js
  ├── day.test.js
  ├── index.js
  ├── index.test.js
  ├── logic
  │ ├── calculate-days-from-today.js
  │ ├── calculate-days-from-today.test.js
  │ ├── calculate-month-days.js
  │ ├── calculate-month-days.test.js
  │ ├── index.js
  │ └── index.test.js
  ├── month.js
  ├── month.test.js
  ├── year.js
  └── year.test.js

* Because of the way that Node (webpack/browserify) resolves modules (specifically a folder’s index.js file), you can simply do:
  - `require('./datepicker') // pointing to the folder`
  - Which will resolve to `'./datepicker/index.js'`

## BEM

- https://en.bem.info/methodology/filestructure/#file-system-organization-of-a-bem-project

---
