---
id: chapter1
sidebar_position: 1
title: Introduction to Next.js
---

# Introduction to Next.js

Welcome to the world of Next.js! This chapter will introduce you to the core concepts of Next.js, a powerful React framework that enables you to build production-ready web applications with ease.

Next.js provides a robust set of features, including server-side rendering (SSR), static site generation (SSG), API routes, and file-system based routing, which significantly enhance developer experience and application performance.

## What is Next.js?

Next.js is an open-source React framework for building full-stack web applications. It extends React's capabilities by offering a structured approach to building pages, handling data fetching, and optimizing for performance and SEO out of the box.

### Why Choose Next.js?

1.  **Server-Side Rendering (SSR) & Static Site Generation (SSG)**: Next.js allows you to pre-render pages at build time (SSG) or on each request (SSR), leading to faster page loads and improved SEO.
2.  **File-system Based Routing**: Pages are automatically routed based on their file names in the `pages` directory (or `app` directory in newer versions), simplifying navigation.
3.  **API Routes**: Easily build backend API endpoints within your Next.js project, making it a full-stack solution.
4.  **Optimized Performance**: Features like automatic image optimization, code splitting, and fast refresh enhance the user and developer experience.
5.  **Developer Experience**: A thriving ecosystem, excellent documentation, and a strong community support make development enjoyable.

**Diagram Suggestion**: A simple flow diagram showing how a request goes to a Next.js server, which then fetches data (if needed), renders the React component, and sends the HTML to the client.

## Setting up a Basic Next.js Project

Let's get started by creating a new Next.js application. You'll need Node.js installed on your machine.

### Step 1: Create a New Project

Open your terminal and run the following command:

```bash
npx create-next-app my-nextjs-app
```

This command will prompt you to configure your project. You can choose default options or customize them as per your preference. For this example, let's assume you've chosen:

*   Project name: `my-nextjs-app`
*   TypeScript: No
*   ESLint: Yes
*   Tailwind CSS: No
*   `src/` directory: No
*   App Router: Yes (recommended for new projects)
*   Import alias: No

### Step 2: Navigate to Your Project

```bash
cd my-nextjs-app
```

### Step 3: Run the Development Server

```bash
npm run dev
```

Your Next.js application will now be running at `http://localhost:3000`. Open your browser and navigate to this URL to see your new application.

**Code Example**: The default `app/page.js` content from a `create-next-app` project. Explain its structure and how it renders a basic page.

```javascript
// app/page.js
export default function Home() {
  return (
    <main>
      <h1>Welcome to Next.js!</h1>
      <p>Get started by editing `app/page.js`</p>
    </main>
  )
}
```

**Diagram Suggestion**: A screenshot of the default Next.js starter page in the browser.

## File-system Based Routing (App Router)

Next.js uses a file-system based router, where files and folders in the `app` directory are used to define routes. Each folder represents a route segment, and a `page.js` file inside a folder makes the route publicly accessible.

### Creating a New Page

To create a new page, simply create a new folder inside the `app` directory and add a `page.js` file. For example, to create an `about` page:

1.  Create a folder named `about` inside `app`.
2.  Inside `app/about`, create `page.js`.

**Code Example**: `app/about/page.js` content.

```javascript
// app/about/page.js
export default function About() {
  return (
    <main>
      <h1>About Us</h1>
      <p>This is the about page.</p>
    </main>
  )
}
```

Now, if you navigate to `http://localhost:3000/about`, you will see your new about page.

### Nested Routes

You can create nested routes by nesting folders. For instance, `app/dashboard/settings/page.js` would create the route `/dashboard/settings`.

**Code Example**: `app/dashboard/settings/page.js` content.

```javascript
// app/dashboard/settings/page.js
export default function DashboardSettings() {
  return (
    <main>
      <h1>Dashboard Settings</h1>
      <p>Manage your dashboard settings here.</p>
    </main>
  )
}
```

## Quiz: Introduction to Next.js

### Question 1

Which of the following is NOT a core feature of Next.js?

a) Server-Side Rendering (SSR)

b) File-system Based Routing

c) Built-in database management

d) API Routes

**Answer**: c) Built-in database management

### Question 2

To create a new Next.js project, which command would you typically use?

a) `npm create-react-app`

b) `npx create-next-app`

c) `next init`

d) `yarn start-next-app`

**Answer**: b) `npx create-next-app`

### Question 3

In the App Router, what file makes a route segment publicly accessible?

a) `index.js`

b) `route.js`

c) `page.js`

d) `layout.js`

**Answer**: c) `page.js`
