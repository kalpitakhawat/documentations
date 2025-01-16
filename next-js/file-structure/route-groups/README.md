# Route Groups in Next.js

## Overview

Route Groups in Next.js allow you to logically organize routes without affecting the URL structure. They are especially useful for grouping related routes, managing layouts, and simplifying complex applications. This guide explains how to define and use route groups effectively.

---

## Defining Route Groups

### Using Parentheses

- Enclose folder names in parentheses `()` to create a route group.
- Files and folders inside the group are not reflected in the URL.

#### Example Directory Structure

```plaintext
app/
├── (marketing)/
│   ├── home/
│   │   └── page.js       // Maps to '/home'
│   └── about/
│       └── page.js       // Maps to '/about'
├── (dashboard)/
│   ├── layout.js         // Layout specific to the dashboard
│   ├── stats/
│   │   └── page.js       // Maps to '/stats'
│   └── settings/
│       └── page.js       // Maps to '/settings'
├── layout.js             // Root layout
└── page.js               // Homepage route ('/')
```

#### Generated Routes

- `/home`: Rendered by `app/(marketing)/home/page.js`
- `/about`: Rendered by `app/(marketing)/about/page.js`
- `/stats`: Rendered by `app/(dashboard)/stats/page.js`
- `/settings`: Rendered by `app/(dashboard)/settings/page.js`

---

## Benefits of Route Groups

1. **URL Simplification**:
   - The grouping folder names are not part of the URL, keeping URLs clean and user-friendly.

2. **Improved Organization**:
   - Group related routes under a logical folder hierarchy.

3. **Shared Layouts**:
   - Apply layouts to grouped routes by defining a `layout.js` file in the group folder.

4. **Collaboration and Maintenance**:
   - Makes the codebase easier to understand and maintain, especially in large applications.

---

## Applying Shared Layouts in Route Groups

Route groups enable shared layouts for grouped routes. Define a `layout.js` file inside the route group folder to apply a common layout.

#### Example

```plaintext
app/
├── (dashboard)/
│   ├── layout.js      // Layout for all dashboard routes
│   ├── stats/
│   │   └── page.js
│   └── settings/
│       └── page.js
```

#### Code

```javascript
// app/(dashboard)/layout.js
export default function DashboardLayout({ children }) {
  return (
    <>
      <header>Dashboard Header</header>
      <nav>Sidebar Navigation</nav>
      <main>{children}</main>
    </>
  );
}

// app/(dashboard)/stats/page.js
export default function StatsPage() {
  return <h1>Dashboard Stats</h1>;
}
```

#### Rendered Output for `/stats`

```html
<header>Dashboard Header</header>
<nav>Sidebar Navigation</nav>
<main>
  <h1>Dashboard Stats</h1>
</main>
```

---

## Nested Route Groups

You can nest route groups to organize complex applications further.

#### Example Structure

```plaintext
app/
├── (marketing)/
│   ├── layout.js         // Shared layout for marketing routes
│   ├── home/
│   │   └── page.js       // Maps to '/home'
│   └── about/
│       └── page.js       // Maps to '/about'
├── (dashboard)/
│   ├── (admin)/
│   │   ├── users/
│   │   │   └── page.js   // Maps to '/users'
│   │   └── settings/
│   │       └── page.js   // Maps to '/settings'
│   ├── stats/
│   │   └── page.js       // Maps to '/stats'
│   └── layout.js         // Layout for all dashboard routes
└── layout.js             // Root layout
```

---

## Best Practices

1. **Organize by Feature**:
   - Use route groups to logically separate features like marketing, dashboards, or user management.

2. **Keep URLs Simple**:
   - Avoid exposing technical folder structures in URLs.

3. **Shared Layouts**:
   - Leverage `layout.js` files to maintain consistent UI across grouped routes.

4. **Limit Nesting**:
   - Avoid deep nesting to keep the folder structure readable and maintainable.

---

## Conclusion

Route Groups in Next.js provide an elegant way to organize complex applications without affecting the URL structure. By leveraging route groups and shared layouts, you can maintain a clean codebase while delivering a seamless user experience.

## Official Documentation

- [Route Groups in Next.js](https://nextjs.org/docs/app/building-your-application/routing/route-groups)

