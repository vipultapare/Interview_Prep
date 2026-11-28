
# React: Props vs State

This README explains **Props** and **State** in React in simple words, with practical examples and interview-focused explanations.

## Table of Contents

1. [What are Props?](#1-what-are-props)
2. [What is State?](#2-what-is-state)
3. [Props vs State](#3-props-vs-state)
4. [Using Props and State Together](#4-using-props-and-state-together)
5. [How Can a Child Update Parent State?](#5-how-can-a-child-update-parent-state)
6. [Lifting State Up](#6-lifting-state-up)
7. [Real-World Example](#7-real-world-example)
8. [Interview Answer](#8-interview-answer)
9. [Quick Revision](#9-quick-revision)

---

# 1. What are Props?

## Definition

Props (short for properties) are data passed from a parent component to a child component.

Props allow React components to communicate and share data.

Think of props as arguments passed to a function.

## Example

```jsx
function Welcome(props) {
    return <h1>Hello, {props.name}</h1>;
}

function App() {
    return <Welcome name="Vipul" />;
}
```

### Output

```text
Hello, Vipul
```

### How does it work?

1. `App` is the parent component.
2. `Welcome` is the child component.
3. `App` passes `name="Vipul"` to `Welcome`.
4. `Welcome` receives the value through `props`.
5. The component displays the received value.

### Component Flow

```text
App (Parent)
    |
    | Passes name="Vipul"
    | 
    v
Welcome (Child)
    |
    v
Hello, Vipul
```

## Using Props with Destructuring

Instead of:

```jsx
function Welcome(props) {
    return <h1>Hello, {props.name}</h1>;
}
```

We can write:

```jsx
function Welcome({ name }) {
    return <h1>Hello, {name}</h1>;
}
```

Destructuring allows us to directly extract values from the props object.

## Example with Multiple Props

```jsx
function UserProfile({ name, age, role }) {
    return (
        <div>
            <h2>{name}</h2>
            <p>Age: {age}</p>
            <p>Role: {role}</p>
        </div>
    );
}

function App() {
    return (
        <UserProfile
            name="Vipul"
            age={24}
            role="Full Stack Developer"
        />
    );
}
```

## Can a Child Modify Props?

Props should be treated as read-only by the receiving component.

A child component should not directly modify the props it receives.

However, a parent can render with new prop values, and the child can receive those updated values.

### Remember

**Props = Data passed from parent to child.**

---

# 2. What is State?

## Definition

State is data managed by a component or its state owner that can change over time.

State is used to store information that affects what is displayed on the UI.

Examples:

- Counter value
- Input field value
- Selected tab
- Modal visibility
- Shopping cart quantity
- Login status

In React functional components, we use the `useState()` Hook to manage state.

## Example: Counter

```jsx
import { useState } from "react";

function Counter() {
    const [count, setCount] = useState(0);

    return (
        <div>
            <h1>{count}</h1>

            <button onClick={() => setCount(count + 1)}>
                Increment
            </button>
        </div>
    );
}
```

### Output

Initially:

```text
0
```

After clicking the button:

```text
1
2
3
4
```

## Understanding useState()

```jsx
const [count, setCount] = useState(0);
```

| Part | Meaning |
|---|---|
| `count` | Current state value |
| `setCount` | Function used to update state |
| `0` | Initial state value |

### How does it work?

1. `useState(0)` initializes the state with `0`.
2. `count` contains the current state value.
3. `setCount()` updates the state.
4. React schedules a re-render.
5. The UI reflects the updated value.

## Updating State

```jsx
setCount(count + 1);
```

We should not directly modify state.

### Incorrect

```jsx
count = count + 1;
```

### Correct

```jsx
setCount(count + 1);
```

## Using Functional State Updates

When the next state depends on the previous state, we can use a functional update.

```jsx
setCount((previousCount) => previousCount + 1);
```

This is especially useful when multiple state updates depend on the previous value.

### Remember

**State = Data managed by a state owner that can change over time.**

---

# 3. Props vs State

| Props | State |
|---|---|
| Passed from parent to child | Managed by a component or state owner |
| Read-only for the receiving component | Updated using state setter functions |
| Used to pass data between components | Used to manage changing data |
| Parent provides the value | State owner controls the value |
| Similar to function arguments | Similar to component memory |
| Can change when the parent renders with new values | Can change when the state setter is called |

## Simple Comparison

```text
PROPS

Parent Component
      |
      | Passes data
      v
Child Component
      |
      v
Displays received data
```

```text
STATE

Component / State Owner
      |
      | Manages data
      v
State changes
      |
      v
React re-renders UI
```

### Props Example

```jsx
function UserProfile({ name }) {
    return <h1>{name}</h1>;
}

function App() {
    return <UserProfile name="Vipul" />;
}
```

Here, `name` is a prop.

### State Example

```jsx
import { useState } from "react";

function Counter() {
    const [count, setCount] = useState(0);

    return (
        <button onClick={() => setCount(count + 1)}>
            {count}
        </button>
    );
}
```

Here, `count` is state.

---

# 4. Using Props and State Together

Props and state can work together.

A parent component can maintain state and pass that state to a child component through props.

## Example

```jsx
import { useState } from "react";

function App() {
    const [username, setUsername] = useState("Vipul");

    return (
        <div>
            <UserProfile name={username} />
        </div>
    );
}

function UserProfile({ name }) {
    return <h1>Hello, {name}</h1>;
}
```

### How does it work?

1. `App` manages the state `username`.
2. `App` passes `username` to `UserProfile` as a prop.
3. `UserProfile` receives the value.
4. `UserProfile` displays the value.
5. If the parent's state changes, React renders again and the child can receive the updated prop.

### Flow

```text
App Component
    |
    | State: username = "Vipul"
    |
    | Passes username through props
    v
UserProfile Component
    |
    | Receives name
    v
Hello, Vipul
```

---

# 5. How Can a Child Update Parent State?

A child cannot directly modify the parent's state.

However, the parent can pass a function to the child through props.

The child can call that function to request an update to the parent's state.

## Example

```jsx
import { useState } from "react";

function App() {
    const [count, setCount] = useState(0);

    return (
        <div>
            <h1>Parent Count: {count}</h1>

            <Child
                onIncrement={() => setCount((prev) => prev + 1)}
            />
        </div>
    );
}

function Child({ onIncrement }) {
    return (
        <button onClick={onIncrement}>
            Increment Parent Count
        </button>
    );
}
```

### How does it work?

1. `App` owns the `count` state.
2. `App` passes `onIncrement` to `Child`.
3. The child calls `onIncrement` when the button is clicked.
4. The callback updates the parent's state.
5. React renders again with the new value.

### Flow

```text
Parent Component
    |
    | Owns count state
    |
    | Passes callback through props
    v
Child Component
    |
    | Calls callback
    v
Parent State Updated
    |
    v
React Re-render
```

### Remember

**Props can pass data down, and callback functions can allow children to trigger updates in the parent.**

---

# 6. Lifting State Up

## What is Lifting State Up?

Lifting state up means moving state from a child component to a common parent component when multiple components need access to the same state.

## Example

Imagine two components:

- `InputComponent` allows the user to enter a name.
- `DisplayComponent` displays that name.

If both components need the same data, we can maintain the state in their common parent.

```jsx
import { useState } from "react";

function App() {
    const [name, setName] = useState("");

    return (
        <div>
            <InputComponent name={name} setName={setName} />

            <DisplayComponent name={name} />
        </div>
    );
}

function InputComponent({ name, setName }) {
    return (
        <input
            value={name}
            onChange={(e) => setName(e.target.value)}
            placeholder="Enter your name"
        />
    );
}

function DisplayComponent({ name }) {
    return <h1>Hello, {name}</h1>;
}
```

### How does it work?

1. `App` owns the state.
2. `App` passes the value and setter function to `InputComponent`.
3. `InputComponent` updates the state through the setter function.
4. `App` passes the updated value to `DisplayComponent`.
5. `DisplayComponent` displays the updated value.

### Flow

```text
                 App
          (State: name)
             /     \
            /       \
           v         v
    InputComponent  DisplayComponent
       Updates       Displays
        State         Value
```

### Remember

**Lifting State Up = Move shared state to a common parent.**

---

# 7. Real-World Example

Imagine an e-commerce application.

## Props

We can pass product information to a ProductCard component.

```jsx
function ProductCard({ name, price, image }) {
    return (
        <div>
            <img src={image} alt={name} />

            <h2>{name}</h2>

            <p>Price: ₹{price}</p>
        </div>
    );
}

function App() {
    return (
        <ProductCard
            name="Laptop"
            price={50000}
            image="laptop.jpg"
        />
    );
}
```

Here:

- `name` is a prop.
- `price` is a prop.
- `image` is a prop.

## State

We can manage the quantity of a product.

```jsx
import { useState } from "react";

function ProductCard({ name, price }) {
    const [quantity, setQuantity] = useState(1);

    return (
        <div>
            <h2>{name}</h2>

            <p>Price: ₹{price}</p>

            <p>Quantity: {quantity}</p>

            <button
                onClick={() => setQuantity((prev) => prev + 1)}
            >
                Increase Quantity
            </button>

            <p>Total: ₹{price * quantity}</p>
        </div>
    );
}
```

Here:

- `name` and `price` are props.
- `quantity` is state.
- `setQuantity` updates the state.
- The total changes when quantity changes.

---

# 8. Interview Answer

## What is the difference between Props and State in React?

Props and state are both used to manage data in React, but they serve different purposes.

Props are data passed from a parent component to a child component. The receiving component treats props as read-only and uses them to render its UI.

State is data managed by a component or its state owner that can change over time. In functional components, we use the `useState` Hook to manage state. When state is updated, React schedules a re-render so the UI reflects the updated value.

For example, in a user profile component, the username can be passed as a prop from the parent, whereas the selected tab or input value can be maintained as state.

We can also pass callback functions as props to allow child components to trigger state updates in their parent components.

---

# 9. Quick Revision

| Concept | Meaning |
|---|---|
| Props | Data passed from parent to child |
| State | Data managed by a state owner |
| `useState()` | Hook used to manage state |
| State setter | Function used to update state |
| Re-render | React renders the component again based on updated data |
| Lifting state up | Moving shared state to a common parent |
| Callback props | Functions passed to children to trigger actions or updates |

## My Revision Shortcut

- **PROPS** → Data received
- **STATE** → Data managed
- **PROPS** → Parent to child
- **CALLBACKS** → Child can trigger parent updates
- **LIFTING STATE UP** → Move shared state to a common parent
- **`useState()`** → Manage state in functional components

---

## Final Takeaway

Props and state are fundamental concepts in React.

Props allow components to receive data from other components, while state allows a state owner to manage changing data.

Both work together to build dynamic, reusable and interactive React applications.



# React Hooks – `useState`, `useEffect`, `useMemo`, `useCallback`

## Table of Contents

- [What are React Hooks?](#what-are-react-hooks)
- [1. useState](#1-usestate)
- [2. useEffect](#2-useeffect)
- [3. useMemo](#3-usememo)
- [4. useCallback](#4-usecallback)
- [useMemo vs useCallback](#usememo-vs-usecallback)
- [React.memo](#reactmemo)
- [Real-World Example](#real-world-example)
- [Common Mistakes](#common-mistakes)
- [Interview Questions](#interview-questions)
- [Interview-Ready Explanation](#interview-ready-explanation)
- [Quick Revision](#quick-revision)

---

# What are React Hooks?

React Hooks are special functions that allow functional components to use React features such as state, side effects and performance optimizations.

Before Hooks, developers primarily used class components to manage state and lifecycle-related behavior.

Hooks allow us to use these features inside functional components.

### Commonly used Hooks

| Hook | Purpose |
|---|---|
| `useState` | Manage component state |
| `useEffect` | Handle side effects |
| `useMemo` | Memoize calculated values |
| `useCallback` | Memoize function references |

---

# 1. `useState`

## What is `useState`?

`useState` is a React Hook that allows us to store, manage and update data inside a functional component.

Think of it as the memory of a component.

For example:

- Counter value
- Form inputs
- Login status
- Modal visibility
- Selected dropdown value
- Shopping cart quantity

When state changes, React re-renders the component and updates the UI.

## Syntax

```jsx
const [state, setState] = useState(initialValue);
```

| Part | Meaning |
|---|---|
| `state` | Current state value |
| `setState` | Function used to update the state |
| `initialValue` | Initial value of the state |

## Example: Counter

```jsx
import { useState } from 'react';

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <h2>Count: {count}</h2>

      <button onClick={() => setCount(count + 1)}>
        Increase
      </button>

      <button onClick={() => setCount(count - 1)}>
        Decrease
      </button>
    </div>
  );
}

export default Counter;
```

## How does it work?

1. `useState(0)` initializes the count with `0`.
2. `count` contains the current value.
3. `setCount()` updates the state.
4. React re-renders the component when the state changes.
5. The UI displays the updated value.

## Updating state using the previous value

When the next state depends on the previous state, use the functional updater form.

```jsx
setCount(previousCount => previousCount + 1);
```

This is useful because React may batch multiple state updates.

### Example

```jsx
function Counter() {
  const [count, setCount] = useState(0);

  const increaseCount = () => {
    setCount(previousCount => previousCount + 1);
  };

  return (
    <button onClick={increaseCount}>
      {count}
    </button>
  );
}
```

## Interview Answer

`useState` is a React Hook that allows functional components to manage state. It returns the current state value and a setter function. When we update the state using the setter function, React schedules a re-render to update the UI.

---

# 2. `useEffect`

## What is `useEffect`?

`useEffect` is a React Hook used to handle side effects in functional components.

A side effect is an operation that interacts with something outside the component's normal rendering process.

### Common use cases

- Fetching data from APIs
- Setting timers
- Adding event listeners
- WebSocket connections
- Subscribing to events
- Updating document title

## Syntax

```jsx
useEffect(() => {
  // Side effect logic

  return () => {
    // Cleanup logic
  };
}, [dependencies]);
```

## Understanding the dependency array

### 1. Without dependency array

```jsx
useEffect(() => {
  console.log('Effect executed');
});
```

The Effect runs after every render.

### 2. Empty dependency array

```jsx
useEffect(() => {
  console.log('Component mounted');
}, []);
```

The Effect runs after the initial mount.

In development, React Strict Mode may run an additional setup and cleanup cycle to help identify bugs.

### 3. With dependencies

```jsx
useEffect(() => {
  console.log('Count changed');
}, [count]);
```

The Effect runs after the initial mount and when `count` changes.

## Example: Fetch API data

```jsx
import { useEffect, useState } from 'react';

function Users() {
  const [users, setUsers] = useState([]);
  const [loading, setLoading] = useState(true);

  useEffect(() => {
    async function fetchUsers() {
      try {
        const response = await fetch(
          'https://jsonplaceholder.typicode.com/users'
        );

        const data = await response.json();

        setUsers(data);
      } catch (error) {
        console.error(error);
      } finally {
        setLoading(false);
      }
    }

    fetchUsers();
  }, []);

  if (loading) {
    return <p>Loading...</p>;
  }

  return (
    <div>
      <h2>Users</h2>

      {users.map(user => (
        <p key={user.id}>{user.name}</p>
      ))}
    </div>
  );
}

export default Users;
```

## How does it work?

1. The component renders.
2. React commits the render.
3. The Effect executes.
4. The API request is made.
5. The API returns data.
6. `setUsers()` updates state.
7. React re-renders the component with the users.

## Cleanup function

Sometimes, we need to clean up something that we started.

For example:

- Stop timers
- Remove event listeners
- Disconnect WebSockets
- Cancel or ignore outdated asynchronous work

### Example: Timer

```jsx
import { useEffect } from 'react';

function Timer() {
  useEffect(() => {
    const timer = setInterval(() => {
      console.log('Hello');
    }, 1000);

    return () => {
      clearInterval(timer);
    };
  }, []);

  return <h2>Timer Component</h2>;
}
```

### How does cleanup work?

1. The timer starts when the component mounts.
2. The timer executes every second.
3. When the component unmounts, the cleanup function runs.
4. `clearInterval()` stops the timer.

## Interview Answer

`useEffect` is used to handle side effects in functional components. It is commonly used for API calls, timers, event listeners and subscriptions. It executes after React commits a render and uses a dependency array to control when it runs. It can also return a cleanup function to clean up resources.

---

# 3. `useMemo`

## What is `useMemo`?

`useMemo` is a React Hook that memoizes the result of a calculation.

Think of it as remembering the result of a calculation so that React doesn't need to perform the calculation again unnecessarily.

It is primarily used for performance optimization when calculations are expensive.

## Syntax

```jsx
const memoizedValue = useMemo(() => {
  return calculation();
}, [dependencies]);
```

| Part | Meaning |
|---|---|
| Function | Performs the calculation |
| Dependencies | Values that determine when the calculation should run again |
| Return value | The memoized calculation result |

## Example: Filtering employees

```jsx
import { useMemo, useState } from 'react';

const employees = [
  { name: 'Amit', salary: 40000 },
  { name: 'Rahul', salary: 60000 },
  { name: 'Sneha', salary: 80000 },
  { name: 'Priya', salary: 30000 }
];

function Employees() {
  const [count, setCount] = useState(0);

  const highSalaryEmployees = useMemo(() => {
    console.log('Filtering employees');

    return employees.filter(
      employee => employee.salary > 50000
    );
  }, []);

  return (
    <div>
      <h2>High Salary Employees</h2>

      {highSalaryEmployees.map(employee => (
        <p key={employee.name}>
          {employee.name} - {employee.salary}
        </p>
      ))}

      <button onClick={() => setCount(count + 1)}>
        Counter: {count}
      </button>
    </div>
  );
}

export default Employees;
```

## How does it work?

1. React executes the calculation on the initial render.
2. React stores the calculated result.
3. When the component re-renders, React checks the dependencies.
4. If dependencies haven't changed, React reuses the previous result.
5. If dependencies change, React calculates the value again.

In the above example, clicking the counter doesn't require filtering the employees again because the employee array is defined outside the component and the dependencies are unchanged.

## Example with dependencies

```jsx
import { useMemo, useState } from 'react';

const employees = [
  { name: 'Amit', salary: 40000 },
  { name: 'Rahul', salary: 60000 },
  { name: 'Sneha', salary: 80000 }
];

function Employees() {
  const [minimumSalary, setMinimumSalary] = useState(50000);

  const filteredEmployees = useMemo(() => {
    return employees.filter(
      employee => employee.salary > minimumSalary
    );
  }, [minimumSalary]);

  return (
    <div>
      <input
        type="number"
        value={minimumSalary}
        onChange={event =>
          setMinimumSalary(Number(event.target.value))
        }
      />

      {filteredEmployees.map(employee => (
        <p key={employee.name}>
          {employee.name} - {employee.salary}
        </p>
      ))}
    </div>
  );
}
```

Here, the calculation runs again when `minimumSalary` changes.

## When should we use `useMemo`?

Use it when:

- A calculation is expensive.
- Filtering or sorting large datasets.
- A computed value is passed to a memoized child and referential stability matters.
- You have identified a performance problem and memoization helps.

Don't use it for every calculation. Most simple calculations don't require memoization.

## Interview Answer

`useMemo` is a performance optimization Hook that memoizes the result of a calculation. It recalculates the value only when its dependencies change, helping avoid unnecessary expensive calculations during re-renders.

---

# 4. `useCallback`

## What is `useCallback`?

`useCallback` is a React Hook that memoizes a function reference.

Think of it as remembering the function itself instead of creating a new function reference on every render.

It is useful when passing functions to memoized child components or when a stable function reference is required.

## Syntax

```jsx
const memoizedFunction = useCallback(() => {
  // Function logic
}, [dependencies]);
```

## Example

```jsx
import { useCallback, useState } from 'react';

function Parent() {
  const [count, setCount] = useState(0);

  const handleClick = useCallback(() => {
    console.log('Button clicked');
  }, []);

  return (
    <div>
      <h2>Count: {count}</h2>

      <button onClick={() => setCount(count + 1)}>
        Increase
      </button>

      <Child onClick={handleClick} />
    </div>
  );
}

function Child({ onClick }) {
  console.log('Child rendered');

  return (
    <button onClick={onClick}>
      Click Child
    </button>
  );
}

export default Parent;
```

In this example, `handleClick` is memoized.

However, the child can still re-render when the parent re-renders. `useCallback` alone doesn't prevent child re-renders.

## `useCallback` with `React.memo`

```jsx
import React, { useCallback, useState } from 'react';

function Parent() {
  const [count, setCount] = useState(0);

  const handleClick = useCallback(() => {
    console.log('Button clicked');
  }, []);

  return (
    <div>
      <h2>Count: {count}</h2>

      <button onClick={() => setCount(count + 1)}>
        Increase
      </button>

      <Child onClick={handleClick} />
    </div>
  );
}

const Child = React.memo(function Child({ onClick }) {
  console.log('Child rendered');

  return (
    <button onClick={onClick}>
      Click Child
    </button>
  );
});

export default Parent;
```

## How does it work?

1. The parent component renders.
2. React creates the function during the initial render and stores its reference.
3. When the parent re-renders, React checks the dependencies.
4. If dependencies haven't changed, React reuses the previous function reference.
5. `React.memo` compares the child's props.
6. If the props haven't changed, the child can skip re-rendering.

## When should we use `useCallback`?

Use it when:

- Passing functions to memoized child components.
- Preventing unnecessary child re-renders when referential stability matters.
- A function is used as a dependency in another Hook.
- You have identified a performance issue where a stable callback helps.

## Interview Answer

`useCallback` is a React Hook that memoizes a function reference and returns the same function between renders until its dependencies change. It is useful for performance optimization, especially when passing functions to memoized child components.

---

# useMemo vs useCallback

Both Hooks are used for performance optimization, but they memoize different things.

| Feature | `useMemo` | `useCallback` |
|---|---|---|
| What does it memoize? | A calculated value | A function reference |
| What does it return? | Memoized result | Memoized function |
| Main purpose | Avoid recalculations | Maintain stable function references |
| Typical example | Filtering large arrays | Passing callbacks to child components |

### `useMemo`

```jsx
const value = useMemo(() => {
  return calculateValue();
}, [dependency]);
```

It remembers the result of the calculation.

### `useCallback`

```jsx
const handleClick = useCallback(() => {
  doSomething();
}, [dependency]);
```

It remembers the function reference.

### Easy way to remember

- `useMemo` = Remember the value.
- `useCallback` = Remember the function.

---

# React.memo

## What is `React.memo`?

`React.memo` is a React API that allows a component to skip re-rendering when its props haven't changed.

It is useful for optimizing components that receive the same props frequently.

## Example

```jsx
import React from 'react';

const Child = React.memo(function Child({ name }) {
  console.log('Child rendered');

  return <h2>Hello {name}</h2>;
});

export default Child;
```

If the `name` prop remains unchanged, React can skip re-rendering the child when its parent renders again.

### Important

- `React.memo` memoizes a component based on its props.
- `useMemo` memoizes a calculated value.
- `useCallback` memoizes a function reference.

They are related, but they solve different problems.

---

# Real-World Example

## Product Card

Imagine an e-commerce application.

We have:

- Product name
- Product price
- Quantity
- Total price
- An increment button

We can use `useState` for quantity and `useMemo` for calculating the total price.

```jsx
import { useMemo, useState } from 'react';

function ProductCard() {
  const [quantity, setQuantity] = useState(1);

  const price = 1000;

  const totalPrice = useMemo(() => {
    return price * quantity;
  }, [price, quantity]);

  return (
    <div>
      <h2>Product: Laptop</h2>

      <p>Price: ₹{price}</p>

      <p>Quantity: {quantity}</p>

      <button onClick={() => setQuantity(q => q + 1)}>
        Increase Quantity
      </button>

      <button
        onClick={() =>
          setQuantity(q => Math.max(1, q - 1))
        }
      >
        Decrease Quantity
      </button>

      <h3>Total: ₹{totalPrice}</h3>
    </div>
  );
}

export default ProductCard;
```

### Hooks used

| Hook | Usage |
|---|---|
| `useState` | Manage quantity |
| `useMemo` | Calculate total price |

Note: The total price calculation is very simple, so `useMemo` isn't necessary in this particular example. It is included to demonstrate how it works.

---

# Common Mistakes

## 1. Updating state directly

Incorrect:

```jsx
count = count + 1;
```

Correct:

```jsx
setCount(count + 1);
```

React state should be updated using the state setter.

---

## 2. Using `useEffect` without understanding dependencies

```jsx
useEffect(() => {
  fetchData();
}, []);
```

The empty dependency array means the Effect runs after the initial mount, not every time any state changes.

---

## 3. Using `useMemo` everywhere

Incorrect mindset:

> Every calculation should use `useMemo`.

Correct mindset:

> Use `useMemo` when a calculation is expensive or memoization is beneficial for performance.

---

## 4. Thinking `useCallback` prevents re-renders

`useCallback` does not directly prevent a component from re-rendering.

It memoizes a function reference.

For a child component to skip rendering based on unchanged props, `React.memo` may also be useful.

---

## 5. Missing dependencies

```jsx
useEffect(() => {
  console.log(count);
}, []);
```

If the Effect is supposed to react to changes in `count`, then `count` should be included in the dependency array.

```jsx
useEffect(() => {
  console.log(count);
}, [count]);
```

Always follow the dependency rules and lint recommendations.

---

# Interview Questions

## 1. What are React Hooks?

React Hooks are functions that allow functional components to use React features such as state, side effects and other functionality.

## 2. What is `useState`?

`useState` is used to manage state inside functional components. It returns the current state and a setter function.

## 3. What is `useEffect`?

`useEffect` is used to handle side effects such as API calls, timers, event listeners and subscriptions.

## 4. What is the difference between `useEffect` with an empty dependency array and without a dependency array?

- Empty dependency array: runs after the initial mount.
- No dependency array: runs after every render.

## 5. What is `useMemo`?

`useMemo` memoizes the result of a calculation and recalculates it when its dependencies change.

## 6. What is `useCallback`?

`useCallback` memoizes a function reference and returns the same function between renders until dependencies change.

## 7. What is the difference between `useMemo` and `useCallback`?

`useMemo` memoizes a calculated value, whereas `useCallback` memoizes a function reference.

## 8. Does `useCallback` prevent re-renders?

No. It memoizes a function reference. `React.memo` can help a child component skip re-rendering when its props remain unchanged.

## 9. What is the purpose of the cleanup function in `useEffect`?

It cleans up resources such as timers, subscriptions and event listeners when the Effect is cleaned up.

## 10. Can we use Hooks inside loops or conditions?

No. Hooks should be called at the top level of React function components or custom Hooks, not inside loops, conditions or nested functions.

## 11. What is `React.memo`?

`React.memo` is used to memoize a component so React can skip re-rendering it when its props remain unchanged.

## 12. What is the difference between state and props?

- State is managed by a component or its state owner.
- Props are values passed from a parent component to a child component.

---

# Interview-Ready Explanation

If an interviewer asks you to explain these Hooks, you can answer:

> React Hooks allow us to use React features inside functional components.
>
> `useState` is used to manage component state, such as form data, counters and UI visibility. Whenever state changes, React re-renders the component.
>
> `useEffect` is used to handle side effects such as API calls, event listeners, timers and subscriptions. We can control when it executes using the dependency array and return a cleanup function when necessary.
>
> `useMemo` is used to memoize the result of a calculation to avoid unnecessary recalculations when dependencies haven't changed.
>
> `useCallback` is used to memoize a function reference. It is particularly useful when passing callbacks to memoized child components to avoid unnecessary re-renders.
>
> I use `useMemo` and `useCallback` primarily when there is a performance benefit, rather than using them everywhere.

---

# Quick Revision

| Hook | Remember | Example |
|---|---|---|
| `useState` | Data | Counter, form |
| `useEffect` | Side effects | API call, timer |
| `useMemo` | Value | Filter, sort, calculation |
| `useCallback` | Function | Callback prop |
| `React.memo` | Component | Avoid unnecessary child render |

### Easy mnemonic

- **State** → Store data.
- **Effect** → Do something after render.
- **Memo** → Remember a calculated value.
- **Callback** → Remember a function.
- **Memo component** → Skip rendering when props haven't changed.

---

## Recommended learning order

1. `useState`
2. `useEffect`
3. Props and State
4. Conditional Rendering
5. Lists and Keys
6. `useMemo`
7. `useCallback`
8. `React.memo`
9. Custom Hooks

---

