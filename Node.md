# _Node_

- https://nodejs.org/en/
- https://nodejs.org/en/docs/
- Allows JavaScript to run in a non-browser context

* A server is a computer or program that handles sending, retrieving, and manipulating resources for a client
* An HTTP Server handles any network requests by providing responses that can be HTML pages, files, data, etc to the browser (client)
* Endpoints (e.g. `https://www.turing.io/api/v1/curriculum/`) are created by the back-end developers on a team to help the front-end developers access and interact with application data on a server

---

# _Modules_

- If you want to access built-in functionality, you have to ask the module system for it
- The CommonJS module system, based on the `require` function, is built into Node
- It is used to load anything from built-in modules, to downloaded packages, to files that are part of your own program

## _URL_

- ` const`` ``url`` ``=`` ``require``(``'url'``); `

## _**File System**_

- Exports functions for working with files and directories
- To read a file, use `fs.readFileSync('/path/to/file')`
  - Returns a `Buffer` object containing the complete contents of the file
    - `Buffer` objects are Node's way of efficiently representing arbitrary arrays of data, whether it be ascii, binary or some other format
    - Can be converted to strings by simply calling the `toString()` method on them

### Methods

- `readFile` reads a file and then calls a callback with the file’s contents

```
let {readFile} = require("fs");

readFile("file.txt", "utf8", (error, text) => {
  if (error) throw error;
  console.log("The file contains:", text);
});
```

- `writeFile` writes a file to the disk

```
const {writeFile} = require("fs");

writeFile("graffiti.txt", "Node was here", err => {
  if (err) console.log(`Failed to write file: ${err}`);
  else console.log("File written.");
});
```

- `readdir` will return the files in a directory as an array of strings
- `stat` will retrieve information about a file
- `rename` will rename a file
- `unlink` will remove a file

## _http_

- ` const`` ``http`` ``=`` ``require``(``'http'``); `
- Provides functionality for running HTTP servers and making HTTP requests
- When the server receives a request from a client, a “request” event is emitted, and the server responds with a simple HTTP response

* `createServer()`
  - `const server = http.createServer();`
  - The `http.createServer` module inherits from `EventEmitter`
  - Listens and responds to particular events, such as requests from a client
    - response
      - `response.writeHead(statusCode[, statusMessage][, headers])`
        - Sends a response header to the request
      - `response.write(chunk[, encoding][, callback])`
        - Sends a chunk of the response body
      - `response.end([data][, encoding][, callback])`
        - Signals to the server that all of the response headers and body have been sent
        - The server should consider this message complete
        - Must be called on each response

- To start an HTTP server:

```
const {createServer} = require("http");

const server = createServer((request, response) => {
  response.writeHead(200, {"Content-Type": "text/html"});
  response.write(`
    <h1>Hello!</h1>
    <p>You asked for <code>${request.url}</code></p>`);
  response.end();
});
server.listen(8000);
console.log("Listening! (port 8000)");
```

- Headers

  - The headers of a request or response allow the client and the server to pass additional information about the request/response to each other.
  - Think of headers as metadata that allow a client or server to handle the request/response properly
  - A hash of key-value pairs:
    - `{ "Content-Type": "text-html" }`
  - `Accept`

    - Allows you to set what media types are acceptable
      - `Accept: application/json`

  - `Content-Length`
    - Indicates the length of the body
    - Measured in bytes
  - `Status code`
    - Tells us what happened to our request

- Body
  - Send a body with your request so that the server can parse the data in it and update a resource based on the resulting body object
  - When the resource is successfully updated, the server will send a response with a status code of `200`, and usually a body object that contains the entire resource, reflecting the new changes that were just made

## _crypto_

- `randomBytes`
  - Run synchronously with callbacks
  - `const { randomBytes } = require('crypto');`

## _util_

- `promisify`
  - Turns synchronous function into asynchronous promises
  - `const { promisify } = require('util');`

```
const randomBytesPromiseified = promisify(randomBytes);
const resetToken = (await randomBytesPromiseified(20)).toString('hex');
```

---

# _Bindings_

- `Process` binding
  - Provides various ways to inspect and manipulate the current program.
  - The `exit` method ends the process and can be given an exit status code, which tells the program that started `node` whether the program completed successfully (code zero) or encountered an error (any other code)
  - To find the command-line arguments given to your script, you can read `process.argv`, which is an array of strings
- `Console` binding
  - The `console.log` method prints out a piece of text to the process’s standard output stream
  - When running `node` from the command line, you see the logged values in your terminal

---

# _Streams_

## Writable streams

- Such objects have a `write` method that can be passed a string or a `Buffer` object to write something to the stream
- Their `end` method closes the stream and optionally takes a value to write to the stream before closing
- Both of these methods can also be given a callback as an additional argument, which they will call when the writing or closing has finished

## Readable streams

- Both the `request` binding that was passed to the HTTP server’s callback and the `response` binding passed to the HTTP client’s callback are readable streams
- A server reads requests and then writes responses, whereas a client first writes a request and then reads a response
- Reading from a stream is done using event handlers, rather than methods.

---

# _Clustering_

- [https://nodejs.org/api/cluster.html](https://nodejs.org/api/cluster.html#cluster_how_it_works)
- By default, Node runs on a single CPU core
- In production, if your app is running on a machine with multiple cores, you should start a different Node process for each core

---

# _Misc_

- To execute your program:
  - `node filename.js`
  - If you run `node` without giving it a file, it provides you with a prompt at which you can type JavaScript code and immediately see the result
- To load a "global" module:
  - `var fs = require('module')`

## **Idiomatic node convention**

- `(err, data)`
- This convention stipulates that unless there's an error, the first argument passed to the callback will be null, and the second will be your data.

```
function bar (callback) {
  foo(function (err, data) {
    if (err)
      return callback(err) // early return

        // ... no error, continue doing cool things with `data`

        // all went well, call callback with `null` for the error argument

        callback(null, data)
  })
}
```

---

# _Resources_

## Best Practices

- https://github.com/i0natan/nodebestpractices

---
