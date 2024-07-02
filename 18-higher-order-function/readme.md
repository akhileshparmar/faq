# Higher Order Functions

In JavaScript, **higher-order functions** are functions that either:

1. **Take other functions as arguments**, or
2. **Return functions as their result**.

Higher-order functions are a core concept in functional programming and enable a wide range of powerful and expressive programming patterns. They allow you to write more abstract and reusable code.

### 1. Functions that Take Other Functions as Arguments

Higher-order functions can accept other functions as arguments. This allows you to create more general functions that can operate on various functions passed to them.

**Example: `map` Function**

The `map` function is a classic example of a higher-order function. It takes a function as an argument and applies that function to each element of an array.

```javascript
const numbers = [1, 2, 3, 4];
const doubled = numbers.map(function (number) {
  return number * 2;
});
console.log(doubled); // Output: [2, 4, 6, 8]
```

In this example, `map` is a higher-order function because it takes a function as its argument and applies it to each element of the array.

### 2. Functions that Return Other Functions

Higher-order functions can also return other functions. This is useful for creating function factories or for creating functions with pre-set parameters.

**Example: Function Factory**

Here’s an example of a higher-order function that returns another function:

```javascript
function createMultiplier(factor) {
  return function (number) {
    return number * factor;
  };
}

const multiplyBy2 = createMultiplier(2);
const multiplyBy5 = createMultiplier(5);

console.log(multiplyBy2(10)); // Output: 20
console.log(multiplyBy5(10)); // Output: 50
```

In this example, `createMultiplier` is a higher-order function because it returns a new function that multiplies a number by a specified factor.

### Common Higher-Order Functions in JavaScript

JavaScript provides several built-in higher-order functions, particularly for working with arrays:

- **`map()`**: Creates a new array with the results of calling a provided function on every element in the calling array.
- **`filter()`**: Creates a new array with all elements that pass the test implemented by the provided function.
- **`reduce()`**: Executes a reducer function (that you provide) on each element of the array, resulting in a single output value.
- **`forEach()`**: Executes a provided function once for each array element.
- **`sort()`**: Sorts the elements of an array in place and returns the sorted array.

**Examples:**

**`filter()` Function**

```javascript
const numbers = [1, 2, 3, 4, 5];
const evenNumbers = numbers.filter(function (number) {
  return number % 2 === 0;
});
console.log(evenNumbers); // Output: [2, 4]
```

**`reduce()` Function**

```javascript
const numbers = [1, 2, 3, 4];
const sum = numbers.reduce(function (accumulator, current) {
  return accumulator + current;
}, 0);
console.log(sum); // Output: 10
```

### Why Higher-Order Functions Matter

- **Abstraction**: They allow you to abstract over actions, enabling you to write more general and reusable code.
- **Composition**: They facilitate function composition, where you can build complex operations by combining simple functions.
- **Code Reusability**: Higher-order functions promote code reusability by allowing you to pass in different functions to achieve different outcomes with the same higher-order function.

Higher-order functions are fundamental in JavaScript and are a powerful tool in writing clean, efficient, and maintainable code.
