# 9. Refs — useRef

## What a ref is

A **ref** is a container for a value that React remembers across renders — but changing it does **not** trigger a re-render. Think of it as an escape hatch for holding onto something outside the normal render → state → re-render cycle.

## Creating a ref with useRef

`useRef(initialValue)` returns an object with a single mutable property, `current`, set to `initialValue` on the first render.

```jsx
import { useRef } from "react";

function Example() {
  const renderCount = useRef(0);
  // renderCount.current starts at 0 and stays the same object across renders
  return <p>Ref object: {JSON.stringify(renderCount)}</p>;
}
```

## ref.current

Read and write the value through `.current`. Unlike state, updating it doesn't schedule a re-render — the change just happens "silently".

```jsx
function Stopwatch() {
  const intervalId = useRef(null);

  function start() {
    intervalId.current = setInterval(() => console.log("tick"), 1000);
  }

  function stop() {
    clearInterval(intervalId.current);
  }

  return (
    <div>
      <button onClick={start}>Start</button>
      <button onClick={stop}>Stop</button>
    </div>
  );
}
```

## Referencing a component

Pass a ref to a `ref` attribute on a DOM element (or component) to get direct access to the underlying node — most commonly to call an imperative method like `.focus()`.

```jsx
function SearchField() {
  const inputRef = useRef(null);

  function focusInput() {
    inputRef.current.focus();
  }

  return (
    <div>
      <input ref={inputRef} type="text" />
      <button onClick={focusInput}>Focus the input</button>
    </div>
  );
}
```

`inputRef.current` is `null` until React mounts the `<input>`, then it points at the actual DOM node.

## Persisting a value without rerendering

Refs are perfect for values you need to remember between renders but that shouldn't affect what's on screen — a timer id, a previous prop value, a mutable counter, a flag for "is this the first render".

```jsx
function TrackPreviousValue({ value }) {
  const previous = useRef(value);

  useEffect(() => {
    previous.current = value; // save for next render, after this one paints
  }, [value]);

  return (
    <p>
      Now: {value}, before: {previous.current}
    </p>
  );
}
```

## Refs vs state

| | State (`useState`) | Ref (`useRef`) |
| --- | --- | --- |
| Triggers a re-render on change? | Yes | No |
| Value available during render? | Yes, always up to date | Yes, but changing it won't show up until something else re-renders |
| Use for | Anything that affects what's rendered | DOM access, timers/subscriptions, values that don't affect the UI |

Rule of thumb: **if the UI needs to change when the value changes, use state; if you just need to remember something between renders, use a ref.**

## Checklist

- [ ] Creating a ref with useRef
- [ ] ref.current
- [ ] Referencing a component
- [ ] Persisting a value without rerendering
- [ ] Refs vs state

## Try it yourself

```jsx
// Build a <Stopwatch /> that:
//   - keeps `elapsed` in state (seconds, shown on screen)
//   - keeps the setInterval id in a ref (not state — it shouldn't cause re-renders itself)
//   - a "Start" button starts the interval, incrementing `elapsed` each second
//   - a "Stop" button clears the interval using the ref
//   - a "Reset" button stops it and sets `elapsed` back to 0
// Bonus: add an <input ref={...} /> that auto-focuses on mount via useEffect.
```

Next up: [10. Component Composition](10-component-composition.md) →
