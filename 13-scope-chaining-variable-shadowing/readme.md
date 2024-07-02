# Scope Chaining

**Scope chaining** refers to the process by which JavaScript resolves variable names. When a variable is referenced, JavaScript starts looking for it in the current scope. If it doesn't find the variable there, it moves up to the next outer scope, and continues this process until it either finds the variable or reaches the global scope.

Here's an example to illustrate scope chaining:

```javascript
let globalVar = "I'm global";

function outerFunction() {
  let outerVar = "I'm outer";

  function innerFunction() {
    let innerVar = "I'm inner";
    console.log(innerVar); // Output: I'm inner
    console.log(outerVar); // Output: I'm outer
    console.log(globalVar); // Output: I'm global
  }

  innerFunction();
}

outerFunction();
```

In the `innerFunction`, the JavaScript engine first looks for the variables `innerVar`, `outerVar`, and `globalVar` within its own scope. When it doesn't find `outerVar` and `globalVar`, it moves up the scope chain to `outerFunction` and then to the global scope, respectively.

### Variable Shadowing

**Variable shadowing** occurs when a variable declared within a certain scope (inner scope) has the same name as a variable declared in an outer scope. The inner scope variable "shadows" the outer scope variable, meaning the inner variable takes precedence within its scope.

Here's an example of variable shadowing:

```javascript
let name = "John";

function greet() {
  let name = "Jane"; // Shadows the global 'name' variable
  console.log(name); // Output: Jane
}

greet();
console.log(name); // Output: John
```

In this example, the `name` variable inside the `greet` function shadows the global `name` variable. Inside the function, `name` refers to `"Jane"`, while outside, it still refers to `"John"`.

### Illegal Shadowing

**Illegal shadowing** occurs in certain situations where JavaScript does not allow a variable to shadow another variable. This typically involves the use of `let` or `const` in blocks where a variable with the same name is already defined in the outer scope using `var`.

Here's an example of illegal shadowing:

```javascript
var x = 10;

if (true) {
  let x = 20; // Legal shadowing
  console.log(x); // Output: 20
}

function exampleFunction() {
  let y = 30;

  if (true) {
    // This would cause an error because 'let' or 'const' can't shadow 'var' in the same scope
    var y = 40; // Illegal shadowing
  }

  console.log(y);
}

exampleFunction();
```

In the `exampleFunction`, the inner `var y` declaration is illegal because it attempts to shadow the `let y` variable from the outer scope. This would result in a `SyntaxError` due to illegal shadowing.

#### Summary

- **Scope Chaining**: The process of resolving variable names by searching from the current scope up through outer scopes until the global scope.
- **Variable Shadowing**: When an inner scope variable has the same name as an outer scope variable, taking precedence in the inner scope.
- **Illegal Shadowing**: Situations where JavaScript disallows shadowing, such as when a `var` declaration attempts to shadow a `let` or `const` declaration in the same or outer scope, leading to a `SyntaxError`.
