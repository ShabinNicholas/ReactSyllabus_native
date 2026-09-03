# 3. State — useState

## Why components need state

**Props** come from the parent and never change on their own. But most UIs have data that *changes over time in response to the user* — a counter, a text input's value, whether a menu is open.

That kind of data is **state**. When state changes, React re-renders the component so the screen matches the new data.

## useState hook

`useState` is a function from React that gives your component a piece of state.

```jsx
import { useState } from "react";

function Counter() {
  const [count, setCount] = useState(0);
  //     ^value  ^setter        ^initial value

  return (
    <button onClick={() => setCount(count + 1)}>
      Clicked {count} times
    </button>
  );
}
```

`useState` returns an array with exactly two items, and we destructure it:

1. the **current value**
2. a **setter function** to update it

## Initial state value

The argument to `useState` is the value on the **first render only**. After that it's ignored.

```jsx
const [name, setName] = useState("");        // starts as empty string
const [items, setItems] = useState([]);      // starts as empty array
const [user, setUser] = useState(null);      // starts as null
```

If computing the initial value is expensive, pass a function — React calls it once:

```jsx
const [data, setData] = useState(() => expensiveInitialCalc());
```

## Reading state

Just use the variable. It always holds the value for the current render.

```jsx
function Counter() {
  const [count, setCount] = useState(0);
  return <p>The count is {count}</p>;
}
```

## Updating state (setter function)

Call the setter. **Never** assign to the state variable directly — React wouldn't know to re-render.

```jsx
setCount(5);            // set to a specific value
setCount(count + 1);    // set based on the value we rendered with
```

When the new value depends on the previous one, prefer the **updater function** form — it's always given the latest value:

```jsx
setCount(prev => prev + 1);

// This matters when you update more than once in a row:
setCount(prev => prev + 1);
setCount(prev => prev + 1); // now really +2
```

State updates are asynchronous — `count` doesn't change until the next render.

## State with strings / numbers / booleans

```jsx
const [text, setText] = useState("");
const [age, setAge] = useState(18);
const [isOpen, setIsOpen] = useState(false);

setText("hello");
setAge(age + 1);
setIsOpen(!isOpen);   // toggle
```

## State with objects

State is replaced, not merged. Spread the old object and override the fields that changed.

```jsx
const [form, setForm] = useState({ name: "", email: "" });

// ✅ new object, old fields copied, one field changed
setForm(prev => ({ ...prev, name: "Ava" }));

// ❌ never mutate state directly
// form.name = "Ava";  setForm(form);
```

## State with arrays

Same rule — create a **new** array instead of mutating.

```jsx
const [todos, setTodos] = useState(["Learn JSX"]);

// add
setTodos(prev => [...prev, "Learn props"]);

// remove by index
setTodos(prev => prev.filter((_, i) => i !== 2));

// update one item
setTodos(prev => prev.map((t, i) => (i === 0 ? "Learned JSX" : t)));
```

Avoid `push`, `pop`, `splice`, `sort` on state arrays — they mutate.

## Multiple useState calls

A component can call `useState` as many times as it needs. Keep unrelated values separate.

```jsx
function SignupForm() {
  const [name, setName] = useState("");
  const [email, setEmail] = useState("");
  const [agreed, setAgreed] = useState(false);
  // ...
}
```

Rules of hooks: call them at the **top level** of the component, never inside `if`, loops, or nested functions — the order must be the same on every render.

## Checklist

- [ ] Why components need state
- [ ] useState hook
- [ ] Initial state value
- [ ] Reading state
- [ ] Updating state (setter function)
- [ ] State with strings / numbers / booleans
- [ ] State with objects
- [ ] State with arrays
- [ ] Multiple useState calls

## Try it yourself

```jsx
// Build a <Profile /> component with:
//   - a text input bound to a `name` state (value + onChange)
//   - a number showing `visits`, with a "Visit" button that does setVisits(v => v + 1)
//   - a "Dark mode" checkbox bound to a `dark` boolean state
// Show all three values in a <pre>{JSON.stringify(...)}</pre> so you can watch them change.
```

Next up: [4. Event Handling](04-event-handling.md) →
