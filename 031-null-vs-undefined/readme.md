# null vs undefined

In JavaScript, `null` and `undefined` are both primitive values that represent the absence of value, but they are used in different contexts and have distinct meanings:

### `null`

- **Type**: `object` (though this is considered a historical bug in JavaScript)
- **Purpose**: Represents the intentional absence of any object value.
- **Use Case**: Typically assigned to a variable to indicate that it does not currently hold a value, but might later.
- **Example**:
  ```javascript
  let foo = null;
  console.log(foo); // Output: null
  ```

### `undefined`

- **Type**: `undefined`
- **Purpose**: Indicates that a variable has been declared but has not yet been assigned a value.
- **Use Case**:
  - Default value for uninitialized variables.
  - Returned by functions if they do not explicitly return a value.
  - Indicates missing properties on objects or elements in arrays.
  - Used as the default value for function parameters that are not provided.
- **Example**:

  ```javascript
  let bar;
  console.log(bar); // Output: undefined

  function baz() {}
  console.log(baz()); // Output: undefined

  const obj = {};
  console.log(obj.missingProperty); // Output: undefined
  ```

### Key Differences

- **Intentional vs Unintentional**: `null` is used to explicitly indicate the absence of value. `undefined` typically indicates that something has not been initialized or is missing.
- **Assignment**: `null` is assigned by the programmer to indicate "no value". `undefined` is usually the default state of variables or properties that have not been assigned a value.
- **Type**: `null` is of type `object`. `undefined` is of type `undefined`.

### Comparison

- **Equality (`==`)**: `null` and `undefined` are equal (`==`) to each other but not to any other value.
  ```javascript
  console.log(null == undefined); // Output: true
  ```
- **Identity (`===`)**: `null` and `undefined` are not strictly equal (`===`) to each other or any other value.
  ```javascript
  console.log(null === undefined); // Output: false
  ```

### Examples of Use

- **`null`**:
  ```javascript
  let user = {
    name: "Alice",
    age: 30,
    address: null, // We know that user does not have an address yet.
  };
  ```
- **`undefined`**:

  ```javascript
  let user;
  console.log(user); // Output: undefined

  function getUserInfo() {}
  console.log(getUserInfo()); // Output: undefined

  let settings = {
    theme: "dark",
  };
  console.log(settings.language); // Output: undefined
  ```

Understanding the differences between `null` and `undefined` helps in writing clearer, more predictable JavaScript code and can aid in debugging issues related to uninitialized or missing values.

Here's a tabular comparison of `null` and `undefined` in JavaScript:

| Feature                    | `null`                                                   | `undefined`                                                                                  |
| -------------------------- | -------------------------------------------------------- | -------------------------------------------------------------------------------------------- |
| **Type**                   | `object` (historical bug)                                | `undefined`                                                                                  |
| **Purpose**                | Represents the intentional absence of any object value   | Indicates that a variable has been declared but not yet assigned a value                     |
| **Assignment**             | Assigned explicitly by the programmer                    | Default value for uninitialized variables, missing object properties, or function parameters |
| **Use Case**               | Used to explicitly indicate "no value"                   | Indicates variables or properties that are not initialized or missing                        |
| **Example**                | `let foo = null;`                                        | `let bar;`, `console.log(bar);`                                                              |
| **Equality Check (`==`)**  | `null == undefined` is `true`                            | `null == undefined` is `true`                                                                |
| **Identity Check (`===`)** | `null === undefined` is `false`                          | `null === undefined` is `false`                                                              |
| **Default Value**          | Not a default value                                      | Default value for variables and function parameters that are not initialized or provided     |
| **Use in Objects**         | Can be used to indicate an object is intentionally empty | Missing properties of objects result in `undefined`                                          |
| **Return Value**           | Not a default return value                               | Functions return `undefined` if no return value is specified                                 |
| **Behavior in JSON**       | Represented as `null` in JSON                            | Properties with `undefined` are omitted from JSON serialization                              |

### Summary:

- `null` is used to explicitly signify the intentional absence of any object value.
- `undefined` is used to indicate that a variable has been declared but has not yet been assigned a value or that a property is missing.

Understanding these differences helps in writing clearer and more predictable JavaScript code, especially in debugging and handling uninitialized or missing values.
