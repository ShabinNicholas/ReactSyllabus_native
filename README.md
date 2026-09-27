# React Syllabus Checklist

Welcome! This is a friendly, hands-on reference for the **core React concepts you need before starting React Native**. It follows the *React Syllabus Checklist* — tick off each topic as you cover it.

Every page follows the same shape:

- **What it is** — a plain-English explanation, no jargon dumps.
- **Why it matters** — when you'd actually reach for this.
- **Code you can run** — short, heavily commented examples.
- **Checklist** — the exact items from the syllabus this page covers.
- **Try it yourself** — a tiny challenge to lock the concept in.

## How to use this site

Pick a topic from the sidebar, or follow the syllabus in order if you're learning React from scratch. The topics build on each other:

1. **[React Basics](guide/01-react-basics.md)** — what React is, components, JSX.
2. **[Props](guide/02-props.md)** — passing data into components.
3. **[State — useState](guide/03-state-usestate.md)** — data that changes over time.
4. **[Event Handling](guide/04-event-handling.md)** — responding to the user.
5. **[Controlled Components](guide/05-controlled-components.md)** — form inputs driven by state.
6. **[Conditional Rendering](guide/06-conditional-rendering.md)** — showing UI based on state.
7. **[Rendering Lists](guide/07-rendering-lists.md)** — turning arrays into UI.
8. **[Side Effects — useEffect](guide/08-side-effects-useeffect.md)** — syncing with the outside world.
9. **[Data Fetching (with Axios)](guide/09-data-fetching-axios.md)** — getting real data from an API.
10. **[Refs — useRef](guide/10-refs-useref.md)** — direct DOM access and values that skip re-renders.
11. **[Component Composition](guide/11-component-composition.md)** — building bigger UIs from small pieces.

See the **[Full Checklist](checklist.md)** for every item on one page.

## Running the examples

The fastest way to try React with no install:

- Open the [React playground on StackBlitz](https://stackblitz.com/edit/react) or [CodeSandbox](https://codesandbox.io/s/new), **or**
- Scaffold locally with Vite:

```bash
npm create vite@latest my-app -- --template react
cd my-app
npm install
npm run dev
```

## About this site

This documentation is built with [Docsify](https://docsify.js.org/) — no build step, just Markdown files rendered on the fly. It's designed to be hosted for free on **GitHub Pages**.

Ready? Start with **[1. React Basics](guide/01-react-basics.md)** →
