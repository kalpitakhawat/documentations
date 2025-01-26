# React Hooks Guide

## Introduction

React Hooks are functions that let developers use state and other React features in functional components. Introduced in React 16.8, hooks provide a way to handle state, lifecycle events, and side effects without writing class components.

## Why Use Hooks?

- **Simplified Code**: Hooks allow for cleaner and more concise functional components.
- **Stateful Logic Reuse**: Hooks make it easy to reuse stateful logic without changing component hierarchy.
- **Enhanced Readability**: Code readability improves as hooks eliminate the need for lifecycle methods in class components.
- **Side Effects Management**: Hooks like `useEffect` help manage side effects directly within functional components.

## Core Hooks

### 1. `useState`

`useState` allows you to add state to functional components.

```javascript
import React, { useState } from 'react';

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  );
}
```

### 2. `useEffect`

`useEffect` allows you to perform side effects in functional components.

```javascript
import React, { useEffect, useState } from 'react';

function Example() {
  const [count, setCount] = useState(0);

  // Function will be called every time "count" changes.
  useEffect(() => {
    document.title = `You clicked ${count} times`;
  }, [count]);

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  );
}
```

### 3. `useContext`

`useContext` lets you subscribe to React context without introducing nesting.

```javascript
import React, { useContext } from 'react';

const ThemeContext = React.createContext('light');

// The "ThemeButton" or it's parent component should be wrapped in context provider.
function ThemeButton() {
  const theme = useContext(ThemeContext);
  return <button className={theme}>I am styled by theme context!</button>;
}
```

### 4. `useReducer`

`useReducer` is a more advanced alternative to `useState` for managing state logic.

```javascript
import React, { useReducer } from 'react';

function reducer(state, action) {
  switch (action.type) {
    case 'increment':
      return { count: state.count + 1 };
    case 'decrement':
      return { count: state.count - 1 };
    default:
      throw new Error();
  }
}

function Counter() {
  const [state, dispatch] = useReducer(reducer, { count: 0 });

  return (
    <div>
      <p>Count: {state.count}</p>
      <button onClick={() => dispatch({ type: 'increment' })}>+</button>
      <button onClick={() => dispatch({ type: 'decrement' })}>-</button>
    </div>
  );
}
```

### 5. `useRef`

`useRef` lets you access a DOM element or persist a mutable value across renders without causing a re-render.

```javascript
import React, { useRef } from 'react';

function TextInputWithFocusButton() {
  const inputEl = useRef(null);

  const onButtonClick = () => {
    inputEl.current.focus();
  };

  return (
    <>
      <input ref={inputEl} type="text" />
      <button onClick={onButtonClick}>Focus the input</button>
    </>
  );
}
```

### 6. `useMemo` and `useCallback`

- **`useMemo`**: Memoizes the result of a computation.
- **`useCallback`**: Memoizes a callback function.

```javascript
import React, { useMemo, useCallback } from 'react';

function Example({ items }) {
  const computeExpensiveValue = useCallback((num) => {
    console.log('Computing expensive value');
    return num * 2;
  }, []);

  // "value" will only be re-calculated when there is change in the length of items array or the reference to the function stored by "computeExpensiveValue" is changed.
  const value = useMemo(() => computeExpensiveValue(items.length), [items.length, computeExpensiveValue]);

  return <div>{value}</div>;
}
```

## Custom Hooks

Custom hooks allow you to extract and reuse stateful logic across multiple components. They start with the word "use" and can call other hooks inside them.

### Creating a Custom Hook

```javascript
import { useState, useEffect } from 'react';

function useFetch(url) {
  const [data, setData] = useState(null);
  const [loading, setLoading] = useState(true);

  useEffect(() => {
    fetch(url)
      .then(response => response.json())
      .then(data => {
        setData(data);
        setLoading(false);
      });
  }, [url]);

  return { data, loading };
}
```

### Using a Custom Hook

```javascript
function App() {
  const { data, loading } = useFetch('https://api.example.com/data');

  if (loading) {
    return <p>Loading...</p>;
  }

  return (
    <div>
      <h1>Data</h1>
      <pre>{JSON.stringify(data, null, 2)}</pre>
    </div>
  );
}
```

### Benefits of Custom Hooks

- **Reusability**: Custom hooks allow you to reuse stateful logic across different components.
- **Cleaner Code**: By moving complex logic into custom hooks, your component code becomes cleaner and more focused.
- **Testability**: Custom hooks can be tested independently from the components using them, making your codebase more maintainable.

## Best Practices

- **Keep Side Effects Outside Rendering**: Use `useEffect` to handle side effects outside the main rendering logic.
- **Optimize Performance**: Use `useMemo` and `useCallback` to optimize performance for expensive computations and functions.
- **Use Custom Hooks**: Encapsulate reusable logic into custom hooks for better readability and maintainability.
- **Avoid Overusing Hooks**: Don't overcomplicate components by overusing hooks; keep them simple and focused.

## Dos and Don'ts

### Dos

- **Do Use Hooks for Reusable Logic**: Create custom hooks for reusable logic across components.
- **Do Manage State Locally**: Use `useState` for local state management.
- **Do Handle Side Effects Properly**: Use `useEffect` to handle side effects such as data fetching and subscriptions.

### Don'ts

- **Don't Use Hooks in Class Components**: Hooks can only be used in functional components.
- **Don't Call Hooks Conditionally**: Always call hooks at the top level of your component to ensure consistent behavior.
- **Don't Ignore Dependency Arrays**: Specify all dependencies in `useEffect`, `useMemo`, and `useCallback` to avoid stale closures.

## Conclusion

Hooks have revolutionized how state and side effects are managed in React applications. By understanding and applying the core hooks, developers can create cleaner, more efficient components.

## Official Documentation Links
- [React Hooks](https://react.dev/docs/hooks-intro)
- [useState](https://react.dev/docs/hooks-reference#usestate)
- [useEffect](https://react.dev/docs/hooks-reference#useeffect)
- [useContext](https://react.dev/docs/hooks-reference#usecontext)
- [useReducer](https://react.dev/docs/hooks-reference#usereducer)
- [useRef](https://react.dev/docs/hooks-reference#useref)
- [useMemo](https://react.dev/docs/hooks-reference#usememo)
- [useCallback](https://react.dev/docs/hooks-reference#usecallback)
- [Custom Hooks](https://react.dev/docs/hooks-custom)

