# 2. Props

## What props are

**Props** (short for "properties") are the inputs to a component. They let a parent pass data down to a child, so the same component can render different things in different places.

Think of a component as a function and props as its arguments.

## Passing props to a component

You pass props like HTML attributes when you render the component.

```jsx
function App() {
  return (
    <div>
      <Greeting name="Ava" age={30} isAdmin />
      <Greeting name="Sam" age={25} />
    </div>
  );
}
```

- Strings use quotes: `name="Ava"`
- Everything else (numbers, booleans, arrays, objects, expressions) uses braces: `age={30}`
- A bare prop like `isAdmin` is shorthand for `isAdmin={true}`

## Reading props

The component receives a single `props` object as its first argument.

```jsx
function Greeting(props) {
  return (
    <p>
      Hello {props.name}, age {props.age}
      {props.isAdmin ? " (admin)" : ""}
    </p>
  );
}
```

## Props destructuring

It's idiomatic to destructure props right in the parameter list.

```jsx
function Greeting({ name, age, isAdmin }) {
  return (
    <p>
      Hello {name}, age {age}
      {isAdmin ? " (admin)" : ""}
    </p>
  );
}
```

Cleaner to read, and the component's inputs are visible at a glance.

## Default prop values

Give a prop a fallback with a default value in the destructuring.

```jsx
function Button({ label = "Click me", type = "button" }) {
  return <button type={type}>{label}</button>;
}

<Button />;                 // renders "Click me"
<Button label="Save" />;    // renders "Save"
```

## children prop

Whatever you put **between** a component's opening and closing tags arrives as the special `children` prop.

```jsx
function Card({ title, children }) {
  return (
    <div className="card">
      <h3>{title}</h3>
      <div className="card-body">{children}</div>
    </div>
  );
}

function App() {
  return (
    <Card title="Welcome">
      <p>This paragraph is the children prop.</p>
      <button>Got it</button>
    </Card>
  );
}
```

`children` is what makes wrapper/layout components possible.

## Props are read-only

A component must **never** modify its own props. Props flow one way: down from parent to child.

```jsx
function Greeting({ name }) {
  // ❌ Never do this — props are immutable
  // name = name.toUpperCase();

  // ✅ Derive a new value instead
  const shouted = name.toUpperCase();
  return <p>HELLO {shouted}</p>;
}
```

If a value needs to change over time, it belongs in [state](03-state-usestate.md), not props.

## Checklist

- [ ] Passing props to a component
- [ ] Reading props
- [ ] Props destructuring
- [ ] Default prop values
- [ ] children prop
- [ ] Props are read-only

## Try it yourself

```jsx
// Build an <Alert type="..." > component:
//   - it accepts a `type` prop that defaults to "info"
//   - it renders its `children` inside a <div>
//   - it shows an emoji based on type: info → ℹ️, success → ✅, error → ❌
// Render three <Alert> elements with different types and messages.
```

Next up: [3. State — useState](03-state-usestate.md) →
