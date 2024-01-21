# freeCodeCamp Back End Development and APIs Notes

- I had trouble getting the tests to pass using GitHub pages or Replit or Netlify for static hosting. glitch.com seems to work though

## 2 - Start a Working Express Server

In the first two lines of the file myApp.js, you can see how easy it is to create an Express app object. 

```js
let express = require('express');
let app = express();
```

This object has several methods. One fundamental method is app.listen(port). It tells your server to listen on a given port, putting it in running state. For testing reasons, we need the app to be running in the background so we added this method in the server.js file for you.

In Express, routes takes the following structure: `app.METHOD(PATH, HANDLER)`
- METHOD is an http method in lowercase
- PATH is a relative path on the server (string or regex)
- HANDLER is a function that Express calls when the route is matched `function(req, res) {...}`

### Use the app.get() method to serve the string "Hello Express" to GET requests matching the / (root) path

```js
...
app.get('/', (req, res) => {
    res.send("Hello Express");
});
```

## Serve an HTML File

You can respond to requests with a file using the `res.sendFile(path)` method. You can put it inside the app.get('/', ...) route handler
- Behind the scenes, this method will set the appropriate headers to instruct your browser on how to handle the file you want to send, according to its type. Then it will read and send the file.
- This method needs an absolute file path, such using the Node global variable `__dirname`

```js
const absolute path = __dirname + '/relative/path/file.txt'
```

### Send the `/views/index.html` file as a response to `GET` requests to the `/` path.

```js
app.get('/', (req, res) => {
  const absolutePath = __dirname + '/views/index.html';
  res.sendFile(absolutePath)
})
```

## Serve Static Assets
An HTML server usually has one or more directories that are accessible by the user. You can place there the static assets needed by your application (stylesheets, scripts, images).

In Express, you can put in place this functionality using the middleware express.static(path), where the path parameter is the absolute path of the folder containing the assets.

Middleware are functions that intercept route handlers, adding some kind of information. A middleware needs to be mounted using the method `app.use(path, middlewareFunction)`
- The first `path` argument is optional. If you don’t pass it, the middleware will be executed for all requests

### Mount the express.static() middleware to the path /public with app.use()

The absolute path to the assets folder is __dirname + /public.

```js
const absPath = __dirname + '/public';
app.use('/public', express.static(absPath))
```

## Serve JSON on a Specific Route

While an HTML server serves HTML, an API serves data.

The client only needs to know where the resource is (the URL), and the action it wants to perform on it (the verb)

### Serve the object {"message": "Hello json"} as a response, in JSON format, to GET requests to the /json route

Inside the route handler, use the method res.json()

```js

```
