# 9. Data Fetching (with Axios)

## What Axios is & why use it

**Axios** is a promise-based HTTP client for the browser (and Node). It does the same job as the built-in `fetch`, but with a friendlier API:

- Automatically parses JSON responses — no manual `.json()` call.
- Throws on non-2xx status codes, so error handling is a normal `catch`.
- Lets you set defaults (base URL, headers) once and reuse them everywhere.

```bash
npm install axios
```

```jsx
import axios from "axios";
```

## Making a GET request

`axios.get(url)` returns a promise that resolves to a response object; the parsed body is on `.data`.

```jsx
axios.get("https://jsonplaceholder.typicode.com/users").then((response) => {
  console.log(response.data); // already-parsed JSON array
});
```

Or with `async`/`await`:

```jsx
async function loadUsers() {
  const response = await axios.get("https://jsonplaceholder.typicode.com/users");
  console.log(response.data);
}
```

## Fetching data inside useEffect

Requests are side effects, so they belong in `useEffect` — most commonly with an empty dependency array to fetch once when the component mounts.

```jsx
import { useEffect, useState } from "react";
import axios from "axios";

function UserList() {
  const [users, setUsers] = useState([]);

  useEffect(() => {
    axios
      .get("https://jsonplaceholder.typicode.com/users")
      .then((response) => setUsers(response.data));
  }, []); // ← runs once, on mount

  return (
    <ul>
      {users.map((user) => (
        <li key={user.id}>{user.name}</li>
      ))}
    </ul>
  );
}
```

`useEffect`'s callback can't be `async` itself (it must return nothing or a cleanup function), so define an inner `async` function and call it:

```jsx
useEffect(() => {
  async function fetchUsers() {
    const response = await axios.get("https://jsonplaceholder.typicode.com/users");
    setUsers(response.data);
  }
  fetchUsers();
}, []);
```

## Loading & error states

A real fetch has three states: loading, success, and error. Track them alongside the data.

```jsx
function UserList() {
  const [users, setUsers] = useState([]);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);

  useEffect(() => {
    async function fetchUsers() {
      try {
        const response = await axios.get("https://jsonplaceholder.typicode.com/users");
        setUsers(response.data);
      } catch (err) {
        setError(err.message);
      } finally {
        setLoading(false);
      }
    }
    fetchUsers();
  }, []);

  if (loading) return <p>Loading…</p>;
  if (error) return <p>Something went wrong: {error}</p>;

  return (
    <ul>
      {users.map((user) => (
        <li key={user.id}>{user.name}</li>
      ))}
    </ul>
  );
}
```

`finally` runs whether the request succeeded or failed, so it's the right place to turn `loading` off either way.

## Displaying fetched data

Once data lands in state, rendering it is just conditional rendering + rendering a list — nothing new.

```jsx
function UserProfile({ userId }) {
  const [user, setUser] = useState(null);
  const [loading, setLoading] = useState(true);

  useEffect(() => {
    setLoading(true);
    axios
      .get(`https://jsonplaceholder.typicode.com/users/${userId}`)
      .then((response) => setUser(response.data))
      .finally(() => setLoading(false));
  }, [userId]); // ← re-fetch when userId changes

  if (loading) return <p>Loading…</p>;
  if (!user) return <p>User not found.</p>;

  return (
    <div>
      <h2>{user.name}</h2>
      <p>{user.email}</p>
      <p>{user.company?.name}</p>
    </div>
  );
}
```

## Checklist

- [ ] What Axios is & why use it
- [ ] Making a GET request
- [ ] Fetching data inside useEffect
- [ ] Loading & error states
- [ ] Displaying fetched data

## Try it yourself

```jsx
// Build a <PostList /> that:
//   - fetches https://jsonplaceholder.typicode.com/posts with axios inside useEffect
//   - tracks loading, error, and posts in state
//   - shows "Loading…" while the request is in flight
//   - shows an error message if the request fails
//   - once loaded, renders each post's title in a <ul>, keyed by post.id
// Bonus: add a "Retry" button that re-runs the fetch after an error.
```

Next up: [10. Refs — useRef](10-refs-useref.md) →
