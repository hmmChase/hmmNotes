# _React Libraries_

- https://reactresources.com/

---

# _Starters_

- https://reactjs.org/community/starter-kits.html
- https://github.com/rwieruch/fullstack-apollo-react-express-boilerplate-project
  - Express, PostgreSQL/MongoDB, Apollo, Sequelize, Authentication, Authorization, dataloader, Testing, Pagination
- https://github.com/HappyZombies/application-setup
  - Express, Knex, MySQL, Redux, Styled Components, Socket.io, Winston
- https://github.com/monsieurBoutte/react-pwa-boilerplate
  - PWA(workbox), Redux(easy-peasy), Material UI, Netlify, Routing, react-app-rewired
- https://github.com/react-boilerplate/react-boilerplate
  - Sagas, Redux, Styled-Components, Sanitize, Router, Express, Offline, SEO, i18n, Testing, PWA

---

# _Examples_

- https://github.com/FotonTech/gigatron
  - Mono-repo, Apollo, Now, Styled-components, MongoDB, JWT, Auth, Testing

---

# _create-react-app_

- https://facebook.github.io/create-react-app/
- Create React apps with no build configuration
- Install boilerplate globally:
  - `npm install -g create-react-app`
- Create a new project:
  - `create-react-app my-app`--use-npm``
  - `cd my-app`
  - `npm start`
- Updating
  - `npm install react-scripts@latest`

## Includes

- Autoprefixer
- Babel
- Browserify
- ESLint
- ESLint-plugin-react
- Handlebars
- Jest
- Lodash
- PostCSS
  - Autoprefixer
- React
- React-dev-utils
- React-dom
- React-error-overlay
- React-scripts
  - SASS
  - TypeScript
- Source Map
- Uglify
- Webpack
  - CommonJS

## react-scripts

- start
  -
- build
  - Compiles and minifies app into single JS and CSS files and leaves out things only needed for development
- eject
  - Copies all of CRAs configurations to your project and hands over full control over to you

## VSCode Debugging

- You would need to have the latest version of [VS Code](https://code.visualstudio.com/) and VS Code [Chrome Debugger Extension](https://marketplace.visualstudio.com/items?itemName=msjsdiag.debugger-for-chrome) installed.
- Then add the block below to your `launch.json` file and put it inside the `.vscode` folder in your app’s root directory.

```
{
  "version": "0.2.0",
  "configurations": [
    {
      "name": "Chrome",
      "type": "chrome",
      "request": "launch",
      "url": "http://localhost:3000",
      "webRoot": "${workspaceRoot}/src",
      "sourceMapPathOverrides": {
        "webpack:///src/*": "${webRoot}/*"
      }
    }
  ]
}
```

## Configure Webpack:

- `/node_modules/react-scripts/config/webpack.config.dev.js`
  - to change the sourcemapping:
    - `devtool: 'cheap-module-source-map',`

## SCSS

- https://github.com/facebook/create-react-app/blob/master/packages/react-scripts/template/README.md#adding-a-css-preprocessor-sass-less-etc

## MISC

- [https://github.com/facebook/create-react-app/blob/master/packages/react-scripts/template/README.md](https://github.com/facebook/create-react-app/blob/master/packages/react-scripts/template/README.md#adding-a-sass-stylesheet)

## Environment Variables

- Create a `.env` file in the root of your project folder and define any variables your wish to use in your files
- Prefix any environment variable you wish to define with `REACT_APP` and Create React App will replace it with its actual value when building your files
- By default you will have `NODE_ENV` defined for you
  - You can read it from `process.env.NODE_ENV`
  - When you run `npm start`, it is always equal to `'development'`
  - When you run `npm test` it is always equal to `'test'`
  - When you run `npm run build` to make a production bundle, it is always equal to `'production'`
- Any other environment variables must start with `REACT_APP_`

```
REACT_APP_CLIENT_SECRET=client-secret
REACT_APP_CLIENT_KEY=client-key
```

## HTTPS

- During development, one might need the development server to serve pages over `HTTPS`
- Set the `HTTPS` environment variable to `true` before starting the server
- instead of running:
  - `npm start`
- On Windows cmd you run:
  - `set HTTPS=true&&npm start`
- On Powershell run:
  - `($env:HTTPS = $true) -and (npm start)`
- On Linux and macOS run:
  - `HTTPS=true npm start`

---

# _Tutorials_

- How to Create a React app from scratch using Webpack 4
  - https://medium.freecodecamp.org/part-1-react-app-from-scratch-using-webpack-4-562b1d231e75
- Build with React
  - http://buildwithreact.com/tutorial/
- Build Youtube
  - https://productioncoder.com/build-youtube-in-react-part-1/

---

# _UI_

- https://github.com/jaywcjlove/awesome-uikit
- https://github.com/anubhavsrivastava/awesome-ui-component-library

## Material-UI

- https://material-ui.com/

## Reactstrap

- https://reactstrap.github.io/

## Carbon Components React

- https://github.com/ibm/carbon-components-react

## Ant Design

- https://ant.design/

---

# _Components_

- https://github.com/brillout/awesome-react-components

## Drag and Drop

- https://medium.com/@siffogh3/how-to-make-and-test-your-own-react-drag-and-drop-list-with-0-dependencies-6fb461603780

## react-window

- React components for efficiently rendering large lists and tabular data
- https://github.com/bvaughn/react-window

## Collections

- https://www.primefaces.org/primereact/#/
- https://github.com/froala/react-froala-design-blocks

## ArchitectUI

- Modern Responsive Bootstrap 4 jQuery HTML Dashboard Template
- https://architectui.com/#/

## redux-form

- A Higher Order Component using react-redux to keep form state in a Redux store
- https://github.com/erikras/redux-form

## Formik

- Build forms in React, without the tears
- https://github.com/jaredpalmer/formik

## react-adopt

- Compose render props components like a pro
- https://github.com/pedronauck/react-adopt
- Combines render props

## Downshift

- Primitive to build simple, flexible, WAI-ARIA compliant enhanced input React components
- https://github.com/paypal/downshift

## React-Select

- The Select control for [React](https://reactjs.com/)
- https://github.com/JedWatson/react-select

## react-styled-select

- This project was built with [styled-components](https://github.com/styled-components/styled-components) and is a "rethink" of the awesome project [react-select](https://github.com/JedWatson/react-select)
- https://github.com/agutoli/react-styled-select

## React-Grid-Layout

- A grid layout system
- Gapless, draggable grid layouts
- https://github.com/STRML/react-grid-layout

---

# _Data_

## react-virtualized

- React components for efficiently rendering large lists and tabular data
- https://github.com/bvaughn/react-virtualized
- https://bvaughn.github.io/react-virtualized/
- `npm install react-virtualized --save`

---

# _Database_

## re-base

- A Relay inspired library for building React.js + Firebase applications
- https://github.com/tylermcginnis/re-base

---

# _Redux_

## Redux Persist

- Persist and rehydrate a redux store
- https://github.com/rt2zz/redux-persist
- `npm install redux-persist`

---

# _CSS_

## styled-components

- CSS-in-JS
  - Abstracts the CSS model to the component level, rather than the document level
- https://www.styled-components.com/
- https://github.com/styled-components/styled-components
- `npm install --save styled-components`
- Instead of add a `className` to a component, you replace the component with the styles attached to it
- You should only create a new component if you are reusing it
- You can still use selectors
- JSX works in the CSS rule values
- Can be written in a component file or extracted into a separate file and imported in

```
import React, { Component } from 'react';
import styled from 'styled-components';

const MyButton = styled.button`
  background: red;
  font-size: ${props => (props.huge ? '100px' : '50px')};
  span {
    color: blue;
    font-size: 50px;
  }
`;

class MyComponent extends Component {
  render() {
    return (
      <div>
        <MyButton huge>
          Click
          <span>Me</span>
        </MyButton>
      </div>
    );
  }
}

export default MyComponent;
```

**injectGlobal**

- Just call anywhere in your app, and it will inject the `injectGlobal` rules globally

```
injectGlobal`
  @font-face {
    font-family: 'radnika_next';
    src: url('/static/radnikanext-medium-webfont.woff2') format('woff2');
    font-weight: normal;
    font-style: normal;
  }
  html {
    box-sizing: border-box;
    font-size: 10px;
  }
  *, *:before, *:after {
    box-sizing: inherit;
  }
  body {
    padding: 0;
    margin: 0;
    font-size: 1.5rem;
    line-height: 2;
    font-family: 'radnika_next';
  }
  a {
    text-decoration: none;
    color: ${theme.black};
  }
`;
```

### Themes

- An object of property values that you wish to use throughout your app
- Uses context API
- Import `ThemeProvider` and `injectGlobal`
  - `import styled, { ThemeProvider, injectGlobal } from 'styled-components';`
- Define the theme object in the `<Page>` component
- Wrap everything in the `<Page>` components `render()` in a `<ThemeProvider>` component and pass in the `theme` object
- To access the theme properties in sub components, just wrap their `render()` in `<ThemeProvider>`
  - No need to pass in a theme object again

```
const theme = {
  red: '#FF0000',
  maxWidth: '1000px',
  bs: '0 12px 24px 0 rgba(0, 0, 0, 0.09)'
};

class Page extends Component {
  render() {
    return (
      <ThemeProvider theme={theme}>
        <StyledPage>
          <Meta />
          <Header />
          <Inner>{this.props.children}</Inner>
        </StyledPage>
      </ThemeProvider>
    );
  }
}
```

### Server-Side Rending

- By default, CSS-in-JS doesn't load on the server
- First, Next.js renders the app on the server
- Then, the client picks it up and checks for any updates that need to happen
- When you refresh the page, it mounts each component and its corresponding styles synchronously
- This results in viewing a flash of unstyled elements every time the app is refreshed
- To prevent this, all the CSS is required at time of the initial render
- Must add a custom `<Document>` in your Next.js app
- Create `_document.js` in `/pages/`
- Will crawl the component tree before rendering, collect all the styles used, compile them into one, insert them into the app, then send off to the client

```
import Document, { Head, Main, NextScript } from 'next/document';
import { ServerStyleSheet } from 'styled-components';

export default class MyDocument extends Document {
  static getInitialProps({ renderPage }) {
    const sheet = new ServerStyleSheet();
    const page = renderPage(App => props =>
      sheet.collectStyles(<App {...props} />)
    );
    const styleTags = sheet.getStyleElement();
    return { ...page, styleTags };
  }

  render() {
    return (
      <html>
        <Head>{this.props.styleTags}</Head>
        <body>
          <Main />
          <NextScript />
        </body>
      </html>
    );
  }
}
```

### UI libraries

- https://github.com/styled-components/awesome-styled-components#built-with-styled-components
- https://github.com/rebassjs/rebass
- https://github.com/grommet/grommet

---

# _Animations_

## react-transition-group

- An easy way to perform animations when a React component enters or leaves the DOM
- https://github.com/reactjs/react-transition-group
- https://reactcommunity.org/react-transition-group/
- `npm install react-transition-group --save`
- Provides timed auto adding and removing of classes

```
.count-enter
  transition .5s
  transform translateY(100%)
  &.count-enter-active
    transform translateY(0)

.count-exit
  transform translateY(0)
  transition .5s
  position absolute
  left 0
  bottom 0
  &.count-exit-active
    transform translateY(-100%)
```

```
const transitionOptions = {
  classNames: "order",
  key,
  timeout: { enter: 500, exit: 500 }
};

<TransitionGroup className="count" component="span">
  <CSSTransition {...transitionOptions}>
    <span>{count}</span>
  </CSSTransition>
</TransitionGroup>

```

## react-motion

- A spring that solves your animation problems
- https://github.com/chenglou/react-motion

---

# _Internationalization_

- https://react.i18next.com/
- https://github.com/yahoo/react-intl

---

# Renderers

- https://github.com/chentsulin/awesome-react-renderer

---

# _Styleguides_

- https://github.com/streamich/awesome-styleguides

---

# _Misc_

## React Lifecycle Visualizer

- Real-time visualizer for React lifecycle methods
- https://github.com/Oblosys/react-lifecycle-visualizer
- https://stackblitz.com/github/Oblosys/react-lifecycle-visualizer/tree/master/examples/parent-child-demo?file=src/samples/New.js

## prop-types

- Runtime type checking for React props and similar objects
- https://github.com/facebook/prop-types
- `npm install --save prop-types`

---

# Optimization

## react-lazyload

- Lazy load your component, image or anything matters the performance
- https://github.com/jasonslyvia/react-lazyload
- `npm install --save react-lazyload`

## react-loadable

- A higher order component for loading components with promises
- https://github.com/jamiebuilds/react-loadable
- `npm i react-loadable`

---
