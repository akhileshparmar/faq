# How JavaScript Works Behind the Scenes

## Introduction

Do you know? When you run a JavaScript program, a lot of things are happening behind the scenes inside the JavaScript engine. We'll be covering everything right now.

## Recap

we discussed that everything in JavaScript happens inside an **Execution Context**. Remember? And JavaScript isn't possible without this beautiful Execution Context. So here's one question for you: What happens when you run a JavaScript program?

Yes, you are right. An **execution context** is created. Let us now see how this beautiful execution context is created with the help of a JavaScript program.

## Example JavaScript Program

```javascript
var n = 2;

function square(num) {
  return num * num;
}

var square2 = square(n);
var square4 = square(4);
```

## Global Execution Context

When you run this whole code, a **global execution context** is created. Let us create this execution context. So remember we told that it's like a big box and it has two components:

1. **Memory Component** (also known as the Variable Environment)
2. **Code Component** (also known as the Thread of Execution)

### Phases of Execution Context

This execution context is created in two phases:

1. **Creation Phase (Memory Creation Phase)**: This is a very critical phase. Let us see how this phase is done. During this phase, JavaScript will allocate memory to all the variables and functions.

   - As soon as JS encounters `var n = 2;`, it allocates memory to `n`.
   - Similarly, when JS encounters the function `square`, it allocates memory to `square`.
   - The same goes for `square2` and `square4`.

2. **Execution Phase (Code Execution Phase)**: After the memory allocation, JavaScript runs through this whole JS program line by line and executes the code now. This is the point when all these functions and every calculation in the program are done.

### Memory Creation Phase

Let's see how this phase is done:

- As soon as JS encounters `var n = 2;`, it allocates memory to `n`:

  ```javascript
  n: undefined;
  ```

- When JS encounters the function `square`, it allocates memory to `square`:

  ```javascript
  square: function code
  ```

- JS then allocates memory to `square2` and `square4`:
  ```javascript
  square2: undefined;
  square4: undefined;
  ```

In this phase, JavaScript skims through the whole program line by line and allocates memory to all the variables and functions. For variables, it stores a special value, `undefined`, and for functions, it stores the whole function code.

### Code Execution Phase

Let's see how this code is executed after the memory allocation:

- JavaScript, once again, runs through this whole JS program line by line and executes the code now.
- As soon as it encounters `var n = 2;`, it actually places the `2` inside the `n`:

  ```javascript
  n = 2;
  ```

- When JS encounters `square2 = square(n);`, it invokes the `square` function. Whenever a new function is invoked, an altogether new execution context is created. This function, a brand new execution context, is created.

## Function Invocation and Execution Context

Whenever you see a function name with parentheses, it means that the function is now being executed. Functions are the heart of JavaScript and behave very differently in JavaScript than any other language. Functions in JS are like mini-programs, and whenever a new function is invoked, a mini-program is invoked, and a new execution context is created.

### Example with `square(n)`

Let's create this execution context:

1. **Memory Creation Phase**:

   - Memory is allocated to variables and functions inside this function, involving the parameters (`num`) and other variables (`ans`):
     ```javascript
     num: undefined;
     ans: undefined;
     ```

2. **Code Execution Phase**:

   - The value of `n` (which is 2) is passed to `num`.
   - `num` is multiplied by itself (`num * num`) and the result is stored in `ans`:

     ```javascript
     ans = 2 * 2 = 4;
     ```

   - The `return` statement returns the control back to the execution context where the function was invoked.

     ```javascript
     square2 = square(n); // square2 = 4
     ```

### Example with `square(4)`

1. **Memory Creation Phase**:

   - Memory is allocated to `num` and `ans`:
     ```javascript
     num: undefined;
     ans: undefined;
     ```

2. **Code Execution Phase**:

   - The value `4` is passed to `num`.
   - `num` is multiplied by itself (`num * num`) and the result is stored in `ans`:

     ```javascript
     ans = 4 * 4 = 16;
     ```

   - The `return` statement returns the control back to the execution context where the function was invoked.

     ```javascript
     square4 = square(4); // square4 = 16
     ```

### Call Stack

Don't you think that all this is too much to manage for the JS engine? Execution contexts are created one by one, inside one another, and all these things are very tough to manage. Suppose if there was a function invocation inside the function, what would have happened is you would have created an execution context INSIDE an execution context.

JavaScript manages this beautifully using a **call stack**. This is known as the call stack.

### What is a Call Stack?

The call stack is like a stack. At the bottom of the stack, we have our global execution context. Whenever any JS program is run, this call stack is populated with this Global Execution Context. This whole execution context is pushed inside this stack.

Whenever a function is invoked, or a new execution context is created, it is pushed into the stack. Once the function is executed, it is popped off the stack, and the control goes back to the global execution context where it left off.

### Example of Call Stack

1. The global execution context is created and pushed onto the stack.
2. When `square(n)` is invoked, a new execution context (`E1`) is created and pushed onto the stack.
3. Once `square(n)` is executed, `E1` is popped off the stack.
4. When `square(4)` is invoked, a new execution context (`E2`) is created and pushed onto the stack.
5. Once `square(4)` is executed, `E2` is popped off the stack.
6. Finally, the global execution context is also popped off the stack when the program finishes.

### Conclusion

- JavaScript code execution involves creating and managing execution contexts.
- The **call stack** manages the order of execution of these contexts.
- Execution contexts are created in two phases: **Memory Creation** and **Code Execution**.
- Call stack maintains the order of execution of execution contexts.
- It is also known by various names such as Execution Context Stack, Program Stack, Control Stack, Runtime Stack, Machine Stack.
