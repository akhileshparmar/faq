# Authentication Mechanisms

There are several authentication mechanisms that can be used in Node.js applications, each with its own strengths and use cases. Here are some of the most common methods:

### 1. **Basic Authentication**

**Description:**  
Basic Authentication uses HTTP headers to pass credentials (username and password) encoded in Base64.

**Implementation:**

- The client sends an HTTP request with the Authorization header containing the word Basic followed by a space and a base64-encoded string username:password.
- The server decodes and validates the credentials.

**Use Case:**  
Simple and quick to implement for internal or low-security applications.

**Example:**

```js
const express = require("express");
const app = express();

app.use((req, res, next) => {
  const authHeader = req.headers.authorization;
  if (authHeader) {
    const base64Credentials = authHeader.split(" ")[1];
    const credentials = Buffer.from(base64Credentials, "base64").toString(
      "ascii"
    );
    const [username, password] = credentials.split(":");

    // Validate username and password
    if (username === "admin" && password === "password") {
      return next();
    }
  }
  res.setHeader("WWW-Authenticate", "Basic");
  res.sendStatus(401);
});

app.get("/", (req, res) => {
  res.send("Authenticated!");
});

app.listen(3000);
```

### 2. **Token-Based Authentication (JWT)**

**Description:**  
Token-based authentication uses JSON Web Tokens (JWT) to maintain user sessions in a stateless manner.

**Implementation:**

- The client sends credentials to obtain a token.
- The server issues a signed JWT.
- The client includes the JWT in the Authorization header for subsequent requests.

**Use Case:**  
Widely used for modern web applications, especially SPAs and mobile apps.

**Example:**

```js
const jwt = require("jsonwebtoken");
const express = require("express");
const app = express();
const secretKey = "your_secret_key";

app.post("/login", (req, res) => {
  // Authenticate user
  const token = jwt.sign({ userId: 1 }, secretKey, { expiresIn: "1h" });
  res.json({ token });
});

app.use((req, res, next) => {
  const token = req.headers.authorization.split(" ")[1];
  try {
    const decoded = jwt.verify(token, secretKey);
    req.user = decoded;
    next();
  } catch (err) {
    res.sendStatus(401);
  }
});

app.get("/", (req, res) => {
  res.send("Authenticated!");
});

app.listen(3000);
```

### 3. **OAuth 2.0**

**Description:**  
OAuth 2.0 is an authorization framework that enables third-party applications to obtain limited access to user accounts on an HTTP service.

**Implementation:**

- The client obtains an access token from an OAuth provider.
- The client uses the access token to access protected resources.

**Use Case:**  
Used for third-party integrations, social logins, and APIs requiring delegated access.

**Example:**

- Using Passport.js with a provider like Google or GitHub.

### 4. **Session-Based Authentication**

**Description:**  
Session-based authentication uses server-side sessions to maintain user state.

**Implementation:**

- The server creates a session for the authenticated user and stores it in memory or a database.
- A session ID is sent to the client in a cookie.
- The client sends the session ID cookie in subsequent requests.

**Use Case:**  
Traditional web applications, especially when maintaining state server-side.

**Example:**

```js
const express = require("express");
const session = require("express-session");
const app = express();

app.use(
  session({
    secret: "your_secret_key",
    resave: false,
    saveUninitialized: true,
  })
);

app.post("/login", (req, res) => {
  // Authenticate user
  req.session.userId = 1;
  res.send("Logged in");
});

app.use((req, res, next) => {
  if (req.session.userId) {
    next();
  } else {
    res.sendStatus(401);
  }
});

app.get("/", (req, res) => {
  res.send("Authenticated!");
});

app.listen(3000);
```

### 5. **OpenID Connect**

**Description:**  
OpenID Connect (OIDC) is an authentication layer on top of OAuth 2.0, allowing clients to verify the identity of users.

**Implementation:**

- The client redirects the user to the OpenID provider for authentication.
- The provider sends an ID token to the client upon successful authentication.

**Use Case:**  
Used for single sign-on (SSO) and identity federation.

**Example:**

- Using Passport.js with an OpenID Connect provider.

### 6. **Multi-Factor Authentication (MFA)**

**Description:**  
MFA requires users to provide multiple forms of verification to gain access.

**Implementation:**

- Combine any primary authentication method (e.g., password) with secondary factors (e.g., OTP, biometrics).

**Use Case:**  
Enhancing security for sensitive applications and data.

**Example:**

- Implementing TOTP (Time-based One-Time Password) with libraries like `otplib`.

### Summary

| Authentication Method | Description                                     | Use Case                                       |
| --------------------- | ----------------------------------------------- | ---------------------------------------------- |
| Basic Authentication  | Simple, uses HTTP headers for credentials.      | Internal or low-security applications.         |
| Token-Based (JWT)     | Stateless, uses tokens for session management.  | Modern web and mobile applications.            |
| OAuth 2.0             | Authorization framework for third-party access. | Third-party integrations, social logins.       |
| Session-Based         | Server-side session storage with cookies.       | Traditional web applications.                  |
| OpenID Connect (OIDC) | Authentication layer on top of OAuth 2.0.       | Single sign-on (SSO), identity federation.     |
| Multi-Factor (MFA)    | Requires multiple forms of verification.        | Enhancing security for sensitive applications. |

Each authentication method has its specific use cases and implementation details, providing flexibility in securing different types of Node.js applications.
