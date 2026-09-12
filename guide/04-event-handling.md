# 4. Event Handling

## What event handling is

Event handlers are functions you attach to JSX elements to respond to user actions — clicks, typing, submitting a form, hovering. React wraps the browser's events in a consistent cross-browser layer called a *synthetic event*.

## Handling click events

Pass a function to the `onClick` prop. **Pass the function, don't call it.**

```jsx
function SaveButton() {
  return <button onClick={handleClick}>Save</button>;
}

function handleClick() {
  console.log("Saved!");
}
```

```jsx
// ❌ This calls handleClick immediately during render, then passes its return value
<button onClick={handleClick()}>Save</button>
```

Other common ones: `onChange` (inputs), `onSubmit` (forms), `onMouseEnter`, `onKeyDown`.

## Writing event handler functions

The handler receives the event object as its argument.

```jsx
function SearchBox() {
  function handleChange(event) {
    console.log("New value:", event.target.value);
  }

  function handleSubmit(event) {
    event.preventDefault(); // stop the browser reloading the page
    console.log("Form submitted");
  }

  return (
    <form onSubmit={handleSubmit}>
      <input onChange={handleChange} />
      <button type="submit">Go</button>
    </form>
  );
}
```

## Inline vs named handlers

**Named** — defined separately. Good when the logic is more than a line, or reused.

```jsx
function handleClick() {
  console.log("clicked");
}

<button onClick={handleClick}>Click</button>;
```

**Inline** — an arrow function right in the JSX. Good for one-liners.

```jsx
<button onClick={() => console.log("clicked")}>Click</button>
```

Both are fine. Reach for inline when it's short; extract a named function when it grows.

## Passing arguments to a handler

Wrap the call in an arrow function so it runs *on the event*, not during render.

```jsx
function ItemList() {
  function handleDelete(id) {
    console.log("Deleting", id);
  }

  return (
    <ul>
      <li>
        Apple <button onClick={() => handleDelete(1)}>x</button>
      </li>
      <li>
        Pear <button onClick={() => handleDelete(2)}>x</button>
      </li>
    </ul>
  );
}
```

```jsx
// ❌ runs handleDelete(1) during render
<button onClick={handleDelete(1)}>x</button>
```

## Updating state from an event

The most common pattern: an event handler calls a state setter.

```jsx
import { useState } from "react";

function Counter() {
  const [count, setCount] = useState(0);

  function increment() {
    setCount(prev => prev + 1);
  }

  return (
    <div>
      <p>{count}</p>
      <button onClick={increment}>+1</button>
      <button onClick={() => setCount(0)}>Reset</button>
    </div>
  );
}
```

A **controlled input** is the same idea — state holds the value, `onChange` updates it:

```jsx
function NameField() {
  const [name, setName] = useState("");
  return (
    <input
      value={name}
      onChange={(e) => setName(e.target.value)}
      placeholder="Your name"
    />
  );
}
```

## Checklist

- [ ] Handling click events
- [ ] Writing event handler functions
- [ ] Inline vs named handlers
- [ ] Passing arguments to a handler
- [ ] Updating state from an event

## Try it yourself

```jsx
// Build a <Stepper /> with:
//   - a `count` state starting at 0
//   - "−" and "+" buttons (named handlers) that step by 1
//   - a row of buttons [5, 10, 25] that each add their amount,
//     using onClick={() => addAmount(n)}
//   - a "Reset" button (inline handler) that sets count back to 0
```

Next up: [5. Controlled Components](05-controlled-components.md) →
