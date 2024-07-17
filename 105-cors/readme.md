# CORS

### What is CORS?

**CORS** (Cross-Origin Resource Sharing) is a security feature implemented by web browsers to control how resources on a web server can be requested from a different origin (domain, protocol, or port) than the one from which the resource originated. This mechanism helps prevent malicious websites from making unauthorized requests to other websites on behalf of the user.

### How CORS Works

When a web application running in a browser makes a request to a server on a different origin (cross-origin request), the browser sends an HTTP request with an `Origin` header indicating the origin of the request. The server can then decide whether to allow or deny the request based on the value of this `Origin` header.

### CORS Request Flow:

1. **Preflight Request (OPTIONS)**

   - For certain types of requests (e.g., those with custom headers or methods other than GET, POST, or HEAD), the browser sends an initial "preflight" request using the HTTP `OPTIONS` method. This preflight request checks with the server if the actual request is allowed.
   - The server responds with the allowed methods, headers, and other information in the `Access-Control-Allow-*` headers.

2. **Actual Request**

   - If the preflight request is successful and the server responds with the appropriate headers, the browser then sends the actual request (e.g., GET, POST) to the server.

3. **Server Response**
   - The server includes specific CORS headers in its response to indicate whether the request is allowed or denied.

### Key CORS Headers:

- **`Access-Control-Allow-Origin`**: Specifies which origins are allowed to access the resource. It can be a specific origin or `*` (allow all origins).

  ```http
  Access-Control-Allow-Origin: http://example.com
  ```

- **`Access-Control-Allow-Methods`**: Specifies the HTTP methods that are allowed when accessing the resource.

  ```http
  Access-Control-Allow-Methods: GET, POST, PUT
  ```

- **`Access-Control-Allow-Headers`**: Specifies the headers that can be used in the actual request.

  ```http
  Access-Control-Allow-Headers: Content-Type, Authorization
  ```

- **`Access-Control-Allow-Credentials`**: Indicates whether credentials (like cookies or HTTP authentication) are allowed to be sent with the request.

  ```http
  Access-Control-Allow-Credentials: true
  ```

- **`Access-Control-Expose-Headers`**: Specifies which headers can be exposed to the browser.

  ```http
  Access-Control-Expose-Headers: X-Custom-Header
  ```

- **`Access-Control-Max-Age`**: Specifies how long the results of a preflight request can be cached.

  ```http
  Access-Control-Max-Age: 3600
  ```

### Example Scenario

Suppose you have a frontend application hosted on `http://frontend.example.com` and a backend API on `http://api.example.com`. If your frontend makes a request to the backend API, the browser will perform a CORS check.

If the backend server includes the following headers in its response:

```http
Access-Control-Allow-Origin: http://frontend.example.com
Access-Control-Allow-Methods: GET, POST
Access-Control-Allow-Headers: Content-Type
```

The browser will allow the request to proceed. If the server does not include these headers or does not include the correct values, the browser will block the request and report a CORS error.

### CORS in Express.js

In an Express.js application, you can handle CORS by using the `cors` middleware.

**Installation:**

```bash
npm install cors
```

**Usage:**

```javascript
const express = require("express");
const cors = require("cors");
const app = express();

app.use(cors()); // Enable CORS for all routes

app.get("/", (req, res) => {
  res.send("Hello World");
});

app.listen(3000, () => {
  console.log("Server running on http://localhost:3000");
});
```

You can also configure the `cors` middleware to allow requests only from specific origins or to allow specific HTTP methods and headers.

### Summary

- **CORS** is a security feature that controls how resources on a server can be accessed from different origins.
- **Preflight requests** are sent for certain types of cross-origin requests to check if the server allows them.
- **CORS headers** such as `Access-Control-Allow-Origin`, `Access-Control-Allow-Methods`, and `Access-Control-Allow-Headers` are used to specify which origins, methods, and headers are allowed.
- **Express.js** uses the `cors` middleware to manage CORS policies.
