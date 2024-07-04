# Event Propagation

Event propagation is the process by which an event travels through the DOM tree when it is triggered. There are three phases of event propagation in the DOM:

1. **Capturing Phase (Event Capturing)**
2. **Target Phase**
3. **Bubbling Phase (Event Bubbling)**

### Capturing Phase (Event Capturing)

In the capturing phase, the event starts from the root of the DOM tree and travels downwards to the target element. This phase allows parent elements to capture the event before it reaches the target element.

### Target Phase

The target phase occurs when the event has reached the target element, which is the element that originally triggered the event.

### Bubbling Phase (Event Bubbling)

In the bubbling phase, the event bubbles up from the target element back to the root of the DOM tree. This means the event starts at the target element and travels upwards to its ancestors.

### Example

Consider the following HTML structure:

```html
<div id="parent">
  <button id="child">Click Me!</button>
</div>
```

And the JavaScript code:

```javascript
document.getElementById("parent").addEventListener(
  "click",
  (event) => {
    console.log("Parent clicked");
  },
  true
); // Capturing phase

document.getElementById("child").addEventListener("click", (event) => {
  console.log("Child clicked");
});

document.getElementById("parent").addEventListener("click", (event) => {
  console.log("Parent clicked");
}); // Bubbling phase
```

### Output Explanation

When you click the button (`child`), you will see the following in the console:

1. "Parent clicked" (capturing phase)
2. "Child clicked" (target phase)
3. "Parent clicked" (bubbling phase)

### Stopping Propagation

You can stop the propagation of an event in any phase using the `stopPropagation` method.

```javascript
document.getElementById("child").addEventListener("click", (event) => {
  event.stopPropagation();
  console.log("Child clicked");
});
```

In this case, clicking the button will only log "Child clicked" because the event propagation stops at the target element and does not bubble up to the parent.

### Summary

| Phase         | Description                                           |
| ------------- | ----------------------------------------------------- |
| **Capturing** | Event travels from the root to the target element.    |
| **Target**    | Event reaches the target element.                     |
| **Bubbling**  | Event travels from the target element up to the root. |

Event propagation allows for more flexible and powerful event handling by enabling both capturing and bubbling phases, giving developers control over how and when events are processed.
