# Lexical Environment

A **lexical environment** in JavaScript is a data structure that holds the identifiers (variables, constants, and functions) defined in a particular scope and their corresponding values. Each lexical environment is associated with some specific part of the program (usually a function or a block), and it keeps track of the variable bindings for that scope.

## Components of a Lexical Environment

A lexical environment consists of two main components:

1. **Environment Record**: This is a record of all the variable and function declarations in the lexical environment.
2. **Outer Lexical Environment Reference**: This is a reference to the outer lexical environment (i.e., the environment in which the current environment is nested).

## How Lexical Environments Work

### Creation of Lexical Environments

When a JavaScript function is executed, a new lexical environment is created. This lexical environment keeps track of:

- Local variables declared inside the function.
- Arguments passed to the function.
- Functions defined inside the function.

### Example

```javascript
function outerFunction() {
  let outerVar = "I am outside!";

  function innerFunction() {
    let innerVar = "I am inside!";
    console.log(outerVar); // Accessing outer variable
  }

  innerFunction();
  console.log(innerVar); // ReferenceError: innerVar is not defined
}

outerFunction();
```

In this example:

- When `outerFunction` is called, a new lexical environment is created for it. This environment contains the `outerVar` variable.
- When `innerFunction` is called, another new lexical environment is created for it. This environment contains the `innerVar` variable and a reference to the `outerFunction`'s lexical environment.

### Scope Chain and Lexical Environments

When you try to access a variable in JavaScript, the JavaScript engine will look for the variable in the current lexical environment. If it doesn't find it, it will move to the outer lexical environment, and so on, until it reaches the global environment. This chain of environments is called the **scope chain**.

### Global Lexical Environment

The global environment is the outermost lexical environment. It contains globally defined variables and functions.

### Function Lexical Environment

Each time a function is called, a new lexical environment is created for that function call. This environment keeps track of the local variables and arguments for that particular function invocation.

## Summary

- **Lexical Environment**: A structure that holds variable and function declarations and their values for a particular scope.
- **Environment Record**: Part of the lexical environment that stores variable bindings.
- **Outer Lexical Environment Reference**: Reference to the parent lexical environment.
- **Scope Chain**: Series of lexical environments that the JavaScript engine uses to resolve variable references.
- **Global Lexical Environment**: The top-level environment that contains global variables and functions.
- **Function Lexical Environment**: A new lexical environment created each time a function is called.

Understanding lexical environments is crucial for grasping how JavaScript handles variable scoping and closures.
