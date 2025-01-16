# Middleware in Next.js

## Overview

Middleware in Next.js allows you to execute code during the request lifecycle, enabling advanced functionalities like authentication, request validation, and dynamic routing. Middleware runs before a request completes, making it ideal for tasks that need to intercept or modify requests and responses.

---

## Defining Middleware

Middleware is defined in a `middleware.js` file located at the root of your project or in specific directories for route-specific behavior.

### Example Directory Structure

```plaintext
project/
├── app/
├── middleware.js       // Global middleware
```

---

## Basic Middleware Example

### Example: Logging Requests

```javascript
// middleware.js
import { NextResponse } from 'next/server';

export function middleware(request) {
  console.log(`Request made to: ${request.url}`);
  return NextResponse.next();
}
```

- Logs the URL of every incoming request.
- `NextResponse.next()` allows the request to proceed to the next handler.

---

## Middleware Features

### 1. **Matching Routes**

You can restrict middleware to specific routes using the `matcher` configuration.

#### Example

```javascript
export const config = {
  matcher: ['/dashboard/:path*', '/profile/:path*'],
};
```

- The middleware runs only for requests to `/dashboard` or `/profile` and their subroutes.

### 2. **Redirecting Requests**

Use `NextResponse.redirect()` to redirect requests dynamically.

#### Example

```javascript
// middleware.js
import { NextResponse } from 'next/server';

export function middleware(request) {
  const url = request.nextUrl;

  if (url.pathname === '/old-route') {
    return NextResponse.redirect(new URL('/new-route', url));
  }

  return NextResponse.next();
}
```

- Requests to `/old-route` are redirected to `/new-route`.

### 3. **Modifying Headers**

You can modify request or response headers using `NextResponse`.

#### Example

```javascript
// middleware.js
import { NextResponse } from 'next/server';

export function middleware(request) {
  const response = NextResponse.next();
  response.headers.set('X-Custom-Header', 'My Custom Header');
  return response;
}
```

- Adds a custom header (`X-Custom-Header`) to the response.

### 4. **Authentication**

Middleware is commonly used to validate authentication tokens or sessions.

#### Example: JWT Authentication

```javascript
// middleware.js
import { NextResponse } from 'next/server';

export function middleware(request) {
  const token = request.cookies.get('auth-token');

  if (!token) {
    return NextResponse.redirect(new URL('/login', request.url));
  }

  return NextResponse.next();
}
```

- Redirects unauthenticated users to the login page.

---

## Middleware API

### `NextResponse`

`NextResponse` provides methods for controlling the response behavior in middleware.

#### Common Methods

1. **`NextResponse.next()`**:
   - Passes the request to the next handler.

2. **`NextResponse.redirect(url)`**:
   - Redirects the request to a specified URL.

3. **`NextResponse.rewrite(url)`**:
   - Rewrites the request to a new URL without changing the visible URL.

4. **`NextResponse.json(data)`**:
   - Sends a JSON response.

---

## Best Practices

1. **Use Middleware Sparingly**:
   - Middleware runs on every matching request; avoid heavy computations.

2. **Restrict Routes**:
   - Use the `matcher` configuration to limit middleware execution to specific routes.

3. **Optimize Performance**:
   - Minimize operations in middleware to reduce latency.

4. **Secure Sensitive Data**:
   - Validate all inputs and sanitize responses to prevent vulnerabilities.

5. **Debugging**:
   - Use logging to monitor middleware behavior during development.

---

## Conclusion

Middleware in Next.js empowers developers to intercept requests and implement custom logic dynamically. By leveraging its capabilities, you can enhance your application with advanced features like authentication, request validation, and dynamic routing.

## Official Documentation

- [Next.js Middleware](https://nextjs.org/docs/app/building-your-application/routing/middleware)
