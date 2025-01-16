# File Conventions in Next.js

## Overview

In Next.js, the organization and naming of files follow specific conventions that streamline development, improve maintainability, and provide predictable behavior. This guide focuses on file conventions used in both the **App Router** and the **Page Router**, as well as their roles in building applications.

---

## Key File Conventions

### 1. `page.js`

- **Purpose**: Represents the main content of a route.
- **Required**: Yes, for each route in the App Router.
- **Usage**:
  ```plaintext
  app/about/page.js → /about
  ```
  ```javascript
  // app/about/page.js
  export default function About() {
    return <h1>About Us</h1>;
  }
  ```

### 2. `layout.js`

- **Purpose**: Defines shared layouts for a route segment and its children.
- **Supports**:
  - Persistent UI elements like headers, footers, or sidebars.
  - Nested layouts for specific route segments.
- **Usage**:
  ```plaintext
  app/dashboard/layout.js → Layout for all dashboard routes
  ```
  ```javascript
  // app/dashboard/layout.js
  export default function DashboardLayout({ children }) {
    return (
      <>
        <header>Dashboard Header</header>
        <main>{children}</main>
      </>
    );
  }
  ```

### 3. `loading.js`

- **Purpose**: Displays a loading indicator during data fetching or server-side rendering.
- **Usage**:
  ```plaintext
  app/dashboard/loading.js → Shown while loading dashboard content
  ```
  ```javascript
  // app/dashboard/loading.js
  export default function Loading() {
    return <p>Loading...</p>;
  }
  ```

### 4. `error.js`

- **Purpose**: Handles errors specific to a route or segment.
- **Supports**:
  - Custom error messages.
  - Retry functionality.
- **Usage**:
  ```plaintext
  app/error.js → Global error handler
  ```
  ```javascript
  // app/error.js
  'use client';

  export default function Error({ error, reset }) {
    return (
      <div>
        <h1>Error: {error.message}</h1>
        <button onClick={reset}>Try Again</button>
      </div>
    );
  }
  ```

### 5. `route.js`

- **Purpose**: Defines API routes in the App Router.
- **Replaces**: The `pages/api` approach used in the Page Router.
- **Usage**:
  ```plaintext
  app/api/user/route.js → API endpoint at /api/user
  ```
  ```javascript
  // app/api/user/route.js
  export async function GET(request) {
    return new Response(JSON.stringify({ name: 'John Doe' }), {
      status: 200,
      headers: { 'Content-Type': 'application/json' },
    });
  }
  ```

### 6. `head.js`

- **Purpose**: Customize the `<head>` section for a specific route.
- **Replaces**: The `next/head` component approach used in the Page Router.
- **Usage**:
  ```plaintext
  app/about/head.js → Adds metadata for the /about route
  ```
  ```javascript
  // app/about/head.js
  export default function Head() {
    return (
      <>
        <title>About Us</title>
        <meta name="description" content="Learn more about us." />
      </>
    );
  }
  ```

---

## File Organization Best Practices

### 1. Group Related Files

- Keep related files (e.g., `page.js`, `layout.js`, `loading.js`) in the same folder for better maintainability.

  ```plaintext
  app/
  ├── dashboard/
  │   ├── page.js
  │   ├── layout.js
  │   ├── loading.js
  │   └── error.js
  ```

### 2. Use Descriptive Names

- Use meaningful folder and file names to reflect their purpose.
  ```plaintext
  app/
  ├── products/
  │   ├── [id]/
  │   │   └── page.js   // Maps to /products/:id
  │   └── layout.js     // Shared layout for products
  ```

### 3. Avoid Deep Nesting

- Limit folder depth to improve readability and maintainability.

### 4. Separate Reusable Components

- Place shared components in a `components/` directory.

  ```plaintext
  components/
  ├── Button.js
  ├── Header.js
  └── Footer.js
  ```

---

## Migration Tips (Page Router to App Router)

### Key Changes

1. **Routing**:
   - Move files from `pages/` to `app/`.
   - Replace dynamic route files (e.g., `[id].js`) with `app/` equivalents.

2. **Layouts**:
   - Use `layout.js` to define shared UI elements.

3. **API Routes**:
   - Replace `pages/api/` files with `route.js` in `app/api/`.

4. **Metadata**:
   - Move `<head>` definitions to `head.js`.

### Example Migration

From:
```plaintext
pages/
├── index.js
├── about.js
└── api/
    └── user.js
```

To:
```plaintext
app/
├── layout.js
├── page.js
├── about/
│   ├── page.js
│   └── head.js
└── api/
    └── user/
        └── route.js
```

---

## Conclusion

Adhering to Next.js file conventions ensures predictable behavior and maintainable code. By leveraging the structure and roles of files like `page.js`, `layout.js`, and `route.js`, you can build efficient and scalable applications.

## Official Documentation

- [File Conventions in Next.js](https://nextjs.org/docs/app/building-your-application/routing)
- [Routing in Next.js](https://nextjs.org/docs/routing/introduction)

