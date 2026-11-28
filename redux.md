
# Redux Architecture – Store, Actions, Reducers & Dispatch

## Table of Contents

1. [What is Redux?](#1-what-is-redux)
2. [Why Do We Need Redux?](#2-why-do-we-need-redux)
3. [Understanding State Management](#3-understanding-state-management)
4. [Redux Architecture](#4-redux-architecture)
5. [Redux Data Flow](#5-redux-data-flow)
6. [Redux Store](#6-redux-store)
7. [Actions](#7-actions)
8. [Reducers](#8-reducers)
9. [Dispatch](#9-dispatch)
10. [Action Creators](#10-action-creators)
11. [Traditional Redux Example](#11-traditional-redux-example)
12. [Redux Toolkit](#12-redux-toolkit)
13. [Implementing Redux Toolkit in React](#13-implementing-redux-toolkit-in-react)
14. [useSelector](#14-useselector)
15. [useDispatch](#15-usedispatch)
16. [Provider](#16-provider)
17. [Complete Redux Flow](#17-complete-redux-flow)
18. [Redux Folder Structure](#18-redux-folder-structure)
19. [Redux Async Operations](#19-redux-async-operations)
20. [createAsyncThunk](#20-createasyncthunk)
21. [Redux vs useState](#21-redux-vs-usestate)
22. [Redux vs Context API](#22-redux-vs-context-api)
23. [When Should We Use Redux?](#23-when-should-we-use-redux)
24. [Common Mistakes](#24-common-mistakes)
25. [Interview Questions](#25-interview-questions)
26. [Interview-Ready Explanation](#26-interview-ready-explanation)
27. [Quick Revision](#27-quick-revision)

---

# 1. What is Redux?

Redux is a state management library used to manage and maintain shared application state in a centralized location.

In a React application, different components may require access to the same data.

For example:

- Navbar needs the logged-in user's information.
- Dashboard needs the user's information.
- Profile page needs the user's information.
- Sidebar needs the user's role.
- Notification component needs notifications.

Instead of passing this data from one component to another through props, Redux provides a centralized store.

### In simple words

Redux provides a central location where application data is stored and managed.

Components can read data from this store and request changes to it.

---

# 2. Why Do We Need Redux?

Consider the following React component structure:

```text
App
│
├── Navbar
│   └── UserProfile
│
├── Sidebar
│
└── Dashboard
    ├── ProjectList
    └── ProjectDetails
```

Suppose the logged-in user information is stored inside `App`.

The `UserProfile`, `Sidebar`, and `Dashboard` components all need this information.

Without centralized state management, we may need to pass data through multiple components using props.

This is called Prop Drilling.

### Without Redux

```text
App
 │
 ├── Navbar
 │    └── UserProfile
 │
 ├── Sidebar
 │
 └── Dashboard
      └── ProjectList
```

The data may need to travel through components that don't actually need it.

### With Redux

```text
              Redux Store
                  |
     ┌────────────┼────────────┐
     |            |            |
   Navbar       Sidebar      Dashboard
     |                         |
 UserProfile               ProjectList
```

All components can access the shared state when required.

---

# 3. Understanding State Management

State is data that an application maintains and that can change over time.

Examples:

- Logged-in user
- Authentication status
- Selected project
- Notifications
- Shopping cart
- Theme
- Sidebar visibility
- Filters
- Application settings

### Local State

State that belongs to a particular component.

Example:

```jsx
const [isModalOpen, setIsModalOpen] = useState(false);
```

This state may only be required by one component.

### Global State

State that multiple components need to access.

Example:

```javascript
{
  user: {
    name: "Vipul",
    role: "Admin"
  },
  notifications: [],
  theme: "dark"
}
```

Redux is commonly used to manage global state.

---

# 4. Redux Architecture

Redux follows a predictable, unidirectional data flow.

The major components are:

- Store
- Actions
- Reducers
- Dispatch

```text
         React Component
                |
                |
             Dispatch
                |
                v
              Action
                |
                v
             Reducer
                |
                v
          Redux Store
                |
                v
       Updated Application State
                |
                v
         React Components
```

### Responsibilities

| Component | Responsibility |
|---|---|
| Store | Holds application state |
| Action | Describes what happened |
| Reducer | Determines how state changes |
| Dispatch | Sends an action to Redux |
| Selector | Reads state from the Store |

---

# 5. Redux Data Flow

Redux follows a one-way data flow.

### Step 1: User interacts with UI

For example, the user clicks an Increment button.

### Step 2: Component dispatches an action

```javascript
dispatch(increment());
```

### Step 3: Redux receives the action

Redux receives the action object.

```javascript
{
  type: "counter/increment"
}
```

### Step 4: Reducer processes the action

The reducer checks the action type and determines how the state should change.

### Step 5: Store updates

Redux stores the new state.

### Step 6: React components receive updated state

Components using the changed state are updated.

```text
User Click
    |
    v
Dispatch Action
    |
    v
Action
    |
    v
Reducer
    |
    v
Store Updated
    |
    v
React UI Updated
```

---

# 6. Redux Store

The Store is the central container that holds the application's global state.

### Example

```javascript
{
  counter: {
    value: 10
  },

  user: {
    name: "Vipul",
    role: "Admin"
  },

  notifications: {
    items: []
  }
}
```

The Store contains the different state slices of the application.

### Responsibilities of Store

- Store application state.
- Provide access to state.
- Receive dispatched actions.
- Update state through reducers.
- Notify subscribers when state changes.

### Important

Components should not directly modify the Redux Store.

State changes happen through dispatched actions processed by reducers.

---

# 7. Actions

An Action describes something that happened in the application.

Actions are generally JavaScript objects containing:

- `type`
- `payload` (optional)

### Example

```javascript
{
  type: "counter/increment"
}
```

Another example:

```javascript
{
  type: "user/login",
  payload: {
    name: "Vipul",
    role: "Admin"
  }
}
```

### Action Types

The `type` describes the event.

Examples:

```javascript
"counter/increment"

"counter/decrement"

"user/login"

"user/logout"

"project/fetchSuccess"

"notification/add"
```

### Payload

Payload is the additional information carried by an action.

```javascript
{
  type: "counter/incrementByAmount",
  payload: 5
}
```

Here, `5` is the payload.

---

# 8. Reducers

A Reducer is a function that determines how the application state should change when an action is received.

A reducer generally receives:

1. Current state
2. Action

It returns the next state.

### Basic Reducer

```javascript
function counterReducer(state, action) {
  switch (action.type) {

    case "increment":
      return state + 1;

    case "decrement":
      return state - 1;

    default:
      return state;
  }
}
```

### Reducer Flow

```text
Current State + Action
          |
          v
       Reducer
          |
          v
      Next State
```

### Important Reducer Rules

Reducers should:

- Be predictable.
- Avoid side effects.
- Avoid directly mutating state in traditional Redux.
- Return the next state.
- Avoid API calls.
- Avoid timers and random operations.

Reducers should be pure functions.

---

# 9. Dispatch

Dispatch is the mechanism used to send an action to the Redux Store.

### Example

```javascript
dispatch({
  type: "counter/increment"
});
```

When dispatch is called:

1. Redux receives the action.
2. Redux passes the action to the reducer.
3. The reducer calculates the new state.
4. The Store updates.
5. Components subscribed to relevant state are notified.

### In simple words

Dispatch tells Redux:

"Something happened in the application. Please process this action."

---

# 10. Action Creators

An Action Creator is a function that creates an action.

### Without Action Creator

```javascript
dispatch({
  type: "counter/increment"
});
```

### With Action Creator

```javascript
function increment() {
  return {
    type: "counter/increment"
  };
}
```

Now:

```javascript
dispatch(increment());
```

Action creators help avoid manually creating action objects.

Redux Toolkit automatically generates action creators when using `createSlice`.

---

# 11. Traditional Redux Example

## Initial State

```javascript
const initialState = {
  value: 0
};
```

## Reducer

```javascript
function counterReducer(state = initialState, action) {

  switch (action.type) {

    case "counter/increment":
      return {
        ...state,
        value: state.value + 1
      };

    case "counter/decrement":
      return {
        ...state,
        value: state.value - 1
      };

    case "counter/reset":
      return {
        ...state,
        value: 0
      };

    default:
      return state;
  }
}
```

### Why Spread Operator?

```javascript
return {
  ...state,
  value: state.value + 1
};
```

The spread operator copies the existing state and creates a new object with the updated value.

Traditional Redux requires immutable state updates.

---

# 12. Redux Toolkit

Redux Toolkit is the official recommended way to write Redux logic.

It simplifies Redux development by providing:

- `configureStore`
- `createSlice`
- `createAsyncThunk`
- RTK Query
- Simplified reducer logic
- Automatically generated action creators
- Built-in Immer for immutable updates

Instead of manually creating reducers and action types, Redux Toolkit simplifies the process.

---

# 13. Implementing Redux Toolkit in React

## Step 1: Install Packages

Using npm:

```bash
npm install @reduxjs/toolkit react-redux
```

Using pnpm:

```bash
pnpm add @reduxjs/toolkit react-redux
```

---

## Step 2: Create a Slice

Create:

```text
src/features/counter/counterSlice.ts
```

### counterSlice.ts

```typescript
import { createSlice } from "@reduxjs/toolkit";

interface CounterState {
  value: number;
}

const initialState: CounterState = {
  value: 0
};

const counterSlice = createSlice({
  name: "counter",

  initialState,

  reducers: {

    increment: (state) => {
      state.value += 1;
    },

    decrement: (state) => {
      state.value -= 1;
    },

    reset: (state) => {
      state.value = 0;
    },

    incrementByAmount: (state, action) => {
      state.value += action.payload;
    }
  }
});

export const {
  increment,
  decrement,
  reset,
  incrementByAmount
} = counterSlice.actions;

export default counterSlice.reducer;
```

### What Does createSlice Do?

`createSlice` combines:

- Reducer logic
- Action types
- Action creators

It automatically generates actions for the reducers defined inside the slice.

### Example Generated Action

```javascript
increment();
```

Generates an action similar to:

```javascript
{
  type: "counter/increment"
}
```

### Why Can We Mutate State Here?

```typescript
state.value += 1;
```

Redux Toolkit uses Immer internally.

Immer allows mutation-like syntax while producing an immutable state update.

Therefore, this syntax is safe inside Redux Toolkit slice reducers.

---

# 14. Configure Redux Store

Create:

```text
src/app/store.ts
```

### store.ts

```typescript
import { configureStore } from "@reduxjs/toolkit";

import counterReducer from "../features/counter/counterSlice";

export const store = configureStore({

  reducer: {

    counter: counterReducer

  }

});

export type RootState = ReturnType<typeof store.getState>;

export type AppDispatch = typeof store.dispatch;
```

### What is configureStore?

`configureStore` creates and configures the Redux Store.

It provides:

- Reducer registration
- Redux DevTools integration
- Middleware configuration
- Default middleware

### State Structure

Because we registered the reducer like this:

```typescript
reducer: {
  counter: counterReducer
}
```

Our Redux state looks like this:

```javascript
{
  counter: {
    value: 0
  }
}
```

---

# 15. useSelector

`useSelector` is a React Redux hook used to read data from the Redux Store.

### Example

```tsx
import { useSelector } from "react-redux";

import type { RootState } from "../../app/store";

function Counter() {

  const count = useSelector(
    (state: RootState) => state.counter.value
  );

  return (
    <h1>Count: {count}</h1>
  );

}

export default Counter;
```

### What Does useSelector Do?

```typescript
const count = useSelector(
  (state: RootState) => state.counter.value
);
```

It:

1. Accesses the Redux Store.
2. Reads `counter.value`.
3. Subscribes the component to that selected value.
4. Updates the component when the selected value changes.

---

# 16. useDispatch

`useDispatch` provides access to the Redux dispatch function.

### Example

```tsx
import { useDispatch } from "react-redux";

import {
  increment,
  decrement,
  reset
} from "../../features/counter/counterSlice";

import type { AppDispatch } from "../../app/store";

function CounterButtons() {

  const dispatch = useDispatch<AppDispatch>();

  return (

    <div>

      <button onClick={() => dispatch(increment())}>
        Increment
      </button>

      <button onClick={() => dispatch(decrement())}>
        Decrement
      </button>

      <button onClick={() => dispatch(reset())}>
        Reset
      </button>

    </div>

  );

}

export default CounterButtons;
```

### What Happens?

When the user clicks Increment:

```typescript
dispatch(increment());
```

Redux receives the action and updates the Store through the reducer.

---

# 17. Provider

The Provider makes the Redux Store available to React components.

Create or update:

```text
src/main.tsx
```

### main.tsx

```tsx
import React from "react";

import ReactDOM from "react-dom/client";

import { Provider } from "react-redux";

import { store } from "./app/store";

import App from "./App";

ReactDOM.createRoot(
  document.getElementById("root")!
).render(

  <React.StrictMode>

    <Provider store={store}>

      <App />

    </Provider>

  </React.StrictMode>

);
```

### Why Provider?

Without Provider, components cannot access the Redux Store using React Redux hooks.

Provider supplies the Store to the React component tree.

---

# 18. Complete Redux Flow

## Counter Component

```tsx
import { useSelector, useDispatch } from "react-redux";

import type { RootState, AppDispatch } from "../../app/store";

import {
  increment,
  decrement,
  reset
} from "./counterSlice";

function Counter() {

  const count = useSelector(
    (state: RootState) => state.counter.value
  );

  const dispatch = useDispatch<AppDispatch>();

  return (

    <div>

      <h1>{count}</h1>

      <button onClick={() => dispatch(increment())}>
        Increment
      </button>

      <button onClick={() => dispatch(decrement())}>
        Decrement
      </button>

      <button onClick={() => dispatch(reset())}>
        Reset
      </button>

    </div>

  );

}

export default Counter;
```

## Complete Flow

```text
User Clicks Increment
          |
          v
dispatch(increment())
          |
          v
     Action Created
          |
          v
     Redux Reducer
          |
          v
  counter.value Updated
          |
          v
      Redux Store
          |
          v
    useSelector Detects
          |
          v
     React Rerenders
```

---

# 19. Redux Folder Structure

A scalable Redux project structure:

```text
src/
│
├── app/
│   ├── store.ts
│   └── hooks.ts
│
├── features/
│   │
│   ├── counter/
│   │   ├── counterSlice.ts
│   │   └── Counter.tsx
│   │
│   ├── auth/
│   │   ├── authSlice.ts
│   │   └── Auth.tsx
│   │
│   ├── projects/
│   │   ├── projectSlice.ts
│   │   └── ProjectList.tsx
│   │
│   └── notifications/
│       ├── notificationSlice.ts
│       └── NotificationList.tsx
│
├── components/
│
├── pages/
│
├── services/
│
└── main.tsx
```

### Feature-Based Architecture

Each feature contains its own Redux logic and related components.

Examples:

- Authentication
- Projects
- Clients
- Notifications
- Dashboard

This makes the application easier to maintain.

---

# 20. Redux Async Operations

Applications frequently need asynchronous operations.

Examples:

- API calls
- Fetching users
- Fetching projects
- Login
- Uploading files
- Sending notifications

Reducers themselves should not perform asynchronous operations.

We generally use middleware and Redux Toolkit utilities for async operations.

Redux Toolkit provides:

`createAsyncThunk`

---

# 21. createAsyncThunk

`createAsyncThunk` helps manage asynchronous operations.

It automatically generates lifecycle actions:

- `pending`
- `fulfilled`
- `rejected`

### Example: Fetch Projects

Create:

```text
src/features/projects/projectSlice.ts
```

### projectSlice.ts

```typescript
import {
  createSlice,
  createAsyncThunk
} from "@reduxjs/toolkit";

import axios from "axios";

export const fetchProjects = createAsyncThunk(
  "projects/fetchProjects",

  async () => {

    const response = await axios.get(
      "https://api.example.com/projects"
    );

    return response.data;

  }
);

const projectSlice = createSlice({

  name: "projects",

  initialState: {
    projects: [],
    loading: false,
    error: null
  },

  reducers: {},

  extraReducers: (builder) => {

    builder

      .addCase(fetchProjects.pending, (state) => {
        state.loading = true;
      })

      .addCase(fetchProjects.fulfilled, (state, action) => {
        state.loading = false;
        state.projects = action.payload;
      })

      .addCase(fetchProjects.rejected, (state) => {
        state.loading = false;
        state.error = "Failed to fetch projects";
      });

  }

});

export default projectSlice.reducer;
```

### Async Flow

```text
Component
   |
   v
dispatch(fetchProjects())
   |
   v
Pending Action
   |
   v
API Request
   |
   ├── Success
   |      |
   |      v
   |  Fulfilled Action
   |
   └── Failure
          |
          v
      Rejected Action
```

### Pending

```javascript
loading = true;
```

### Fulfilled

```javascript
projects = response.data;
loading = false;
```

### Rejected

```javascript
error = "Failed to fetch projects";
loading = false;
```

---

# 22. Redux vs useState

| Feature | useState | Redux |
|---|---|---|
| Scope | Component-level | Application-level/shared |
| Data sharing | Limited | Multiple components |
| Complexity | Simple | Structured global state |
| Setup | Built into React | Additional setup |
| Suitable for | Local UI state | Shared state |
| Example | Modal visibility | Logged-in user |

### useState Example

```jsx
const [isOpen, setIsOpen] = useState(false);
```

Use this for local state.

### Redux Example

```javascript
{
  user: {
    id: 1,
    name: "Vipul"
  }
}
```

Use Redux when multiple components need access to shared state.

---

# 23. Redux vs Context API

| Feature | Context API | Redux |
|---|---|---|
| Built into React | Yes | No |
| Setup | Simple | More structured |
| Global state | Yes | Yes |
| Complex state logic | Possible | Well suited |
| DevTools | Limited built-in support | Redux DevTools |
| Middleware | Not built into Context | Supported |
| Async workflows | Usually custom logic | Middleware/toolkit |
| Large applications | Can work | Often useful |

Context API is not inherently bad.

Redux becomes useful when state management needs more structure, predictable transitions, middleware, debugging tools, and a dedicated ecosystem.

---

# 24. When Should We Use Redux?

Redux may be useful when:

- Multiple components need the same state.
- State changes frequently.
- Application state is becoming difficult to manage.
- Prop drilling becomes excessive.
- State transitions need predictable structure.
- You need debugging tools.
- You need centralized management of complex shared state.

### Examples

| State | Suggested Approach |
|---|---|
| Modal open/close | useState |
| Input field | useState |
| Dropdown visibility | useState |
| Logged-in user | Redux or Context |
| Global theme | Context or Redux |
| Shared filters | Redux, depending on complexity |
| Notifications | Redux |
| Shopping cart | Redux |
| API caching | RTK Query or TanStack Query |
| Server-side data | Often RTK Query or TanStack Query |

---

# 25. Common Mistakes

## Mistake 1: Direct State Mutation in Traditional Redux

Incorrect:

```javascript
state.value++;
```

In a traditional Redux reducer, directly modifying state is not allowed.

Correct:

```javascript
return {
  ...state,
  value: state.value + 1
};
```

Redux Toolkit allows mutation-like syntax inside its reducers because of Immer.

---

## Mistake 2: Performing API Calls Inside Reducers

Incorrect:

```javascript
function reducer(state, action) {

  fetch("/api/projects");

  return state;

}
```

Reducers should remain pure.

Use:

- `createAsyncThunk`
- RTK Query
- Middleware

---

## Mistake 3: Using Redux for Everything

Not every state needs to be global.

Avoid putting every input field, dropdown, and modal inside Redux.

Use local component state where appropriate.

---

## Mistake 4: Confusing Action and Dispatch

Action:

```javascript
{
  type: "counter/increment"
}
```

Dispatch:

```javascript
dispatch(increment());
```

Action describes an event.

Dispatch sends that action to Redux.

---

# 26. Interview Questions

## Q1. What is Redux?

Redux is a state management library that helps maintain shared application state in a centralized Store. Components can access shared state and dispatch actions to update it through reducers.

---

## Q2. What is the Redux Store?

The Redux Store is the centralized container that holds the application's global state.

---

## Q3. What is an Action?

An Action is an object describing an event that occurred in the application.

---

## Q4. What is a Reducer?

A Reducer is a function that receives the current state and an action and determines the next state.

---

## Q5. What is Dispatch?

Dispatch is used to send an action to the Redux Store.

---

## Q6. What is Redux Toolkit?

Redux Toolkit is the official recommended approach for writing Redux logic. It simplifies Store configuration, reducer creation, action generation and asynchronous operations.

---

## Q7. What is createSlice?

`createSlice` creates reducers and automatically generates corresponding action creators and action types.

---

## Q8. What is useSelector?

`useSelector` is a React Redux hook used to read selected state from the Redux Store.

---

## Q9. What is useDispatch?

`useDispatch` is a React Redux hook used to access the dispatch function.

---

## Q10. What is Provider?

Provider makes the Redux Store accessible to React components throughout the component tree.

---

## Q11. Why are reducers pure functions?

Pure reducers make state transitions predictable, easier to test and easier to debug.

---

## Q12. Can we directly modify state in Redux Toolkit?

Yes, mutation-like syntax is allowed inside Redux Toolkit reducers because Immer internally produces immutable updates.

---

## Q13. What is createAsyncThunk?

`createAsyncThunk` is a Redux Toolkit utility that handles asynchronous operations and generates pending, fulfilled and rejected actions.

---

## Q14. What is the difference between Redux and useState?

`useState` manages local component state, while Redux is generally used for shared application state that multiple components may need.

---

## Q15. What is the difference between an Action and a Reducer?

An Action describes what happened.

A Reducer determines how the state should change in response to that action.

---

## Q16. What is the difference between Dispatch and Action?

An Action describes an event.

Dispatch sends the action to the Store.

---

## Q17. What is unidirectional data flow?

It means data and state updates follow a predictable direction.

In Redux:

```text
UI -> Dispatch -> Action -> Reducer -> Store -> UI
```

---

## Q18. Why use Redux instead of Prop Drilling?

Redux allows components to access shared state directly from the Store without passing data through multiple intermediate components.

---

## Q19. What is Redux middleware?

Middleware intercepts or processes dispatched actions before or around their processing by reducers.

Middleware is commonly used for:

- Async operations
- Logging
- Analytics
- Side effects

---

## Q20. Should API data always be stored in Redux?

No.

For server data, RTK Query or TanStack Query may be better suited because they provide caching, loading states, refetching and cache invalidation.

---

# 27. Interview-Ready Explanation

If an interviewer asks:

**"Explain Redux architecture."**

You can answer:

Redux is a state management library that helps manage shared application state in a centralized Store.

In Redux, the Store contains the application's global state. When a user interacts with the UI, the component dispatches an Action describing what happened. Redux passes that Action to the Reducer, which determines how the state should change and returns the updated state. The Store then contains the updated state, and React components subscribed to that state are updated.

Redux follows a unidirectional data flow, which makes state updates predictable and easier to debug.

In modern React applications, we generally use Redux Toolkit instead of writing traditional Redux manually. Redux Toolkit provides `configureStore`, `createSlice`, and `createAsyncThunk`, which simplify Store configuration, reducer creation, action generation and asynchronous operations.

---

# 28. Quick Revision

| Concept | Meaning |
|---|---|
| Redux | Global state management |
| Store | Holds global application state |
| Action | Describes what happened |
| Payload | Data carried by an action |
| Reducer | Determines the next state |
| Dispatch | Sends an action |
| Action Creator | Creates an action |
| useSelector | Reads state |
| useDispatch | Dispatches actions |
| Provider | Connects React components to Redux |
| createSlice | Creates reducers and actions |
| configureStore | Configures the Redux Store |
| createAsyncThunk | Handles async action lifecycle |
| RTK Query | API fetching and caching tool |
| Middleware | Handles logic around dispatched actions |

---

# 29. Recommended Learning Order

1. Understand State.
2. Understand Props.
3. Understand Prop Drilling.
4. Understand Redux.
5. Understand Store.
6. Understand Actions.
7. Understand Reducers.
8. Understand Dispatch.
9. Learn Redux Toolkit.
10. Learn `configureStore`.
11. Learn `createSlice`.
12. Learn `useSelector`.
13. Learn `useDispatch`.
14. Learn `createAsyncThunk`.
15. Learn RTK Query.
16. Implement Redux in a real React project.

---

# Conclusion

Redux helps manage shared application state in a structured and predictable way.

Its core architecture revolves around:

- Store
- Actions
- Reducers
- Dispatch

Modern Redux development should generally use Redux Toolkit, which reduces boilerplate and simplifies implementation.

Redux should be used when shared state management becomes complex, rather than for every piece of component state.

```

---

<text color="success" weight="semibold">Recommended next topic:</text> **Redux Toolkit in a real-world React application — Auth, API calls, loading states, token handling, and RTK Query.** This would be the practical next step after understanding Redux architecture.

