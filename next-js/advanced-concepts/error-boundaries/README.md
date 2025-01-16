# Error Boundaries in Next.js

## Overview

Error boundaries are React components that catch JavaScript errors anywhere in their child component tree, log those errors, and display a fallback UI instead of crashing the entire application. In Next.js, error boundaries are implemented using the `error.js` file in the App Router or through custom React error boundary components.

This guide explores how to implement and use error boundaries effectively in Next.js.

---

## Error Handling in the App Router

### Using `error.js`

The `error.js` file provides a way to define a fallback UI for a specific route or route segment. It is triggered when an error occurs in the corresponding route or its children.

#### Example Directory Structure

```plaintext
app/
├── dashboard/
│   ├── layout.js       // Shared layout for dashboard
│   ├── page.js         // Main content for /dashboard
│   ├── error.js        // Error boundary for /dashboard
```

#### Example: Basic `error.js`

```javascript
// app/dashboard/error.js
'use client';

export default function Error({ error, reset }) {
  return (
    <div>
      <h1>Something went wrong!</h1>
      <p>{error.message}</p>
      <button onClick={reset}>Try Again</button>
    </div>
  );
}
```

- **Parameters**:
  - `error`: The error object.
  - `reset`: A function to reset the error boundary and retry rendering.

### Usage

- When an error occurs in `/dashboard`, the `error.js` file renders a fallback UI.
- The `reset` function allows users to retry the rendering process.

---

## Custom React Error Boundaries

In addition to using `error.js`, you can create custom error boundaries for finer control over error handling in specific components.

### Example: Creating a Custom Error Boundary

```javascript
import React from 'react';

class ErrorBoundary extends React.Component {
  constructor(props) {
    super(props);
    this.state = { hasError: false, error: null };
  }

  static getDerivedStateFromError(error) {
    return { hasError: true, error };
  }

  componentDidCatch(error, errorInfo) {
    console.error('Error caught by ErrorBoundary:', error, errorInfo);
  }

  resetError = () => {
    this.setState({ hasError: false, error: null });
  };

  render() {
    if (this.state.hasError) {
      return (
        <div>
          <h1>Something went wrong.</h1>
          <p>{this.state.error.message}</p>
          <button onClick={this.resetError}>Try Again</button>
        </div>
      );
    }

    return this.props.children;
  }
}

export default ErrorBoundary;
```

### Wrapping Components

```javascript
import ErrorBoundary from './ErrorBoundary';
import Dashboard from './Dashboard';

export default function App() {
  return (
    <ErrorBoundary>
      <Dashboard />
    </ErrorBoundary>
  );
}
```

---

## When to Use `error.js` vs. Custom Error Boundaries

- **Use `error.js`**:
  - For route-specific error handling in the App Router.
  - When you want to handle errors at a page or layout level.

- **Use Custom Error Boundaries**:
  - For component-level error handling.
  - When building reusable components that need localized error handling.

---

## Best Practices

1. **Provide User-Friendly Messages**:
   - Display meaningful error messages to help users understand the issue.

2. **Log Errors**:
   - Use logging tools (e.g., Sentry) to track errors in production.

3. **Test Error Scenarios**:
   - Simulate errors during development to ensure fallback UI works as expected.

4. **Use `reset` Functionality**:
   - Allow users to retry rendering when possible.

5. **Avoid Silent Failures**:
   - Ensure that errors are logged or displayed rather than ignored.

---

## Conclusion

Error boundaries are an essential tool for building resilient applications in Next.js. By using `error.js` for route-level errors and custom error boundaries for component-level issues, you can enhance the user experience and maintain application stability.

## Official Documentation

- [Error Boundaries in React](https://reactjs.org/docs/error-boundaries.html)
- [Error Handling in Next.js](https://nextjs.org/docs/app/building-your-application/routing/error-handling)

