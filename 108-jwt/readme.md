# JSON Web Token (JWT)

**JSON Web Token (JWT)** is a compact, URL-safe means of representing claims to be transferred between two parties. The claims in a JWT are encoded as a JSON object that is used as the payload of a JSON Web Signature (JWS) structure or as the plaintext of a JSON Web Encryption (JWE) structure, enabling the claims to be digitally signed or integrity-protected with a Message Authentication Code (MAC) and/or encrypted.

### Structure of JWT

A JWT is composed of three parts separated by dots (`.`):

1. **Header**
2. **Payload**
3. **Signature**

**1. Header**

The header typically consists of two parts:

- **Type of token**, which is JWT.
- **Signing algorithm** being used, such as HMAC SHA256 or RSA.

Example:

```json
{
  "alg": "HS256",
  "typ": "JWT"
}
```

This JSON is Base64Url encoded to form the first part of the JWT.

**2. Payload**

The payload contains the claims. Claims are statements about an entity (typically, the user) and additional data. There are three types of claims:

- **Registered claims:** A set of predefined claims which are not mandatory but recommended to provide a set of useful, interoperable claims. Examples include `iss` (issuer), `exp` (expiration time), `sub` (subject), and `aud` (audience).
- **Public claims:** These can be defined at will by those using JWTs. To avoid collisions, they should be defined in the IANA JSON Web Token Registry or be defined as a URI that contains a collision-resistant namespace.
- **Private claims:** These are custom claims created to share information between parties that agree on using them.

Example:

```json
{
  "sub": "1234567890",
  "name": "John Doe",
  "admin": true
}
```

This JSON is Base64Url encoded to form the second part of the JWT.

**3. Signature**

To create the signature part, you have to take the encoded header, the encoded payload, a secret, the algorithm specified in the header, and sign that.

For example, if you want to use the HMAC SHA256 algorithm, the signature will be created in the following way:

```
HMACSHA256(
  base64UrlEncode(header) + "." +
  base64UrlEncode(payload),
  secret
)
```

The signature is used to verify that the sender of the JWT is who it says it is and to ensure that the message wasn't changed along the way.

### Advantages of JWT

1. **Compact:** JWTs are compact in size, which makes them ideal for being passed around in HTML and HTTP environments.
2. **Self-contained:** JWTs carry all the required information about the user, reducing the need to query the database multiple times.
3. **Stateless:** Since the token is self-contained, the server does not need to store session information, making it easier to scale and maintain.
4. **Security:** The tokens are signed using a secret or a public/private key pair, making it possible to verify the token's authenticity and integrity.

### Disadvantages of JWT

1. **Revocation:** Once a JWT is issued, it is valid until it expires. If there is a need to revoke a token before its expiration, it becomes more complex since JWTs are stateless.
2. **Size:** JWTs can become large, especially if they include many claims. This can be an issue for some applications with strict size constraints.
3. **Exposure:** If a JWT is compromised, it can be used by anyone until it expires. Proper security measures (e.g., HTTPS, secure storage) must be in place to protect the JWT.
4. **Complexity:** Implementing JWT securely can be complex, requiring careful handling of secrets and algorithms.

### Example of a JWT

Here is a complete example of a JWT:

**Header:**

```json
{
  "alg": "HS256",
  "typ": "JWT"
}
```

**Payload:**

```json
{
  "sub": "1234567890",
  "name": "John Doe",
  "admin": true,
  "iat": 1516239022
}
```

**Secret:**

```
my-secret-key
```

**JWT:**

```
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiYWRtaW4iOnRydWUsImlhdCI6MTUxNjIzOTAyMn0.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c
```

This JWT can be used to authenticate a user and verify their claims in a secure and stateless manner.
