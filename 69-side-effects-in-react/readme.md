# Effects in React: Without Cleanup and With Cleanup

In React, the `useEffect` hook is used to handle side effects in functional components. Effects can be categorized into two types: those without cleanup and those with cleanup.

#### Effects Without Cleanup

Effects without cleanup are those that do not require any cleanup when the component re-renders or unmounts. These effects are typically used for operations that do not set up any ongoing processes or subscriptions that need to be cleaned up later.

##### Example

A common example of an effect without cleanup is updating the document title based on the component state.

```javascript
import React, { useState, useEffect } from "react";

function ExampleComponent() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    document.title = `You clicked ${count} times`;
  }, [count]); // Effect runs when 'count' changes

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>Click me</button>
    </div>
  );
}

export default ExampleComponent;
```

In this example, the effect updates the document title whenever the `count` state changes. There's no ongoing process or subscription to clean up, so no cleanup function is needed.

#### Effects With Cleanup

Effects with cleanup are those that set up some kind of ongoing process or subscription that needs to be cleaned up when the component re-renders or unmounts. This is important to avoid memory leaks or unwanted behavior.

##### Example

A common example of an effect with cleanup is setting up a subscription or a timer.

```javascript
import React, { useState, useEffect } from "react";

function ExampleComponent() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    // Setting up a timer
    const timer = setInterval(() => {
      console.log(`Count is ${count}`);
    }, 1000);

    // Cleanup function to clear the timer
    return () => {
      clearInterval(timer);
    };
  }, [count]); // Effect runs when 'count' changes

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>Click me</button>
    </div>
  );
}

export default ExampleComponent;
```

In this example, a timer is set up to log the `count` value every second. The cleanup function, returned from the effect, clears the timer when the component re-renders or unmounts to avoid multiple timers running simultaneously and potential memory leaks.

#### Key Differences

- **Without Cleanup**: No ongoing processes or subscriptions to clean up.

  - Example: Updating document title, logging to console, fetching data once.
  - Usage: When the side effect doesn't need to be reversed or cleaned up.

- **With Cleanup**: Sets up processes or subscriptions that need to be cleaned up.
  - Example: Setting up timers, subscriptions (like WebSocket or event listeners).
  - Usage: When the side effect creates a persistent resource or subscription that needs to be released or cleaned up to avoid resource leaks or unintended behavior.

#### Summary

Understanding when and how to use cleanup in effects is crucial for managing resources and ensuring the stability of your React applications. Effects without cleanup are straightforward and used for simple operations, while effects with cleanup are essential for managing ongoing processes and avoiding resource leaks.
