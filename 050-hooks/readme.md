# React Hooks

**React Hooks** are a feature introduced in React 16.8 that allow functional components to use state and other React features without writing a class. Hooks provide a way to use stateful logic and lifecycle features in functional components, which were previously only available in class components.

### Why Hooks Were Introduced

1. **Simplify Component Logic**: Hooks allow you to use state and other React features in functional components, leading to simpler and more readable code. This avoids the complexity of class-based components.
2. **Reusability of Logic**: Hooks make it easier to reuse logic across multiple components. Custom hooks can encapsulate stateful logic and share it across different components.

3. **Better Separation of Concerns**: Hooks help in managing component logic in a more modular way. You can separate stateful logic from rendering logic more effectively.

4. **Avoid Class Component Issues**: Hooks eliminate common issues associated with class components, such as `this` binding, complex lifecycle methods, and handling state updates.

### Types of Hooks

1. **Basic Hooks**:

   - `useState`: Adds state to functional components.
   - `useEffect`: Handles side effects like data fetching, subscriptions, and manual DOM manipulations.
   - `useContext`: Accesses context data without needing to wrap components in `Context.Consumer`.

2. **Additional Hooks**:

   - `useReducer`: Manages more complex state logic.
   - `useCallback`: Memoizes callback functions to prevent unnecessary re-renders.
   - `useMemo`: Memoizes values to optimize performance.
   - `useRef`: Accesses and manipulates DOM elements or stores mutable values without causing re-renders.

3. **Custom Hooks**:
   - You can create custom hooks to encapsulate reusable logic. Custom hooks are functions that use one or more of the basic hooks.

### Rules of Hooks

To use hooks correctly, you must follow these rules:

1. **Only Call Hooks at the Top Level**:

   - Hooks should be called at the top level of a functional component or custom hook. This means you should not call hooks inside loops, conditions, or nested functions. This rule ensures that hooks are always called in the same order on every render.

   ```jsx
   // Correct
   function MyComponent() {
     const [count, setCount] = useState(0);
     useEffect(() => {
       // Side effect code
     }, []);
     //...
   }

   // Incorrect
   function MyComponent() {
     if (condition) {
       const [count, setCount] = useState(0); // Incorrect: Hooks inside a condition
     }
     //...
   }
   ```

2. **Only Call Hooks from React Functions**:

   - Hooks should only be called from functional components or custom hooks, not from regular JavaScript functions. This ensures that hooks follow the React lifecycle and behave as expected.

   ```jsx
   // Correct
   function MyComponent() {
     const [count, setCount] = useState(0);
     //...
   }

   function useCustomHook() {
     const [value, setValue] = useState(0);
     //...
     return [value, setValue];
   }

   // Incorrect
   function notAComponent() {
     const [count, setCount] = useState(0); // Incorrect: Hooks not in a React function
     //...
   }
   ```

### Example Usage of Hooks

**Using `useState` and `useEffect`**:

```jsx
import React, { useState, useEffect } from "react";

function Example() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    document.title = `You clicked ${count} times`;

    return () => {
      // Cleanup function if needed
    };
  }, [count]); // Dependency array

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>Click me</button>
    </div>
  );
}
```

**Creating a Custom Hook**:

```jsx
import { useState, useEffect } from "react";

// Custom hook
function useLocalStorage(key, initialValue) {
  const [storedValue, setStoredValue] = useState(() => {
    try {
      const item = window.localStorage.getItem(key);
      return item ? JSON.parse(item) : initialValue;
    } catch (error) {
      return initialValue;
    }
  });

  useEffect(() => {
    try {
      window.localStorage.setItem(key, JSON.stringify(storedValue));
    } catch (error) {
      console.error(error);
    }
  }, [key, storedValue]);

  return [storedValue, setStoredValue];
}

export default useLocalStorage;
```

By using hooks, developers can write more readable, maintainable, and reusable code while leveraging the full power of React's features in functional components.
