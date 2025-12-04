---
id: chapter3
sidebar_position: 3
title: Data Fetching in Next.js
---

# Data Fetching in Next.js

Data fetching is a core aspect of building dynamic web applications, and Next.js offers a highly flexible and optimized approach to it. This chapter will dive deeper into the various data fetching strategies available in Next.js, particularly focusing on the App Router model and how to effectively use them.

## Client-Side Data Fetching
While Next.js excels at server-side rendering, client-side data fetching is still a common and valid strategy for certain use cases, especially for user-specific data or data that updates frequently after the initial page load.

### Using `useEffect` and Fetch API

This is the traditional React way to fetch data on the client side after the component has mounted.

**Code Example**: Client-side data fetching with `useEffect`.

```javascript
// app/dashboard/client-data/page.js
'use client'; // Mark as Client Component

import { useState, useEffect } from 'react';

export default function ClientDataPage() {
  const [data, setData] = useState(null);
  const [isLoading, setLoading] = useState(true);

  useEffect(() => {
    fetch('/api/hello') // Your API route or external API
      .then((res) => res.json())
      .then((data) => {
        setData(data);
        setLoading(false);
      });
  }, []);

  if (isLoading) return <p>Loading data...</p>;
  if (!data) return <p>No data</p>;

  return (
    <div>
      <h1>Client-Side Data</h1>
      <p>Data from API: {data.name}</p>
    </div>
  );
}
```

### Using SWR or React Query

For more advanced client-side data fetching, caching, and revalidation, libraries like SWR and React Query are highly recommended.

**Code Example**: Client-side data fetching with SWR.

```javascript
// app/profile/page.js
'use client';

import useSWR from 'swr';

const fetcher = (url) => fetch(url).then((res) => res.json());

export default function Profile() {
  const { data, error, isLoading } = useSWR('/api/user', fetcher);

  if (error) return <div>Failed to load</div>;
  if (isLoading) return <div>Loading...</div>;

  return <div>Hello {data.name}!</div>;
}
```

**Diagram Suggestion**: A diagram contrasting client-side vs. server-side data fetching, highlighting when each is appropriate.

## Server-Side Data Fetching in App Router

The App Router embraces server components by default, offering flexible ways to fetch data directly on the server.

### Fetching Data in Server Components

You can use `async/await` directly in your Server Components (including Layouts and Pages) to fetch data.

**Code Example**: Data fetching in a Server Component.

```javascript
// app/products/page.js
// This is a Server Component by default

async function getProducts() {
  const res = await fetch('https://api.example.com/products', { cache: 'no-store' }); // No caching
  // The return value is *not* serialized
  // You can return Date, Map, Set, etc.
  if (!res.ok) {
    // This will activate the closest `error.js` Error Boundary
    throw new Error('Failed to fetch data');
  }
  return res.json();
}

export default async function ProductsPage() {
  const products = await getProducts();

  return (
    <div>
      <h1>Products</h1>
      <ul>
        {products.map((product) => (
          <li key={product.id}>{product.name}</li>
        ))}
      </ul>
    </div>
  );
}
```

### Data Caching and Revalidation

Next.js automatically caches `fetch` requests. You can configure caching behavior using `cache` options or `revalidate` for time-based revalidation.

*   `cache: 'force-cache'` (default): Cache indefinitely.
*   `cache: 'no-store'`: Never cache, re-fetch on every request.
*   `next: { revalidate: 60 }`: Revalidate data every 60 seconds (like ISR).

**Diagram Suggestion**: A diagram illustrating the data caching mechanisms in Next.js Server Components, showing different `fetch` options.

## Combining Server and Client Components

You can combine Server and Client Components to build complex UIs. Server Components fetch data and pass it as props to Client Components, which then handle interactivity.

**Code Example**: Passing server-fetched data to a Client Component.

```javascript
// app/dashboard/layout.js (Server Component)
import { countUsers } from '@/lib/user-data'; // Server-side function
import UserGreeting from './UserGreeting'; // Client Component

export default async function DashboardLayout({ children }) {
  const userCount = await countUsers(); // Data fetched on server

  return (
    <div>
      <UserGreeting count={userCount} /> {/* Pass data to Client Component */}
      {children}
    </div>
  );
}

// app/dashboard/UserGreeting.js (Client Component)
'use client';

import { useState } from 'react';

export default function UserGreeting({ count }) {
  const [greeting, setGreeting] = useState(`There are ${count} users.`);

  return (
    <div>
      <p>{greeting}</p>
      <button onClick={() => alert('Hello!')}>Say Hello</button>
    </div>
  );
}
```

## Quiz: Data Fetching in Next.js

### Question 1

Which of the following is typically used for client-side data fetching in a React component after it mounts?

a) `getServerSideProps`

b) `getStaticProps`

c) `useEffect`

d) `fetch` directly in a Server Component

**Answer**: c) `useEffect`

### Question 2

In a Next.js App Router Server Component, how do you prevent `fetch` from caching data and ensure it re-fetches on every request?

a) Set `revalidate: 0` in `next: { ... }` option.

b) Use `cache: 'force-cache'`.

c) Use `cache: 'no-store'`.

d) Remove the `fetch` call.

**Answer**: c) Use `cache: 'no-store'`.

### Question 3

When combining Server and Client Components in Next.js, what is a common pattern for passing data fetched on the server to an interactive client component?

a) Directly call server-side functions from the client component.

b) Use context APIs to share data across the component tree.

c) Pass the data as props from the Server Component to the Client Component.

d) Store data in local storage on the server and retrieve it on the client.

**Answer**: c) Pass the data as props from the Server Component to the Client Component.