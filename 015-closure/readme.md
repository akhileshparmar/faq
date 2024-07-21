# Closures in JavaScript

**Closure** is a feature in JavaScript where an inner function has access to its own scope, the outer function’s scope, and the global scope. Closures allow a function to retain access to its lexical scope even when that function is executed outside of its original scope.

Here's a breakdown of what a closure can access:

- **Own scope**: Variables defined within its own function body.
- **Outer function’s scope**: Variables defined in the outer function.
- **Global scope**: Variables defined in the global scope.

#### How Closures Work

Closures are created whenever a function is defined inside another function, and the inner function retains access to the variables and parameters of the outer function even after the outer function has finished executing.

Here's an example to illustrate closures:

```javascript
function outerFunction(outerVariable) {
  const outerConst = "I am outer";

  return function innerFunction(innerVariable) {
    console.log("Outer variable:", outerVariable);
    console.log("Outer constant:", outerConst);
    console.log("Inner variable:", innerVariable);
  };
}

const newFunction = outerFunction("I am outer variable");
newFunction("I am inner variable");
```

**Explanation**:

1. `outerFunction` is called with `'I am outer variable'`, creating a closure.
2. `innerFunction` is returned from `outerFunction` and assigned to `newFunction`.
3. When `newFunction` is called with `'I am inner variable'`, it still has access to `outerVariable` and `outerConst` from the `outerFunction` scope, even though `outerFunction` has already finished executing.

#### Practical Uses of Closures

**1. Encapsulation:**
Closures can be used to create private variables and functions.

```javascript
function createCounter() {
  let count = 0;
  return {
    increment: function () {
      count++;
      return count;
    },
    decrement: function () {
      count--;
      return count;
    },
  };
}

const counter = createCounter();
console.log(counter.increment()); // Output: 1
console.log(counter.increment()); // Output: 2
console.log(counter.decrement()); // Output: 1
```

In this example, `count` is a private variable that can only be accessed and modified by the `increment` and `decrement` functions.

**2. Function Factories:**
Closures can be used to create functions that are pre-configured with specific data.

```javascript
function createGreeting(greeting) {
  return function (name) {
    console.log(greeting + ", " + name);
  };
}

const sayHello = createGreeting("Hello");
sayHello("John"); // Output: Hello, John

const sayHi = createGreeting("Hi");
sayHi("Jane"); // Output: Hi, Jane
```

In this example, `createGreeting` returns a new function that remembers the `greeting` passed to it.

**3. Maintaining State in Asynchronous Code:**
Closures are particularly useful in asynchronous code, such as event handlers or `setTimeout` callbacks, to maintain access to the scope at the time of creation.

```javascript
function setupTimeouts() {
  for (let i = 1; i <= 3; i++) {
    setTimeout(function () {
      console.log("Timeout:", i);
    }, i * 1000);
  }
}

setupTimeouts();
// Output after 1 second: Timeout: 1
// Output after 2 seconds: Timeout: 2
// Output after 3 seconds: Timeout: 3
```

In this example, each `setTimeout` callback retains access to the value of `i` at the time the callback was created, demonstrating how closures can preserve state in asynchronous code.

#### Summary

- **Closures** allow functions to access variables from their lexical scope even after the outer function has completed.
- Closures are useful for **encapsulation**, creating **function factories**, and maintaining state in **asynchronous code**.
- They provide a powerful way to handle data privacy and state management within functions.
