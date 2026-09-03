# 8. Component Composition

## What composition is

Composition is building complex UI by **combining small, focused components** rather than writing one giant component. React has no inheritance for UI — you compose.

## Breaking UI into components

Look at a screen and draw boxes around the repeated or self-contained parts. Each box is a candidate component.

```jsx
// One big blob…
function Page() {
  return (
    <div>
      {/* header markup */}
      {/* sidebar markup */}
      {/* article markup */}
      {/* footer markup */}
    </div>
  );
}

// …broken into pieces
function Page() {
  return (
    <div>
      <Header />
      <Sidebar />
      <Article />
      <Footer />
    </div>
  );
}
```

A good component does **one thing** and has a name that says what it is.

## Nesting components

Components render other components, forming a tree.

```jsx
function App() {
  return (
    <Layout>
      <Navbar />
      <PostList>
        <Post title="Hello" />
        <Post title="World" />
      </PostList>
    </Layout>
  );
}
```

Data flows **down** the tree through props; events flow **up** through callback props.

## Passing data down via props

Parent owns the data, children receive slices of it.

```jsx
function App() {
  const user = { name: "Ava", avatar: "/ava.png" };
  return <Profile name={user.name} avatar={user.avatar} />;
}

function Profile({ name, avatar }) {
  return (
    <div>
      <Avatar src={avatar} />
      <span>{name}</span>
    </div>
  );
}

function Avatar({ src }) {
  return <img className="avatar" src={src} alt="" />;
}
```

## Passing functions down as props

To let a child tell the parent something happened, pass a **function** as a prop. The child calls it; the parent decides what to do.

```jsx
import { useState } from "react";

function App() {
  const [count, setCount] = useState(0);

  function handleAdd(amount) {
    setCount((c) => c + amount);
  }

  return (
    <div>
      <p>Total: {count}</p>
      <AddButton amount={1} onAdd={handleAdd} />
      <AddButton amount={5} onAdd={handleAdd} />
    </div>
  );
}

function AddButton({ amount, onAdd }) {
  return <button onClick={() => onAdd(amount)}>+{amount}</button>;
}
```

The state lives in the parent (`App`); `AddButton` is reusable and doesn't own any state. This pattern is called **lifting state up**.

## Reusable components

Design a component so its behavior comes from props, not hard-coded values.

```jsx
// Reusable: caller controls label, style, and what happens on click
function Button({ label, variant = "primary", onClick }) {
  return (
    <button className={`btn btn-${variant}`} onClick={onClick}>
      {label}
    </button>
  );
}

// Reusable wrapper via children
function Card({ title, children }) {
  return (
    <section className="card">
      {title && <h3>{title}</h3>}
      {children}
    </section>
  );
}

function App() {
  return (
    <Card title="Account">
      <p>Signed in as Ava.</p>
      <Button label="Sign out" variant="danger" onClick={() => {}} />
    </Card>
  );
}
```

Signs a component is reusable: no hard-coded text, no assumptions about where it's used, configurable through props and `children`.

## Checklist

- [ ] Breaking UI into components
- [ ] Nesting components
- [ ] Passing data down via props
- [ ] Passing functions down as props
- [ ] Reusable components

## Try it yourself

```jsx
// Build a small <TodoApp />:
//   - <TodoApp> owns the todos array in state and an addTodo(text) function
//   - <AddTodoForm onAdd={addTodo} /> is a child with its own input state;
//     on submit it calls onAdd and clears the field
//   - <TodoList todos={todos} onToggle={toggleTodo} /> maps over todos
//   - <TodoItem todo={t} onToggle={onToggle} /> renders one row
// Notice how state lives only in <TodoApp> and flows down; events flow up.
```

Next up: [Where to go from here](09-next-steps.md) →
