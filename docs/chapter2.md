---
id: chapter2
sidebar_position: 2
title: Project Structure & Routing in Next.js
---

# Project Structure & Routing in Next.js

Understanding the project structure and routing mechanisms is fundamental to building scalable and maintainable applications with Next.js. This chapter will guide you through organizing your Next.js project and mastering its powerful routing capabilities, especially with the App Router.

## Next.js Project Structure (App Router)

The App Router, introduced in Next.js 13, is a powerful and flexible way to build applications. It uses a file-system based routing approach where directories define routes and special files create UI for those routes.

### Key Directories and Files

*   `app/`: The root of the App Router. Directories inside `app/` define route segments.
    *   `layout.js`: Defines shared UI for a route segment and its children. Essential for consistent navigation and global elements.
    *   `page.js`: Makes a route segment publicly accessible. This file defines the UI unique to a route.
    *   `loading.js`: Defines UI to be shown while a route segment is loading its data.
    *   `error.js`: Defines UI to be shown when an error occurs within a route segment.
    *   `template.js`: Similar to `layout.js` but creates a new instance for each navigation, preserving state.
    *   `not-found.js`: Defines UI for a 404 not found page.
    *   `default.js`: Used with parallel routes to render a fallback when an active slot doesn't have a match.
*   `public/`: For static assets like images, fonts, and other files that need to be served directly.
*   `components/`: (Convention) A common place to store reusable React components.
*   `lib/` or `utils/`: (Convention) For utility functions, helper methods, and other non-component logic.

**Diagram Suggestion**: A tree diagram illustrating a typical Next.js project structure with `app/`, `public/`, `components/`, and `lib/` directories, showing `layout.js`, `page.js`, `loading.js`, `error.js` within `app/` route segments.

## Routing Fundamentals with App Router

The App Router organizes your application by directories, making routing intuitive and powerful.

### Defining Routes

Each folder within the `app` directory represents a route segment. A `page.js` file inside a folder makes that segment accessible as a URL path.

**Code Example**: Basic route definition.

```javascript
// app/dashboard/page.js
// This file defines the /dashboard route

export default function DashboardPage() {
  return (
    <div>
      <h1>Welcome to your Dashboard</h1>
      <p>Overview of your metrics and activities.</p>
    </div>
  );
}
```

### Nested Routes and Layouts

By nesting folders, you create nested routes. Each nested route can have its own `layout.js` to define UI that is shared across its children.

**Code Example**: Nested route with a shared layout.

```javascript
// app/dashboard/layout.js
// This layout will apply to /dashboard and /dashboard/settings

export default function DashboardLayout({ children }) {
  return (
    <section>
      <nav>
        <a href="/dashboard">Dashboard</a>
        <a href="/dashboard/settings">Settings</a>
      </nav>
      {children}
    </section>
  );
}

// app/dashboard/settings/page.js
// This page will render within the DashboardLayout

export default function DashboardSettingsPage() {
  return (
    <div>
      <h2>Dashboard Settings</h2>
      <p>Adjust your preferences here.</p>
    </div>
  );
}
```

### Dynamic Routes

Next.js supports dynamic routes, allowing you to create routes that match variable segments. This is achieved by enclosing a folder name in square brackets, e.g., `[id]`.

**Code Example**: Dynamic route for a user profile.

```javascript
// app/users/[userId]/page.js
// Matches /users/1, /users/abc, etc.

export default function UserProfilePage({ params }) {
  return (
    <div>
      <h1>User Profile: {params.userId}</h1>
      <p>Details for user with ID: {params.userId}</p>
    </div>
  );
}
```

**Diagram Suggestion**: A diagram showing how a dynamic route like `app/products/[productId]/page.js` can handle multiple product IDs.

## Navigation

Next.js provides the `next/link` component for client-side navigation between routes, which is faster and more efficient than traditional `<a>` tags.

**Code Example**: Using `next/link` for navigation.

```javascript
import Link from 'next/link';

export default function HomePage() {
  return (
    <main>
      <h1>Home</h1>
      <p>
        Go to <Link href="/about">About Us</Link>
      </p>
      <p>
        Visit <Link href="/dashboard">Dashboard</Link>
      </p>
    </main>
  );
}
```

## Quiz: Project Structure & Routing

### Question 1

In the Next.js App Router, which file is responsible for making a route segment publicly accessible and defines its unique UI?

a) `layout.js`

b) `template.js`

c) `page.js`

d) `route.js`

**Answer**: c) `page.js`

### Question 2

What is the primary purpose of `layout.js` in the App Router?

a) To define API endpoints.

b) To handle data fetching for a route.

c) To define shared UI for a route segment and its children.

d) To render content when an error occurs.

**Answer**: c) To define shared UI for a route segment and its children.

### Question 3

How do you create a dynamic route segment (e.g., for a user ID) in the App Router?

a) By naming the folder `_id`.

b) By naming the folder `[id]`.

c) By using a `dynamic.js` file.

d) By configuring it in `next.config.js`.

**Answer**: b) By naming the folder `[id]`.
