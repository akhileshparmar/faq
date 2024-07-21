# state vs props

In React, both **state** and **props** are used to manage data and control how components behave and render. However, they have distinct roles and characteristics:

### Comparison of State and Props

| Feature            | State                                                                                                                         | Props                                                                            |
| ------------------ | ----------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------- |
| **Definition**     | A built-in feature in React that allows components to maintain and manage their own data.                                     | Data passed from a parent component to a child component.                        |
| **Mutability**     | Mutable; can be changed within the component that owns it.                                                                    | Immutable; cannot be changed by the child component.                             |
| **Source**         | Managed within the component itself.                                                                                          | Managed by the parent component and passed down.                                 |
| **Initialization** | Initialized within the component, typically in the constructor (class components) or with `useState` (functional components). | Initialized and set by the parent component when it renders the child component. |
| **Update**         | Can be updated using `setState` in class components or setter functions from `useState` in functional components.             | Cannot be updated by the child component; can only be updated by the parent.     |
| **Purpose**        | Used to manage dynamic data that affects the rendering of a component.                                                        | Used to pass static or dynamic data from a parent component to child components. |
| **Re-rendering**   | Changes to state trigger a re-render of the component that owns the state.                                                    | Changes to props trigger a re-render of the child component receiving the props. |
| **Scope**          | Local to the component; each component has its own state.                                                                     | Global to the component tree; accessible to child components through props.      |

### Summary

- **State** is used to manage data that changes over time and affects the component's behavior and rendering. It is mutable and managed within the component.
- **Props** are used to pass data from a parent component to a child component. They are immutable and controlled by the parent component.

Understanding the differences between state and props is crucial for effective React development, as it helps in designing components that are reusable, maintainable, and efficient.
