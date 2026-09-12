# 1. React Basics

## What is React

React is a JavaScript library for building **user interfaces**. Instead of manually finding elements and updating the DOM by hand, you describe *what the UI should look like* for a given set of data, and React figures out the DOM changes for you.

- You write **components** — functions that return UI.
- When your data changes, React **re-renders** the affected components and updates the screen efficiently.

## Component-based UI

A React app is a tree of components. Each component is a self-contained piece of UI — a button, a form, a page — that you can reuse and combine.

```jsx
// A component is just a function that returns some UI.
function App() {
  return (
    <div>
      <Header />
      <Content />
      <Footer />
    </div>
  );
}
```

Thinking in components means breaking a screen into small, named pieces and assembling them.

## JSX syntax

JSX is the HTML-like syntax you write inside components. It is **not** a string and **not** HTML — it compiles to `React.createElement(...)` calls.

```jsx
const element = <h1 className="title">Hello, React</h1>;
```

Key differences from HTML:

- `class` becomes `className`
- `for` becomes `htmlFor`
- attributes are camelCase: `onClick`, `tabIndex`, `maxLength`
- every tag must be closed: `<img />`, `<br />`

## JSX expressions ( { } )

Curly braces let you drop any JavaScript **expression** into JSX.

```jsx
function Greeting() {
  const name = "Ava";
  const hour = new Date().getHours();

  return (
    <div>
      <p>Hello, {name}!</p>
      <p>2 + 2 = {2 + 2}</p>
      <p>{hour < 12 ? "Good morning" : "Good afternoon"}</p>
      <p>{name.toUpperCase()}</p>
    </div>
  );
}
```

Expressions only — you can put a value or a ternary in `{ }`, but not an `if` statement or a `for` loop.

## Functional components

A functional component is a function whose name starts with a **capital letter** and returns JSX (or `null`).

```jsx
function WelcomeBanner() {
  return <h2>Welcome aboard 🚀</h2>;
}

// Arrow-function form is equally valid:
const WelcomeBanner2 = () => <h2>Welcome aboard 🚀</h2>;
```

The capital letter matters: `<welcomeBanner />` is treated as an HTML tag, `<WelcomeBanner />` as your component.

## Rendering a component

At the app's entry point you mount the root component into a real DOM node.

```jsx
import { createRoot } from "react-dom/client";

const root = createRoot(document.getElementById("root"));
root.render(<App />);
```

Inside other components, you "render" a component by using it as a tag: `<WelcomeBanner />`.

## One root element rule

A component must return **one** parent element. This returns two siblings and is a syntax error:

```jsx
// ❌ Adjacent JSX elements must be wrapped
function Broken() {
  return (
    <h1>Title</h1>
    <p>Body</p>
  );
}
```

Wrap them in a single parent:

```jsx
// ✅ One wrapping <div>
function Fixed() {
  return (
    <div>
      <h1>Title</h1>
      <p>Body</p>
    </div>
  );
}
```

## Fragments ( &lt;&gt;...&lt;/&gt; )

When you don't want an extra wrapper `<div>` in the DOM, use a **Fragment**.

```jsx
function Fixed() {
  return (
    <>
      <h1>Title</h1>
      <p>Body</p>
    </>
  );
}
```

`<>...</>` is shorthand for `<React.Fragment>...</React.Fragment>`. Use the long form when you need a `key` (see [Rendering Lists](07-rendering-lists.md)).

## Checklist

- [ ] What is React
- [ ] Component-based UI
- [ ] JSX syntax
- [ ] JSX expressions ( { } )
- [ ] Functional components
- [ ] Rendering a component
- [ ] One root element rule
- [ ] Fragments ( &lt;&gt;...&lt;/&gt; )

## Try it yourself

```jsx
// Build a <ProfileCard /> functional component that shows:
//   - your name in an <h2>
//   - your role in a <p>
//   - the current year, computed with new Date().getFullYear(), in JSX braces
// Return the three elements wrapped in a Fragment (no extra div).
// Then render <ProfileCard /> inside <App />.
```

Next up: [2. Props](02-props.md) →
