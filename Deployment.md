# _Deployment_

---

# _Continuous Integration_

- It clones a repo and runs the build process, verifying tests before a PR is merged
- Watches a repo and looks for changes

## _Branch Workflow_

- commit changes
- submit PR
  - tests failed
    - fix code
      - repeat
  - tests passed
    - merged
      - run build for master branch which contains the merged change
        - does build pass?
          - no
          - yes
            - automatically deploy to production

---

# _Travis CI_

- [https://docs.travis-ci.com](https://docs.travis-ci.com/)
- http://frontend.turing.io/lessons/module-4/continuous-integration.html
- http://frontend.turing.io/lessons/module-4/continuous-integration-walkthrough.html

* Install CLI tool
  - https://github.com/travis-ci/travis.rb#installation

- Go to [https://travis-ci.org](https://travis-ci.org/) and add the repository to the dashboard
- Add config file to root directory
  - `.travis.yml`
  - Uses `YML`
    - `JSON` with curly brackets
    - whitespace matters

```
// specify that project is using node
language: node_js

// specify node verson
// found out with node --version
node_js: '10'

// specify database type
services:
  - postgresql

// create a database
before_script:
  - psql -c 'create database database-name_test;' -U postgres

// turn off email notifications
notifications:
  email: false

// deployment settings
deploy:
  provider: heroku
  api_key:
    secure: hPF4SnFv...
  app: my-app
  skip_cleanup: true
  on:
    repo: hmmChase/repo-name
    branch: master

// enviromental variables
env:
  global:
    secure: EGNg/v5n...
```

- basic config:

```
language: node_js
node_js: '10'
notifications:
  email: false
```

- Automatically deploy if build passes
  - https://docs.travis-ci.com/user/deployment

## Environment variables

- https://docs.travis-ci.com/user/encryption-keys/
- `travis encrypt SOMEVAR="secretvalue" --add`

---

# _Apex Up_

- https://github.com/apex/up

## Installation

1. Download binary from https://github.com/apex/up/releases
   1. for 64-bit Windows
2. Extract the tarball file
   1. Might want to use 7-Zip
3. Copy `up.exe` into `"c:\Program Files\up"`
4. Add `C:\Program Files\up` to your `Path` environment variables

### AWS Credentials

- You need to install the [AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-welcome.html) and create your credentials with it
  - https://docs.aws.amazon.com/cli/latest/userguide/install-windows.html#install-msi-on-windows
- Once the AWS CLI is installed, you can go ahead and create your credentials
  - This requires you to have an AWS account and provide an **_AWS Access Key ID_** as well as the belonging **_AWS Secret Access Key_**

### Long and Didnt work

- From the [AWS documentation](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-getting-started.html), here is how you get access to these:
- Open the [IAM console](https://console.aws.amazon.com/iam/home?#home)
- In the navigation pane of the console, choose **Users**
- Choose your IAM user name (not the check box)
- Choose the **Security credentials** tab and then choose **Create access key**
- To see the new access key, choose **Show**. Your credentials will look something like this:
  - `AKIAIOSFODNN7EXAMPLE` (_Access Key ID_)
  - `wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY` (_Secret Access Key_)
- To download the key pair, choose **Download .csv file**. Store the keys in a secure location
- Keep the keys confidential in order to protect your AWS account, and never email them
  - Do not share them outside your organization, even if an inquiry appears to come from AWS or Amazon.com
  - No one who legitimately represents Amazon will ever ask you for your secret key
- Once you have the _Access Key ID_ and the _Secret Access Key_ accessible, run the following command and provide them when prompted:
  - `aws configure`
- If you need more help with setting up the credentials, you can check the corresponding section in the [Up documentation](https://up.docs.apex.sh/#aws_credentials.aws_credential_profiles) or [AWS](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-getting-started.html) directly
- The end result will be that you now have a hidden `.aws` directory inside your home folder
  - In there, you’ll find a file called `credentials` looking similar to this:
    - `[default]aws_access_key_id = xxxxxxxxaws_secret_access_key = xxxxxxxxxxxxxxxxxxxxxxxx`

### Short and Works

- Click on your name in upper-right corner
- Select Your Security Credentials
  - https://console.aws.amazon.com/iam/home#/security_credentials
- Select Access Keys
- Select Create New Access Key
  - Save access key ID and secret access key
- Run `aws configure`
  - Enter access key ID and secret access key
- Run `npx up --no-build`

### Bootstrap the GraphQL server

-

---

# _Heroku_

- http://frontend.turing.io/lessons/module-4/deploy-to-heroku.html

- Install CLI tool
  - https://devcenter.heroku.com/articles/getting-started-with-nodejs#set-up

```
"scripts": {
  "heroku-prebuild": "This runs before Heroku installs your dependencies.",
  "heroku-postbuild": "This runs afterwards."
}
```

---

# _Servers_

- https://nginxconfig.io/

* Error: listen EADDRINUSE: address already in use :::8080
  - `taskkill /F /IM node.exe`

---

# _Other_

## Deploy Create-React-App on Github pages

- https://github.com/gitname/react-gh-pages
- https://github.com/facebook/create-react-app/blob/master/packages/react-scripts/template/README.md#github-pages

* `npm install gh-pages --save-dev`
* Add configs to `package.json`

```
`"homepage": "http://username.github.io/repo-name"`
"scripts": {
  //...
  "predeploy": "npm run build",
  "deploy": "gh-pages -d build"
}
```

- `npm run deploy`
  - If this doesn't work in the terminal, use Git Bash

---
