# _Express_

- https://expressjs.com/en/4x/api.html
- `npm install express`--save``

- `const express = require('express');`

- Enables you to create a web server that is more readable, flexible, and maintainable than you would be able to create using only the Node HTTP library
- A small framework built on top of the web server functionality provided by Node.js
- Helps to simplify and organize the server-side functionality of your application by providing abstractions over the more confusing parts of Node.js, and adding helpful utilities and features

---

# _Server_

## App

- `const app = express();`

- `app.listen()`
  - Tells the server to start listening for connections on a particular port
  - When the server is ready to listen for connections, the callback is called

```
app.listen(3000, () => {
  console.log('Express Intro running on localhost:3000');
});
```

- `app.get()`
  - Creates a route handler to listen for `GET` requests from a client

```
app.get('/', (request, response) => {
  response.send('hello world');
});
```

    * The first argument in this function is the route path
        * In this case, we’re listening for GET requests on `localhost:3000/`
    * The second argument is a callback function that takes a request object and a response object

- `app.post()`
  - Creates a route handler to listen for POST requests from a client

## Request object

- Contains information about the request that came from the client (request headers, query parameters, request body, etc.)

* `request.params`
  - Allow you to access dynamic endpoint

```
app.get('/api/v1/messages/:id', (request, response) => {
  const { id } = request.params;
  const message = app.locals.messages.find(message => message.id === id);
  return response.status(200).json(message);
});
```

## Response object

- Contains information that we want to send as a response back to the client
  - Also has functions that enable us to send a response

* `response.send()`
  - Sends the HTTP response with content in the body of the response

- `response.status()`
  - sets that status in the header

* `response.sendStatus()`
  - sends the status immediately
  - mainly for 404 and 500 errors

- `response.sendFile()`
  - Transfers the file at the given `path`
  - `.sendFile('/sunsets.html', { root: __dirname + '/public/' });`

* `response.json()`
  - Short hand for setting the response type as `application/json`
  - Automatically serializes our object as JSON

---

# _Serving Static assets_

- Static assets are any content that can be delivered to an end user without having to be generated, modified, or processed
- Most HTML, CSS, images, and client-side JavaScript files

## Serve HTML

- For Express to know that the `index.html` file is in the public directory, we have to configure the static assets path
  - `app.use(express.static('public'))`
  - `app.use()` configures your application to use a middleware function
    - For every request to the server, it runs the function passed in, like a callback function
    - `express.static('public')` defines the path to your static assets
    - `'public'` refers to the directory where your static files are stored

```
const express = require('express');
const app = express();

app.use(express.static('public'));
app.get('/', (request, response) => {
  // We don't need to explicitly use this handler or send a response
  // because Express is using the default path of the static assets
  // to serve this content
});
app.listen(3000, () => {
  console.log('Express Intro running on localhost:3000');
});
```

## Serve JSON

```
app.get('/json', (request, response) => {
  // Respond with JSON data here
  response.status(200).json({"name": "Robbie"});
});
```

---

# _Middleware_

- https://expressjs.com/en/guide/using-middleware.html

- With plain Node `http`, you create a single function to handle all requests
  - This single function can get large and unwieldy as your application grows in complexity
- Express middleware allows you to break this single function into many smaller functions that only handle one thing at a time
- Functions that run after a request is received but before the route handler function (i.e. `app.get()`)
- They have access to the request object, response object, and a function called `next` to pass control to the next middleware function, or to the route handler

```
// Middleware functions
const middlewareFuncName = (request, response, next) => {
  // Middleware code to run here

  // Move on to next middleware function or the route handler
  next();
};

// Add the middleware as a callback in the route handler
app.get('/json', middlewareFuncName, (request, response) => {
  response.status(200).json({"name": "Robbie"});
});
```

- To ensure every route uses the middleware functions:
  - `app.use(middlewareFuncName);`
- Now you don’t have to specify the callback functions for every single route handler

```
// Middleware functions
const middlewareFuncName = (request, response, next) => {
  // Middleware code to run here

  // Move on to next middleware function or the route handler
  next();
};

`app.use(middlewareFuncName);`

// Add the middleware as a callback in the route handler
app.get('/json', (request, response) => {
  response.status(200).json({"name": "Robbie"});
});
```

- Logs the request URL to the terminal:

```
const urlLogger = (request, response, next) => {
  console.log('Request URL:', request.url);
  next();
};
```

- Logs the time that a client requests a page from the server

```
const timeLogger = (request, response, next) => {
  console.log('Datetime:', new Date(Date.now()).toString());
  next();
};
```

## body-parser

- `npm i body-parser --save`
- Parses the body of an HTTP request

* `const bodyParser = require('body-parser');`
* `app.use(bodyParser.json());`
* `app.use(bodyParser.urlencoded({ extended: true }));`

---

# _Boilerplate_

```
const express = require('express');
const app = express();
const environment = process.env.NODE_ENV || 'development';
const configuration = require('./knexfile')[environment];
const database = require('knex')(configuration);
const bodyParser = require('body-parser');
// const cors = require('express-cors');
// const path = require('path');
// const enforce = require('express-sslify');
// const environment = process.env.NODE_ENV || 'development';

app.set('port', process.env.PORT || 5000);
app.use(bodyParser.json());
app.use(bodyParser.urlencoded({ extended: true }));

// app.use(enforce.HTTPS({ trustProtoHeader: true }));
// app.use(cors());
// app.use(function(req, res, next) {
//   res.header('Access-Control-Allow-Origin', '*');
//   res.header('Access-Control-Allow-Methods', '*');
//   res.header(
//     'Access-Control-Allow-Headers',
//     'Origin, X-Requested-With, Content-Type, Accept'
//   );
//   next();
// });

if (process.env.NODE_ENV === 'production') {
  // Serve any static files
  app.use(express.static(path.join(__dirname, 'client/build')));
  // Handle React routing, return all requests to React app
  // app.get('*', (req, res) => {
  //   res.sendFile(path.join(__dirname, 'client/build', 'index.html'));
  // });
} else {
  // Serve any static files
  app.use(express.static('public'));
}

app.listen(app.get('port'), () => {
  // eslint-disable-next-line
  console.log(`Server is running on ${app.get('port')}`);
});

module.exports = app;
```

---

# _Generator_

- https://expressjs.com/en/starter/generator.html
- Use the application generator tool, `express-generator`, to quickly create an application skeleton
- `npm install express-generator -g`
- `express myapp`--view=pug``
- `express myapp`--no-view``

---

# _Misc_
