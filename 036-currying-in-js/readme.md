# Currying

Currying is a technique in functional programming where a function is transformed into a sequence of functions, each taking a single argument. Instead of taking all arguments at once, a curried function takes the first argument and returns a new function that takes the second argument, and so on, until all arguments are provided. This allows for partial application of functions, where some arguments are fixed in advance, creating a new function with fewer arguments.

### Example in JavaScript

Here’s a simple example to illustrate currying in JavaScript:

#### Non-curried Function

```javascript
function add(a, b, c) {
  return a + b + c;
}

console.log(add(1, 2, 3)); // 6
```

#### Curried Function

```javascript
function curriedAdd(a) {
  return function (b) {
    return function (c) {
      return a + b + c;
    };
  };
}

console.log(curriedAdd(1)(2)(3)); // 6

// You can also use partial application
const addOne = curriedAdd(1);
const addOneAndTwo = addOne(2);
console.log(addOneAndTwo(3)); // 6
```

### Benefits of Currying

1. **Partial Application**: Currying allows you to fix some arguments of the function in advance, making it easier to create specialized functions.

   ```javascript
   function multiply(a) {
     return function (b) {
       return a * b;
     };
   }

   const double = multiply(2);
   console.log(double(5)); // 10
   ```

2. **Code Reusability**: It promotes code reusability by allowing the creation of smaller, reusable functions.

   ```javascript
   function greet(greeting) {
     return function (name) {
       return `${greeting}, ${name}!`;
     };
   }

   const sayHello = greet("Hello");
   console.log(sayHello("Alice")); // Hello, Alice!
   ```

3. **Function Composition**: Currying makes it easier to compose functions and create more complex functions from simple ones.

   ```javascript
   const add = (a) => (b) => a + b;
   const multiply = (a) => (b) => a * b;

   const addThenMultiply = (a) => (b) => (c) => multiply(add(a)(b))(c);
   console.log(addThenMultiply(1)(2)(3)); // (1 + 2) * 3 = 9
   ```

### Implementation of Currying

To generalize currying for any function, you can create a curry function that converts any given function into its curried form.

```javascript
function curry(fn) {
  return function curried(...args) {
    if (args.length >= fn.length) {
      return fn.apply(this, args);
    } else {
      return function (...nextArgs) {
        return curried.apply(this, args.concat(nextArgs));
      };
    }
  };
}

function add(a, b, c) {
  return a + b + c;
}

const curriedAdd = curry(add);
console.log(curriedAdd(1)(2)(3)); // 6
console.log(curriedAdd(1, 2)(3)); // 6
console.log(curriedAdd(1)(2, 3)); // 6
```

### Conclusion

Currying is a powerful technique in functional programming that can lead to more reusable, modular, and readable code. It allows functions to be partially applied, making them more flexible and easier to work with in various contexts.
