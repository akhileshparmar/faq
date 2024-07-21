# props

In React, **props** (short for properties) are a mechanism for passing data and event handlers from a parent component to a child component. They allow components to communicate and share data in a unidirectional flow, meaning data flows only from parent to child components.

### Key Points About Props

1. **Read-Only**:

   - Props are immutable, meaning they cannot be changed by the child component. They are meant to be used as read-only data passed from a parent component.

2. **Data Flow**:

   - Props enable a unidirectional data flow from parent to child components. This helps maintain a clear and predictable structure for component interaction.

3. **Functional Components**:

   - In functional components, props are passed as an argument to the function. Example:
     ```jsx
     function MyComponent(props) {
       return <div>{props.message}</div>;
     }
     ```

4. **Class Components**:

   - In class components, props are accessed via `this.props`. Example:
     ```jsx
     class MyComponent extends React.Component {
       render() {
         return <div>{this.props.message}</div>;
       }
     }
     ```

5. **Default Props**:

   - You can define default values for props using the `defaultProps` property. This ensures that a component has default values if no props are provided.
     ```jsx
     MyComponent.defaultProps = {
       message: "Default message",
     };
     ```

6. **Prop Types**:

   - You can define the expected types of props using the `prop-types` package. This helps with validation and ensures that the component receives the correct data types.

     ```jsx
     import PropTypes from "prop-types";

     MyComponent.propTypes = {
       message: PropTypes.string.isRequired,
     };
     ```

### Example

Here’s a simple example of how props are used:

**Parent Component**:

```jsx
function ParentComponent() {
  return <ChildComponent message="Hello, World!" />;
}
```

**Child Component**:

```jsx
function ChildComponent(props) {
  return <div>{props.message}</div>;
}
```

In this example, `ParentComponent` passes a prop called `message` to `ChildComponent`. The `ChildComponent` then uses this prop to render its content.

### Summary

- **Props** are a fundamental concept in React for passing data and event handlers between components.
- They help in achieving component reusability and maintaining a clear data flow.
- Props are read-only and help ensure that components are predictable and easy to manage.
