# 5. Controlled Components

## What a controlled component is

A **controlled component** is a form element (`input`, `textarea`, `select`) whose value is driven entirely by React state, instead of the DOM keeping track of it internally. React becomes the "single source of truth" for what's in the field.

The opposite is an **uncontrolled component** — the DOM manages its own value, and you read it only when you need to (e.g. via a ref).

## Controlled vs uncontrolled inputs

```jsx
// Uncontrolled — the browser owns the value; React doesn't know it changed
function UncontrolledField() {
  return <input defaultValue="" />;
}

// Controlled — React owns the value; every change flows through state
function ControlledField() {
  const [value, setValue] = useState("");
  return <input value={value} onChange={(e) => setValue(e.target.value)} />;
}
```

Controlled inputs let you validate, transform, or react to every keystroke, and keep the UI and your data model in sync. Uncontrolled inputs are simpler for basic cases but harder to reason about as the form grows.

## value driven by state

The `value` prop is set from state — the input can only ever show what state says it should show.

```jsx
import { useState } from "react";

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

⚠️ **Gotcha:** if you set `value` but forget `onChange`, React logs a warning and the field becomes read-only — the user can't type anything because state never updates.

## onChange updates state

The `onChange` handler is what makes typing actually work. It fires on every keystroke and pushes the new value into state, which re-renders the input with that value.

```jsx
function SearchBox() {
  const [query, setQuery] = useState("");

  function handleChange(event) {
    setQuery(event.target.value);
  }

  return (
    <div>
      <input value={query} onChange={handleChange} />
      <p>Searching for: {query}</p>
    </div>
  );
}
```

## Reading input value from state

Because the value always lives in state, you never need to "ask the DOM" what's in the field — just read the state variable.

```jsx
function EmailField() {
  const [email, setEmail] = useState("");
  const isValid = email.includes("@");

  return (
    <div>
      <input value={email} onChange={(e) => setEmail(e.target.value)} />
      {!isValid && email.length > 0 && <p>Enter a valid email</p>}
    </div>
  );
}
```

## Controlled checkbox / select

Checkboxes use `checked` instead of `value`; selects use `value` on the `<select>` itself.

```jsx
function Preferences() {
  const [subscribed, setSubscribed] = useState(false);
  const [plan, setPlan] = useState("free");

  return (
    <div>
      <label>
        <input
          type="checkbox"
          checked={subscribed}
          onChange={(e) => setSubscribed(e.target.checked)}
        />
        Subscribe to updates
      </label>

      <select value={plan} onChange={(e) => setPlan(e.target.value)}>
        <option value="free">Free</option>
        <option value="pro">Pro</option>
        <option value="team">Team</option>
      </select>
    </div>
  );
}
```

## Managing multiple form fields with one state object

Instead of a separate `useState` per field, store the whole form as one object and update it by key.

```jsx
function SignupForm() {
  const [form, setForm] = useState({ username: "", email: "", plan: "free" });

  function handleChange(event) {
    const { name, value } = event.target;
    setForm((prev) => ({ ...prev, [name]: value }));
  }

  return (
    <form>
      <input name="username" value={form.username} onChange={handleChange} />
      <input name="email" value={form.email} onChange={handleChange} />
      <select name="plan" value={form.plan} onChange={handleChange}>
        <option value="free">Free</option>
        <option value="pro">Pro</option>
      </select>
    </form>
  );
}
```

Giving each field a matching `name` attribute lets one `handleChange` update any of them via `[name]: value` — no need for a separate handler per field.

## Checklist

- [ ] Controlled vs uncontrolled inputs
- [ ] value driven by state
- [ ] onChange updates state
- [ ] Reading input value from state
- [ ] Controlled checkbox / select
- [ ] Managing multiple form fields with one state object

## Try it yourself

```jsx
// Build a <SignupForm /> with one state object { username, email, agree }:
//   - text inputs for username and email, both controlled
//   - a checkbox for "I agree to the terms", controlled via `checked`
//   - a single handleChange that updates any field by its `name` attribute
//   - a submit button that is disabled unless agree is true and both fields are non-empty
```

Next up: [6. Conditional Rendering](06-conditional-rendering.md) →
