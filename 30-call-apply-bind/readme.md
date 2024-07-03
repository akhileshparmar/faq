# call, apply and bind

In JavaScript, `call`, `apply`, and `bind` are methods used to control the `this` context of functions. They are all methods of function objects and are used to set the `this` value for function execution, but they work in different ways.

### `call`

- **Purpose**: Invokes a function with a specified `this` value and individual arguments.
- **Syntax**: `func.call(thisArg, arg1, arg2, ...)`
- **How It Works**: The `call` method calls the function immediately and sets the `this` context to the provided `thisArg`. You can pass arguments to the function directly after the `thisArg`.

**Example**:

```javascript
function greet(greeting, punctuation) {
  console.log(`${greeting}, ${this.name}${punctuation}`);
}

const person = { name: "John" };

greet.call(person, "Hello", "!"); // Output: Hello, John!
```

### `apply`

- **Purpose**: Similar to `call`, but accepts arguments as an array.
- **Syntax**: `func.apply(thisArg, [arg1, arg2, ...])`
- **How It Works**: The `apply` method calls the function immediately with the `this` context set to `thisArg`. The second parameter is an array or array-like object containing the arguments.

**Example**:

```javascript
function greet(greeting, punctuation) {
  console.log(`${greeting}, ${this.name}${punctuation}`);
}

const person = { name: "Jane" };

greet.apply(person, ["Hi", "?"]); // Output: Hi, Jane?
```

### `bind`

- **Purpose**: Creates a new function with a specified `this` context and optional arguments, but does not invoke the function immediately.
- **Syntax**: `const boundFunc = func.bind(thisArg, arg1, arg2, ...)`
- **How It Works**: The `bind` method returns a new function where `this` is set to `thisArg`. You can also preset arguments that will be used when the bound function is eventually called.

**Example**:

```javascript
function greet(greeting, punctuation) {
  console.log(`${greeting}, ${this.name}${punctuation}`);
}

const person = { name: "Doe" };
const greetPerson = greet.bind(person, "Hey");
greetPerson("!"); // Output: Hey, Doe!
```

### Summary of Differences

- **`call`**: Calls the function immediately with the provided `this` context and arguments.
- **`apply`**: Calls the function immediately with the provided `this` context and arguments in the form of an array.
- **`bind`**: Creates a new function with a fixed `this` context and optionally pre-set arguments. The new function can be invoked later.

These methods are useful for controlling the execution context of functions, enabling function reuse, and managing how functions interact with different objects.
