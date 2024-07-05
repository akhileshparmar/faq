# React Fiber

React Fiber is the reimplementation of the React core algorithm. It is a complete rewrite of the previous reconciliation algorithm to address limitations in its architecture, particularly around responsiveness and the ability to handle complex updates. React Fiber aims to make React more efficient and provide a more powerful foundation for future improvements. Here's an in-depth look at what React Fiber is and how it works:

### Key Goals of React Fiber

1. **Incremental Rendering**:

   - **Time-Slicing**: Breaks rendering work into chunks and spreads it over multiple frames. This approach helps in maintaining a smooth user experience by avoiding blocking the main thread for extended periods.
   - **Prioritization**: React Fiber assigns different priorities to different types of updates, ensuring that more critical updates (like user input) are handled before less critical ones (like data fetching).

2. **Better Handling of Complex UIs**:

   - **Concurrency**: Supports concurrent rendering, allowing React to pause and resume work. This makes it easier to handle complex UIs without dropping frames or causing jank.
   - **Error Handling**: Improved error boundaries for better error handling and recovery in React components.

3. **Animation and Layout**:
   - **Smooth Animations**: Fiber can better schedule animations, ensuring that they run smoothly without being interrupted by other tasks.

### How React Fiber Works

#### 1. Fiber Nodes

Each Fiber node corresponds to a React element, such as a component, DOM element, or text node. These nodes form a Fiber tree that represents the component tree of the application.

#### 2. Two Phases of Fiber

1. **Reconciliation (Render Phase)**:

   - **Work Preparation**: Fiber starts by creating a work-in-progress Fiber tree.
   - **Task Scheduling**: Fiber traverses the tree, scheduling tasks based on their priority.
   - **Virtual DOM Updates**: During this phase, Fiber builds up the work to be done but does not apply changes to the actual DOM yet.

2. **Commit Phase**:
   - **Applying Changes**: Once the reconciliation phase is complete, the commit phase updates the real DOM with the changes computed during the render phase.
   - **Single Synchronous Process**: Unlike the render phase, which can be interrupted, the commit phase is a synchronous process where all updates are applied in one go.

#### 3. Scheduling and Prioritization

React Fiber introduces a scheduling mechanism that prioritizes updates based on their type and urgency:

- **High Priority**: User interactions like typing, clicking, and input focus.
- **Medium Priority**: Animations and transitions.
- **Low Priority**: Data fetching, background updates, and non-critical tasks.

#### 4. Time-Slicing

Time-slicing allows React to split rendering work into chunks and spread it over multiple frames. This ensures that high-priority updates are not blocked by low-priority ones, and the UI remains responsive.

### Advantages of React Fiber

1. **Improved Performance**: By breaking work into chunks and prioritizing tasks, React Fiber ensures smoother updates and a more responsive UI.
2. **Concurrent Rendering**: Supports interruptible rendering, allowing React to pause and resume work as needed.
3. **Better Animations**: Ensures smoother animations by giving them higher priority and avoiding interruptions.
4. **Error Boundaries**: Improved error handling with error boundaries that allow React components to gracefully handle errors and recover.

### Example of React Fiber in Action

Here’s a simple example demonstrating how React Fiber can prioritize updates:

```jsx
class App extends React.Component {
  state = {
    text: "",
    items: [],
  };

  handleChange = (e) => {
    this.setState({ text: e.target.value });
  };

  handleAddItem = () => {
    this.setState((state) => ({
      items: [...state.items, state.text],
      text: "",
    }));
  };

  render() {
    return (
      <div>
        <input
          type="text"
          value={this.state.text}
          onChange={this.handleChange}
          placeholder="Add item"
        />
        <button onClick={this.handleAddItem}>Add</button>
        <ul>
          {this.state.items.map((item, index) => (
            <li key={index}>{item}</li>
          ))}
        </ul>
      </div>
    );
  }
}
```

In this example, updating the input field (a high-priority task) remains responsive even as new items are added to the list (a lower-priority task), demonstrating React Fiber’s prioritization and scheduling capabilities.

### Conclusion

React Fiber represents a significant improvement over the previous reconciliation algorithm, making React more efficient and capable of handling complex applications. By supporting incremental rendering, prioritization, and concurrency, React Fiber ensures that applications remain responsive and performant, providing a solid foundation for future enhancements.
