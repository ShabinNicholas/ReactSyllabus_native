# 5. Conditional Rendering

## What conditional rendering is

Showing different UI depending on some condition — usually a prop or a piece of state. React has no special "if" directive; you use plain JavaScript.

## if / else rendering

Because JSX can't hold an `if` statement, do the branching **before** the `return`.

```jsx
function Greeting({ isLoggedIn }) {
  if (isLoggedIn) {
    return <h1>Welcome back!</h1>;
  }
  return <h1>Please sign in.</h1>;
}
```

You can also assign to a variable, then use it:

```jsx
function Status({ state }) {
  let message;
  if (state === "loading") message = <Spinner />;
  else if (state === "error") message = <p>Something went wrong</p>;
  else message = <DataView />;

  return <div className="status">{message}</div>;
}
```

## Ternary operator in JSX

For an inline either/or, use `condition ? a : b` inside braces.

```jsx
function LoginButton({ isLoggedIn }) {
  return (
    <button>
      {isLoggedIn ? "Log out" : "Log in"}
    </button>
  );
}
```

Works for whole elements too:

```jsx
<div>
  {hasItems ? <Cart items={items} /> : <p>Your cart is empty</p>}
</div>
```

## && short-circuit rendering

When you want to render something **or nothing**, use `&&`.

```jsx
function Inbox({ unreadCount }) {
  return (
    <div>
      <h2>Inbox</h2>
      {unreadCount > 0 && <span className="badge">{unreadCount}</span>}
    </div>
  );
}
```

If the left side is falsy, React renders nothing.

⚠️ **Gotcha:** `0` is falsy but still renders as the text "0". Use a real boolean:

```jsx
{items.length > 0 && <List items={items} />}   // ✅
{items.length && <List items={items} />}        // ❌ renders "0" when empty
```

## Showing / hiding UI based on state

Combine a boolean state with a toggle handler.

```jsx
import { useState } from "react";

function FaqItem({ question, answer }) {
  const [open, setOpen] = useState(false);

  return (
    <div>
      <button onClick={() => setOpen(o => !o)}>
        {open ? "▼" : "▶"} {question}
      </button>

      {open && <p>{answer}</p>}
    </div>
  );
}
```

Returning `null` from a component renders nothing at all:

```jsx
function Warning({ show }) {
  if (!show) return null;
  return <p className="warning">Careful!</p>;
}
```

## Checklist

- [ ] if / else rendering
- [ ] Ternary operator in JSX
- [ ] && short-circuit rendering
- [ ] Showing / hiding UI based on state

## Try it yourself

```jsx
// Build a <PasswordField /> that:
//   - keeps a `value` state and a `visible` boolean state
//   - renders <input type={visible ? "text" : "password"} />
//   - has a button that toggles `visible` and shows "Hide" / "Show"
//   - below the input, shows "Too short" (via &&) only when value.length is 1–7
```

Next up: [6. Rendering Lists](06-rendering-lists.md) →
