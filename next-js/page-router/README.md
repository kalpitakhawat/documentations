# Next.js Page Router

## Overview

The Next.js Page Router is a foundational feature that organizes routing based on the `pages` directory structure. Each file in the `pages` directory corresponds to a route in the application, simplifying the creation of routes and enabling a predictable file-based routing system.

## Key Features

### 1. File-Based Routing

- **Automatic Route Mapping**:
  - Files in the `pages` directory automatically become routes.
  - Example:
    - `pages/index.js` maps to `/`.
    - `pages/about.js` maps to `/about`.

- **Built-in 404 Pages**:
  - Add `pages/404.js` for a custom 404 page to handle unmatched routes.

### 2. Dynamic Routing

- Define dynamic segments in routes using square brackets.
  ```javascript
  // pages/post/[id].js
  import { useRouter } from 'next/router';

  export default function Post() {
    const { query } = useRouter();
    return <h1>Post ID: {query.id}</h1>;
  }
  ```
- Dynamic routes are useful for paths like `/post/1`, `/post/2`, etc.

### 3. API Routes

- Build API endpoints by creating files in the `pages/api` directory.
  ```javascript
  // pages/api/hello.js
  export default function handler(req, res) {
    res.status(200).json({ message: 'Hello, API!' });
  }
  ```
- These routes serve as lightweight serverless functions.

### 4. Client-Side Navigation

- Use the `<Link>` component for navigation.
  ```javascript
  import Link from 'next/link';

  export default function Home() {
    return <Link href="/about">Go to About</Link>;
  }
  ```
- Prefetching is enabled by default for faster transitions.

---

## Rendering Strategies

### 1. Static Site Generation (SSG)

Pages are generated at build time and served as static assets.

```javascript
export async function getStaticProps() {
  return { props: { message: 'Static Content' } };
}

export default function SSGPage({ message }) {
  return <h1>{message}</h1>;
}
```

### 2. Server-Side Rendering (SSR)

Pages are rendered on the server for every request.

```javascript
export async function getServerSideProps(context) {
  const data = await fetchDataFromAPI();
  return { props: { data } };
}

export default function SSRPage({ data }) {
  return <h1>{data}</h1>;
}
```

### 3. Incremental Static Regeneration (ISR)

Combines static generation with revalidation.

```javascript
export async function getStaticProps() {
  return {
    props: { message: 'ISR Content' },
    revalidate: 10, // Regenerate every 10 seconds
  };
}

export default function ISRPage({ message }) {
  return <h1>{message}</h1>;
}
```

### 4. Client-Side Rendering (CSR)

Pages are rendered entirely on the client after fetching data.

```javascript
import { useEffect, useState } from 'react';

export default function CSRPage() {
  const [data, setData] = useState(null);

  useEffect(() => {
    fetch('/api/data').then((res) => res.json()).then((data) => setData(data));
  }, []);

  if (!data) return <p>Loading...</p>;

  return <h1>{data}</h1>;
}
```

---

## Comparison: SSR vs CSR vs ISR vs SSG

| Feature                | SSR          | CSR              | ISR              | SSG              |
| ---------------------- | ------------ | ---------------- | ---------------- | ---------------- |
| **Rendering Location** | Server       | Client           | Server + Static  | Build Time       |
| **Use Case**           | Dynamic Data | Interactive Apps | Hybrid Rendering | Static Content   |
| **Performance**        | Slower       | Fast             | Fast             | Fast             |
| **SEO**                | Excellent    | Limited          | Excellent        | Excellent        |

---

## Best Practices

1. **Choose the Right Strategy**:
   - Use SSG for static content and ISR for frequently updated data.
   - Opt for SSR for highly dynamic or personalized data.

2. **Prefetch Links**:
   - Use `<Link>` for internal navigation to leverage built-in prefetching.

3. **Structure Routes Logically**:
   - Organize files in the `pages` directory to match your app's navigation structure.

4. **Use API Routes Efficiently**:
   - Keep serverless functions lightweight and focused.

---

## Conclusion

The Next.js Page Router combines simplicity and flexibility to create powerful routing systems. By leveraging features like dynamic routing, API routes, and various rendering strategies, developers can build scalable, high-performance web applications.

## Official Documentation

- [Next.js Routing](https://nextjs.org/docs/routing/introduction)
- [Data Fetching](https://nextjs.org/docs/basic-features/data-fetching)

