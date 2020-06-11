# _React_

- http://babeljs.io/repl/
- https://reactjs.org/docs/
- https://devhints.io/react

* Import the react library using `import React from 'react';`

---

# _JSX_

- _JSX_ is a syntax extension for JavaScript. It was written to be used with React. JSX code looks a lot like HTML
- Allows us to write XML in our JavaScript
- To write Javascript in our JSX, we put it in curly braces `{}`
- You must include the slash `/` for self-closing tags
- Functions only return a single value, so you can only return one element
  - multiple elements are wrapped in a single `<div>`
- If a JSX expression takes up more than one line, then you must wrap it in parentheses so that JavaScript doesn’t insert a semicolon after `return` and break our code

```
function ButtonAndLabel () {
  let myFavoriteNumber = 2 + 2;

  return (
    <div>
      <label>My Favorite Number is { myFavoriteNumber }</label>
      <button> Click Me </button>
    </div>
  )
}
```

---

# _React DOM_

- `ReactDOM` contains several React-specific methods, all of which deal with [the DOM](http://www.w3schools.com/js/js_htmldom.asp)
- ` import`` ``ReactDOM`` ``from`` ``'react-dom'``; `

## Methods

- `ReactDOM.render()`
  - `ReactDOM.render(<App />, document.getElementById('root'));`
  - The most common way to render JSX
  - It takes a JSX expression, creates a corresponding tree of DOM nodes, and adds that tree to the DOM
  - The first argument passed to `render()` should evaluate to a JSX expression
  - The first argument is appended to whatever element is selected by the second argument
  - Only updates DOM elements that have changed
    - If you render the exact same thing twice in a row, the second render will do nothing

---

# _Components_

- https://reactjs.org/docs/react-component.html
- JS constructor functions that compile our JSX and return HTML
- Blueprints for HTML
- Components tell React what to render
- JSX elements can be either HTML-like, or component instances
  - JSX uses capitalization to distinguish between the two
- React components render in parallel
  - There is no guarantee what order that they finish rendering

## **Functional components**

- A function
- Stateless
- returns JSX based on data passed in through props
- Only consist of a `return` method

## Class components

- A factory that builds components
- Use when:
  - keep track of data
  - use lifecycle methods

```
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    this.state = { /* initial state */ };
  }
}
```

- Must include render() method with a return statement
- React components always have to call `super()` in their constructors to be set up properly
  - `super()` calls the parent components constructor (the component it extends)
    - If React, it gives the component access the React.Component `this`
- If stateless, you can omit the constructor. React will add a default constructor automatically
- Must pass in props in constructor and super only if you need to use props

```
class MyComponentClass extends React.Component {
  render() {
    return <h1>Hello world</h1>;
  }
}
```

- `React.Component`
  - every component must come from a component class
    - `React.Component` is a JavaScript class. To create your own component class, you must subclass `React.Component`

### ES5

```
var MyComponent = React.createClass({
  getInitialState() {
    return { /* initial state */ };
  },
});
```

### Misc

- ES5 functions are on a class are methods
- ES6 functions on a class are properties
- The `contructor()` is optional
  - It will be included on compile
  - You can still you state as usual with `this.state = {}`

## Component Instance

- To make a React component, write a JSX element using the same name as the component
  - Make sure to import the module
  - ` <``MyComponent`` ``/> `

## Controlled component

- A component that does not maintain any internal state

## Uncontrolled component

- A component that maintains its own internal state

## Container components

- Any component that is not presentational
- Does the work of figuring out what to display
- A component shouldn't render HTML-like JSX if:
  - it has `state`
  - makes calculations based on `props`
  - manages any other complex logic
- Instead, a container should render another component that renders HTML-like JSX
- This pattern separates your business logic from your presentational logic
- Typically placed in a `/containers/` folder

* A container does data fetching and then renders its corresponding sub-component. That’s it.
  - “Corresponding” meaning a component that shares the same name:
    - StockWidgetContainer => **StockWidget**
    - TagCloudContainer => **TagCloud**
    - PartyPooperListContainer => **PartyPooperList**

## Presentational components

- Does the work of actually displaying it
- Its only job is to render HTML-like JSX
- Typically placed in a `/components/` folder

* In general, functions should be outside of components whenever possible because every time a component renders, it creates the function over again.

## Higher Order Components

- A function that receives a regular component, and wraps it with a new component with additional logic/data
  - Such as pulling data out of the context object and passing it to the original component
- Example of a generic HOC that will take any component and pass the context object it:

```
// functional component
import React from 'react';
import PropTypes from 'prop-types';

const storeProvider = Component => {
  const WithStore = (props, context) => {
    return <Component {...props} store={context.store} />;
  };

  WithStore.contextTypes = {
    store: PropTypes.object
  };

  WithStore.displayName = `${Component.name}Container`;

  return WithStore;
};

export default storeProvider;
```

```
// class component
import React, { Component } from 'react';
import PropTypes from 'prop-types';

const storeProvider = OriginalComponent => {
  return class extends Component {
    static displayName = `${OriginalComponent.name}Container`;
    static contextTypes = {
      store: PropTypes.object
    };

    render() {
      return <OriginalComponent {...this.props} store={this.context.store} />;
    }
  };
};

export default storeProvider;
```

---

# _Props_

- A component's `props` is an object
- It holds information passed to that component
- Allows you to pass custom attribute values into instances of components
- Used to pass data down to child components
- `props` is the name of the object that stores passed-in information
- Is immutable, a component should never modify its props

* Pass information to a component by giving that component an attribute
  - `<Greeting name="Frarthur" town="Flundon" age={2} haunted={false} />`
* Access and display a passed-in prop
  - `render() { return <h1>{this.props.name}</h1>; }`

```
// Creates a tic-tac-toe board

class Square extends React.Component {
  render() {
    return (
      <button className="square">
        {this.props.value}
      </button>
    );
  }
}

class Board extends React.Component {
  renderSquare(i) {
    return <Square value={i}/>;
  }

  render() {
    return (
      <div>
        <div className="board-row">
          {this.renderSquare(0)}
          {this.renderSquare(1)}
          {this.renderSquare(2)}
        </div>
        <div className="board-row">
          {this.renderSquare(3)}
          {this.renderSquare(4)}
          {this.renderSquare(5)}
        </div>
        <div className="board-row">
          {this.renderSquare(6)}
          {this.renderSquare(7)}
          {this.renderSquare(8)}
        </div>
      </div>
    );
  }
}
```

```
// Renders the DOM as:

<div>
  <div class="board-row">
    <button class="square">0</button>
    <button class="square">1</button>
    <button class="square">2</button>
  </div>
  <div class="board-row">
    <button class="square">3</button>
    <button class="square">4</button>
    <button class="square">5</button>
  </div>
  <div class="board-row">
    <button class="square">6</button>
    <button class="square">7</button>
    <button class="square">8</button>
  </div>
</div>
```

## `this.props`

- refers to the props storage object

## `this.props.children`

- Every component's `props` object has a property named `children`
- Returns everything in between a component's opening and closing JSX tags

## `defaultProps`

- Provides default values for props
- Should be equal to an object
- Allows you to specify a default (or a backup) value for certain props just in case those props are never passed into the component.
- `defaultProps` will be used to ensure that `this.props.text` will have a value if it was not specified by the parent component
-

```
`class MyClass extends React {
}
MyClass.defaultProps = { text: 'default text' };`
```

## Render Props

- https://reactjs.org/docs/render-props.html
- A technique for sharing code between React components using a prop whose value is a function
- A component with a render prop takes a function that returns a React element and calls it instead of implementing its own render logic

```
<DataProvider render={data => (
  <h1>Hello {data.target}</h1>
)}/>
```

---

# _State_

- State vs Stateless

  - Stateful - keeps track of data that can be manipulated
    - State is needed if data will change over the life of a component
    - Must use ES6 classes
    - export class MyComponentClass extends React.Component {
      constructor(props) {
      super(props)
            this.state = {}
          }
          render() {
            return <h1>{this.props.title}</h1>;
          }
      }
  - Stateless - just renders to the DOM
    - Can use regular functions
    - export const MyComponentClass = (props) => {
      return <h1>{props.title}</h1>;
      }

- React components can have state by setting `this.state` in the constructor
- `state` is similar to `props`, but it is private and fully controlled by the component
- Must create a class that extends the `Component` method of `React`
  - Class components should always call the base constructor and super with `props`
  - This lets us use additional features such as local state and lifecycle hooks
  - ?? If you don’t use something in `render()`, it shouldn’t be in the state
- Never mutate the state
  - Make a copy of the current state
  - Add, change, remove data of the copy
  - Then set the new modified copy into state
  - Dont:

```
fakeArticle = {
  id: '123',
  text: 'fake article'
  };

articles[fakeArticle.id] = fakeArticle
```

    * Do:

```
fakeArticle = {
  id: '123',
  article: 'fake article'
};

updatedArticles = {
  ...this.articles,
  [this.fakeArticle.id]: this.fakeArticle
};
```

- `this.state` should always have an object value

```
class Clock extends React.Component {
  constructor(props) {
    super(props);
    this.state = {date: new Date()};
  }
```

- When you want to aggregate data from multiple children or to have two child components communicate with each other, move the state upwards so that it lives in the parent component
- The parent can then pass the state back down to the children via props, so that the child components are always in sync with each other and with the parent

## `setState()`

- A method of the Component class
- Updates state which triggers a re-render
- When you call `setState()`, React merges the object you provide into the current state
- Do Not Modify State Directly
  - The only place where you can assign `this.state` is the constructor
- `setState` is an asynchronous function
- State updates may be asynchronous
  - React may batch multiple `setState()` calls into a single update for performance
  - It does not always immediately update the component
  - It may batch or defer the update until later
- Takes two arguments:
  - An object that will update the component's state
  - An optional callback that is guaranteed to fire after the update has been applied

```
this.setState(
  { someFlag: true },
  () => (this.state.someFlag ? console.log('isTrue') : console.log('isFalse'))
); // 'isTrue'
```

- Never set state in render, it will create an infinite loop
- The DOM is not updated as soon as `setState` is invoked

  - Rather, React batches multiple updates into one update and then renders the DOM
  - You may receive outdated values while querying the `state` object

- Never mutate state
  - Always make a copy of the existing state, update the new object, then set the new object in state
- You can also pass a function to `setState` which receives `prevState` and `props` as arguments
  - Use only when a state update requires the previous state
  - The return value of this function is merged in with the existing state to form the new state

```
this.setState((prevState, props) => ({
  counter: prevState.counter + props.increment
}));
```

```
// no
this.setState({correctData: !this.state.correctData});

// yes
this.setState((prevState, props) => ({
  correctData: !prevState.correctData
}));
```

---

# _Lifecycle Methods_

- In applications with many components, it’s important to free up resources taken by the components when they are destroyed
- We can declare special methods on the component class to run some code when a component mounts and unmounts
- These methods are called “lifecycle hooks”

## Props/State Updating

1. Which lifecycle methods fire:
   1. `componentWillReceiveProps()`
   2. `shouldComponentUpdate()`
   3. `componentWillUpdate()`
   4. `render()`
   5. `componentDidUpdate()`
2. Can I set state in each method?
   1. all except for render(), component
3. What arguments does each lifecycle method take?
   1. `componentWillReceiveProps()`
      1. next props
   2. render
      1. none
   3. `componentDidUpdate()`
      1. nextprops and next state
4. What happens if I don't define a given lifecycle method
   1. they all have default behavior
5. How to test?
   1. must use mount in your tests to test lifecycle method

## Phase 1: Mounting

- A component "mounts" when it renders for the first time
- Mounting lifecycle events only execute the first time that a component renders
- When a component mounts, it automatically calls these methods, in order:

1. `constructor()`
2. `componentWillMount()`
   1. deprecated
3. `static getDerivedStateFromProps()`
   1. after a component is instantiated
   2. returns an object that state will be updated with
   3. when the component receives new props
   4. moves the state along
   5. common use case is UI changes based on prop changes
   6. does not have access to `this`
4. `render()`
5. `componentDidMount()`
   1. Runs after the component, and all child components, has been rendered to the DOM
   2. Good for retrieving data that doesn't update instantly

## Phase 2: Updating

- A component updates when there are changes to the `props` or `state`
- When a component updates, it automatically calls these methods, in order:

1. `componentWillReceiveProps()`
   1. deprecated
   2. Only gets called if the component will receive `props`
   3. Automatically gets passed one argument: an object called `nextProps`
      1. `nextProps` is a preview of the upcoming `props` object that the component is about to receive
   4. Gets the new props before `render`, so you can use them before the component is rendered

```

componentWillReceiveProps(nextProps) {
  console.log(nextProps);
}
```

```
// componentWillReceiveProps will get called here:
ReactDOM.render(
  <Example prop="myVal" />,
  document.getElementById('app')
);

// componentWillReceiveProps will NOT get called here:
ReactDOM.render(
  <Example />,
  document.getElementById('app')
);
```

1. `shouldComponentUpdate(nextProps, nextState)`
   1. Must return true or false
      1. If `true`, component will continue to mount as normal
      2. If `false`, the component will not update
         1. None of the remaining lifecycle methods for that updating period will be called, including `render`
   2. Use by having it return `false` only under certain conditions
      1. If those conditions are met, then your component will not update
   3. Use when a component doesn't need to re-render
      1. Such as when none of the props or states have changed
   4. Should have a default case
   5. Automatically receives two arguments: `nextProps` and `nextState`
   6. It's typical to compare `nextProps` and `nextState` to the current `this.props` and `this.state`, and use the results to decide what to do

```
shouldComponentUpdate(nextProps, nextState) {
    return this.props.number !== nextProps.number;
}

shouldComponentUpdate(nextProps, nextState) {
  if ((this.props.text === nextProps.text) &&
    (this.state.subtext === nextState.subtext)) {
    return false; // won't update
  } else {
    return true;  // will update
  }
}
```

1. `componentWillUpdate()`
   1. Will be deprecated with React 17
   2. Automatically receives two arguments: `nextProps` and `nextState`
   3. Cannot be used to call `this.setState`
   4. ? Use when you want to use a previous prop or state
   5. The main purpose is to interact with things outside of the React architecture
      1. If you need to do non-React setup before a component renders
         1. Such as checking the `window` size or interacting with an API
2. `render()`
   1. renders JSX to the DOM
3. `getSnapshotBeforeUpdate()`
4. `componentDidUpdate(prevProps, prevState)`
   1. Gets called after any rendered HTML has finished loading
   2. Automatically receives two arguments: `prevProps` and `prevState`
      1. They are references to the component's `props` and `state` before the current updating period
      2. You can compare them to the current `props` and `state`
   3. Can be used to run a function every time the `props` or `state` change
   4. Usually used for interacting with things outside of the React environment, like the browser or APIs

## Phase 3: Unmounting

- The unmounting period occurs just before a component is removed from the DOM
- This could happen if:

  - the DOM is rerendered without the component
  - the user navigates to a different website
  - the user closes their web browser

- When a component unmounts, it automatically calls this method:
  - `componentWillUnmount()`
    - Automatically receives two arguments: `prevProps` and `prevState`
    - Use if a component initiates any functions that require cleanup after it is unmounted
      - For example, API calls that stream data

## Error Handling

1. `componentDidCatch(error, info)`
   1. Called when there is an error:
      1. during rendering
      2. in a lifecycle method
      3. in the constructor of any child component
   2. A class component becomes an error boundary if it defines this lifecycle method
      1. will prevent the error from bubbling up to parents
   3. can be used to send errors to an external service
      1. good to have in App.js

---

# _Virtual Dom_

- An in-memory object that represents a DOM structure and can be manipulated with JavaScript before updating the real DOM

---

# _Controlled Forms_

- Controlled components have functions to govern the data going into them on every `onChange` event
  - rather than grabbing the data only once, e.g. when a user clicks a submit button. This 'governed' data is then saved to state
- You want to update the server any time a user enters or deletes any character
- Data displayed by a controlled component is received through props passed down from it's parent/container component
- In a controlled form, the value is always going to come from the state

```
export class Input extends React.Component {
  constructor(props) {
    super(props);

    this.state = { userInput: '' };
  }

  handleUserInput = (e) => {
    this.setState({userInput: e.target.value});
  }

  render() {
    return (
      <div>
        <input type="text"
          onChange={this.handleUserInput}
          value={this.state.userInput}
        />
        <h1>{this.state.userInput}</h1>
      </div>
    );
  }
}
```

---

# _Styles_

- Style property names are written in camelCase, not kebab-case

## className

- Define CSS rules in a stylesheet
- Import stylesheet to component
  - `import './App.css';`
- Apply styles using `className`
  - ` <h1 className='heading'``>Hello world</h1> `

## Inline

- `<h1 style={{ color: 'red' }}>Hello world</h1>`

## Object

- Add a prop of `style` to a component or tag, passing in the styles object
- Define a variable named `styles` in the top-level scope
- `<MyComponent style={styles} />`

```
const styles = {`
    color: 'darkcyan',
    background: 'mintcream'
}`
```

- `<article style**=**{styles.article}></`article`>`

```
const styles = {
  article: {
    paddingTop: 10,
    paddingBottom: 10
  }
};
```

---

# _History_

---

# _Fragments_

- https://reactjs.org/docs/fragments.html
- Fragments let you group a list of children without adding extra nodes to the DOM
- Use instead of dummy `<div>`s

```
import React, { Component, Fragment } from 'react';

class Columns extends Component {
  render() {
    return (
      <Fragment>
        <td>Hello</td>
        <td>World</td>
      </Fragment>
    );
  }
}
```

- short syntax

```
class Columns extends Component {
  render() {
    return (
      <>
        <td>Hello</td>
        <td>World</td>
      </>
    );
  }
}
```

---

# _Context API_

- If we pass a function down to a child component, through a middle child component, it introduces unnecessary code because the middle component doesn't need to use that function
- A solution is to make the function a global variable, while associating the function with the instance of the App
- This is what the Context API does

* Create a function called `getChildContext()` in the `App` component
  - The return value is the context object
* Define a context type for each property of the context object using Proptypes

```
static childContextTypes = {
  store: PropTypes.object
};
getChildContext() {
  return {
    store: this.props.store
  };
}
```

- The context object will be available to every component that defines the context type in it

```
Article.contextTypes = {
  store: PropTypes.object
};
```

- Class components access using `this.context.store`
- A functional component can access the context using the optional second argument
  - defining contextType no longer necessary

```
const Article = (props, context) => {
  const store = context.store;
}
```

---

# _Refs_

- Provides a way to access DOM nodes or React elements created in the render method

* There are a few good use cases for refs:
  - Managing focus, text selection, or media playback
  - Triggering imperative animations
  - Integrating with third-party DOM libraries

```
class AutoFocusTextInput extends React.Component {
  constructor(props) {
    super(props);
    this.textInput = React.createRef();
  }

  componentDidMount() {
    this.textInput.current.focus();
  }

  render() {
    return (
      <input ref={this.textInput} />
    );
  }
}
```

---

# _PropTypes_

- https://reactjs.org/docs/typechecking-with-proptypes.html
- Runtime type checking for React props and similar objects
- `npm i --save prop-types`
- `import` `PropTypes` `from` ``'`prop-types`'``;``
- Allows you to specify what type of props you are expecting in a certain component
  - This is known as “typechecking”
- Checks if props are passed in and as the type you're expecting

```
myComponent.propTypes = {
    propName1: PropTypes.string,
    propName2: PropTypes.number,
    propName3: PropTypes.object,
    propName4: PropTypes.array,
    propName5: PropTypes.bool,
    propName6: PropTypes.func,
    propName7: PropTypes.symbol,
    propName8: PropTypes.any,

    // You can ensure that your prop is limited to specific values by treating
    // it as an enum.
    optionalEnum: PropTypes.oneOf(['News', 'Photos']),

    // An object that could be one of many types
    optionalUnion: PropTypes.oneOfType([
        PropTypes.string,
        PropTypes.number,
        PropTypes.instanceOf(Message)
    ]),

    // An array of a certain type
    // checks each element of an array
    optionalArrayOf: PropTypes.arrayOf(PropTypes.number),

    // An object with property values of a certain type
    // checks the value of each key
    optionalObjectOf: PropTypes.objectOf(PropTypes.number),

    // An object taking on a particular shape (keys)
    optionalObjectWithShape: PropTypes.shape({
        color: PropTypes.string,
        fontSize: PropTypes.number
    }),
};
```

- `.isRequired`
  - imposes stricter guidelines
  - will log a console warning if a `prop` isn't sent
- Place before export default

---

# _Keys_

- A `key` is a JSX attribute
- The attribute's name is `key`
- The attribute's value should be something unique, similar to an `id` attribute
- React uses `keys` internally to keep track of lists
- If you don't use keys when you're supposed to, React might accidentally scramble your list-items into the wrong order
- You can use an arrays index as the key
  - ` key``=``{``'person_'`` ``+`` ``index``} `

* A list needs `keys` if either of the following are true:
  - The list-items have memory from one render to the next
    - For instance, when a to-do list renders, each item must "remember" whether it was checked off
    - The items shouldn't get amnesia when they render
  - A list's order might be shuffled
    - For instance, a list of search results might be shuffled from one render to the next

- Any key that you are going to use should be:
  - **Unique** — The key of an element should be unique among its siblings. It is not necessary to have globally unique keys
  - **Stable** — The key for the same element should not change with time, or page refresh, or re-ordering of elements
  - **Predictable** — You can always get the same key again if you want. That is, the key should not be generated randomly

* In general, you should rely on the ID generated by databases such as primary key in Relational databases, and Object IDs in Mongo. If a database ID is not available, you can generate a hash of the content and use that as a key

---

# _Conditionals_

- You can not inject an `if` statement into a JSX expression
- Put JSX inside the conditional
- `if` statements must be located inside of the render function
- `if` statements cannot be in return statements, but return statements can be inside `if` statements

```
let message;

if (user.age >= drinkingAge) {
  message = (
    <h1>
      Hey, check out this alcoholic beverage!
    </h1>
  );
} else {
  message = (
    <h1>
      Hey, check out these earrings I got at Claire's!
    </h1>
  );
}

ReactDOM.render(
  message,
  document.getElementById('app')
);
```

- The ternary operator is used often in React

```
const headline = (
  <h1>
    { age >= drinkingAge ? 'Buy Drink' : 'Do Teen Stuff' }
  </h1>
);
```

- `&&` operator
  - Works best in conditionals that will sometimes do an action, but other times do nothing at all
  - If the left side is true, will do the right side

```
const tasty = (
  <ul>
    <li>Applesauce</li>
    { !baby && <li>Pizza</li> }
    { age > 15 && <li>Brussels Sprouts</li> }
    { age > 20 && <li>Oysters</li> }
    { age > 25 && <li>Grappa</li> }
  </ul>
);
```

---

# _This_

- `this` refers to the object on which `this`'s enclosing method, in this case `.render()` is called
- `this` is uninitialized if `super()` is not called
- When you write a component class method that uses `this`, then you need to bind that method

  - can be done inside of your constructor function
    - `this.myMethod = this.myMethod.bind(this);`
  - or just make your methods arrow functions
  - use for 2 reasons:

    1. to save memory so it's not binding everytime the method is called
    2. changing context to refer to the correct component, i.e. the parent component

---

# _Event Listeners_

- Define event handlers as methods on a component class
- Assign an event listener by giving a JSX element a prop
- ` <``img`` ``onClick``=``{myFunc}`` ``/> `
- An event listener attribute's value should be a function
- List of valid event names:
  - https://reactjs.org/docs/events.html#supported-events
- Naming convention
  - For a "click" event, name the event handler `handleClick`
  - For a "keyPress" event, name the event handler `handleKeyPress`
  - The prop name should be the word `on`, plus the event type

---

# _Server-side rendering_

- Search engines index websites with JavaScript disabled???
- This problem can be fixed by rendering the same app that's on the client, on the server as well
  - Allows the website to load even with JavaScript disabled
- Provides performance optimization because if the browser/client already has a copy of the app that matches the server, then React will do nothing
  - The app is pre-rendered on the server sent to the client as HTML
- Must ensure that the client-side and server-side apps are rendered with the same data
  - Have the initial data fetched by the server and exposed to the client-side as a global variable on the window

---

# _PureComponent_

- https://codeburst.io/when-to-use-component-or-purecomponent-a60cfad01a81
- https://medium.com/front-end-weekly/using-a-purecomponent-in-reacts-262972f9f1e0
- `PureComponent` is similar to `Component`
- The difference between them is that `Component` doesn’t implement `shouldComponentUpdate()`, but `PureComponent` implements it with a shallow prop and state comparison
- Gives a considerable increase in performance because it reduces the number of render operation in the application
- When props or state changes, `PureComponent` will do a shallow comparison on both props and state
  - If you are updating an object with nested values the component will not re-render as React has not noticed a change
  - Compares primitive values like numbers and strings
  - When comparing objects it compares only references
  - Changes inside `props` or `state` will be ignored
- Will always re-render if the state or props reference a new object
  - Create a new copy of the state, then update it and set it
- Skips prop updates for the whole component subtree
  - Make sure all the children components are also “pure”
- Only extend `PureComponent` when you expect to have simple props and state, or use `forceUpdate()` when you know deep data structures have changed
- Use `PureComponent` when you can satisfy any of the below conditions:
  - State/Props should be an immutable object
  - State/Props should not have a hierarchy
  - You should call `forceUpdate()` when data changes

---

# _File Structure_

- Mantra
  - https://medium.com/wertarbyte/structure-your-react-apps-the-mantra-way-3a831ffd1580

---

# _Optimization_

- https://houssein.me/progressive-react

## Lifecycle methods

- Use should
- Use `componentDidUpdate` to see what and when components update

```
componentDidUpdate = (nextProps, nextState) => {
  console.log('Component Updated');
};
```

## React DevTools

- React DevTools has an option under Preferences called Hightlight Updates which flashes a border on any component that updates
  - The color of the border is based on the frequency of the updates
- Profiler
  - https://reactjs.org/blog/2018/09/10/introducing-the-react-profiler.html

## Chrome DevTools

- https://reactjs.org/docs/optimizing-performance.html#profiling-components-with-the-chrome-performance-tab
- https://building.calibreapp.com/debugging-react-performance-with-react-16-and-chrome-devtools-c90698a522ad
- Append `?react_perf` to the to view a special report showing the performance of every component mount and unmount
  - `http://localhost:8080/?react_perf`
- Under the Performance tab, expand the User Timing arrow

## why-did-you-update

- https://github.com/maicki/why-did-you-update
- `npm install --save why-did-you-update`
- `import whyDidYouUpdate from 'why-did-you-update';`
- `whyDidYouUpdate(React);`

## Props

- Should only pass the exact data to a component that it needs in order to prevent wasteful rerenders when data changes that's not being used

## PureComponent

- Use `PureComponent` unless you can't
- Functional components are dumb and may re-render even with the props or state change
  - Change to a `PureComponent` if possible

## Debounce

- Wrap functions that execute many times in quick succession in a debounce function
- Such as only executing a find every 300ms instead of after each letter is typed in a search input

---

# _Misc_

- https://reactpatterns.com/

* It is convention in React apps to use `on*` names for the attributes and `handle*` for the handler methods

## Inheritance vs. Composition

- https://reactjs.org/docs/composition-vs-inheritance.html
- https://www.codementor.io/imbhargav5/extending-react-components-inheritance-composition-qo59dqili
- Inheritance
  - Allows one class to inherit another class's properties to duplicate behavior and add more features
- Composition
  - Allows us to combine one or more components into a newer, enhanced component capable of greater behavior
  - Recommended

## Immutability

- Easier Undo/Redo and Time Travel
- Tracking Changes
- Determining When to Re-render in React

## Fetching data

- You have to fetch data somewhere... no matter where, you will have to setState and trigger a re-render
- Therefore, data should be fetched in the component it is being used in, or the closest ancestor of the components sharing the fetched data
- You do this to prevent the re-render of components that do not require the fetched data

## Console

- typing `$r` in the console will return the `this` of the selected element

---

- `className`
  - In JSX, you can't use the word `class`. You have to use `className` instead
  - This is because JSX gets translated into JavaScript, and `class` is a reserved word in JavaScript

* `render()`
  - A component takes in parameters, called `props`, and returns a hierarchy of views to display via the `render` method
  - The `render` method returns a description of what you want to render, and then React takes that description and renders it to the screen
  - used with classes

- `return ()`

* `React.Component`

- ` import`` ``React`` ``from`` ``'react'``; `
  - creates a new variable named `React`, and its value is a particular, imported JavaScript object
  - This imported object contains methods that you need in order to use React. The object is called the React _library._

* `React.createElement()`
  - write React code without using JSX
  - Every JSX element is secretly a call to `React.createElement()`
  - when a JSX element is _compiled_, it transforms into a `React.createElement()` call

```
// The following JSX expression:
const h1 = <h1>Hello world</h1>;

// can be rewritten without JSX, like this:
const h1 = React.createElement(
  "h1",
  null,
  "Hello, world"
);
```

- Data (and functions) down, Actions up

---
