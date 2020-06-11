# _Misc_

---

# _Concepts_

## _Pure functions_

- Functions which will always return the same output for a given input
- Doesn't change the state of the world around them
  - That is handled outside of the function
- Predictable
- Easier to test
- Execution doesn't depend on the state of the app
- Does not produce side effects
- Doesn't modify variables outside of it's scope
- Example of impure function:
  - network requests

```
// pure
cont add = (n1, n2) => {
    return n1 + n2;
}


// impure
cont add = (n1, n2) => {
    return n1 + Math.rand(n2)
}
```

- If you’re passed an array or an object, and you want to return a changed version of that object, you can’t just make the changes to the object and return it
- You have to create a new copy of the object with the required changes

```
// pure
const signInUser = user => ({...user, isSignedIn: true });
const foo = {
  name: 'Foo',
  isSignedIn: false
};
// foo was not mutated
console.log(
  signInUser(foo), // { name: "Foo", isSignedIn: true }
  foo              // { name: "Foo", isSignedIn: false }
);


// impure
const signInUser = user => user.isSignedIn = true;
const foo = {
  name: 'Foo',
  isSignedIn: false
};
// foo was mutated
console.log(
  signInUser(foo), // true
  foo              // { name: "Foo", isSignedIn: true }
);
```

## _Higher-order functions_

- Takes one or more functions as arguments (i.e., [procedural parameters](https://en.wikipedia.org/wiki/Procedural_parameter)),
- Or returns a function as its result
- All other functions are first-order functions
- Functions that operate on other functions, either by taking them as arguments or by returning them
- Allows us to make less functions

## _Curried functions_

- Taking a single function with multiple arguments and transforming it into a series of intermediate functions that take a single argument
- When you break down a function that takes multiple arguments into a series of functions that take part of the arguments
- Decomposing a function that breaks a function into a series of functions

## _Helper functions_

- Functions that perform part of the computation of another function

## _First-class functions_

- JavaScript functions are first-class-citizens
- Using functions as a variable
- Functions are objects
- They can have properties and methods just like any other object

## _Debounce functions_

- Prevents a function from being called several times in succession
- Limits the rate at which a function can fire
- Built on JavaScript's native `setTimeout` function
- Example: A resize listener on the window which does some element dimension calculations and (possibly) repositions a few elements
  - Being repeatedly fired after numerous resizes will really slow your site down
- `lodash.debounce`

```
function debounce(func, wait, immediate) {
  // 'private' variable for instance
  // The returned function will be able to reference this due to closure.
  // Each call to the returned function will share this common timer.
  var timeout;

  // Calling debounce returns a new anonymous function
  return function() {
    // reference the context and args for the setTimeout function
    var context = this,
      args = arguments;

    // Should the function be called now? If immediate is true
    // and not already in a timeout then the answer is: Yes
    var callNow = immediate && !timeout;

    // This is the basic debounce behaviour where you can call this
    // function several times, but it will only execute once
    // [before or after imposing a delay].
    // Each time the returned function is called, the timer starts over.
    clearTimeout(timeout);

    // Set the new timeout
    timeout = setTimeout(function() {
      // Inside the timeout function, clear the timeout variable
      // which will let the next execution run when in 'immediate' mode
      timeout = null;

      // Check if the function already ran with the immediate flag
      if (!immediate) {
        // Call the original function with apply
        // apply lets you define the 'this' object as well as the arguments
        // (both captured before setTimeout)
        func.apply(context, args);
      }
    }, wait);

    // Immediate mode and no wait timer? Execute the function..
    if (callNow) func.apply(context, args);
  };
}
```

## _Inheritance vs Composition_

- https://www.youtube.com/watch?v=wfMtDGfHWpA

## _Coupling_

- The degree to which a unit of code (module, function, class, etc…) depends upon other units of code

## _Tight coupling_

- A high degree of coupling, refers to how likely a unit is to break when changes are made to its dependencies
- The tighter the coupling, the harder it is to maintain or extend the application

## _Function composition_

- The process of applying a function to the return value of another function
- In other words, you create a pipeline of functions, then pass a value to the pipeline, and the value will go through each function like a stage in an assembly line, transforming the value in some way before it’s passed to the next function in the pipeline
- Eventually, the last function in the pipeline returns the final value.

## **_Synchronous vs Asynchronous _**

- **Synchronous code (blocking):**

```
a()
b()
```

    * Function b() cannot run until a() is totally finished. Synchronous code is fine for things that happen fast, but it's horrible for things that require saving, loading, downloading or uploading.

- **Asynchronous (non-blocking):**

```
a(b)
```

- In the non-blocking version b is a callback to a. In the blocking version a and b are both called/invoked (they both have () after them which executes the functions immediately). In the non-blocking version, you will notice that only a gets invoked, and b is simply passed in to a as an argument.

* In the blocking version, there is no explicit relationship between a and b. In the non-blocking version, it becomes a's job to do what it needs to do and then call b when it is done. Using functions in this way is called callbacks because your callback function, in this case b, gets called later on when a is all done.

- Callbacks are just functions that call other functions after some asynchronous task.

## _Object-Oriented Programming (OOP)_

- Structuring code with objects instead of functions
- Benefits:
  - reusability
  - encapsulation
  - scalability
  - maintainability

## _Closures_

- Expressions, usually functions, which can work with variables set within a certain context
- In other words, a closure is an inner function that has access to the outer (enclosing) function’s variables’ scope chain
- Or, to try and make it easier, inner functions referring to local variables of its outer function create closures

---

# _**Debugger**_

- invokes any available debugging functionality

- Syntax:

  - `debugger;`

- when the debugger code is invoked, execution is paused at the debugger statement. It is like a breakpoint in the script source.
- You can type it into the console, and then invoke a function after it
- Can create a function to make it easier to use

```
function debugger(functionName) {
  debugger;
  functionName();
}
```

---

# **_DOM_**

object oriented representation of a web page

---

# _.document_

---

.getElementByID

.createElement

.querySelector()

- returns the first element found

.querySelectorAll()

- returns an array of all elements found

\_ \_
_.value_
_.valueasnumber_
\_ \_
_.textContent_
\_ \_
_.appendChild_
\_ \_
_nodelist_
\_ \_

---

# _Refactoring_

- Technical debt
  - the build up of code that might be inefficient, fragile, unreadable, and/or difficult to maintain

* Functions should be single function, concise, and reusable.
* Shorten long line lengths by using variables

---

# _Performance_

- https://web.dev/
- https://gtmetrix.com/

* https://developers.google.com/speed/pagespeed/insights/

---

# _MacOS_

- Make a new folder (aka make directory)
  - `mkdir <FOLDERNAME>`
- Navigate into an existing folder (aka change directory)
  - `cd <FOLDERNAME>`
- List the items in a folder
  - `ls`

---

# _RESTful API_

- REST stands for representational state transfer
- This means that web resources communicate using a set of stateless, uniform operations
- RESTful architecture includes sending HTTP methods to a URL to get back information from a request
  - This is the implementation of that ‘uniform interface’ constraint

* The six architectural constraints of REST are:
  - Client-server
    - Separation of GUI and data
  - Stateless
    - No client context is stored by server, each client request provides all the information to fulfill the request
  - Cacheable
    - Server responses are defined as cacheable or not. (Speeds up future interactions)
  - Layered system
    - Modularity, each ‘layer’ serves only a single high-level purpose - multiple servers can handle steps of a request (data/authentication), but the user cannot tell that their request/response went through multiple servers
  - Code on demand
    - Instead of just JSON or XML, return JS script tag within HTML document
    - optional, can still be considered RESTful without this
  - Uniform interface
    - Ability to identify resources and manipulate them based on standard information provided

## CRUD

- Methods:
  - Create - `POST`
    - Create a new resource
    - Send new data
  - Read - `GET`
    - Retrieve resource information identified by the request
    - Retrieve existing data
  - Update - `PUT`
    - Fully update a specific resource in its entirety
    - Don't use `PATCH`
      - Update only a portion of a specific resource
  - Destroy - `DELETE`
    - Destroy an entire specific resource by the request

## Status codes

- post
  - success
    - 201
      - created
  - fail
    - 422
      - incomplete info
- put/patch
  - success
    - 200
  - fail
    - 404
      - id not in database
    - 422
      - incomplete info
- delete
  - success
    - 200
      - with content returned
    - 204
      - no content returned
  - fail
    - 404
      - id not in database
- 200's
  - good
- 300's
  - goaway
- 400's
  - client errors
  - 404
    - file not found
- 500's
  - server/app errors
  - 500
    - server not found

---

# _Agile Development_

- Short cycles consisting of:
  - Design
  - Achitect
  - Implement
  - Test

---

# _MVC_

- Separation of concerns
- Model
  - business logic
  - anything that stores information
- View
  - UI
  - renders to the browser
- Controller
  - go between of model and view
  - when something happens on the UI, the controller tells the model what happened
  - the model sends new data to the controller, which tells the view what to display

```
import React, { Component } from 'react';

class App extends Component {
  constructor() {
    super()

 // model
    this.state = {
      count: 0,
    }
  }


// controller
  handleCounter = (event) => {
    const increment = event.target.name === '+' ? 1 : -1
    this.setState({count: this.state.count + increment})
  }


// view
  render() {
    return (
      <div className="App">
        <h1>{this.state.count}</h1>
        <button onClick={this.handleCounter} name="-">-</button>
        <button onClick={this.handleCounter} name="+">+</button>
      </div>
    );
  }
}

export default App;
```

---

# _Lighthouse_

- Auditing tool built into Chrome
- developer tools → Audits

---

# _Bash_

- https://github.com/Ecksi/xcBash

---

# _hasOwnProperty_

```
export let clone = (obj) => {
    let newObj = {};
    for (let prop in obj) {
        if (obj.hasOwnProperty(prop)) {
            newObj[prop] = obj[prop];
        }
    }
    return newObj;
}
```

---

# _Powershell_

- https://github.com/janikvonrotz/awesome-powershell
- https://gist.github.com/jchandra74/5b0c94385175c7a8d1cb39bc5157365e
- https://taraksharma.com/supercharging-powershell-with-hyper-oh-my-posh-posh-git/

* Edit config
  - `code $PROFILE`
* View colors
  - `Get-PSReadlineOption | Select *color`
  - `Show-ThemeColors`
  - `Show-Colors`
  - `Get-ConsoleTheme -ListAvailable`

## Config

```
# PSReadLine
Import-Module PSReadLine

Set-PSReadlineOption -ResetTokenColors

# Ensure oh-my-posh is loaded
Import-Module -Name oh-my-posh

# Ensure posh-git is loaded
Import-Module -Name posh-git

# Set the default prompt theme
Set-Theme Darkblood

# PSConsoleTheme
Import-Module PSConsoleTheme

Set-ConsoleTheme 'Solarized Light'
```

---

# _HyperTerm_

- https://hyper.is/
- https://github.com/bnb/awesome-hyper

* config

```
 verminal: {
 *// fontFamily: 'fire-code',*
 fontSize: 16
 },
 hyperTabs: {
 *// trafficButtons: true,*
 *// border: true,*
 *// tabIconsColored: true,*
 *// activityColor: 'green',*
 closeAlign: 'right',
 }
```

- plugins

```
 plugins: [
 *// Themes*
 *// 'hypertheme',*
 'hyper-ayu-light',
 *// 'hyper-one-light',*
 *// 'verminal',*
 *// Extenstions*
 'hyperpower',
 'hyperterm-tabs',
 'hyperterm-paste',
 'hypercwd',
 'hyperline',
 'hyperterm-dibdabs',
 'hyperlinks',
 'hyper-statusline',
 'hyper-alt-click',
 'hyper-tabs-enhanced',
 'gitrocket',
 'space-pull'
 ],
```

---

# _Terms_

- https://developer.mozilla.org/en-US/docs/Glossary

* Preset
  - a group of related plugins

- selector:

* modifier:

- parameter
  - when you declare a function, and you stipulate the function will accept some bits of information
  - they are placeholders

````
`// parameters named on declaration of function`
`function`` ``myDreamCar``(``make``, ``model``) {`
``  ```return`` ``"Buy me "`` ``+`` ``make`` ``+`` ``" "`` ``+`` ``model``;`
`}`
````

- argument
  - when you pass the values of the parameters, those are called arguments
  - the real data used by parameters

```
`// arguments "Audi" and "R8" passed into a called function`
`myDreamCar``(``"Audi"``, ``"R8"``);`
```

- Boolean
  - may only be one of two values: true or false. They are basically little on-off switches, where true is "on" and false is "off."

* call:

- queue
  - an abstract Data Structure where items are kept in order. New items can be added at the back of the queue and old items are taken off from the front of the queue

* Callback Functions
  - The functions that are passed into higher order functions

- Event delegation
  - a mechanism of responding to ui-events via a single common parent rather than each child, through the magic of event "bubbling" (aka event propagation)

* Method
  - function as a value in an object

- Instance
  - an object that contains the property names and methods of a class, but with unique property values

* Recursion

- Function Expressions
  - defines a function, but instead of giving the name to the function itself, the function is left anonymous and the name is instead assigned to a variable

* Anonymous functions
  - commonly used as arguments to other functions

- Callback functions

* Code smell
  - a surface indication that usually corresponds to a deeper problem in the system

- Lazy loading
  - A design pattern commonly used in computer programming to defer initialization of an object until the point at which it is needed

* glob
  - A pattern-matching syntax that shells use
  - Like when you do `rm *.js` , the `*.js` is a glob
  - https://en.wikipedia.org/wiki/Glob_(programming)

---
