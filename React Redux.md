# _React Redux_

- https://redux.js.org/
- `npm i redux react-redux`

* A single source of truth
* For communication between two components that don't have a parent-child relationship
* Redux offers a solution for storing all your application state in one place, called a "store"

- When to use:
  - If multiple react components will need access to some data, put it in your Redux store
  - If only one component needs access, use the React component state

---

# _Principles_

1. Everything that changes in your app is contained in a single object called a state or state-tree
2. The state-tree is redundant, you can not modify or write to it
3. To change the state, must dispatch an action, which is handled by a reducer

## Cheatsheet

- https://github.com/uanders/react-redux-cheatsheet

---

# _Components_

## _Containers_

- react component that is connected to the Redux store
- use connect to create a container component

## \__Components/\_Presentational_

- doesn't need access to store
- the rest of the app doesn't need access to it's state

---

# _Store_

- Instead of holding our state in components, we store it in a Redux store
  - also called a state tree
  - an object
- Can be thought of as a "middleman of information" for all state changes in the application
- Holds references to the reducers
- Has the dispatch method

```
const store = {

  account: []

}
```

---

# _Actions_

- An object of information containing what happened and what needs to change
- Describes a change to the store
- Sends the new/changed data to the reducer, which updates the store

* consists of two key/value pairs:
  - type:
    - describes what change we want to make
    - name should be all uppercase snake_case
  - payload:
    - additional info reducer will need to alter the store
    - optional

---

# _Action creators_

- Functions that create and return actions
- locate in `actions` folder
- Have an actions file for each reducer
- Don't need to pass in type
- Do need to pass in payload info

```
const deposit = (accNum, amount) => {
  return {
    type: 'DEPOSIT_MONEY',
    accNum,
    amount
  };
};
```

---

# _dispatch_

- Components then "dispatch" state changes to the store, not directly to other components

* a method of Redux

* takes an action from the action creator and sends it to the reducers

- in order to invoke a reducer, you must use dispatch to send action to the reducer
- you dispatch actions
- when you dispatch an action, all of the reducers runs

---

# _Reducers_

- Handles updating the store
- Create a reducer for each key in the store
- Create in a `/reducers/` folder

* A function that takes two arguments:
  - the current state
  - action

- Steps:

1. takes in the existing state and action
2. matches the action type
3. modifies existing state
4. returns the new state

- The reducer listens for a dispatched action, and then it handles the actions
- Everytime an action is dispatched, every reducer will run
  - Must tell each reducer which actions it is interested in

* Consists of a switch statement
  - a case for each action type
  - provide a default initial state
  - each case returns the new state
    - takes in the current state, modifies it, and returns the new state
    - cannot mutate original state
  - always returns a default state:
    - when first ran
    - when an action doesn't match a case

```
const initialState = [];
const accountsReducer = (state = initialState, action) => {
  switch (action.type) {
    case 'DEPOSIT_MONEY':
      return [...state, { amount: action.amount }];
      break;

    default:
      return state;
  }
};
```

## _root reducer_

- `import { combineReducers } from 'redux';`
- Import every other reducer file

- Contains all of the reducers
- Combines all reducers into an object
- Creates the structure (keys) of our store

* Create in `/reducers/index.js`

```
export const rootReducer = combineReducers({
  accounts: accountsReducer
});
```

## Composition

- A reducer gives a subreducer just a slice of the state to manage, and the subreducer knows how to update just that slice
- This is called reducer composition, and it's the fundamental pattern of building Redux apps

```
function postComments(state = [], action) {
  switch (action.type) {
    case 'ADD_COMMENT':
      // return the new state with the new comment
      return [
        ...state,
        {
          user: action.author,
          text: action.comment
        }
      ];
    default:
      return state;
  }
  return state;
}

function comments(state = [], action) {
  if (typeof action.postId !== 'undefined') {
    return {
      // take the current state
      ...state,
      // overwrite this post with a new one
      [action.postId]: postComments(state[action.postId], action)
    };
  }
  return state;
}

export default comments;
```

---

# _Provider_

- `**import** { Provider } **from** 'react-redux';`

* React component
* Typically used in `index.js`

- Gives every child component context (access) to everything in the store
- Creates the keys/structure of our store
- Must wrap entire app
  - including `<BrowserRouter>` if using Router

* `<Provider store={store} />`
  - pass in the context of the store
    - `store={store}`
    - passes data to child components

```
import { Provider } from 'react-redux';
import { createStore } from 'redux';
import rootReducer from './reducers';

const devTools =
  window.__REDUX_DEVTOOLS_EXTENSION__ && window.__REDUX_DEVTOOLS_EXTENSION__();

const store = createStore(rootReducer, devTools);

ReactDOM.render(
  <Provider store={store}>
    <App />
  </Provider>,
  document.getElementById('root')
);
```

---

# _connect_

- `**import** { connect } **from** 'react-redux';`
- injects data at whatever level it is needed
- a higher order function

* for Container components
* a function that returns a function

- instead of exporting a file, we export `connect()`
  - `export default connect`

* `connect(mapStateToProps, mapDispatchToProps)(component)`

- the second call will create a new component giving access to the part of the store defined in mapStateToProps
  - access the key in mapStateToProps using this.props

---

# _mapStateToProps_

- a function that returns an object
- takes in state
- gives our component access to keys in our store
- put in everything from state that the component needs to know about
- if not needed, use null
- can now access this state in the component using this.props

```
const mapStateToProps = state =>
return {
    // key:  root reducer key
    todos: state.todos
}
```

---

# _mapDispatchToProps_

- a function that returns an object
- takes in dispatch
- methods / behavior
- adds an action to props
- if not needed, can omit

```
const mapDispatchToProps = dispatch =>
return {
    // addTodo is an action from an actionCreator in actions.js
    addTodos: (todo) => dispatch(addTodo(todo))
}
```

---

# _createStore_

- `**import** { createStore } **from** 'redux';`

* used to create the Redux store
* use as a property of the `<Provider>` component

* `const store = createStore(rootReducer)`

---

# _combineReducers_

- ` import```` ````{```` combineReducers ````}```` ````from```` ````'redux' `

* used to create a root reducer

---

# _subscribe_

- The components that need to be aware of state changes can "subscribe" to the store

---

# _bindActionCreators_

- `**import** { bindActionCreators } **from** 'redux';`

---

# _compose_

- `**import** { compose } **from** 'redux';`
- Lets you write deeply nested function transformations without the rightward drift of the code

---

# _Redux-dev-tools_

- `npm install --save-dev redux-devtools-extension`
- A Chrome dev tools extension to help us look into what Redux is doing behind the scenes
  - [redux dev tool extension](https://chrome.google.com/webstore/detail/redux-devtools/lmhkpmbekcpmknklioeibfkpmmfibljd)
- If you install the tools and fire them up immediately, you’ll get a helpful error message.
  - `No store found. Make sure to follow the instructions.`
- Here are [the instructions](https://github.com/zalmoxisus/redux-devtools-extension#usage).
- Basically, we need to tell our app to add this extra step as part of the “middleware” of our app. So in between all of the interactions (components –> containers –> actions –> reducers) send the information through these dev tools first to keep us posted.
- For now, we will set up our tools like so:

```
`// src/index.js
// ... IMPORT LINES UP HERE
const devTools = window.__REDUX_DEVTOOLS_EXTENSION__ && window.__REDUX_DEVTOOLS_EXTENSION__()
const store = createStore(rootReducer, devTools);
// ... RENDER DOWN HERE`
```

- With middleware

```
`import { createStore, applyMiddleware } from 'redux';
import { composeWithDevTools } from 'redux-devtools-extension';

const store = createStore(rootReducer, composeWithDevTools(applyMiddleware(thunk)))

// or

`import { createStore, applyMiddleware } from 'redux';
`import createSagaMiddleware from 'redux-saga';

const sagaMiddleware = createSagaMiddleware()
`const store = createStore(rootReducer, composeWithDevTools(applyMiddleware(sagaMiddleware)))
``
```

---

# _Hot reloading_

- Add to file where you created the store (`createStore()`)

```
if (module.hot) {
  module.hot.accept('./reducers/', () => {
    const nextRootReducer = require('./reducers/index').default;
    store.replaceReducer(nextRootReducer);
  });
}
```

---

# _Libaries_

- https://github.com/reduxjs/redux-starter-kit

---
