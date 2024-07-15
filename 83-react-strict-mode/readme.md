# React Strict Mode

When using React Strict Mode with functional components, it helps you catch issues related to hooks and side effects that might not be immediately obvious. Here's how React Strict Mode interacts with functional components and what it does behind the scenes:

### How React Strict Mode Affects Functional Components

1. **Double Invoking Lifecycle Methods**:
   Strict Mode can double-invoke certain lifecycle methods like `useEffect` callbacks to ensure that side effects are cleaned up correctly and do not have unintended consequences. This helps in identifying potential issues with effects that might not clean up properly.

2. **Detecting Unsafe Effects**:
   It helps in detecting problems with `useEffect` and other hooks that could lead to side effects being executed unexpectedly or multiple times. This is crucial for ensuring that your effects are predictable and clean up as expected.

3. **Validating Hooks Usage**:
   React Strict Mode validates that hooks are called in the correct order and only within functional components or other hooks. This helps prevent issues with hooks being called conditionally or incorrectly.

### Example of React Strict Mode with Functional Components

#### Basic Functional Component with Hooks

Here's a simple functional component using `useEffect`:

```jsx
import React, { useEffect, useState } from "react";

function MyComponent() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    // Side effect: logging count
    console.log("Count:", count);

    // Cleanup function
    return () => {
      console.log("Cleanup");
    };
  }, [count]);

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
}

export default MyComponent;
```

#### Using React Strict Mode

To enable Strict Mode, wrap your component or application with `<React.StrictMode>`:

```jsx
import React from "react";
import ReactDOM from "react-dom";
import MyComponent from "./MyComponent";

ReactDOM.render(
  <React.StrictMode>
    <MyComponent />
  </React.StrictMode>,
  document.getElementById("root")
);
```

### What Happens with Strict Mode

1. **Double Invocation of `useEffect`**:
   React Strict Mode will double-invoke the `useEffect` callback to ensure that it is idempotent and that the cleanup function properly resets state. This helps catch bugs where the effect might not clean up correctly.

   ```plaintext
   Count: 0
   Cleanup
   Count: 1
   Cleanup
   ```

   The logs show that `useEffect` runs twice, and each time it performs cleanup before the next run.

2. **Validation of Hooks**:
   Strict Mode enforces rules for hooks:

   - Hooks must be called at the top level of functional components or custom hooks.
   - Hooks must not be called conditionally or within loops.

   If you violate these rules, React will provide warnings in the console to help you correct the issues.

### Summary

In summary, React Strict Mode for functional components:

- **Double Invokes `useEffect`**: To ensure effects are clean and idempotent.
- **Validates Hooks**: Ensures hooks are used correctly and consistently.
- **Highlights Potential Problems**: Detects issues with side effects and hook usage early in development.

Strict Mode is a valuable tool for improving the reliability and maintainability of functional components by catching potential issues before they become bigger problems in production.
