# _NPM_

- https://www.npmjs.com/
- https://docs.npmjs.com/

---

## Install

- Included with Node.js

## Upgrade

- https://docs.npmjs.com/troubleshooting/try-the-latest-stable-version-of-npm

---

## npx

- npx is a tool bundled with npm for easily running packages that are not installed globally

---

## **_Commands_**

- Create a package.json
  - `npm init`

* Create a package.json automatically
  - `npm init -f`

- View all locally installed packages
  - `npm list -depth=0`

* View all globally installed packages
  - `npm list -g -depth=0`

- Find out which global packages need to be updated
  - `npm outdated -g —depth=0`

* Find out which packages need to be updated
  - `npm outdated`

- Update global packages
  - `npm install -g <package>`

* Update all global packages
  - `npm update -g`

- Update all local packages
  - `npm update`
  - If a package is at version `1.3.5`, but the latest version is `3.0.5`, the package would only update to the latest `minor` version

* Update a package to latest version
  - `npm install <package name>@latest`

- Install a local package
  - `npm install`<package>``
  - `npm i`<package>``

* Install a global package
  - `npm install -g`<package>``

- Uninstall a local package
  - `npm uninstall`<package>``
  - `npm un <package>`
  - `npm rm <package>`

* Uninstall a global package
  - `npm uninstall -g`<package>``

- Delete all data out of the cache folder
  - `npm cache clean`
  - `npm cache clear`

* packages needed for production
  - `npm --save (-S)`

- packages needed for development
  - `npm --save-dev (-D)`

* username is your NPM username
  - `npm init --scope=username`

- publishes a public package
  - `npm publish --access=public`

* unpublishes a package
  - `npm unpublish --force`

- This runs an arbitrary command specified in the package's "start" property of its "scripts" object. If no "start" property is specified on the "scripts" object, it will run node server.js.
  - `npm start`

* To see who you're logged in as
  - `npm whoami`

- To see what dependencies are installed
  - `npm ls`

* To run tests from your test file
  - `npm test`

- To list outdated packages
  - `npm outdated`

---

# _Misc_

- `--`
  - Will append commands to the command you are about to run
  - It appends the NPM script with everything after `--`

---
