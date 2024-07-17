# Built-In Middleware

#### Node.js Built-In Middleware

Node.js itself does not come with built-in middleware functions for HTTP handling. Middleware functions in Node.js are typically created manually or using additional libraries. However, the `http` module in Node.js provides basic mechanisms for handling HTTP requests and responses, which can be used to build custom middleware.

For example, Node.js does not have built-in middleware like Express, but you can create middleware-like functions manually:

```javascript
const http = require("http");

// Custom middleware function
function logRequests(req, res, next) {
  console.log(`${req.method} ${req.url}`);
  next();
}

// Simple server using custom middleware
const server = http.createServer((req, res) => {
  logRequests(req, res, () => {
    res.writeHead(200, { "Content-Type": "text/plain" });
    res.end("Hello, world!");
  });
});

server.listen(3000, () => {
  console.log("Server listening on port 3000");
});
```

#### Express.js Built-In Middleware

Express.js provides a set of built-in middleware functions that handle common tasks such as parsing request bodies, serving static files, and more. Here are some of the most commonly used built-in middleware functions in Express:

1. **express.json()**

   Parses incoming requests with JSON payloads. It is used to handle `application/json` content type.

   ```javascript
   const express = require("express");
   const app = express();

   app.use(express.json());

   app.post("/data", (req, res) => {
     res.send(req.body);
   });

   app.listen(3000, () => {
     console.log("Server listening on port 3000");
   });
   ```

2. **express.urlencoded()**

   Parses incoming requests with URL-encoded payloads. It is used to handle `application/x-www-form-urlencoded` content type.

   ```javascript
   const express = require("express");
   const app = express();

   app.use(express.urlencoded({ extended: true }));

   app.post("/data", (req, res) => {
     res.send(req.body);
   });

   app.listen(3000, () => {
     console.log("Server listening on port 3000");
   });
   ```

3. **express.static()**

   Serves static files from a directory. It is used to serve files such as HTML, CSS, JavaScript, and images.

   ```javascript
   const express = require("express");
   const app = express();

   app.use(express.static("public"));

   app.listen(3000, () => {
     console.log("Server listening on port 3000");
   });
   ```

4. **express.Router()**

   Not exactly middleware, but a built-in utility for creating modular, mountable route handlers. It can be used to define routes and middleware for specific subsets of your application.

   ```javascript
   const express = require("express");
   const app = express();
   const router = express.Router();

   router.get("/", (req, res) => {
     res.send("Hello from the router!");
   });

   app.use("/router", router);

   app.listen(3000, () => {
     console.log("Server listening on port 3000");
   });
   ```

5. **express.Application#use()**

   A method that adds middleware to the application. This method is used to apply built-in middleware as well as custom middleware functions.

   ```javascript
   const express = require("express");
   const app = express();

   app.use(express.json());
   app.use(express.static("public"));

   app.listen(3000, () => {
     console.log("Server listening on port 3000");
   });
   ```

### Summary

- **Node.js** does not have built-in middleware like Express but allows for custom middleware creation using its `http` module.
- **Express.js** provides several built-in middleware functions for common tasks such as parsing request bodies (`express.json()`, `express.urlencoded()`) and serving static files (`express.static()`).

By leveraging these built-in middleware functions, you can efficiently handle various aspects of web development and streamline your server-side code.
