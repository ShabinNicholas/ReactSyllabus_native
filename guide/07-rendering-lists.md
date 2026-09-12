# 7. Rendering Lists

## What list rendering is

Turning an array of data into an array of JSX elements. This is how you render menus, tables, feeds, search results — anything repeated.

## Rendering arrays with map()

`.map()` transforms each item in a data array into an element. React renders arrays of elements directly.

```jsx
function ShoppingList() {
  const items = ["Apples", "Bread", "Coffee"];

  return (
    <ul>
      {items.map((item) => (
        <li key={item}>{item}</li>
      ))}
    </ul>
  );
}
```

The `{ }` holds the array `items.map(...)` returns; React renders each `<li>` in it.

## The key prop

Every element produced by `.map()` needs a **`key`** — a string or number that is **unique among its siblings**.

```jsx
function UserList({ users }) {
  return (
    <ul>
      {users.map((user) => (
        <li key={user.id}>{user.name}</li>
      ))}
    </ul>
  );
}
```

- Use a stable id from your data (`user.id`), not the array index when the list can reorder, filter, or have items inserted/removed.
- The key goes on the **outermost** element returned by the map callback.
- Keys are a hint for React, not a prop you can read inside the component.

## Why keys matter

When the list changes, React compares the new elements to the old ones. Keys tell it *which item is which*, so it can move, keep, or remove the right DOM nodes (and their state) instead of rebuilding everything.

Without stable keys you get subtle bugs: wrong items animating, input values jumping to the wrong row, extra re-renders. Using the array index as a key is fine only for a static list that never changes order.

```jsx
// ⚠️ index as key — okay only if the list is fixed and never reordered
{items.map((item, index) => <li key={index}>{item}</li>)}
```

## Rendering a list of components

The items don't have to be plain tags — map to your own components and pass props.

```jsx
function ProductCard({ name, price }) {
  return (
    <div className="card">
      <h3>{name}</h3>
      <p>${price}</p>
    </div>
  );
}

function Catalog() {
  const products = [
    { id: "a1", name: "Mug", price: 9 },
    { id: "a2", name: "Notebook", price: 6 },
    { id: "a3", name: "Pen", price: 2 },
  ];

  return (
    <div className="grid">
      {products.map((p) => (
        <ProductCard key={p.id} name={p.name} price={p.price} />
      ))}
    </div>
  );
}
```

Combine with `.filter()` to render a subset:

```jsx
{products
  .filter((p) => p.price < 8)
  .map((p) => <ProductCard key={p.id} {...p} />)}
```

## Checklist

- [ ] Rendering arrays with map()
- [ ] The key prop
- [ ] Why keys matter
- [ ] Rendering a list of components

## Try it yourself

```jsx
// Given: const todos = [
//   { id: 1, text: "Learn map()", done: true },
//   { id: 2, text: "Learn keys", done: false },
//   { id: 3, text: "Build a list", done: false },
// ];
// Build a <TodoList /> that:
//   - renders a <TodoItem key={t.id} ... /> for each todo
//   - <TodoItem> shows the text, struck through when done
//   - above the list, shows "X of Y done" computed from the array
```

Next up: [8. Side Effects — useEffect](08-side-effects-useeffect.md) →
