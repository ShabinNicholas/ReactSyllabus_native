# 8. Side Effects — useEffect

## Why side effects are needed

Rendering should be **pure**: given the same props and state, a component returns the same JSX and changes nothing else. But real apps need to do things *outside* of rendering:

- fetch data from an API
- set up a timer or a subscription
- read/write `localStorage`
- manually change the DOM (focus an input, set the document title)

These are **side effects**. `useEffect` is where they belong.

## useEffect hook

`useEffect` runs a function *after* React has rendered and painted the screen.

```jsx
import { useEffect, useState } from "react";

function Title() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    document.title = `Clicked ${count} times`;
  });

  return <button onClick={() => setCount(count + 1)}>Click</button>;
}
```

## Dependency array

The optional second argument controls **when** the effect re-runs. React re-runs it only if a value in the array changed since the last render.

```jsx
useEffect(() => {
  // ...
}, [count, userId]); // runs after renders where count or userId changed
```

## Running on every render

Omit the array entirely — the effect runs after **every** render.

```jsx
useEffect(() => {
  console.log("rendered");
}); // no second argument
```

Rarely what you want; usually a sign you need a dependency array.

## Running once on mount ( [] )

An **empty** array means "no dependencies", so the effect runs **once**, after the first render. Perfect for initial data loading or one-time setup.

```jsx
function Users() {
  const [users, setUsers] = useState([]);

  useEffect(() => {
    fetch("https://jsonplaceholder.typicode.com/users")
      .then((res) => res.json())
      .then((data) => setUsers(data));
  }, []); // ← runs once

  return <ul>{users.map((u) => <li key={u.id}>{u.name}</li>)}</ul>;
}
```

## Running when a value changes

List the value as a dependency. The effect re-runs each time that value changes — e.g. re-fetch when the selected id changes.

```jsx
function UserDetail({ userId }) {
  const [user, setUser] = useState(null);

  useEffect(() => {
    setUser(null); // reset while loading
    fetch(`https://jsonplaceholder.typicode.com/users/${userId}`)
      .then((res) => res.json())
      .then(setUser);
  }, [userId]); // ← re-run when userId changes

  if (!user) return <p>Loading…</p>;
  return <h2>{user.name}</h2>;
}
```

## Cleanup function

If your effect starts something ongoing (a timer, an event listener, a subscription), **return a function** that stops it. React runs the cleanup before the next effect run and when the component unmounts.

```jsx
function Clock() {
  const [now, setNow] = useState(new Date());

  useEffect(() => {
    const id = setInterval(() => setNow(new Date()), 1000);

    return () => clearInterval(id); // ← cleanup
  }, []);

  return <p>{now.toLocaleTimeString()}</p>;
}
```

```jsx
// Event listener example
useEffect(() => {
  function onResize() {
    console.log(window.innerWidth);
  }
  window.addEventListener("resize", onResize);
  return () => window.removeEventListener("resize", onResize);
}, []);
```

Skipping cleanup causes memory leaks and duplicate listeners/timers.

## Effect order with state updates

- Effects run **after** the DOM is updated and the browser has painted — not during render.
- If an effect calls a state setter, React re-renders, then runs effects again (respecting their dependency arrays). Guard this so you don't loop forever:

```jsx
// ❌ infinite loop — every render schedules a state change with no dep guard
useEffect(() => {
  setCount(count + 1);
});

// ✅ only runs when `data` changes
useEffect(() => {
  setSummary(computeSummary(data));
}, [data]);
```

- In development, React 18+ **Strict Mode** intentionally mounts, unmounts, and remounts components once — so mount effects and their cleanup run twice. Writing a correct cleanup function makes this harmless.

## Checklist

- [ ] Why side effects are needed
- [ ] useEffect hook
- [ ] Dependency array
- [ ] Running on every render
- [ ] Running once on mount ( [] )
- [ ] Running when a value changes
- [ ] Cleanup function
- [ ] Effect order with state updates

## Try it yourself

```jsx
// Build a <CountdownTimer seconds={10} /> that:
//   - keeps a `remaining` state initialised from the prop
//   - on mount, starts a setInterval that decrements `remaining` each second
//   - stops the interval (cleanup) when it reaches 0 or the component unmounts
//   - shows "Done!" via conditional rendering when remaining === 0
// Bonus: reset the countdown whenever the `seconds` prop changes.
```

Next up: [9. Refs — useRef](09-refs-useref.md) →
