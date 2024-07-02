# Scope in JS

In JavaScript, "scope" refers to the current context of execution in which values and expressions are accessible. Scopes determine the accessibility (visibility) of variables and functions at various parts of your code.

## Types of Scope in JavaScript

### 1. **Global Scope**

Variables declared outside any function or block are in the global scope. These variables are accessible from anywhere in the code.

```javascript
let globalVar = "I'm a global variable";

function checkGlobalScope() {
  console.log(globalVar); // Accessible here
}

checkGlobalScope();
console.log(globalVar); // Accessible here too
```

### 2. **Function Scope**

Variables declared inside a function are in the function scope (or local scope). These variables are only accessible within the function they are declared in.

```javascript
function checkFunctionScope() {
  let functionVar = "I'm a function variable";
  console.log(functionVar); // Accessible here
}

checkFunctionScope();
console.log(functionVar); // ReferenceError: functionVar is not defined
```

### 3. **Block Scope**

Variables declared inside a block (denoted by curly braces `{}`) using `let` or `const` are block-scoped. These variables are only accessible within the block they are declared in.

```javascript
{
  let blockVar = "I'm a block variable";
  console.log(blockVar); // Accessible here
}

console.log(blockVar); // ReferenceError: blockVar is not defined
```

### 4. **Lexical Scope**

JavaScript follows lexical (or static) scoping, meaning the scope of a variable is determined by its position in the source code. Nested functions have access to variables declared in their outer scope.

```javascript
function outerFunction() {
  let outerVar = "I'm an outer variable";

  function innerFunction() {
    console.log(outerVar); // Accessible here
  }

  innerFunction();
}

outerFunction();
```

### Variable Shadowing

Variable shadowing occurs when a variable declared within a certain scope has the same name as a variable declared in an outer scope. In such cases, the inner variable shadows the outer one.

```javascript
let varName = "outer";

function shadowingExample() {
  let varName = "inner";
  console.log(varName); // Output: "inner"
}

shadowingExample();
console.log(varName); // Output: "outer"
```

### Scope Chain

When trying to access a variable, JavaScript starts looking in the current scope. If it doesn't find it, it moves up to the outer scope, continuing until it reaches the global scope. This chain of scopes is called the scope chain.

```javascript
let globalVar = "global";

function outerFunction() {
  let outerVar = "outer";

  function innerFunction() {
    let innerVar = "inner";
    console.log(globalVar); // Accessible here (global scope)
    console.log(outerVar); // Accessible here (outer function scope)
    console.log(innerVar); // Accessible here (inner function scope)
  }

  innerFunction();
}

outerFunction();
```

### Closures

A closure is a function that retains access to its outer (lexical) scope even after the outer function has finished executing. Closures are created whenever a function is created, and they allow the function to retain access to its scope chain.

```javascript
function createCounter() {
  let count = 0;
  return function () {
    count++;
    console.log(count);
  };
}

const counter = createCounter();
counter(); // Output: 1
counter(); // Output: 2
```

In this example, the inner function retains access to the `count` variable even after `createCounter` has finished executing.

## Summary

- **Global Scope**: Variables declared outside any function or block.
- **Function Scope**: Variables declared inside a function.
- **Block Scope**: Variables declared inside a block using `let` or `const`.
- **Lexical Scope**: Variables are accessible based on their position in the source code.
- **Variable Shadowing**: Inner variables with the same name as outer variables.
- **Scope Chain**: The hierarchy of nested scopes.
- **Closures**: Functions retaining access to their lexical scope.
