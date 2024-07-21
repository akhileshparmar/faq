# state

In React, **state** is a built-in feature that allows components to maintain and manage their own data over time. Unlike props, which are passed from parent to child components, state is managed within the component itself and can be changed in response to user actions or other events.

### Key Points About State

1. **Mutable**:

   - Unlike props, state is mutable. It can be updated by the component, typically using the `setState` method in class components or the `useState` hook in functional components.

2. **Local to Component**:

   - State is local to the component in which it is defined. This means that each component can have its own state and manage it independently of other components.

3. **Initial State**:

   - State can be initialized when a component is created. For class components, this is done in the constructor method, while for functional components, initial state is set using the `useState` hook.

4. **State Updates**:

   - State updates are asynchronous and can be scheduled using `setState` in class components or by calling the setter function returned by `useState` in functional components.

5. **Re-rendering**:

   - When state changes, React triggers a re-render of the component, updating the UI to reflect the new state.

6. **State Management**:
   - For complex state management, especially in larger applications, state management libraries like Redux or Context API can be used to handle state across multiple components.

### Example

**Class Component**:

```jsx
import React, { Component } from "react";

class Counter extends Component {
  constructor(props) {
    super(props);
    // Initialize state
    this.state = {
      count: 0,
    };
  }

  increment = () => {
    // Update state
    this.setState({ count: this.state.count + 1 });
  };

  render() {
    return (
      <div>
        <p>Count: {this.state.count}</p>
        <button onClick={this.increment}>Increment</button>
      </div>
    );
  }
}

export default Counter;
```

**Functional Component with Hooks**:

```jsx
import React, { useState } from "react";

function Counter() {
  // Initialize state
  const [count, setCount] = useState(0);

  const increment = () => {
    // Update state
    setCount(count + 1);
  };

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={increment}>Increment</button>
    </div>
  );
}

export default Counter;
```

### Summary

- **State** in React is used to store and manage data that changes over time within a component.
- It allows components to be interactive and responsive to user inputs or other events.
- State is mutable and can be updated with the `setState` method in class components or the `useState` hook in functional components.
- Managing state effectively is crucial for building dynamic and responsive user interfaces in React applications.
