# Debouncing and Throttling

Debouncing and throttling are two techniques used in JavaScript to control the rate at which a function is executed, particularly useful for handling events that can occur in quick succession, such as scrolling, resizing, and keypress events. These techniques help improve performance and avoid excessive function calls.

### Debouncing

Debouncing ensures that a function is only executed once after a specified delay has elapsed since the last time it was invoked. It's useful for scenarios where you want to wait until the user has finished performing an action before executing the function, such as waiting until the user has finished typing in a search box before making an API call.

#### Example:

```javascript
function debounce(func, delay) {
  let timer;
  return function (...args) {
    clearTimeout(timer);
    timer = setTimeout(() => {
      func.apply(this, args);
    }, delay);
  };
}

window.addEventListener(
  "resize",
  debounce(() => {
    console.log("Resize event handler executed after delay");
  }, 500)
);
```

### Throttling

Throttling ensures that a function is only executed at most once in a specified period, regardless of how many times it is triggered. It's useful for scenarios where you want to limit the rate at which a function is called, such as limiting the number of times a scroll event handler is executed.

#### Example:

```javascript
function throttle(func, limit) {
  let inThrottle;
  return function (...args) {
    if (!inThrottle) {
      func.apply(this, args);
      inThrottle = true;
      setTimeout(() => {
        inThrottle = false;
      }, limit);
    }
  };
}

window.addEventListener(
  "scroll",
  throttle(() => {
    console.log("Scroll event handler executed at most once per limit period");
  }, 100)
);
```

### Comparison

| Feature                   | Debouncing                                       | Throttling                                           |
| ------------------------- | ------------------------------------------------ | ---------------------------------------------------- |
| **Purpose**               | Delay function execution until a pause in events | Limit function execution to once per time period     |
| **Use Case**              | Waiting for the end of user input                | Limiting the rate of event handler execution         |
| **Example Scenario**      | User typing in a search box                      | Scrolling or resizing the window                     |
| **Execution Frequency**   | Once, after a specified delay                    | At most once per specified time period               |
| **Implementation Method** | Uses `setTimeout` to delay function calls        | Uses a flag and `setTimeout` to limit function calls |

### When to Use Each

- **Debouncing**: Use debouncing when you want to wait for a "pause" in events before executing the function. This is useful for actions like form submissions, search input, and window resizing where you want to wait until the user has finished interacting.
- **Throttling**: Use throttling when you want to ensure that a function is called at regular intervals, but not too frequently. This is useful for actions like scrolling, mouse movement, and window resizing where you want to limit the rate of execution to improve performance.

Both debouncing and throttling are essential tools for optimizing event handling in JavaScript, helping to create smoother and more efficient user experiences.
