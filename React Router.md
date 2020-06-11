# _React Router_

- Allows you to change the interface without having to reload the page
- The process of keeping the browser in-sync with what is rendered on the page

- The library consists of react components

---

- Use to:
  - Define which components are rendering based on the URL pathname (dynamic, nested views should have a URL of their own)
  - Bookmark specific page/view within our application to reference at a later time
  - Utilize the `back` and `forward` buttons in our browser

* 3 versions:
  - react-router-dom
  - react-router-native
  - react-router

- 3 types of components:
  - router components
    - `<BrowserRouter></`BrowserRouter>``
  - route matching components
    - `<Route />`
  - navigation components
    - `<Link />` or `<Link></Link>`
    - `<NavLink>`</NavLink>``

---

# _react-router-dom_

- `npm i --save react-router-dom`
- Comes with the following router components:
  - `<BrowserRouter>`
    - A Router that uses the HTML5 history API to keep your UI in sync with the URL
    - Dynamic
    - Can only have one child element, so multiple `<Routes />` must be wrapped in a `<div>`
    - Wraps your entire app
      - Typically used in index.js

```
import { BrowserRouter } from 'react-router-dom';

const router = (
  <BrowserRouter>
    <App />
  </BrowserRouter>
);

ReactDOM.render(router, document.getElementById('root'));
```

    * `<HashRouter>`
        *
    * `<NativeRouter>`
        * mobile
    * `<MemoryRouter>`
        * testing
    * `<StaticRouter>`
        * testing

---

# _Route_

- `import { Route } from 'react-route';`
- `import { Route } from 'react-router-dom';`

- For creating routes
- A component with a `render()` method
- Its most basic responsibility is to render some UI when a URL location matches the route's path

## _Path_

- `<Route>` always has a prop of `path`
  - `<Route path='./pathOfComponent' component={myComponent} />`
  - Assign to the URL endpoint where you want something to be rendered
  - `path='/'` is matched with any path that starts with a forward slash `/`

* Qualifiers
  - `exact path='/'`
  - When `true`, will only match if the path matches the `location.pathname` exactly
  - Doesn't care about a trailing forward slash `/`


    * `strict path='/about/'`
    * When `true`, a `path` that has a trailing slash will only match a `location.pathname` with a trailing slash
    * Does care about a trailing forward slash `/`

- URL Parameters
  - A method by which we can extract parameters from the URL to match a <Route>
  - URLs can be looked at as the gateway to our data, and carry a lot of information that we want to use as context so that the user can return to a particular resource or application state
  - Acts as a variable that is assigned to whatever the URL endpoint is


    * semi-colon `:` declares the variable
        * ``path='```/:myPage'` is matched to whatever comes after `/` in the URL
        * it is matched using `match.params.myPage`



    * to set the param as optional, use a question mark `?` after the param name
        * ```path='``/:myPage?'`



    * to add URL extensions, use a hyphen `-`
        * `path='/:pageee?-:extension?'`

- Regular expressions
  - Use regular expressions to more precisely define the paths to routes
  - ` path``=```" `/:a:b(`\.`[a-z]+)`"``

* Parse Query Parameters
  - React Router v4 ignores query parameters entirely
  - It is up to you to parse them so that you can use that additional information as required
  - ` <``Link to``=```" `/?id=123` "```>``Inline``<``/``Link``> `
  - ` <``Link to``=``{{pathname``:`` ```' `/` '```, search``:`` ```' `id=456` '```}}``>``Object``<``/``Link``> `
  - ` new`` ``URLSearchParams``(``location``.``search``).``get``(```' `id` '```) `

- A `<Route>` without a path will always render
  - Use to create a catch-all route

```
<Switch>
  <Route exact path="/" render={Home} />
  <Route path="/about/" render={About} />
  <Route render={() => <h1>404: Page not found</h1>} />
</Switch>
```

## _Rendering_

- After setting the path, you need to specify what to render
  - There are 3 ways to render something with a Route
    - `component`
      - `<Route path='./unicorns' component={Unicorns} />`
      - Just renders a component
      - The simplest way to render
      - Can't be used for a component that needs props


        * `render`
            * This also allows you to define and pass specific properties to a component dynamically
            * For inline JSX or components with props
            * Takes a callback function that returns whatever component or JSX we want to run

```
// renders a component with props
`<Route path='./unicorns' render={() => <Unicorns todo={myProp} />} />`

// renders JSX
<Route path='/about/' render={() => <h1>About</h1>} />

// render using the match object property params
<Route path='/ideas/:id' render={({ match }) => {
  const idea = ideas.find(idea => idea.id === parseInt(match.params.id));

  if (idea) {
    return <ListItem match={match} {...idea} />;
  }

  return (<div>This idea does not exist!</div>);
}} />
```

        * `children`
            * `<Route path='./unicorns' children={() => <Unicorns todo={myProp} />} />`
            * It works like `render`, except that the callback always gets called whether the path matches or not
            * It's better to render null if the path does not match



        * `Component` supercedes `Render` which supercedes `Children` so be sure to use only one of these props on a given `<Route>`

## _Route Props_

- Objects of information that are passed to the 3 `<Route>` rendering methods

````
*`*`{*`match`*: *`{…}`*, *`location`*: *`{…}`*, *`history`*: *`{…}`*, *`staticContext`*: *`undefined`*}`*`*
`history``:```{`length`:` ``7`,` ``action`:` ``"POP"`,` ``location`:` ``{…}`,` ``createHref`:` `*`ƒ`*,` ``push`:` `*`ƒ`*`, …`}``
`location``:```{`pathname`:` ``"/"`,` ``search`:` ``""`,` ``hash`:` ``""`,` ``state`:` ``undefined`}``
`match``:```{`path`:` ``"/"`,` ``url`:` ``"/"`,` ``isExact`:` ``true`,` ``params`:` ``{…}`}``
`staticContext``:``undefined`
````

- `match`
  - `match({ routes, location, [history], ...options }, cb)`
  - An object that contains information about how a `<Route path>` matched the URL
    - Contains the following properties:
      - `params` - An object with key/value pairs parsed from the URL corresponding to the dynamic segments of the path
        - `path='/unicorns/:5`
        - `match.unicorns.params(5)`
        - allows you to access 5
        - the value is always a string
      - `isExact` - (boolean) `true` if the entire URL was matched (no trailing characters)
      - `path` - (string) The path pattern used to match. Useful for building nested `<Route>`s
      - `url` - (string) The matched portion of the URL. Useful for building nested `<Link>`s
  - You’ll have access `match` objects in various places:
    - Route component as `this.props.match`
    - Route render as `({ match }) => ()`
    - Route children as `({ match }) => ()`
    - withRouter as `this.props.match`
    - matchPath as the return value
  - If a Route does not have a `path`, and therefore always matches, you’ll get the closest parent match
    - Same goes for `withRouter`

```
<Route exact path='/unicorns/:id' render={({ match }) => {
    return <CreatureDetails {...unicornData[match.params.id]} />
  }}
/>
```

- `location`
  - Represents where the app is now, where you want it to go, or where it was
  - The router will provide you with a location object in a few places:
    - Route component as `this.props.location`
    - Route render as `({ location }) => ()`
    - Route children as `({ location }) => ()`
    - withRouter as `this.props.location`
      - If you have a component that is not rendered by a Route, but still needs access to the route props (match/location/history), you will need to use the `withRouter` method provided by React Router
      - This will be necessary to make any of your React Router components (Link, Route, Redirect, Switch, etc.) work correctly
      - Check out [this article](https://hackernoon.com/withrouter-advanced-features-of-react-router-for-single-page-apps-42b2a1a0d315) for more info

* `history`
  - typically have the following properties and methods:
    - `length` - (number) The number of entries in the history stack
    - `action` - (string) The current action (`PUSH`, `REPLACE`, or `POP`)
    - `location` - (object) The current location. May have the following properties:
      - `pathname` - (string) The path of the URL
      - `search` - (string) The URL query string
      - `hash` - (string) The URL hash fragment
      - `state` - (object) location-specific state that was provided to e.g. `push(path, state)` when this location was pushed onto the stack. Only available in browser and memory history.
    - `push(path, [state])` - (function) Pushes a new entry onto the history stack
      - can be used in lou of `<Redirect>`
    - `replace(path, [state])` - (function) Replaces the current entry on the history stack
    - `go(n)` - (function) Moves the pointer in the history stack by `n` entries
    - `goBack()` - (function) Equivalent to `go(-1)`
    - `goForward()` - (function) Equivalent to `go(1)`
    - `block(prompt)` - (function) Prevents navigation

---

# _Link_

- `import { Link } from '`react-router-dom`';`

- Provides declarative, accessible navigation around your application
- Used to create a URL endpoint
- Similar to an `anchor` tag, but instead of an `href=""`, it has a `to=""`

* `<NavLink to**=**'/unicorns' >Unicorns</NavLink>`
* Creates in the HTML
  - `<a href="/unicorns">Unicorn</a>`
* creates in the URL
  - `http://localhost:3000/unicorns`

- Link takes a `to` attribute as well as an optional `replace` attribute
  - `to` tells the app which path to redirect to
  - This can be a string or an object
    - string
      - A string representation of the location to link to, created by concatenating the location’s pathname, search, and hash properties
    - object
      - An object that can have any of the following properties
      - `pathname`: A string representing the path to link to
      - `search`: A string representation of query parameters
      - `hash`: A hash to put in the URL, e.g. `#a-hash`
      - `state`: State to persist to the `location`
    - template literal
      - `to={`/\${category}`}`


    * `replace` is a boolean that when `true` will replace the current entry in the history stack instead of adding a new one
    * Replaces the previous URL with the new URL
        * `<Link to="/my-path" replace />`
    * Example:
        * Having a nested navigation where you want the browser's back button to return to the previous parent URL

- Link can contain an open and closing tag or be a self-closing tag
  - `<Link to='/unicorns' />`
  - `<Link to='/unicorns'>Unicorns</Link>`

---

# _NavLink_

- `import { NavLink } from 'react-router-dom';`

- An extended version of `<Link>` that will add styling attributes to the rendered element when it matches the current URL

* It can take the following attributes:
  - `activeClassName` (string)
    - The class to give the element when it is active
    - The default given class is `active`
    - This will be joined with the `className` prop
  - `activeStyle` (object)
    - The styles to apply to the element when it is active
  - `exact` (bool)
  - `strict` (bool)
  - `isActive` (func)
    - A function to add extra logic for determining whether the link is active
  - `location` (object)
    - The `isActive` compares the current history location (usually the current browser URL)
    - To compare to a different location, a `location` can be passed

- `<NavLink to='/about'>About</NavLink>`

---

# _Redirect_

- `import { Redirect } from 'react-router'`
- `import {`Redirect `} from 'react-router-dom';`

- props to and from are typical uses

- Rendering a `<Redirect />` will navigate to a new location
  - The new location will override the current location in the history stack
    - Like server-side redirects (HTTP 3xx) do

* It can take the following attributes:
  - to: string
  - to: object
  - push: bool
  - from: string

- `<Redirect to='/not/unicorns' />`

```
<Switch>
  <Route exact path='/' component={Home} />
  <Route path='/users/add' component={UserAddPage} />
  <Route path='/users' component={UsersPage} />
  <Redirect to='/' />
</Switch>
```

---

# _Switch_

- `import { Switch } from 'react-router';`
- `import { Switch } from 'react-router-dom';`

- Renders the first child `<Route>` or `<Redirect>` that matches the location
- `<Switch>` is unique in that it renders a route exclusively
  - only one route wins
- In contrast, every `<Route>` that matches the location renders inclusively
  - More than one route can match and render at a time
- Will iterate over its children (routes), and only render the first one that matches the current pathname

* Can be used to conditionally render a <Route>

```
<Switch>
  <Route exact path='/' component={Home} />
  <Route path='/users' component={UsersPage} />
  <Route path="/users/:userid"
    render={({match}) => <h1>Item: {match.params.itemid}</h1>} />
</Switch>
```

---

# _Prompt_

- `import { Router } from 'react-router-dom';`

- Interrupts the Route transition and asks the user a question

---

# _Router_

- `import { Router } from 'react-router';`

---

# _IndexRoute_

- `import { IndexRoute } from 'react-router';`

---

# _browserHistory_``

- `import { browserHistory } from 'react-router';`

---

# _syncHistoryWithStore_

- `import { syncHistoryWithStore } from 'react-router-redux';`

---
