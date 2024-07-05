# Lifting State Up in React

#### What is "Lifting State Up"?

In React, "lifting state up" is a pattern used to share state between multiple components. When multiple components need to access and manipulate the same piece of state, the state should be lifted up to the nearest common ancestor component of those components. This common ancestor can then manage the state and pass it down as props to the child components that need it.

#### Why Lift State Up?

1. **State Synchronization**: Ensures that all components have the same source of truth for a piece of state.
2. **Avoiding Duplication**: Prevents duplication of state across multiple components, reducing the risk of inconsistency.
3. **Simplifies Debugging**: Centralizes state management, making it easier to understand and debug the application.

#### How to Lift State Up

1. **Identify the Common Ancestor**: Determine the nearest common ancestor of the components that need to share the state.
2. **Move State to the Common Ancestor**: Move the state from the individual components to the common ancestor component.
3. **Pass State and Handlers as Props**: Pass the state and any state-manipulating functions as props from the common ancestor to the child components.

#### Example: Lifting State Up

Let's consider an example where we have two components, `TemperatureInput` and `BoilingVerdict`, and both need to access the same temperature value.

##### TemperatureInput Component

```javascript
import React from "react";

const TemperatureInput = ({ temperature, scale, onTemperatureChange }) => {
  const handleChange = (e) => {
    onTemperatureChange(e.target.value);
  };

  return (
    <fieldset>
      <legend>
        Enter temperature in {scale === "c" ? "Celsius" : "Fahrenheit"}:
      </legend>
      <input value={temperature} onChange={handleChange} />
    </fieldset>
  );
};

export default TemperatureInput;
```

##### BoilingVerdict Component

```javascript
import React from "react";

const BoilingVerdict = ({ celsius }) => {
  if (celsius >= 100) {
    return <p>The water would boil.</p>;
  }
  return <p>The water would not boil.</p>;
};

export default BoilingVerdict;
```

##### Calculator Component (Common Ancestor)

```javascript
import React, { useState } from "react";
import TemperatureInput from "./TemperatureInput";
import BoilingVerdict from "./BoilingVerdict";

const toCelsius = (fahrenheit) => ((fahrenheit - 32) * 5) / 9;
const toFahrenheit = (celsius) => (celsius * 9) / 5 + 32;

const tryConvert = (temperature, convert) => {
  const input = parseFloat(temperature);
  if (Number.isNaN(input)) {
    return "";
  }
  const output = convert(input);
  const rounded = Math.round(output * 1000) / 1000;
  return rounded.toString();
};

const Calculator = () => {
  const [temperature, setTemperature] = useState("");
  const [scale, setScale] = useState("c");

  const handleCelsiusChange = (temperature) => {
    setTemperature(temperature);
    setScale("c");
  };

  const handleFahrenheitChange = (temperature) => {
    setTemperature(temperature);
    setScale("f");
  };

  const celsius =
    scale === "f" ? tryConvert(temperature, toCelsius) : temperature;
  const fahrenheit =
    scale === "c" ? tryConvert(temperature, toFahrenheit) : temperature;

  return (
    <div>
      <TemperatureInput
        scale="c"
        temperature={celsius}
        onTemperatureChange={handleCelsiusChange}
      />
      <TemperatureInput
        scale="f"
        temperature={fahrenheit}
        onTemperatureChange={handleFahrenheitChange}
      />
      <BoilingVerdict celsius={parseFloat(celsius)} />
    </div>
  );
};

export default Calculator;
```

##### Explanation

1. **Common Ancestor (Calculator)**: The `Calculator` component is the common ancestor of `TemperatureInput` and `BoilingVerdict`.
2. **State Management**: The `Calculator` component holds the state for the temperature and scale. It manages the state and provides handler functions to update the state.
3. **Passing Props**: The `Calculator` component passes the state and handler functions as props to the `TemperatureInput` components. The `TemperatureInput` components call these handler functions when their input changes, updating the state in the `Calculator`.
4. **Shared State**: The `BoilingVerdict` component receives the current Celsius temperature as a prop from the `Calculator` and uses it to determine whether the water would boil.

By lifting the state up to the `Calculator` component, we ensure that the `TemperatureInput` and `BoilingVerdict` components can share and manipulate the same state, keeping the application logic consistent and centralized.
