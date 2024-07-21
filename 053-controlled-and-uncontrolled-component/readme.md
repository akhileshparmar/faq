# Controlled and Uncontrolled Components in React

In React, form handling is an essential part of building user interfaces. When dealing with forms, components can be classified as either **controlled** or **uncontrolled** based on how they handle their data.

#### Controlled Components

A **controlled component** is a component that renders form elements and controls them by keeping the form data in the component's state. The form data is handled by the React component, making it the single source of truth for the form values.

##### Characteristics:

- The form data is stored in the component's state.
- Input values are controlled by React via the `value` prop.
- Changes in the input are handled via `onChange` event handlers.

##### Example:

```javascript
import React, { useState } from "react";

const ControlledComponent = () => {
  const [name, setName] = useState("");

  const handleChange = (event) => {
    setName(event.target.value);
  };

  const handleSubmit = (event) => {
    event.preventDefault();
    alert(`Submitted name: ${name}`);
  };

  return (
    <form onSubmit={handleSubmit}>
      <label>
        Name:
        <input type="text" value={name} onChange={handleChange} />
      </label>
      <button type="submit">Submit</button>
    </form>
  );
};

export default ControlledComponent;
```

#### Uncontrolled Components

An **uncontrolled component** is a component that renders form elements but does not control their data. Instead, the form data is handled by the DOM itself. Accessing the form data requires using refs to get the value directly from the DOM elements.

##### Characteristics:

- The form data is handled by the DOM, not the component's state.
- Input values are uncontrolled and accessed using refs.
- Easier to integrate with non-React code or libraries.

##### Example:

```javascript
import React, { useRef } from "react";

const UncontrolledComponent = () => {
  const nameInputRef = useRef(null);

  const handleSubmit = (event) => {
    event.preventDefault();
    alert(`Submitted name: ${nameInputRef.current.value}`);
  };

  return (
    <form onSubmit={handleSubmit}>
      <label>
        Name:
        <input type="text" ref={nameInputRef} />
      </label>
      <button type="submit">Submit</button>
    </form>
  );
};

export default UncontrolledComponent;
```

### Comparison: Controlled vs Uncontrolled Components

| Feature                    | Controlled Components                         | Uncontrolled Components                                    |
| -------------------------- | --------------------------------------------- | ---------------------------------------------------------- |
| Data Handling              | Handled by component's state                  | Handled by the DOM                                         |
| Input Value                | Controlled via `value` prop                   | Uncontrolled, accessed via refs                            |
| `onChange` Handler         | Required to update state                      | Not required for state updates                             |
| Integration with Libraries | May require more effort to integrate          | Easier to integrate with non-React libraries               |
| Ease of Debugging          | Easier to debug due to React state management | Can be harder to debug due to direct DOM manipulation      |
| Performance                | May be slower due to frequent state updates   | May be faster for large forms due to reduced state updates |

### When to Use

- **Controlled Components**:

  - When you need to handle or validate form data before submission.
  - When you need to dynamically modify the form values or enforce rules.
  - When you need more control over the form inputs and their values.

- **Uncontrolled Components**:
  - When integrating with third-party libraries that manage their own form state.
  - When building simple forms where React state management is unnecessary.
  - When you want to minimize state management for performance reasons.

Both controlled and uncontrolled components have their use cases, and understanding when to use each will help you build efficient and maintainable forms in your React applications.
