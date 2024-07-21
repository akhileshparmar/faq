# `useMemo` vs. `useCallback` in React

In React, both `useMemo` and `useCallback` are hooks used to optimize performance by memoizing values and functions to prevent unnecessary computations and re-renders. However, they are used in different contexts and for different purposes.

#### `useMemo`

`useMemo` is a hook that memoizes the result of a function, ensuring that the function is only recomputed when one of its dependencies changes. It is primarily used to optimize expensive calculations or operations that should only be performed when necessary.

##### Syntax

```javascript
const memoizedValue = useMemo(() => computeExpensiveValue(a, b), [a, b]);
```

##### Example

```javascript
import React, { useState, useMemo } from "react";

function ExampleComponent() {
  const [count, setCount] = useState(0);
  const [otherValue, setOtherValue] = useState(100);

  const expensiveCalculation = useMemo(() => {
    console.log("Calculating...");
    return count * 2;
  }, [count]);

  return (
    <div>
      <p>Count: {count}</p>
      <p>Expensive Calculation Result: {expensiveCalculation}</p>
      <button onClick={() => setCount(count + 1)}>Increment Count</button>
      <button onClick={() => setOtherValue(otherValue + 1)}>
        Change Other Value
      </button>
    </div>
  );
}

export default ExampleComponent;
```

In this example, the `expensiveCalculation` is only recomputed when `count` changes, not when `otherValue` changes. This avoids unnecessary recalculations.

#### `useCallback`

`useCallback` is a hook that memoizes a function definition, ensuring that the same function instance is returned as long as its dependencies do not change. This is useful for preventing unnecessary re-renders, especially when passing callback functions to child components that rely on referential equality to avoid re-renders.

##### Syntax

```javascript
const memoizedCallback = useCallback(() => {
  doSomething(a, b);
}, [a, b]);
```

##### Example

```javascript
import React, { useState, useCallback } from "react";

function ChildComponent({ onClick }) {
  console.log("Child Component rendered");
  return <button onClick={onClick}>Click me</button>;
}

function ExampleComponent() {
  const [count, setCount] = useState(0);
  const [otherValue, setOtherValue] = useState(100);

  const handleClick = useCallback(() => {
    console.log("Button clicked");
    setCount(count + 1);
  }, [count]);

  return (
    <div>
      <p>Count: {count}</p>
      <ChildComponent onClick={handleClick} />
      <button onClick={() => setOtherValue(otherValue + 1)}>
        Change Other Value
      </button>
    </div>
  );
}

export default ExampleComponent;
```

In this example, the `handleClick` function is only recreated when `count` changes. This ensures that `ChildComponent` does not re-render unnecessarily when `otherValue` changes, because the `onClick` prop reference remains the same.

#### Key Differences

| Feature      | `useMemo`                              | `useCallback`                                                |
| ------------ | -------------------------------------- | ------------------------------------------------------------ |
| Purpose      | Memoizes the result of a computation   | Memoizes a function definition                               |
| Use Case     | Optimizing expensive calculations      | Preventing unnecessary re-renders due to function references |
| Return Value | The result of the memoized function    | The memoized function itself                                 |
| Dependencies | List of dependencies for recomputation | List of dependencies for function recreation                 |

#### Summary

- Use `useMemo` to memoize expensive computations and prevent them from running unnecessarily.
- Use `useCallback` to memoize functions and prevent unnecessary re-renders of child components that depend on these functions.
- Both hooks rely on dependencies to determine when to recompute or recreate their values.

By understanding and utilizing these hooks appropriately, you can optimize the performance of your React applications effectively.
