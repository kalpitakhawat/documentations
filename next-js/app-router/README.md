# Next.js App Router

## Overview

The App Router, introduced in Next.js 13, redefines the way applications are structured and built. It introduces a new, modern approach to routing by utilizing React Server Components and a folder-based structure under the `app` directory.

The App Router provides enhanced flexibility, better rendering options, and a simplified development experience compared to the traditional Page Router.

---

## Key Features

### 1. Folder-Based Routing

- Routes are defined by folders and files inside the `app` directory.
- Example structure:

  ```plaintext
  app/
  ├── page.js       // Maps to the root route ('/')
  ├── about/
  │   └── page.js   // Maps to '/about'
  ├── blog/
  │   ├── [id]/
  │   │   └── page.js   // Maps to '/blog/:id'
  │   └── layout.js     // Shared layout for all blog pages
  └── layout.js    // Root layout
  ```

### 2. React Server Components

- Combines client-side and server-side rendering seamlessly.
- Allows server-rendered components to coexist with client-side interactivity.

### 3. Nested Layouts

- Define shared layouts for specific routes using `layout.js` files.
- Nested layouts allow for consistent UIs, like headers and sidebars, across specific route segments.

  ```plaintext
  app/
  ├── layout.js    // Root layout
  ├── dashboard/
  │   ├── layout.js // Layout specific to the dashboard
  │   └── page.js   // Dashboard content
  ```

### 4. Loading UI

- Implement loading states for routes using `loading.js`.
- Automatically displayed while server components or data are being fetched.

  ```javascript
  // app/dashboard/loading.js
  export default function Loading() {
    return <p>Loading...</p>;
  }
  ```

### 5. Error Handling

- Handle errors for specific routes using `error.js`.
- Provides granular error boundaries for better debugging.

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

### 6. Route Groups and Parallel Routes

- **Route Groups**: Organize routes without affecting the URL structure using parentheses.

  ```plaintext
  app/
  ├── (marketing)/
  │   ├── home/
  │   │   └── page.js
  │   └── about/
  │       └── page.js
  ├── (dashboard)/
  │   └── page.js
  ```

- **Parallel Routes**: Render multiple routes in parallel for advanced use cases, like dashboards with different widgets.

### 7. API Routes in the App Router

- Define API routes using `route.js` files.

  ```javascript
  // app/api/hello/route.js
  export async function GET(request) {
    return new Response(JSON.stringify({ message: 'Hello, API!' }), {
      status: 200,
      headers: { 'Content-Type': 'application/json' },
    });
  }
  ```

---

## Migration from Page Router to App Router

If you're migrating from the Page Router to the App Router, here are key considerations:

1. **Folder Structure**:
   - Move files from `pages` to `app`.
   - Update routing logic to use folders and files like `page.js` and `layout.js`.

2. **React Server Components**:
   - Refactor components to utilize server and client rendering effectively.

3. **New Features**:
   - Leverage `loading.js`, `error.js`, and layouts for improved UX and code organization.

4. **Legacy Features**:
   - The App Router replaces older features like `getStaticProps` and `getServerSideProps` with a more unified data-fetching approach.

---

## Best Practices

1. **Use Layouts Effectively**:
   - Define layouts for shared components like headers and sidebars.
   - Use nested layouts for complex UIs.

2. **Handle Errors Gracefully**:
   - Implement error boundaries with `error.js` for better debugging and UX.

3. **Optimize Data Fetching**:
   - Use the App Router's built-in features for fetching and streaming data.

4. **Organize Routes Logically**:
   - Utilize route groups to keep the file structure clean and manageable.

5. **Test Thoroughly**:
   - Ensure all features, like loading states and error boundaries, work as expected in various scenarios.

---

## Conclusion

The Next.js App Router introduces a modern way to structure and build applications, leveraging features like React Server Components, nested layouts, and granular error handling. By adopting the App Router, developers can build scalable, maintainable, and high-performance applications.

## Official Documentation

- [Next.js App Router](https://nextjs.org/docs/app)

