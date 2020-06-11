# _Web API's_

- https://developer.mozilla.org/en-US/docs/Web/API
- Asynchronous functions

---

# _console_

## console.log()

- Prints to the browser console
- Prints an element in an HTML-like tree
- Destructured console.log:
  - `console.log({myArray})`
  - same as `console.log(“myArray:”, myArray)`

* Logging objects:
  - Don't use `console.log(obj);`,
  - Use `console.log(JSON.parse(JSON.stringify(obj)));`.
  - This way you are sure you are seeing the value of `obj` at the moment you log it.

## console.dir()

- Displays an interactive list of the properties of the specified JavaScript object
- Prints an element in an JSON-like tree

## console.table(data, [column names])

- Can format data, such as JSON

## console.clear()

- Clears the console

## console.assert(expression, error)

- If the expression is false, log an error

---

# Event

- Creates an `Event` object, returning it to the caller

## event.target

- Returns the node that was targeted by the function
- Print element to the console:
  - `console.log(e.target)`
- Print the elements properties to the console:
  - `console.dir(e.target)`

---

# _EventTarget_

## .addEventListener()

- `target.addEventListener(type, listener[, options]);`
- element, document, and window are the most common event targets
- types - https://developer.mozilla.org/en-US/docs/Web/Events

---

# _setTimeout_

- `let`timeoutID `= setTimeout(func|code, delay[, arg1, arg2...])`
- Allows to run a function once after the interval of time
- Defers callback until stack is clear
- Takes two arguments:

  - Callback function
  - Delay time

- When `setTimeout()` runs, it allows other code to run while the timer is waiting

```
sayHi = (phrase, who) => {
  alert( phrase + ', ' + who );
}

`let `timeoutID `= `setTimeout(sayHi, 1000, "Hello", "Chase");
```

- There are two ways of running something regularly:
  - `setInterval`
  - Recursive `setTimeout`
    - Guarantees a fixed delay between executions
    - `setInterval` does not

```
// Schedules the next call right at the end of the current one

let `timeoutID `= setTimeout(function tick() {
  alert('tick');
  timerId = setTimeout(tick, 2000); // (*)
}, 2000);
```

---

# _setInterval_

- `let intervalID = setInterval(func|code, delay[, arg1, arg2...])`
- `delay` is the time, in milliseconds (1,000ms = 1s) the timer should delay in between executions of the specified function or code
- Repeatedly calls a function or executes a code snippet, with a fixed time delay between each call
- Keeps calling the specified function until the `clearInterval()` method is called or the window is closed
- The time taken by the callback execution “consumes” a part of the interval
  - It's possible the execution takes more time than the specified amount
- Returns an `interval ID` which uniquely identifies the interval
  - `const intervalID = scope.setInterval(code, delay);`
- Stop the interval by calling `clearInterval()` using the `interval ID`

```
const intervalID = window.setInterval(myCallback, 500);

function myCallback() {
  // Your code here
}
```

```
// repeat with the interval of 2 seconds
const intervalID = setInterval(() => console.log('tick'), 1000);

// after 5 seconds stop
setTimeout(() => {
  clearInterval(intervalID);
}, 5000);
```

```
let timerId = setInterval(myCallback, 100);

let start = 1
let end = 10

console.log(start);

function myCallback() {
  start++;
  console.log(start);

  if (start === end) {
    clearInterval(timerId);
    console.log('stop');
  }
}
```

---

# _sessionStorage_

- https://developer.mozilla.org/en-US/docs/Web/API/Window/sessionStorage
- Maintains a separate storage area for each given origin that's available for the duration of the page session
  - As long as the browser is open, including page reloads and restores

---

# _localStorage_

- https://developer.mozilla.org/en-US/docs/Web/API/Window/localStorage
- Persists for an indefinite amount of time for a give browser at a certain domain
- Stored at JSON Objects

* Add an item to localStorage
  - Stores a value associated with a key
  - `localStorage.setItem('key', value)`
  - `localStorage.setItem("myProperty", "Hello World");`
  - can be done 3 ways:
    - `localStorage.colorSetting = '#a4509b'; localStorage['colorSetting'] = '#a4509b'; localStorage.setItem('colorSetting', '#a4509b');`
  - complex datatypes must be parsed to JSON before adding
    - `localStorage.setItem(itemIndex, JSON.stringify(item));`

- Retrieve an item from localStorage
  - Retrieves the value associated with the key
  - `localStorage.getItem('key')`
  - `var myProperty = localStorage.getItem("myProperty");`
  - complex datatypes must be parsed to JSON after retrieving
    - `var item = JSON.parse(localStorage.getItem(key));`

* Get the name of a key in localStorage
  - `var aKeyName = storage.key(index);`

- Remove an item from localStorage
  - Removes properties
  - `localStorage.removeItem("`myProperty`");`

* Clear everything in localStorage
  - `localStorage.clear();`

- Get the number of properties stored
  - `localStorage.length`

* Iterate through the keys in localStorage

```
for (var i=0; i < localStorage.length; i++) {
  var propertyName = localStorage.key(i);
  console.log(  i + " : " + propertyName + " = " + localStorage.getItem(propertyName));
}
```

---

# _fetch_

- `fetch(input[, init])`
  - `input` is the path to the resource you want to fetch
    - When the URL doesn’t start with a protocol name (such as http:) it is treated as relative
      - it is interpreted relative to the current document
    - When it starts with a slash (/), it replaces the current path
      - the part after the server name
    - When it does not, the part of the current path up to and including its last slash character is put in front of the relative URL
  - Use optional second argument to add an Option object
  - `init` is an options object containing any custom settings that you want to apply to the request
    - The possible options are:
    - `method`: The request method, e.g., `GET`, `POST`.
      - Types of requests:
        - GET
          - default behavior
        - POST
        - PUT
        - PATCH
        - DELETE
    - `headers`: Any headers you want to add to your request, contained within a [`Headers`](https://developer.mozilla.org/en-US/docs/Web/API/Headers) object or an object literal with [`ByteString`](https://developer.mozilla.org/en-US/docs/Web/API/ByteString) values.
    - `body`: Any body that you want to add to your request: this can be a [`Blob`](https://developer.mozilla.org/en-US/docs/Web/API/Blob), [`BufferSource`](https://developer.mozilla.org/en-US/docs/Web/API/BufferSource), [`FormData`](https://developer.mozilla.org/en-US/docs/Web/API/FormData), [`URLSearchParams`](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams), or [`USVString`](https://developer.mozilla.org/en-US/docs/Web/API/USVString) object. Note that a request using the `GET` or `HEAD` method cannot have a body.
    - `mode`: The mode you want to use for the request, e.g., `cors`, `no-cors`, or `same-origin`.
    - `credentials`: The request credentials you want to use for the request: `omit`, `same-origin`, or `include`. To automatically send cookies for the current domain, this option must be provided. Starting with Chrome 50, this property also takes a [`FederatedCredential`](https://developer.mozilla.org/en-US/docs/Web/API/FederatedCredential) instance or a [`PasswordCredential`](https://developer.mozilla.org/en-US/docs/Web/API/PasswordCredential) instance.
    - `cache`: The cache mode you want to use for the request: `default`, `no-store`, `reload`, `no-cache`, `force-cache`, or `only-if-cached`.
    - `redirect`: The redirect mode to use: `follow` (automatically follow redirects), `error` (abort with an error if a redirect occurs), or `manual` (handle redirects manually). In Chrome the default is `follow` (before Chrome 47 it defaulted to `manual`).
    - `referrer`: A [`USVString`](https://developer.mozilla.org/en-US/docs/Web/API/USVString) specifying `no-referrer`, `client`, or a URL. The default is `client`.
    - `referrerPolicy`: Specifies the value of the referer HTTP header. May be one of `no-referrer`, `no-referrer-when-downgrade`, `origin`, `origin-when-cross-origin`, `unsafe-url`.
    - `integrity`: Contains the [subresource integrity](https://developer.mozilla.org/en-US/docs/Web/Security/Subresource_Integrity) value of the request (e.g., `sha256-BpfBw7ivV8q2jLiT13fxDYAe2tJllusRSZ273h2nFSE=`).
    - `keepalive`: The `keepalive` option can be used to allow the request to outlive the page. Fetch with the `keepalive` flag is a replacement for the [`Navigator.sendBeacon()`](https://developer.mozilla.org/en-US/docs/Web/API/Navigator/sendBeacon) API.
    - `signal`: An [`AbortSignal`](https://developer.mozilla.org/en-US/docs/Web/API/AbortSignal) object instance; allows you to communicate with a fetch request and abort it if desired via an [`AbortController`](https://developer.mozilla.org/en-US/docs/Web/API/AbortController).

* Returns a [`Promise`](https://developer.mozilla.org/en-US/docs/Web/API/Promise) that resolves to a [`Response`](https://developer.mozilla.org/en-US/docs/Web/API/Response) object
  - Status codes
    - https://developer.mozilla.org/en-US/docs/Web/HTTP/Status
    - 200 range means everything is OK, the request was successful
    - 300 range means you are probably being redirected
    - 400 range means you sent a bad request. Do it again, but better
    - 500 range means that something is screwed up with the server, but my request is OK
  - Headers
    - The headers are wrapped in a `Map`-like object that treats its keys (the header names) as case insensitive
    - `headers.get("Content-Type")` and `headers.get("content-TYPE")` will return the same value
* The promise returned by `fetch` resolves successfully even if the server responded with an error code
* It might also be rejected, if there is a network error or if the server that the request is addressed to can’t be found
  - Rejects with a TypeError object

```
myOptionsObject1 = {
  method: 'GET',
  headers: {
    'Content-Type': 'image/jpeg'
  },
  mode: 'cors',
  cache: 'default'
};

myOptionsObject2 = {
  method: 'POST',
  body: JSON.stringify(credentials),
  headers: {
    'Content-Type': 'application/json'
  }
};
```

- ES5: fetch()

```
function fetchGitHubUser(handle) {
  var url = `https://api.github.com/users/${handle}`
  fetch(url) // fetch call
    .then(response => response.json()) // parse response
    .then(data => console.log(data)) // log data
    .catch(err => console.log("Error: ", err.message)) // error case
}
```

- ES6: fetch()

```
// get
const getGitHubUser = async (handle) => {
  try {
    const url = `https://api.github.com/users/${handle}`
    const response = await fetch(url) // fetch call
    if (!response.ok) {
      this.setState({ errorStatus: 'Unable to get user' });
      throw new Error(`Unable to get user. (error: ${response.status})`);
    }
    return await response.json() // parse response
  } catch (error) {
    throw new Error(error.message); // error case
  }
}

// post
export const postGitHubUser = async (credentials, handle) => {
  try {
    const url = `https://api.github.com/users/${handle}`;
    const response = await fetch(url, {
      method: 'POST',
      body: JSON.stringify(credentials),
      headers: {
        'Content-Type': 'application/json'
      }
    });
    if (response.status >= 400) {
      this.setState({ errorStatus: 'Post failed' });
      throw new Error('Post failed');
    }
    return await response.json();
  } catch (error) {
    throw new Error(error.message);
  }
};

// modules
  // app.js
  componentDidMount() {
    this.fetchFilmTitle();
  }

  async fetchFilmTitle() {
    try {
      const root = "https://swapi.co/api";
      const random = Math.floor(Math.random() * 6 + 1);
      const filmData = await doFetch(`${root}/films/${random}`);
      const filmTitle = filmData.title
      this.setState({ filmTitle });
    } catch (error) {
      this.setState({ filmTitleError: error.message });
    }
  };

  // apicall.js
  export const doFetch = async url => {
    try {
      const response = await fetch(url);
      if (!response.ok) {
        throw new Error(`${response.status}`);
      }
      return await response.json();
    } catch (error) {
      throw new Error(`Network request failed. (error: ${error.message})`);
    }
  };
```

- jQuery: \$.get()

```
$.get("https://opentdb.com/api.php?amount=1&category=27&type=multiple")
  .then(data => /* do something if data is returned */ )
  .catch(error => /* do something if an error is returned */ )
```

---

# **_Selection_**

- `document.getElementsByClassName(‘className’);`
  - returns a nodelist of elements match that selection
  - returns a live result of any updates
- `document.querySelector(‘.cssSelector);`
  - returns the first match in the document
- `document.querySelectorAll(‘.cssSelector);`
  - returns a nodelist of all matches in the document
  - returns a static result with the original items
- `document.querySelectorAll(‘.cssSelector li:first-child);`
  - returns the first list item of an element with the class .cssSelector

---

# _Service workers_

- https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API
- A script that your browser runs in the background, separate from a web page, opening the door to features that don't need a web page or user interaction
  - push notifications and background sync
- Act as proxy servers that sit between web applications, the browser, and the network
- Enables the creation of effective offline experiences
- Intercepts network requests and take appropriate action based on whether the network is available, and update assets residing on the server

---

# _Online and offline_

- https://developer.mozilla.org/en-US/docs/Web/API/NavigatorOnLine/Online_and_offline_events

* `navigator.onLine`
  - maintains a `true`/`false` value
    - `true` for online
    - `false` for offline

---

# _Other_

**Graphics & Topography:**
Canvas
Web Animations

**Interaction, Events, & Messaging:**
Battery Status
Clipboard API & Events
Cross Document Messaging
Device & Screen Orientation
Full screen
Geolocation
Media Capture
Notifications
Touch Events
Vibration

**Storage & Files:**
Blob URLS
File API
File Reader
IndexedDB

**Real-time Communication:**
Push API
Server-Sent Events
Web Sockets

**Web Components:**
Custom Elements
Shadow DOM
Templates

**Performance Optimization & Analysis:**
High Resolution Time
Navigation Timing
Page Visibility
User Timing
Web Workers

**Security & Privacy:**
Content Security Policy
Referrer Policy
Web Cryptography

**Miscellaneous Features:**
scripts: async & defer
contentEditable
Drag & Drop
History
Promises
Service Workers

- DOMevents

---
