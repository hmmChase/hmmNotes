# _Testing_

- A test is code that throws an error when the actual result of something does not match the expected output

---

- Set up some state, perform some action, and then make an assertion on the new state
- Helps ensure existing code doesn't break when making changes

- There are four crucial pieces of a test:

  1. Setup
     1. setup the conditions required to execute the action on your SUT
        1. mock your inputs
           1. what the execution dependent on
           2. anything thats going to change the outputs
        2. mock your outputs
           1. what the execution results in
           2. what the function produces
  2. Execution
     1. execute some action on your SUT
  3. Assertion
     1. assert that the action you did had the results you expect
  4. Tear Down
     1. optional as needed

* Don't test code you didn't write
  - frameworks, libraries, built-in functions

- Test happy paths
- Test sad paths
- Think of tests as examples of how the code should work

* Test interfaces
  - how you interact with something

- Basic test:

```
`const actual = true
const expected = false
if (actual !== expected) {
  throw new Error('${actual} is not ${expected}')
}`
```

---

# _Types_

- unit
  - Tests individual units (modules, functions, classes) in isolation from the rest of the program
  - Units are tested using only the public interface of the unit
    - This is referred to as black box testing
  - detects simple problems
  - cheap and quick
- integration
  - Builds on unit tests by combining the units of code and testing that the resulting combination functions correctly
  - Testing functions with side-effect behavior
  - tests 2 unit tests working together
  - detects medium problems
  - doesn't mock anything
- end-to-end
  - tests whole system
  - detects big problems
  - slow and expensive
  - automate clicking through the whole app
  - cypress/puppeteer
- functional
  - Tests the application from the point of view of the user
  - Tests complete user interaction workflows from simulated UI manipulation, to data layer updates, and back to the user output (e.g., the on-screen representation of the app)
  - Functional tests are a subset of integration tests, because they test all of the units of an application, integrated in the context of the running application
- acceptance
  - Performing tests on the full system
  - Client facing tests
  - test features
-
- regression
- stress
- performance
- penetration
- a11y
- i182

---

# _Mocks_

- Mock
  - A test double that stands in for real implementation code during the unit testing process
  - A mock is capable of producing assertions about how it was manipulated by the test subject during the test run
  - Used to isolate test subjects by replacing dependencies with objects that you can control and inspect
- Monkey patching
  - Replacing a function/method/class by another at runtime, for testing purpses, fixing a bug or otherwise changing behaviour
  - In a unit test, you don't want to depend on external data sources, so you replace the function with a stub that returns some fixed data
- Mock functions
  - Also known as "spies"
  - They let you spy on the behavior of a function that is called indirectly by some other code, rather than just testing the output
- Manual mocks
  - Manual mocks are used to stub out functionality with mock data
  - For example, instead of accessing a remote resource like a website or a database, you might want to create a manual mock that allows you to use fake data
  - This ensures your tests will be fast and not flaky

* Things to mock:
  - required inputs
    - any arguments
    - any functions inside the function
  - the expected result of whatever we pass into the expect function

---

- Jest
  - testing framework
    - test runner
    - assertion library
    - mocking utilities
- Mocha
  - testing framework
    - test runner
    - does not include and assertion library
- Enzyme
  - testing utility
    - used to test rendering React components
- Chai
  - assertion library

## _Examples_

### LocalStorage

- Define in `package.json`

```
"jest": {
  "setupfiles": [
    "./src/__mocks__/storageMock.js"
  ]
},
```

- `storageMock.js`
- can also just put this code in `setupTests.js`
  - Must do it this way with CRA

```
global.localStorage = {
  setItem(key, string) {
    global.localStorage[key] = string;
  },
  getItem(key) {
    return global.localStorage[key] || null;
  },
  removeItem(key) {
    delete global.localStorage[key];
  },
  clear() {
    global.localStorage = {};
  }
};
```

```
export class LocalStorageMock {
  constructor() {
    this.store = {};
  }

  setItem(key, value) {
    this.store[key] = value.toString();
  }

  getItem(key) {
    return this.store[key] || null;
  }

  removeItem(key) {
    delete this.store[key];
  }

  clear() {
    this.store = {};
  }
}
```

### preventDefault

- `const mockEvent = { preventDefault: jest.fn() }`

---

# _Mocha_

- A testing framework that runs on Node.js in your terminal, and can also be run in your browser window
- Must be installed globally and locally
- `npm install --global mocha`
- `npm install --save-dev mocha`

```
"scripts": {
  "test": "NODE_ENV=test mocha --exit"
 }
```

## _Hooks_

```
before(function() {
    // runs before all tests in this block
});
```

```
after(function() {
    // runs after all tests in this block
});
```

```
beforeEach(function() {
    // runs before each test in this block
});
```

```
afterEach(function() {
    // runs after each test in this block
});
```

---

# _Chai_

- `npm install` --save-dev`chai`
- Checks that when certain pieces of are code are executed, what we’re getting back is what we expect
- Has 3 methods:
  - Should
  - Expect
  - Assert

* Example: (the “assertion” piece is the part in bold)
  - “After I create a new instance of a unicorn, the unicorn should have a name”
  - “After I create a new instance of a unicorn, and tell it to sing, the unicorn should return a string of text from a song”
  - “After I create a new instance of a unicorn, and the unicorn eats three times, the unicorn should have 300 calories”

```

Import Chai and the assert library, at the top of your test file:
const chai = require('chai');
const assert = chai.assert;
- or -
const { assert } = require(‘chai');
```

- Also export module at the end of your working file:

  - `module.exports = Name;`

## _Chai HTTP_

- http://www.chaijs.com/plugins/chai-http/
- HTTP integration testing with Chai assertions
- `npm install chai-http --save-dev`

```
chaiHttp = require('chai-http');

chai.use(chaiHttp);
```

---

# _Jest_

- https://facebook.github.io/jest/
- https://github.com/facebook/jest/blob/master/docs/Configuration.md
- `npm install --save-dev jest`

* Automatically finds tests
  - Files with `.test.js` suffix
  - Files with `.spec.js` suffix
  - Files with `.js` suffix inside a folder named `__tests__`
* Built on top of [Jasmine](http://jasmine.github.io/)

## _Hooks_

```
beforeEach(function() {
    // runs before each test in this block
});
```

```
afterEach(function() {
    // runs after each test in this block
});
```

```
beforeAll(function() {
    // runs before all tests in this block
});
```

```
afterAll(function() {
    // runs after all tests in this block
});
```

## _Mock functions_

- `jest.fn(implementation)`
  - Creates a mock function
  - Provides features to:
    - Capture calls
    - Set return values
    - Change the implementation
  - If no implementation is given, the mock function will return `undefined` when invoked

```
`getWinner = jest.fn((p1, p2) => p2);`
```

```
// test the captured calls

test("returns undefined by default", () => {
  const mock = jest.fn();

  let result = mock("foo");

  expect(result).toBeUndefined();
  expect(mock).toHaveBeenCalled();
  expect(mock).toHaveBeenCalledTimes(1);
  expect(mock).toHaveBeenCalledWith("foo");
});
```

```
// change return value

test("mock implementation", () => {
  const mock = jest.fn(() => "bar");

  expect(mock("foo")).toBe("bar");
  expect(mock).toHaveBeenCalledWith("foo");
});

test("also mock implementation", () => {
  const mock = jest.fn().mockImplementation(() => "bar");

  expect(mock("foo")).toBe("bar");
  expect(mock).toHaveBeenCalledWith("foo");
});

test("mock implementation one time", () => {
  const mock = jest.fn().mockImplementationOnce(() => "bar");

  expect(mock("foo")).toBe("bar");
  expect(mock).toHaveBeenCalledWith("foo");

  expect(mock("baz")).toBe(undefined);
  expect(mock).toHaveBeenCalledWith("baz");
});

test("mock return value", () => {
  const mock = jest.fn();
  mock.mockReturnValue("bar");

  expect(mock("foo")).toBe("bar");
  expect(mock).toHaveBeenCalledWith("foo");
});

test("mock promise resolution", () => {
  const mock = jest.fn();
  mock.mockResolvedValue("bar");

  expect(mock("foo")).resolves.toBe("bar");
  expect(mock).toHaveBeenCalledWith("foo");
});
```

    * Mocking a class method using enzyme
        *  `const myMethod = (wrapper.instance().`myMethod `= jest.fn());`

- `jest.spyOn(object, methodName)`
  - `const spy = jest.spyOn(wrapper.instance(), 'methodName');`
  - Creates a mock function similar to `jest.fn` but also tracks calls to `object[methodName]`
  - Use when you want the behavior of your function to execute
  - Allows for restoring the original function
  - It is just sugar for the basic `jest.fn` usage
  - Use when you only want to watch a method be called

```
// code
componentDidMount() {
  this.fetchFilmTitle();
}

// test
describe('componentDidMount', () => {
  it('calls fetchFilmTitle', () => {
    const fetchFilmTitle = jest.spyOn(app.instance(), 'fetchFilmTitle');

    app.instance().componentDidMount();

    expect(fetchFilmTitle).toHaveBeenCalledTimes(1);
  });
});
```

- `jest.mock(moduleName, factory, options)`
  - For mocking functions from an imported module
  - Automatically set all exports of a module to a mock function
  - Mocks a module with an auto-mocked version when it is being required
  - `factory` and `options` are optional

```
// test file
import myModule from 'path/to/myModule'

jest.mock('path/to/myModule');
// the module functions are now defined

// if you want to have it return something
myModule.mockImplementation(() => ({ someKey: 'someValue' }));

// to mock a specific function
jest.mock('./api', () => {
  return {
    makeFetch: jest.fn(data => {
      new Promise((resolve, reject) => {
        if (data) {
          resolve(data);
        } else {
          reject();
        }
      });
    })
  };
});
```

    * To separate mock functions of a module into their own file, create a `__mocks__` folder adjacent to the module to be mocked
    * Create a file inside the mock folder with the same name as the module to be mocked
    * Now the tests will use the mock implementations found in the mock file

```
src/
 |-- App.js
 |-- App.test.js
   |utils/
     |__mocks__/
       |-- apiCalls.js
     |-- apiCalls.js
```

- Mocked functions have the following methods:
  - getMockImplementation: [Function]
  - mock: [Getter/Setter]
  - mockClear: [Function]
    - Resets all information stored in the `mockFn.mock.calls` and `mockFn.mock.instances` arrays
    - Often this is useful when you want to clean up a mock's usage data between two assertions
  - mockReset: [Function]
    - Resets all information stored in the mock, including any initial implementation and mock name given
    - This is useful when you want to completely restore a mock back to its initial state
  - mockReturnValueOnce: [Function]
  - mockReturnValue: [Function]
  - mockImplementationOnce: [Function]
  - mockImplementation: [Function]
    - When you don't want the original implementation to be called
  - mockReturnThis: [Function]
  - mockRestore: [Function]

## _Snapshots_

- Tests return of the render statement
- Also can snapshot any data you call it on
- Press U in the test terminal to update the snapshot
- Keeps a recorded history of a component
- Do multiple snapshots based on different prop values
- The output of the current test run is compared with the snapshot of the previous test run
- Everytime the test is run, it will compare the current DOM to the existing one taken in the `/__snapshots__` folder
- Need to mock prop data used in the render/return in order to pass the test

```
it('matches the snapshot', () => {
  expect(wrapper).toMatchSnapshot();
});
```

## _Coverage_

- Uses instanbul to provide code coverage
  - https://istanbul.js.org/

* `npm run test -- --coverage -u`
* or Add a script to `package.json`
  - `"test-cov": "jest --coverage -u",`
  - % Stmts
    - all the statements of the file
  - % Branch
    - all the different possibilities of the file
      - i.e. conditionals
  - % Funcs
    - all the functions of the file
  - % Lines
    - number of lines covered when test is ran
  - Uncovered Lines
    - lines not covered

- only tells you what code has been ran by tests
- red highlighted lines have not been ran
- I icon means `if` block hasn't ran
- E icon means `else` block hasn't ran

* To only test specific files or folders, add the follow to `package.json`

```
"jest": {
  "collectCoverageFrom": [
    "src/**/*.js",
    "!src/index.js"
  ]
}
```

- To view the generated HTML report:
  - macOS
    - `open coverage/lcov-report/*.html`
  - windows
    - `cd coverage/lcov-report/`
    - `index.html`
- Over 90% coverage has diminishing returns
- Don't forget to add the report to `.gitignore`
  - `coverage/`

## _Jest.methods_

- `jest.clearAllMocks()`
  - Clears the `mock.calls` and `mock.instances` properties of all mocks
  - Equivalent to calling `.mockClear()` on every mocked function.
  - If one test calls a mock function, that mock function will count as called for other tests

```
beforeEach(() => {
  jest.clearAllMocks();
});
```

- `jest.resetAllMocks()`
  - Resets the state of all mocks
  - Does everything that `mockFn.`clearAllMocks`()` does, and also removes any mocked return values or implementations
  - Use to prevent mock implementations from polluting other tests
  - Equivalent to calling `.mockReset()` on every mocked function

```
beforeEach(() => {
  jest.resetAllMocks();
});
```

## _Global Methods_

- [`afterAll(fn, timeout)`](https://facebook.github.io/jest/docs/en/api.html#afterallfn-timeout)
- [`afterEach(fn, timeout)`](https://facebook.github.io/jest/docs/en/api.html#aftereachfn-timeout)
- [`beforeAll(fn, timeout)`](https://facebook.github.io/jest/docs/en/api.html#beforeallfn-timeout)
- [`beforeEach(fn, timeout)`](https://facebook.github.io/jest/docs/en/api.html#beforeeachfn-timeout)
- [`describe(name, fn)`](https://facebook.github.io/jest/docs/en/api.html#describename-fn)
- [`describe.only(name, fn)`](https://facebook.github.io/jest/docs/en/api.html#describeonlyname-fn)
- [`describe.skip(name, fn)`](https://facebook.github.io/jest/docs/en/api.html#describeskipname-fn)
- [`require.requireActual(moduleName)`](https://facebook.github.io/jest/docs/en/api.html#requirerequireactualmodulename)
- [`require.requireMock(moduleName)`](https://facebook.github.io/jest/docs/en/api.html#requirerequiremockmodulename)
- [`test(name, fn, timeout)`](https://facebook.github.io/jest/docs/en/api.html#testname-fn-timeout)
  - Alias: `it(name, fn)`
- [`test.only(name, fn, timeout)`](https://facebook.github.io/jest/docs/en/api.html#testonlyname-fn-timeout)
  - Alias: `it.only(name, fn, timeout)` or `fit(name, fn, timeout)`
- [`test.skip(name, fn)`](https://facebook.github.io/jest/docs/en/api.html#testskipname-fn)
  - Aliases: `xit(name, fn)` or `xtest(name, fn)`

## _Expect_

- When you're writing tests, you often need to check that values meet certain conditions
- `expect` gives you access to a number of "matchers" that let you validate different things

* [`.toThrow(error)`](https://facebook.github.io/jest/docs/en/expect.html#tothrowerror)
  - you have to pass a function into expect(function).toThrow(blank or type of error)

```
test("Test description", () => {
  const t = () => {
    throw new TypeError();
  };
  expect(t).toThrow(TypeError);
});
```

    * If you need to test an existing function whether it throws with a set of arguments, you have to wrap it inside an anonymous function in expect()

```
it('throws error if header length equals 0', () => {
  const header = [];
  let expected = 'input must not be of zero length';
  expect(() => parseLinkHeader(header)).toThrow(expected);
});
```

## _Hooks_

```
beforeEach(function() {
    // runs before each test in this describe block
    // if it's a promise, it waits for it to resolve
});
```

```

afterEach(function() {
    // runs after each test in this describe block
    // mainly used to clean up
});
```

```

beforeAll(function() {
    // runs once before all the tests in this describe block
    // more performant
});
```

```

afterAll(function() {
    // runs once after all the tests in this describe block
    // mainly used to clean up
    // more performant
});
```

## _Scripts_

- `"test": "jest —verbose"`
- `"test:watch": "jest --watchAll —verbose"`
- `"test:coverage": "jest --verbose --coverage`-u`"`
- The `--verbose` flag will allow you to display individual test results with test suite hierarchy

## _Debugging_

- https://github.com/facebook/create-react-app/blob/master/packages/react-scripts/template/README.md#debugging-tests
- Add the following to the `scripts` section in your project's `package.json`

```
"scripts": {
  "test:debug": "react-scripts --inspect-brk test --runInBand --env=jsdom"
}
```

- VSCode
  - Use the following `launch.json` configuration file:

```
`{
  "version": "0.2.0",
  "configurations": [
    {
      "name": "Debug CRA Tests",
      "type": "node",
      "request": "launch",
      "runtimeExecutable": "${workspaceRoot}/node_modules/.bin/react-scripts",
      "args": [
        "test",
        "--runInBand",
        "--no-cache",
        "--env=jsdom"
      ],
      "cwd": "${workspaceRoot}",
      "protocol": "inspector",
      "console": "integratedTerminal",
      "internalConsoleOptions": "neverOpen"
    }
  ]
}`
```

## _Resources_

- https://github.com/jest-community/awesome-jest

---

# _Enzyme_

- http://airbnb.io/enzyme/
- Tool for testing the rendered output of react components
- A testing library to render the react component into the DOM and query the DOM tree

## Setup

- `npm i`enzyme `enzyme-adapter-react-16 --save-dev`
- `import { shallow, mount } from 'enzyme';`
- In order to use the most current version of React > 16, install enzyme adapters to provide full compatibility with React

* Add a `src/setupTests.js` file to configure the enzmye adapter for our tests
  - src/setupTests.js should contain the following contents:

```
import { configure } from 'enzyme';
import Adapter from 'enzyme-adapter-react-16';

configure({ adapter: new Adapter() });
```

- Optional, add a `src/tempPolyfills.js` file
  - \*\* \*\*to create the global request animation frame function that React now depends on.
  - src/tempPolyfills.js should contain the following contents:

```
// `tempPolyfills.js`
const requestAnimationFrame = global.requestAnimationFrame = callback => {
  setTimeout(callback, 0);
}

export default requestAnimationFrame;


// change `setupTests.js to look like this
`// The disableLifecyleMethods portion is
// needed to allow us to modify props through different tests

import requestAnimationFrame from './tempPolyfills';

import { configure } from 'enzyme';
import Adapter from 'enzyme-adapter-react-16';

configure({ adapter: new Adapter(), disableLifecycleMethods: true });
```

- If not using Create-React-App
  - Add config to package.json:

```
  "jest": {
    "setupTestFrameworkScriptFile": "./setupTests.js"
  },
```

## _Mounting_

- renders our component’s HTML
- wraps a component, giving that component access to all of enzymes methods
- Difference between Shallow, Mount and render of Enzyme
  - https://gist.github.com/fokusferit/e4558d384e4e9cab95d04e5f35d4f913

### _shallow_

- `import { shallow } from 'enzyme';`
- `const wrapper = shallow(<MyComponent />);`
- creates virtualDOM only 1 level deep
- if our component has child components then it will only render stubs for the child components
- Because shallow does not render the child components it is much faster and should be used by default

### _mount_

- `import { mount } from 'enzyme';`
- `const wrapper = mount(<MyComponent />);`
- creates a complete virtualDOM
- if our component has child components then it will render the child components HTML
- Triggers the child components life-cycle methods

### _optional argument_

- `disableLifecycleMethods` (boolean)
  - `shallow(<App />, {disableLifecycleMethods: true})`
  - If set to true, `componentDidMount` is not called on the component, and `componentDidUpdate` is not called after `setProps` and `setContext`
  - Default to `false`

## _Methods_

- `state()`

  - returns state for root node of wrapper
  - gives access to the state object

- `props()`
  - returns props for root node of wrapper
- `instance()`
  - provides access to all the methods of the component
  - attach to component to check an instance
- `children()`
  - finds children of element
- `text()`
  - returns string, the text of an element
- `debug()`
  - Returns an HTML-like string of the wrapper for debugging purposes
  - use for console.logs
    - `console.log(wrapper.**debug**())`

* `.find()`
  - Finds every node in the render tree of the current wrapper that matches the provided selector
* `.simulate()`
  - Simulate events
  - Change

```
it('user text is echoed', () => {
  wrapper.find('input').simulate('change', {
    target: { value: 'hello' }
  });

  expect(wrapper.find('input').props().value).toEqual('hello');
});
```

    * Submit

```
it("when the form is submitted the event is cancelled", () => {
  let prevented = false;
  wrapper.find("form").simulate("submit", {
    preventDefault: () => {
      prevented = true;
    }
  });
  expect(prevented).toBe(true);
});
```

---

# _Test Helpers_

## enzyme-to-json

- Snapshot test your Enzyme wrappers
- Convert [Enzyme](http://airbnb.io/enzyme/) wrappers to a format compatible with [Jest snapshot testing](https://facebook.github.io/jest/docs/tutorial-react.html#snapshot-testing)
- https://github.com/adriantoine/enzyme-to-json
- `npm install --save-dev enzyme-to-json`

```
import React, {Component} from 'react';
import {shallow} from 'enzyme';
import toJson from 'enzyme-to-json';
import MyComponent from './MyComponent';

it('renders correctly', () => {
  const wrapper = shallow(<MyComponent />);

  expect(toJson(wrapper)).toMatchSnapshot();
});
```

##

casual

- Fake data generator for javascript
- https://github.com/boo1ean/casual
- `npm i -D casual`

```
import casual from 'casual';
// seed it so we get consistent results
casual.seed(777);
```

## waait

- Returns a promise that resolves after how many milliseconds you pass it
- Needed to get past Loading state of a component using Apollo Client
  - A 0ms timeout will put the next line of code at the end of the callstack, which will wait for the next render to happen
- https://github.com/wesbos/waait
- `npm i -D` ```waait`

```
const wait = (amount = 0) => new Promise(resolve => setTimeout(resolve, amount));
```

```
`import wait from 'waait';`

  it('renders with proper data', async () => {
    const mocks = [
      {
        // when someone makes a request with this query and variable combo
        request: { query: SINGLE_ITEM_QUERY, variables: { id: '123' } },
        // return this fake data (mocked data)
        result: {
          data: {
            item: fakeItem()
          }
        }
      }
    ];
    const wrapper = mount(
      <MockedProvider mocks={mocks}>
        <SingleItem id="123" />
      </MockedProvider>
    );
    expect(wrapper.text()).toContain('Loading...');
    await wait();
    wrapper.update();
    // console.log(wrapper.debug());
    expect(toJSON(wrapper.find('h2'))).toMatchSnapshot();
    expect(toJSON(wrapper.find('img'))).toMatchSnapshot();
    expect(toJSON(wrapper.find('p'))).toMatchSnapshot();
  });
```

---

# _React_

- Mainly use Jest and Enzyme to test
- What to test for:
  - Is what I expect to render actually rendering?
  - Are props being passed and accepted correctly?
  - Does the component change / update state?
  - Are the correct functions being called?
  - When the DOM changes is that actually happening?
- Only have to test what's between the constructor and render
- Test that methods do what they should do
- Don't need to test default state
- Components
  - snapshot
  - changes to state
  - methods

---

# _Redux_

- Do test:
  - mapStateToProps
    - when called returns correct object
  - mapDispatchToProps
  - action creators
    - they return what they are supposed to
  - reducers
- Don't test
  - The exported value of a container (`connect()`)

---

# _Router_

- To test a component (with Jest) that contains `<Route>` and `withRouter` you need to import Router in you test, not in your component

```
import { BrowserRouter as Router } from 'react-router-dom';

app = shallow(
  <Router>
    <App />
  </Router>)
```

---

# _Apollo Client_

- https://www.apollographql.com/docs/react/recipes/testing.html
- https://github.com/apollographql/apollo-client/blob/master/docs/source/recipes/testing.md

## Queries

```
const fakeItem = () => ({
  __typename: 'Item',
  id: 'abc123',
  price: 5000,
  user: null,
  image: 'dog-small.jpg',
  title: 'dogs are best',
  description: 'dogs',
  largeImage: 'dog.jpg',
});
```

```
import { mount } from 'enzyme';
import toJSON from 'enzyme-to-json';
import wait from 'waait';
import SingleItem, { SINGLE_ITEM_QUERY } from '../components/SingleItem';
import { MockedProvider } from 'react-apollo/test-utils';

const fakeItem = () => ({
  __typename: 'Item',
  id: 'abc123',
  price: 5000,
  user: null,
  image: 'dog-small.jpg',
  title: 'dogs are best',
  description: 'dogs',
  largeImage: 'dog.jpg',
});

describe('<SingleItem/>', () => {
  it('renders with proper data', async () => {
    const mocks = [
      {
        // when someone makes a request with this query and variable combo
        request: { query: SINGLE_ITEM_QUERY, variables: { id: '123' } },
        // return this fake data (mocked data)
        result: {
          data: {
            item: fakeItem(),
          },
        },
      },
    ];
    const wrapper = mount(
      <MockedProvider mocks={mocks}>
        <SingleItem id="123" />
      </MockedProvider>
    );
    expect(wrapper.text()).toContain('Loading...');
    await wait();
    wrapper.update();
    // console.log(wrapper.debug());
    expect(toJSON(wrapper.find('h2'))).toMatchSnapshot();
    expect(toJSON(wrapper.find('img'))).toMatchSnapshot();
    expect(toJSON(wrapper.find('p'))).toMatchSnapshot();
  });

  it('Errors with a not found item', async () => {
    const mocks = [
      {
        request: { query: SINGLE_ITEM_QUERY, variables: { id: '123' } },
        result: {
          errors: [{ message: 'Items Not Found!' }],
        },
      },
    ];
    const wrapper = mount(
      <MockedProvider mocks={mocks}>
        <SingleItem id="123" />
      </MockedProvider>
    );
    await wait();
    wrapper.update();
    console.log(wrapper.debug());
    const item = wrapper.find('[data-test="graphql-error"]');
    expect(item.text()).toContain('Items Not Found!');
    expect(toJSON(item)).toMatchSnapshot();
  });
});
```

## Mutations

---

# _Test pollution_

- when one test affects another test

---

# _Test-driven Development_

- The process of learning effective TDD is the process of learning how to build more modular applications
- create outline of the interface and all the pieces
- write tests first, then code
- write unit test
- run test
- write code to pass test
- refactor

---

# _Behavior-driven Development_

- A variation of TDD that tests for user scenarios

- consists of scenarios and specifications
  - given
    - a certain state of the app
  - when
    - a certain time of the year/day
  - then
    - some behavior in the app will occur

```
describe('App', () => {
  const app = shallow(<App />)

  describe('when clicking the `add-gift` button', () => {

    beforeEach(() => {
      app.find('.btn-add').simulate('click')
    });

    afterEach(() => {
      app.setState({ gifts: [] })
    });

    it('adds new gift to `state`', () => {
      expect(app.state().gifts).toEqual([{ gift: 1 }])
    })

  });
})
```

---

# _fetch_

- Do test:
  - fetch is called with correct params
  - on error, state is set with correct error status
  - anything else chained onto the fetch
- Don't test:
  - the real API data
- Mock:

```
window.fetch = jest.fn().mockImplementation(() => Promise.resolve({
    json: () => Promise.resolve([mockReturn])
}))

`expect(window.fetch).toHaveBeenCalledWith(...expected)`
```

    * when promise chaining (`.then`), must use `window.update()`

- options object

```
`const expect = [
`    'api/v1/',
    {
        method: 'POST'
        body: // value
        headers: {
          // key/value
        }
    }
`]`
```

---

# _Examples_

## Integration

```
test("renders search results when the articles change", () => {
  const wrapper = mount(<Search articles={[]} />);

  wrapper.setProps({
    articles: [{ webUrl: "http://google.com", webTitle: "Google Search" }]
  });

  expect(wrapper.find("a").prop("href")).toEqual("http://google.com");
});
```

```
test("should render Search component", () => {
  const wrapper = mount(<SearchContainer />);

  expect(wrapper.children(Search).length).toEqual(1);
});
```

```
test("should update articles state", () => {
  const wrapper = mount(<SearchContainer />);

  expect(wrapper.state().articles).toEqual([]);

  const { performSearch } = wrapper.find(Search).props();

  return performSearch().then(() => {
    expect(wrapper.state().articles).toHaveLength(10);
  });
});
```

---

# _Misc_

- https://testingjavascript.com/
- https://github.com/skidding/react-testing-examples
- https://github.com/skidding/react-mock

* Generate fake data
  - https://github.com/marak/Faker.js/

- typechecking
  - static type checkers:
    - typescript
    - flow
    - ReasonML

* what is a JS test
  - a function that throws an error if the result does not equal what's expected

```
if (result !== expected) {
  throw new Error(`${result} is not equal to ${expected}`)
}
```

- the format of a test should be:

```
test(title, () => {
  // arrange
  // act
  // assert
})
```

- `expect` function:

```
function expect(actual) {
  return {
    toBe(expected) {
      if (actual !== expected) {
        throw new Error(`${actual} is not equal to ${expected}`)
      }
    },
  }
}

expect(result).toBe(expected)
```

- `test` function:

```
function test(title, callback) {
  try {
    callback()
    console.log(`✓ ${title}`)
  } catch (error) {
    console.error(`✕ ${title}`)
    console.error(error)
  }
}
```

- calling a `test`:

```
test('sum adds numbers', () => {
  const result = sum(3, 7)
  const expected = 10
  expect(result).toBe(expected)
})
```

## Jest assertions

- other/jest-expect/test/expect-assertions.js/

* it is important to verify that your assertions are running
  - there is no indication in the output that your assertions are running
    - they will show as passing
  - you should make sure the test can fail
    - you can do this by breaking your code temporarily

## Mocks

- to mock a function being called within a function

```
function thumbWar(player1, player2) {
  const numberToWin = 2
  let player1Wins = 0
  let player2Wins = 0
  while (player1Wins < numberToWin && player2Wins < numberToWin) {
    const winner = getWinner(player1, player2)
    if (winner === player1) {
      player1Wins++
    } else if (winner === player2) {
      player2Wins++
    }
  }
  return player1Wins > player2Wins ? player1 : player2
}
```

- we want to mock getWinner() so that the test is using the mock version of getWinner()
  - monkey patching
    - import the getWinner() function
      - `**import** {getWinner} **from** './utils'`
    - change it's return value
      - `utils.**getWinner** **=** (p1, p2) **=>** p2`
  - not a good solution
    - it modifies the function for all tests
    - if the function gets changed, the mock won't reflect that change
    - you when you mock something, you severe the relationship between your real code with a fake thing
- we want getWinner() to be called the way it is expected to be called with all the arguments
  - jest.spyOn
    - will wrap the original function
    - instead of calling the original function , it calls a mocked copy
    - mocked functions created by `spyOn()` have a `mockImplementation()` property

```
// take the utils object, and swap the getWinner property with a mock function
jest.spyOn(utils, 'getWinner')
 utils.getWinner.mockImplementation((p1, p2) => p2)

// restore of the original state of the mock as to not pollute other tests
utils.getWinner.mockRestore()
// can be included in a beforeEach()
```

- .mock()
  - allows us to mock an entire module, and specified functions within
  - `**import** * **as** realModule **from** '../realModule'`


    * to mock the whole module:

```
jest.mock('../realModule')
```

    * to mock specific functions from a module:

```
jest.mock('../realModule', () => {
  return {
    getWinner: jest.fn((p1, p2) => p2),
  }
})
```

- to make a mock module:
  - create a ****mocks**** folder in the same directory as the module you want to make
  - create a file inside the ****mocks**** folder with the same name as the module you want to mock
  - whenever that module is required , jest will automatically use this mock file instead of the real one
  - still have to call the mock
    - `jest.mock('../realModule')`

## Test object factories

- takes the common properties of a mock and put it in a function and return what you are looking for
- any setup that is common to all the tests

```
// outside of your tests
function setup() {
  const req = {
    body: {},
  }
  const res = {}
  const next = jest.fn()
  Object.assign(res, {
    status: jest.fn(
      function status() {
        return this
      }.bind(res),
    ),
    json: jest.fn(
      function json() {
        return this
      }.bind(res),
    ),
    send: jest.fn(
      function send() {
        return this
      }.bind(res),
    ),
  })
  return {req, res, next}
}

// to use inside your tests
const {req, res, next} = setup()
req.body = {password: generate.password()}
```

## Test Driven Development

- TDD
- Write tests first, then write the code
- red, green, refactor
- best to write one test at a time

## Misc

- start jest on a specific file using regex
  - npm test utils.\*auth.todo
  - nr
  - npm run test:expect

* https://github.com/atlassian/jest-in-case

- app
  - client/server
  - api server w/ auth
  - create-react-app

* you can put properties on functions because they are first-class objects
* https://blog.bitsrc.io/how-to-test-react-components-with-jest-and-enzyme-in-depth-145fcd06b90
* https://pixel-tones.com/unit-testing-with-enzyme-and-jest-and-setting-up/

---

# _Performance_

## curl

- Display response time
- For first time on Windows
  - `Remove-item alias:curl`
- `curl -o /dev/null -s -w "time_connect: %{time_connect} + time_starttransfer: %{time_starttransfer} = time_total: %{time_total} /`size_download: %{size_download}`\n" https://www.google.com`

---
