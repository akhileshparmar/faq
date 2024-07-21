# Hoisting in JavaScript

## Introduction

Hoisting is one of the fundamental concepts in JavaScript that can sometimes be confusing for beginners. It allows functions, variables, and classes to be used before they are declared in the code. Understanding hoisting is essential for writing cleaner and bug-free JavaScript code.

## What is Hoisting?

In JavaScript, hoisting is a behavior where variable and function declarations are moved to the top of their containing scope during the compilation phase. This means that no matter where functions and variables are declared, they are moved to the top of their scope before code execution.

## How Hoisting Works

### Variable Hoisting

Variables declared with `var` are hoisted to the top of their function or global scope. However, only the declarations are hoisted, not the initializations. The variables are initialized with `undefined` until their actual initialization line is executed.

#### Example

```javascript
console.log(hoistedVar); // Output: undefined
var hoistedVar = "This is hoisted";
console.log(hoistedVar); // Output: 'This is hoisted'
```

In the above example, the declaration of `hoistedVar` is hoisted to the top, but its initialization is not.

### Function Hoisting

Function declarations are completely hoisted, meaning both the function name and the function body are moved to the top of their scope.

#### Example

```javascript
hoistedFunction(); // Output: 'This function is hoisted'

function hoistedFunction() {
  console.log("This function is hoisted");
}
```

In this example, the function `hoistedFunction` is hoisted to the top, so it can be called before its declaration.

### Let and Const Hoisting

Variables declared with `let` and `const` are also hoisted, but unlike `var`, they are not initialized with `undefined`. Instead, they are placed in a "temporal dead zone" (TDZ) from the start of the block until the declaration is encountered. Accessing them before their declaration results in a `ReferenceError`.

#### Example

```javascript
console.log(hoistedLet); // ReferenceError: Cannot access 'hoistedLet' before initialization
let hoistedLet = "This is hoisted with let";

console.log(hoistedConst); // ReferenceError: Cannot access 'hoistedConst' before initialization
const hoistedConst = "This is hoisted with const";
```

### Class Hoisting

Similar to `let` and `const`, classes are hoisted but not initialized. Attempting to access a class before its declaration results in a `ReferenceError`.

#### Example

```javascript
const instance = new HoistedClass(); // ReferenceError: Cannot access 'HoistedClass' before initialization

class HoistedClass {
  constructor() {
    console.log("This class is hoisted");
  }
}
```

## Practical Implications of Hoisting

### Function Expressions and Hoisting

Function expressions are not hoisted. This means that if you use a function expression before it's defined, you'll get a `TypeError` because the variable is hoisted and initialized as `undefined`.

#### Example

```javascript
hoistedFuncExpression(); // TypeError: hoistedFuncExpression is not a function

var hoistedFuncExpression = function () {
  console.log("This function expression is not hoisted");
};
```

### Best Practices

- Declare variables at the top of their scope to avoid confusion and potential bugs.
- Use `let` and `const` instead of `var` to avoid issues with hoisting and to make use of block-scoping.
- Define functions before you call them to ensure code clarity and maintainability.

## Conclusion

Hoisting is an important concept in JavaScript that affects how variables and functions are accessed and initialized. Understanding hoisting helps avoid common pitfalls and write more predictable code. Remember that `var` declarations are hoisted and initialized with `undefined`, while `let`, `const`, and class declarations are hoisted but not initialized, resulting in a `ReferenceError` if accessed before their declaration.
