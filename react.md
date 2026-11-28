
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
