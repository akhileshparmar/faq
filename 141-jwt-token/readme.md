# What is a JWT?

**JWT** stands for **JSON Web Token**. It is an open standard (RFC 7519) used for securely transmitting information between parties as a JSON object. This information can be verified and trusted because it is digitally signed. JWTs can be signed using a secret (with the HMAC algorithm) or a public/private key pair using RSA or ECDSA.

### What is a Token?

A **token** is a piece of data that represents some authentication or authorization information. In web development, tokens are often used as a mechanism for verifying the identity of a user or for providing access to certain resources or services.

### How JWTs are Created

1. **Header**: The header typically consists of two parts: the type of the token (i.e., JWT) and the signing algorithm being used, such as HMAC SHA256 or RSA.

2. **Payload**: The payload contains the claims. Claims are statements about an entity (typically, the user) and additional metadata. There are three types of claims: registered, public, and private claims.

3. **Signature**: To create the signature part, you have to take the encoded header, the encoded payload, a secret, and sign that.

### Breakdown of a JWT

A JWT consists of three parts separated by dots (`.`):

```
Header.Payload.Signature
```

#### 1. **Header**

The header typically contains two fields:

- **`alg`**: The signing algorithm being used, like `HS256`.
- **`typ`**: The type of token, which is `JWT`.

Example of a header:

```json
{
  "alg": "HS256",
  "typ": "JWT"
}
```

This header is then Base64Url encoded to form the first part of the JWT.

#### 2. **Payload**

The payload contains the claims. Claims are statements about an entity (typically, the user) and additional data. There are three types of claims:

- **Registered Claims**: These are a set of predefined claims which are not mandatory but recommended. Some examples are `iss` (issuer), `exp` (expiration time), `sub` (subject), and `aud` (audience).
- **Public Claims**: These can be defined at will but should be collision-resistant or be defined in the IANA JSON Web Token Registry.
- **Private Claims**: These are the custom claims created to share information between parties that agree to use them.

Example of a payload:

```json
{
  "sub": "1234567890",
  "name": "John Doe",
  "admin": true
}
```

This payload is then Base64Url encoded to form the second part of the JWT.

#### 3. **Signature**

To create the signature part, you take the encoded header, the encoded payload, a secret, the algorithm specified in the header, and sign that.

For example, if you use the HMAC SHA256 algorithm, the signature will be created in this way:

```
HMACSHA256(
  base64UrlEncode(header) + "." +
  base64UrlEncode(payload),
  secret)
```

The output will be a string which is the final part of the JWT.

### Full JWT Example

Suppose we have the following header and payload:

- **Header**:
  ```json
  {
    "alg": "HS256",
    "typ": "JWT"
  }
  ```
- **Payload**:

  ```json
  {
    "sub": "1234567890",
    "name": "John Doe",
    "admin": true
  }
  ```

- **Secret**: `mysecretkey`

Then the JWT will be generated as follows:

- **Header**: Encoded to `eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9`
- **Payload**: Encoded to `eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiYWRtaW4iOnRydWV9`
- **Signature**: Created by signing `eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiYWRtaW4iOnRydWV9` using `mysecretkey` and the algorithm `HS256`, which will result in something like `s3pPLMBiTxaQ9kYGzzhZRbK+xOo=`.

The final JWT will be:

```
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiYWRtaW4iOnRydWV9.s3pPLMBiTxaQ9kYGzzhZRbK+xOo=
```

### How JWTs are Used

- **Authentication**: After a user logs in, a JWT is returned and stored (usually in localStorage or a cookie) on the client-side. On subsequent requests, the client includes this token in the Authorization header.
- **Authorization**: JWTs are often used to check if a user is allowed to perform certain actions. The token is decoded, and the claims are checked to determine the user’s roles or permissions.

- **Stateless Sessions**: Since the server does not need to store any session data, JWTs are often used in stateless authentication systems.

### Important Considerations

- **Security**: While JWTs are signed, they are not encrypted by default. Sensitive information should not be stored in the payload unless the token is encrypted.
- **Expiration**: It is crucial to set expiration (`exp`) claims to limit the validity of the token and mitigate the risks of token theft.

JWTs provide a compact, URL-safe way of representing claims between two parties and are widely used in modern web applications for authentication and authorization.
