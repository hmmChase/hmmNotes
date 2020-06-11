# _React SSR_

- Server-side Rendering

---

## Server-side

- Actions

  1. NodeJS runs JavaScript
  2. React started and all Component constructors run
  3. componentDidMount does not run on server
  4. Component render methods called
  5. Downloads static HTML that is generated from component
  6. All rendered static HTML sent to client browser

## Client-side

- Actions

  1. HTML downloaded from server
  2. Script tags download JavaScript files
  3. JavaScript executes, including all React components
  4. Component constructors run
  5. Component lifecycle events including componentDidMount run
  6. Component render methods called

---

# _Next.js_

- https://github.com/zeit/next.js
- https://nextjs.org/
- Next.js has 2 rendering modes/types
  - Dynamic rendering
    - Once a request comes in to the Next.js server, the page will be `require()`'ed
    - Then we call our lifecycle method `getInitialProps` if it's defined on the page
      - `getInitialProps` is an async function, returning a Promise
      - Provided by Next.js
    - When the Promise is resolved, we go on to render the page using React's `renderToString` method
    - This means that your `getInitialProps` method is `awaited` before starting to render
    - If it takes 3 seconds for your API to return results you will probably want implement caching on the API side, or investigate why your API is slow
  - Static export
    - You pre-build all pages as static html so they can be immediately served
      - without the call to `getInitialProps`
    - To do this, there is a command called `next export`
    - Once you run `next export`, every page definition in the `exportPathMap` is rendered to HTML
    - So at that point it will call `getInitialProps`
    - The export happens concurrently, using multiple cores of your machine, so multiple pages will be rendered at the same time

## General

- `react` is imported automatically

## SSR

- Next.js has 2 "pre-rendering" (server-side rendering) modes:

  1. On demand (traditional SSR)
     1. On demand rendering means for every request that comes in you render a unique page
        1. It's still possible to cache this response of course
     2. This is great for highly dynamic web apps in which content changes often
     3. You have a login state, and similar use cases
     4. This mode requires having a Node.js server running
     5. Examples of this are [zeit.co](https://zeit.co/), [marvel.com](https://marvel.com/), [deliveroo.com](https://deliveroo.com/), [jobs.netflix.com](https://jobs.netflix.com/), and [opencollective.com](https://opencollective.com/)
        1. more found here: https://spectrum.chat/?t=e425a8b6-c9cb-4cd1-90bb-740fb3bd7541
  2. Static export
     1. Render all pages to `.html` files up-front and serve them using any file server
     2. This does not require you to have a Node.js server running
     3. The html can run anywhere
     4. An example of this is [nextjs.org](https://nextjs.org/), [carbon.now.sh](https://carbon.now.sh/), [plot.ly](https://plot.ly/), [material-ui.com](https://material-ui.com/), and [vergecurrency.com](https://vergecurrency.com/)
        1. more found here: https://spectrum.chat/?t=e425a8b6-c9cb-4cd1-90bb-740fb3bd7541

## Meta

- Must create a `/components/Meta.js` file to config the `<Head></Head>` of HTML files
- Import into `Page.js` as the first rendered component
  - `import Meta from './Meta';`
  - `<Meta />`

```
import Head from 'next/head';

const Meta = () => (
  <Head>
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <meta charSet="utf-8" />
    <link rel="shortcut icon" href="/static/favicon.png" />
    <link rel="stylesheet" type="text/css" href="/static/nprogress.css" />
    <title>Sick Fits!</title>
  </Head>
);

export default Meta;
```

## Custom `<App>`

- Next.js uses a hidden `<App>` component to initialize pages
- By default, the entire app is wrapped in an `<App>` component
- You can override the `<App />` and control the page initialization by creating a `/pages/_app.js` file
- `Component` is a prop which represents whatever components are being rendered by a route
- By wrapping every component in `<Page>`, everything that `<Page>` does will persist through the changing components
- Can include a `getInitialProps()` to pass data props to the entire app

```
import App, { Container } from 'next/app';
import Page from '../components/Page';

class MyApp extends App {
  render() {
    const { Component } = this.props;

    return (
      <Container>
        <Page>
          <Component />
        </Page>
      </Container>
    );
  }
}

export default MyApp;
```

## Custom `<Document>`

- Only rendered on the server side
- Is used to change the initial server side rendered document markup
- Create `/pages/_document.js`

```
import Document, { Head, Main, NextScript } from 'next/document'

export default class MyDocument extends Document {
  static async getInitialProps(ctx) {
    const initialProps = await Document.getInitialProps(ctx)
    return { ...initialProps }
  }

  render() {
    return (
      <html>
        <Head>
          <style>{`body { margin: 0 } /* custom! */`}</style>
        </Head>
        <body className="custom_class">
          <Main />
          <NextScript />
        </body>
      </html>
    )
  }
}
```

- The `ctx` object is equivalent to the one received in all `getInitialProps` hooks, with one addition, `renderPage`
- `renderPage` is a callback that executes the actual React rendering logic (synchronously)
  - It's useful to decorate this function in order to support server-rendering wrappers like Aphrodite's `renderStatic`

## Styles

- In production, the stylesheet is compiled to `.next/static/style.css` and served from `/_next/static/style.css`
- To allow use of separate CSS files, you must modify the webpack config using `@zeit/next-css`
- In `next.config.js`:

```
const withCSS = require("@zeit/next-css");
module.exports = withCSS();
```

## Environment Variables

- `npm i dotenv-webpack`
- In `next.config.js`:

```
const withCSS = require('@zeit/next-css');
require("dotenv").config();
const path = require("path");
const Dotenv = require("dotenv-webpack");

module.exports = withCSS({
  webpack(config, options) {
    config.plugins = config.plugins || [];
    config.plugins = [
      ...config.plugins,
      // Read the .env file
      new Dotenv({
        // Specify path to .env file
        path: path.join(__dirname, '.env'),
        systemvars: true
      })
    ];
    return config;
  }
});
```

- Defaults
  - To set env vars not in the `.env` file
  - In `next.config.js`:

```
module.exports = withCSS({
  serverRuntimeConfig: {
    // Will only be available on the server side
  },
  publicRuntimeConfig: {
    // Will be available on both server and client
    RESTURL_SPEAKERS_PROD:
      'https://www.siliconvalley-codecamp.com/rest/speakers/ps',
    RESTURL_SPEAKER_PROD: 'https://www.siliconvalley-codecamp.com/rest/speaker',
    RESTURL_SESSIONS_PROD:
      'https://www.siliconvalley-codecamp.com/rest/sessions'
  },
  ... same as above
});
```

    * To reference env vars:

```
import getConfig from 'next/config';
const { serverRuntimeConfig, publicRuntimeConfig } = getConfig();

// Inside a component
static GetSpeakerUrl() {
  if (process.env.NODE_ENV === 'production') {
    return (
      process.env.RESTURL_SPEAKER_PROD ||
      publicRuntimeConfig.RESTURL_SPEAKER_PROD
    );
  } else {
    return process.env.RESTURL_SPEAKER_DEV;
  }
}
```

## Pages

- Every file in the `/pages` directory is a route
- The route is equal to the name of the file

## Code Splitting

- Each of the files in the `/pages` folder is a separate code segment that renders on its own
- When a user navigates to a page, only the JavaScript for that page is loaded to the browser

## Routing

- https://github.com/zeit/next.js#routing

### Imperative

- Changing the endpoint with code
- Provides several event methods to invoke custom code during the routing process

```
import Router from 'next/router';

Router.push({
  pathname: '/item',
  query: { id: res.data.createItem.id }
});
```

### Link

- A `<Link>` button will push to new endpoint
- Uses HTML5 push state
- Does all the `location.history` handling for you.
- Won't lose data in cache

```
<Link href={{ pathname: '/item' }}>
  <a>{item.title}</a>
</Link>
```

    * `query` will add params to the endpoint
        * `http://localhost:7777/item?id=cjra0n86n3u6i0a46d16esj9n`
    * `prefetch` will cache the link location right away, before being visited
        * doesn't work in development

- The only requirement for components placed inside a Link is they should accept an `onClick` prop

### Query Strings

- `<Link>` has an optional property for query strings

```
<Link href={{ pathname: '/item', query: { id: item.id } }}>
  <a>{item.title}</a>
</Link>
```

### withRouter

- `import { withRouter } from 'next/router';`
- Injects the Next.js router as a prop
- Allow access to the router's `query` object
  - Has the query string params

```
import { withRouter } from 'next/router';

const Page = withRouter(props => (
  <div>
    <h1>{props.router.query.title}</h1>
  </div>
));
```

### Route Masking

- Shows a different URL on the browser than the actual URL that your app sees
- Requires a custom server with custom routes
  - Redirects are only rendered client-side, and the specific page doesn't exist
- `as` is the desired URL

```
<Link
  href={{
    pathname: '/speaker',
    query: { speakerId: this.props.speaker.id }
  }}
  as={`speaker/${this.props.speaker.id}`}>
  <a>Details</a>
</Link>
```

```
server.get('/speaker/:speakerId', (req, res) => {
  const actualPage = '/speaker';
  const queryParams = { speakerId: req.params.speakerId };
  app.render(req, res, actualPage, queryParams);
});
```

## `getInitialProps`

- An `async` static method
- It can asynchronously fetch anything that resolves to a JavaScript plain `Object`, which populates `props`

* Can not be used in children components
  - Only in `/pages`

- Receives a context object with the following properties:
  - `pathname` - path section of URL
  - `query` - query string section of URL parsed as an object
  - `asPath` - `String` of the actual path (including the query) shows in the browser
  - `req` - HTTP request object (server only)
  - `res` - HTTP response object (server only)
  - `jsonPageRes` - [Fetch Response](https://developer.mozilla.org/en-US/docs/Web/API/Response) object (client only)
  - `err` - Error object if any error is encountered during the rendering

* For the initial page load, `getInitialProps` will execute on the server only
* `getInitialProps` will only be executed on the client when navigating to a different route via the `Link` component or using the routing APIs

- When executed server-side:
  - Establishes whatever data it needs to be in the props
  - Gets called before the constructor
  - Calls the constructor and passes the data into it, then the page is rendered
  - Also, it serializes the props and passes them into the HTML that gets downloaded by the client
    - You can view this by inspecting the HTML `<head>`, and finding the `<script>` with `id =__NEXT_DATA__`
  - When the client runs, it picks up the HTML and deserializes the props
  - When a component mounts, the props are fed into the constructor

* Does not run on the Client when it is a landing page load
  - Node runs first, and the client runs the same page second
  - When we land on this page from a client-side redirect, no servers are involved
    - `getInitialProps()` is run strictly on the client
  - Instead, it looks at the `__NEXT_DATA__` `<script>` , looks for the props value, and passes it into the constructor

- Fixes HTML mismatch problem
  - Problem
    - Data on the Client and Server doesn't match
    - Component constructors get called at different times on the Client and Server
  - Solution
    - Take the data generated on the server and pass it to the Client
    - Serialize the data and attach it to the static HTML page that gets rendered to the Browser
    - When the browser loads, unserialize data and pass into constructor
    - The Constructor turns the data into props that get rendered onto the page

## Pages

- Files in `/pages` get ran on both the client and the server
- Next looks for a static method called `getInitialProps()`

## Fetching Data

- https://github.com/zeit/next.js#fetching-data-and-component-lifecycle
- Next.js comes with a standard API to fetch data for pages using an async function called `getInitialProps`
- Will pass the data in as props to our page
- For use on both client and server
- `getInitialProps` is called server-side when the app in being rendered, and the result gets passed to the client
- Can add into any `page` in your app
- When you initially visit or refresh a page, it will fetch data server side
- If you navigate around client-side through links, it will fetch data client-side
- In a functional component:

```
MyPage.getInitialProps = async function() {
  const res = await fetch('https://api.tvmaze.com/search/shows?q=batman')
  const data = await res.json()

  console.log(`Show data fetched. Count: ${data.length}`)

  return {
    shows: data
  }
}
```

## Custom Server

- To serve app from a custom node server
- Update `package.json` scripts

```
"dev": "node server.js",
"build": "next build",
"start": "NODE_ENV=production node server.js",
```

## Image Handling

- `npm i next-images`
  - Allows importing images into a component as a constant
  - Load images from local computer
  - Load images from remote (CDN for example) by setting `assetPrefix`
  - Inline small images to Base64 for reducing http requests
  - Adds a content hash to the file name so images can get cached
- Update `next.config.js`

```
const withImages = require('next-images');

const withCSS = require('@zeit/next-css');
require('dotenv').config();
const path = require('path');
const Dotenv = require('dotenv-webpack');

/* Without CSS Modules, with PostCSS */
module.exports = withCSS(
  withImages({
    // If the resulting image tags are greater than this number,
    // then it will render it as an image tag,
    // else it will render as encoded data in the HTML
    inlineImageLimit: 16384,
    webpack(config, options) {
      config.plugins = config.plugins || [];
      config.plugins = [
        ...config.plugins,
        // Read the .env file
        new Dotenv({
          path: path.join(__dirname, '.env'),
          systemvars: true
        })
      ];
      return config;
    }
  })
);
```

```
`import myImg from '../static/myImg.png';

<img src={`myImg`}/>`
```

## Caching pages

```
const express = require('express');
const next = require('next');
const LRUCache = require('lru-cache');

const dev = process.env.NODE_ENV !== 'production';
const app = next({ dev });
const handle = app.getRequestHandler();

const ssrCache = new LRUCache({
  // Determine how big the passed-in object is
  length: function(n, key) {
    return n.toString().length + key.toString().length;
  },
  // Set max size limit before throwing stuff away
  max: 100 * 1000 * 1000, // 100MB cache soft limit
  // How long to keep in cache
  maxAge: 1000 * 10 // 1000 * 10 is 10 seconds
});

app
  .prepare()
  .then(() => {
    const server = express();

    server.get('/speaker/:speakerId', (req, res) => {
      const actualPage = '/speaker';
      const queryParams = { speakerId: req.params.speakerId };
      app.render(req, res, actualPage, queryParams);
    });

    server.get('*', (req, res) => {
      if (
        req.url === '/' ||
        req.url === '/speakers' ||
        req.url === '/sessions'
      ) {
        return renderAndCache(req, res, req.url, {});
      } else {
        return handle(req, res);
      }
    });

    server.listen(3000, err => {
      if (err) throw err;
      console.log('> Ready on http://localhost:3000');
    });
  })
  .catch(ex => {
    console.error(ex.stack);
    process.exit(1);
  });

// Check to see if the page has been rendered and cached before
// If so, use that, and not go throught the React processing pipeline
// to build the HTML
// i.e. Just grab HTML out of server-based memory, and return it
async function renderAndCache(req, res, pagePath, queryParams) {
  const key = getCacheKey(req);
  // Check ssrCache object if object has been cached before
  if (ssrCache.has(key)) {
    // If so, send it back as the response
    res.setHeader('x-cache', 'HIT');
    res.send(ssrCache.get(key));
    return;
  }
  // If not, call React library on every request
  try {
    const html = await app.renderToHTML(req, res, pagePath, queryParams);
    if (res.statusCode !== 200) {
      res.send(html);
      return;
    }
    // Store HTML in cache
    ssrCache.set(key, html);
    res.setHeader('x-cache', 'MISS');
    // Return HTML to client
    res.send(html);
  } catch (err) {
    app.renderError(err, req, res, pagePath, queryParams);
  }
}

function getCacheKey(req) {
  return `${req.url}`;
}
```

## CDN

- Update next.config.js

```
const isProd = process.env.NODE_ENV === 'production';

module.exports = {
  assetPrefix: isProd
    // CloudFront Domain Name
    ? 'http://d30k733rzexkhf.cloudfront.net'
    : '',
}
```

## Deploying

### Serverless deployment

- https://github.com/zeit/next.js#serverless-deployment
- Serverless deployment dramatically improves reliability and scalability by splitting your application into smaller parts (also called [lambdas](https://zeit.co/docs/v2/deployments/concepts/lambdas/))
- In the case of Next.js, each page in the `pages` directory becomes a serverless lambda
- There are [a number of benefits](https://zeit.co/blog/serverless-express-js-lambdas-with-now-2#benefits-of-serverless-express) to serverless
  - The referenced link talks about some of them in the context of Express, but the principles apply universally
- Serverless allows for distributed points of failure, infinite scalability, and is incredibly affordable with a "pay for what you use" model

### Now v2

- `npm install next@canary`
- add `package.json` script
  - `"now-build": "next build"`
- create `next.config.js` in root

```
module.exports = {
  target: "serverless",
};
```

- create `now.json` in root

```
{
  "name": "next-graphql-starter",
  "version": 2,
  "builds": [
    { "src": "frontend/static/*", "use": "@now/static" },
    { "src": "frontend/package.json", "use": "@now/next" }
  ],
  "routes": [
    { "src": "/static/(.*)", "dest": "/frontend/static/$1" },
    { "src": "/(.*)", "dest": "/frontend/$1" }
  ]
}
```

### Docker

1. Make a docker image
   1. Make a `Dockerfile` file in the root

```
FROM node:alpine

# Create app directory
RUN mkdir -p /usr/src
WORKDIR /usr/src

# Install app dependencies
COPY package.json /usr/src/
COPY package-lock.json /usr/src/
RUN npm install

# Bundle app source
COPY . /usr/src

RUN npm run build
EXPOSE 3000

CMD ["npm", "start"]
```

1. Publish the image to a Docker registry
   1. `docker build -t svccps1 .`
   2. `docker tag`
2. Push image from Docker registry to Digital Ocean
   1. `docker push`
3. Run our app on a public URL
   1. Create droplet
      1. one-click app
         1. docker
   2. Create SSH key
      1. PuTTY Gen
   3. Add SSH to droplet
   4. Get IP of droplet, add to putty
      1. add private key to SSH Auth setting
   5. Login as `root`
   6. Login to docker
   7. `docker pull`
   8. `docker run`

## _Boilerplates_

### create-next-app

- https://github.com/segmentio/create-next-app
- https://open.segment.com/create-next-app/
- `npm install -g create-next-app`
- To create an app:
  - `create-next-app my-app`
  - `cd my-app`
- To build a version for production:
  - `npm run build`
- To run the server in production:
  - `npm run start`
- To start a local server for development:
  - `npm run dev`

## _Starters_

- https://codebushi.com/nextjs-website-starters/
  - Fontawesome, Sass
- https://github.com/nextjs-boilerplate
  - Navigation, more
- https://github.com/nextjs-boilerplate/next.js-boilerplate
  - i18next, next-routes, next-routers, CSRF protect, HTTP2, Cookie, Redux
- https://github.com/nextjs-boilerplate/next-express-redux-i18n
  - i18next, Redux, ES6 server, eslint, JWT, Testing
- https://github.com/iaincollins/nextjs-starter
  - Now, Auth, Passport, Account management, Sass, Bootstrap, Mongodb, dotenv, nodemailer
- https://github.com/YuriBrunetto/next-starter
  - Normalize, Sass
- https://github.com/me-io/nextjs-starter/
  - Docker, Now, PWA, next-routes, Fontawesome, Redux, JWT, Passport, i18n, Dotenv, Express, Eslint, Offline, Sass
- https://github.com/johnpolacek/styled-starter
  - Styled System
- https://github.com/postlight/headless-wp-starter
  - WordPress, Docker, Express, Sass, Normalize,
- https://github.com/yann-yinn/reactpress
  - Wordpress
- https://github.com/keen-studio/react-wp-rest
  - Wordpress
- https://github.com/richg0ld/nextjs-boilerplate
  - TypeScript, immutable, nprogress, redux, redux-saga, react-intl, styled-components, pm2, express, uglifyjs, Testing
- https://github.com/jorngeorg/nextauthtest
  - basic-auth, sanity
- https://github.com/ooade/NextSimpleStarter
  - PWA, workbox, redux
- https://github.com/ooade/NextSimpleStarter
  - PWA
- https://github.com/Sly777/ran
  - PM2, styled-components, offline-plugin, GraphQL, dotenv-webpack, babel-plugin-import-graphql, react-helmet, LRUCache
- https://github.com/saltyshiomix/ark
  - nestjs, passport, typeorm, PostgreSQL, Material UI, typescript

## _Examples_

- https://github.com/zeit/now-examples
- https://github.com/zeit/next.js/tree/master/examples
- https://github.com/zeit/next.js/tree/canary/examples
- https://github.com/now-examples?utf8=%E2%9C%93&q=next&type=&language=
  - Nprogress, Firebase, react-datasheet, mathjs, Now, Static, Docker
- https://github.com/async-labs/saas
  - User auth, Mono-repo, Material-UI, Express, MongoDB, TypeScript, Now, Helmet, Downshift, Stripe, Nprogress, mobx-react, material-ui, express-session
- https://github.com/builderbook/builderbook
  - MongoDB, Express, Material-UI, OAuth, Github API, AWS SES, Stripe, MailChimp, express-session, LRUCache, NProgress
- https://github.com/builderbook/harbor
  - Material-UI, Express, MongoDB, Now, Passport, Stripe, Winston
- https://github.com/fus-marcom/franciscan-react
  - Material UI, Now, Apollo, next-offline, ESLint, Testing, Husky, Algolia, html-entities, compose, PWA, LRUCache
- https://github.com/hanford/personal-website
  - PWA, Now, Github API, TypeScript, next-offline, Husky, emotion
- https://github.com/hanford/trends
  - PWA, Mono-repo, Now, Husky, Github API, Apollo, Offline, TypeScript
- https://github.com/hanford/next-offline
  - Offline, Now, Husky
- https://github.com/coderplanets/coderplanets_web
  - PWA, Styled-Components, Testing, Apollo, ESLint, Testing, mobx, next-seo, lru-cache, antd, sentry
- https://github.com/auth0-blog/nextjs-got
  - https://auth0.com/blog/building-universal-apps-with-nextjs/
  - Auth0
- https://github.com/TejasQ/anna-artemov.now.sh
  - Now, webfontloader, emotion, react-div-100vh
- https://github.com/webpro/bookstore
  - Apollo, Sass, SSL, material-ui, import-graphql, dotenv-webpack, devcert, https
- https://github.com/josephluck/next-typescript-monorepo
  - TypeScript, Mono-repo, styled-components, Express, faker,
- https://github.com/este/este
  - Mono-repo, Now, TypeScript, Relay, Prisma, JWT, Apollo, Nprogress, Native-web, next-plugin-custom-babel-config, next-bundle-analyzer, next-transpile-modules, Sentry, react-intl, react-relay
- https://github.com/bukinoshita/open-source
  - Xo, GitHub API
- https://github.com/orbiting/construction
  - Mandrill, Mailchimp, Apollo, next-routes, Redux, D3, express-basic-auth
- https://github.com/PlatziDev/pulse
  - Electron
- https://github.com/opencollective/opencollective-frontend
  - Now, Apollo, Cloudflare, dotenv, downshift, next-routes, QRcode, bootstrap, rebass, nodemailer, nprogress, express-session, bluebird, lru-cache, styled-components, validator, cookie-parser, google-maps, stripe
- https://github.com/nteract/nteract.io
  - polished, styled-components, gtag, react-fns
- https://github.com/KATT/shop
  - Monorepo, TypeScript, apollo-client, yoga, prisma w/docker, nightwatch, inline-dotenv
- https://github.com/selbekk/react-christmas
  - Now, Styled-Components, hooks, Google Analytics
- https://github.com/benawad/fullstack-graphql-airbnb-clone
  - Monorepo, styled-components, apollo-client, codegen, antd, formik, express-session, graphql-shield, graphql-yoga, ioredis
- https://github.com/benawad/monorepo-boilerplate
  - apollo-boost, styled-components, apollo-server-express, next-css
- https://github.com/maapteh/graphql-modules-app
  - Monorepo, apollo-server-express, codegen, pm2, graphql-depth-limit
- https://github.com/up4life/frontend
  - ALOT

## _Plugins_

- https://github.com/zeit/next-plugins

### next-css

- Import `.css` files in your Next.js project
- https://github.com/zeit/next-plugins/tree/master/packages/next-css
- `npm install --save @zeit/next-css`

### next-compose-plugins

- Provides a cleaner API for enabling and configuring plugins for next.js
- https://github.com/cyrilwanner/next-compose-plugins
- `npm install --save next-compose-plugins`

---

# _Gatsby_

- https://www.gatsbyjs.org/
- https://khaledgarbaya.net/articles/moving-from-create-react-app-to-gatsby-js

- When creating a new Gatsby site, you can use the following command structure to create a new site based on any existing Gatsby starter:
  - `gatsby new [SITE_DIRECTORY_NAME] [URL_OF_STARTER_GITHUB_REPO]`

## Starters

- https://www.gatsbyjs.org/starters/

## Plugins

- https://www.gatsbyjs.org/plugins/

### Source plugins

- Source plugins fetch data from their source
  - The filesystem source plugin knows how to fetch data from the file system
    - ` npm`` ``install`` --save gatsby-source-filesystem `
    - Then add it to your `gatsby-config.js`

```
module.exports = {
  plugins: [
    {
      resolve: `gatsby-source-filesystem`,
      options: {
        name: `src`,
        path: `${__dirname}/src/`,
      }
    }
  ]
}
```

    * The WordPress plugin knows how to fetch data from the WordPress API

- `gatsby-source-filesystem`
  - Includes a function for creating slugs

### Transformer plugins

- Takes raw content from source plugins and transform it into something more usable

## gatsby-browser.js

- https://www.gatsbyjs.org/docs/browser-apis/

## gatsby-config.js

- https://www.gatsbyjs.org/docs/gatsby-config/

## gatsby-node.js

- To implement an API, you export a function with the name of the API from this file

```
exports.onCreateNode = ({ node }) => {
  console.log(node.internal.type)
}
```

- `onCreateNode` will be called by Gatsby whenever a new node is created or updated
- Use this API to add the slugs for your markdown pages to `MarkdownRemark` nodes

```
exports.onCreateNode = ({ node }) => {
  if (node.internal.type === `MarkdownRemark`) {
    console.log(node.internal.type)
  }
}
```

## GraphQL

### page-query

- https://www.gatsbyjs.org/docs/page-query/
- ` import`` ``{`` graphql ``}`` ``from`` ``"gatsby" `
- Only `pages` can make page queries

```
import React from "react"
import { graphql } from "gatsby"
import Layout from "../components/layout"

export default ({ data }) => (
  <Layout>
    <h1>About {data.site.siteMetadata.title}</h1>
    <p>
      We're the only site running on your computer dedicated to showing the best
      photos and videos of pandas eating lots of food.
    </p>
  </Layout>
)

export const query = graphql`
  query {
    site {
      siteMetadata {
        title
      }
    }
  }
`
```

### StaticQuery

- https://www.gatsbyjs.org/docs/static-query/
- Allows components to retrieve data via GraphQL query

```
import React from "react"
import { StaticQuery, graphql } from "gatsby"
import PropTypes from "prop-types"

const Header = ({ data }) => (
  <header>
    <h1>{data.site.siteMetadata.title}</h1>
  </header>
)

export default props => (
  <StaticQuery
    query={graphql`
      query {
        site {
          siteMetadata {
            title
          }
        }
      }
    `}
    render={data => <Header data={data} {...props} />}
  />
)

Header.propTypes = {
  data: PropTypes.shape({
    site: PropTypes.shape({
      siteMetadata: PropTypes.shape({
        title: PropTypes.string.isRequired,
      }).isRequired,
    }).isRequired,
  }).isRequired,
}
```

## Programmatically create pages

- Creating new pages has two steps:
  - Generate the “`path`” or “`slug`” for the page
  - Create the page
- `onCreateNode`

```
const { createFilePath } = require(`gatsby-source-filesystem`)

exports.onCreateNode = ({ node, getNode, actions }) => {
  const { createNodeField } = actions
  if (node.internal.type === `MarkdownRemark`) {
    const slug = createFilePath({ node, getNode, basePath: `pages` })
    createNodeField({
      node,
      name: `slug`,
      value: slug,
    })
  }
}
```

- `createPages`

```
exports.createPages = ({ graphql, actions }) => {
  const { createPage } = actions
  return graphql(`
    {
      allMarkdownRemark {
        edges {
          node {
            fields {
              slug
            }
          }
        }
      }
    }
  `).then(result => {
    result.data.allMarkdownRemark.edges.forEach(({ node }) => {
      createPage({
        path: node.fields.slug,
        component: path.resolve(`./src/templates/blog-post.js`),
        context: {
          // Data passed to context is available
          // in page queries as GraphQL variables.
          slug: node.fields.slug,
        },
      })
    })
  })
}
```

---

# _AWS AppSync_

## Examples

- https://github.com/dabit3/appsync-graphql-real-time-canvas

---
