# _React Middlewear_

- Middleware is some code you can put between the framework receiving a request, and the framework generating a response.

- Side effects are anything asychronous in our applications, such as API calls, fetching information for the browser cache or local storage, or logging information to an external service.

---

# _Thunks_

- `npm install --save redux-thunk`
- Middleware provides a 3rd party between dispatching an action and the moment it reaches a reducer
- It basically allows us to hook into the lifecycle of Redux and run some other code between the time an action is dipatched and the time it gets to the reducer
- Works between the action creator and reducer
- Can be used for making loading screens

* In a fetch, we want to account for:

  1. Loading
  2. Error
  3. Data returned successful

- A thunk is just another name for a function
- But it’s not just any old function… it’s a special name for a function that wraps an expression to delay its evaluation
- Let’s take a look at a very basic example of a thunk

```
`const notAThunk = () => {return () => console.log('do stuff now')}`
```

- The Redux way of fetching data, instead of using React

* Thunks are passed 2 arguments:
  - dispatch
  - getState

```
import React from 'react';
import ReactDOM from 'react-dom';
import App from './App';
import './index.css';
import rootReducer from './reducers';
import { Provider } from 'react-redux';
import { createStore, applyMiddleware } from 'redux';
import { composeWithDevTools } from 'redux-devtools-extension';
import thunk from 'redux-thunk';


const store = createStore(rootReducer, composeWithDevTools(applyMiddleware(thunk)))

ReactDOM.render(
  <Provider store={store}>
    <App />
  </Provider>, document.getElementById('root'));
```

---

# _Sagas_

- `npm install --save redux-saga`

* Redux Sagas are another popular middleware for handling side effects in Redux
  - Redux middleware sits right after the dispatch, before the reducer
  - middlewear intercepts the dispatch
* `redux-saga` is a library that aims to make application side effects (asynchronous, things we have to wait for)(i.e. asynchronous things like data fetching and impure things like accessing the browser cache) easier to manage, more efficient to execute, simple to test, and better at handling failures.
* can dispatch actions
* keeps action creators pure
* they use generators

- Terms:
  - takeEvery
  - takeLatest
    - Spawns a `saga` on each action dispatched to the Store that matches a `pattern`
    - Automatically cancels any previous `saga` task started previous if it's still running
    - Can designate another saga to be called
  - call
    - Creates an Effect description that instructs the middleware to call the function `fn` with `args` as arguments.
    - calls a function
  - put
    - Creates an Effect description that instructs the middleware to dispatch an action to the Store.
      - This effect is non-blocking and any errors that are thrown downstream (e.g. in a reducer) will not bubble back into the saga.
    - takes an action
    - a wrapper for dispatch

```
import React from 'react';
import ReactDOM from 'react-dom';
import { createStore, applyMiddleware } from 'redux';
import createSagaMiddleware from 'redux-saga';
import { Provider } from 'react-redux';
import { BrowserRouter } from 'react-router-dom';
import './index.css';
import App from './components/App';
import rootReducer from './reducers';
import registerServiceWorker from './registerServiceWorker';
import listenForSubmitUserLogin from './sagas';

const sagaMiddleware = createSagaMiddleware()

const store = createStore(
  rootReducer,
  window.__REDUX_DEVTOOLS_EXTENSION__ && window.__REDUX_DEVTOOLS_EXTENSION__(),
  applyMiddleware(sagaMiddleware)
)

sagaMiddleware.run(listenForSubmitUserLogin)

const app = <Provider store={store}>
              <BrowserRouter>
                <App />
              </BrowserRouter>
            </Provider>

ReactDOM.render(app, document.getElementById('root'));
registerServiceWorker();
```

```
// index.js
// ------------------------
// basic

import { createStore, applyMiddleware } from 'redux'
import createSagaMiddleware from 'redux-saga'

import rootReducer from './reducers'
import mySaga from './sagas'

// create the saga middleware
const sagaMiddleware = createSagaMiddleware()

// mount it on the Store
const store = createStore(
  rootReducer,
  applyMiddleware(sagaMiddleware)
)

// then run the saga (we haven't learned what mySaga is yet, do worry, we will)
sagaMiddleware.run(mySaga)


// ------------------------
// extended

import React from 'react';
import ReactDOM from 'react-dom';
import { createStore, applyMiddleware } from 'redux';
import { composeWithDevTools } from 'redux-devtools-extension';
import createSagaMiddleware from 'redux-saga';
import { Provider } from 'react-redux';
import { BrowserRouter } from 'react-router-dom';
import './index.css';
import App from './components/App';
import rootReducer from './reducers';
import registerServiceWorker from './registerServiceWorker';
import listenForSubmitUserLogin from './sagas';

const sagaMiddleware = createSagaMiddleware()

const store = createStore(
  rootReducer,
  composeWithDevTools(applyMiddleware(sagaMiddleware))
);

sagaMiddleware.run(listenForSubmitUserLogin)

const app = <Provider store={store}>
              <BrowserRouter>
                <App />
              </BrowserRouter>
            </Provider>

ReactDOM.render(app, document.getElementById('root'));
registerServiceWorker();
```

```
// /sagas/index.js

import { call, put, takeLatest } from 'redux-saga/effects';
import * as API from '../api';
import * as actions from '../actions';

export function* submitUserLogin(action) {
  try {
    const user = yield call(API.postLoginUser, action.email, action.password);
    yield put(actions.loginUser(user));
  } catch (error) {
    yield put(actions.loginError(error.message));
  }
}

export function* listenForSubmitUserLogin() {
  yield takeLatest('SUBMIT_USER_LOGIN', submitUserLogin);
}

export default listenForSubmitUserLogin;
```

---

# _**Devtools extension**_

- `npm install --save-dev redux-devtools-extension`

```
const store = createStore(
  rootReducer,
  composeWithDevTools(applyMiddleware(sagaMiddleware))
);
```

---
