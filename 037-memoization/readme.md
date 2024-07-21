# Memoization

**Memoization** is a technique used to optimize performance by caching the results of expensive function calls and returning the cached result when the same inputs occur again. This can significantly speed up computations in scenarios where the same function is called repeatedly with the same arguments.

### How Memoization Works

1. **Store Results**: When a function is called with certain arguments, the result is computed and stored in a cache.
2. **Check Cache**: For subsequent calls with the same arguments, the function first checks the cache to see if a result is already available.
3. **Return Cached Result**: If the result is found in the cache, it is returned immediately, avoiding the need for recomputation.

### Benefits of Memoization

- **Improved Performance**: Reduces the time complexity of repeated function calls by avoiding redundant calculations.
- **Efficiency**: Saves computational resources and time by storing results of expensive function calls.

### Simple Example of Memoization

Let's look at a basic example of memoization with a function that computes Fibonacci numbers:

```javascript
// Memoized Fibonacci function
function memoizedFibonacci() {
  const cache = {}; // Object to store computed results

  function fibonacci(n) {
    if (n in cache) {
      return cache[n]; // Return cached result if it exists
    }
    if (n <= 1) {
      return n; // Base case
    }
    // Compute result and store in cache
    cache[n] = fibonacci(n - 1) + fibonacci(n - 2);
    return cache[n];
  }

  return fibonacci;
}

const fib = memoizedFibonacci();

console.log(fib(10)); // 55
console.log(fib(20)); // 6765
console.log(fib(10)); // 55 (cached result)
```

### Explanation

1. **Cache Initialization**: `cache` is an object used to store previously computed Fibonacci numbers.
2. **Check Cache**: Before computing a Fibonacci number, the function checks if the result is already in the `cache`.
3. **Compute and Store**: If the result is not in the cache, the function computes it, stores it in the `cache`, and then returns it.

### Memoization in Practice

- **Use Cases**: Memoization is useful in scenarios involving recursive algorithms, dynamic programming, and functions with expensive calculations.
- **Libraries**: Many libraries and frameworks use memoization techniques to enhance performance. For example, React uses memoization in hooks like `useMemo` and `useCallback` to optimize rendering.

### Summary

Memoization is a powerful optimization technique that improves the performance of functions by storing and reusing previously computed results. It is particularly effective in scenarios where the same computations are repeated with the same inputs.
