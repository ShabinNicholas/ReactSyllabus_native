# Where to go from here

You've covered the ten core areas of the *React Syllabus Checklist*. If every box is ticked, you're ready to start **React Native**.

## You should now be comfortable with

- Writing functional components and JSX, including expressions and Fragments
- Passing and reading props, `children`, and default values
- Managing state with `useState` — primitives, objects, and arrays (immutably)
- Handling events and updating state from them
- Building controlled form inputs, checkboxes, and selects driven by state
- Conditional rendering with `if`, ternaries, and `&&`
- Rendering lists with `.map()` and stable `key`s
- Running side effects with `useEffect`, dependency arrays, and cleanup
- Using `useRef` for DOM access and values that persist without re-rendering
- Composing UIs from small, reusable components and lifting state up

## How these map to React Native

| React (web) | React Native |
| --- | --- |
| `<div>`, `<span>` | `<View>` |
| `<p>`, text nodes | `<Text>` (all text must be inside `<Text>`) |
| `<button>` | `<Pressable>`, `<TouchableOpacity>`, `<Button>` |
| `<img src>` | `<Image source>` |
| `<input onChange>` | `<TextInput onChangeText>` |
| CSS / `className` | `StyleSheet.create` + `style` prop (Flexbox by default) |
| `onClick` | `onPress` |
| scrolling is automatic | `<ScrollView>` / `<FlatList>` |

**The programming model is identical** — components, props, state, `useState`, `useEffect`, composition all work exactly the same. Only the primitive components and styling change.

## Suggested next topics

- The rules of hooks
- Custom hooks (extracting reusable logic)
- Context API (avoiding deep prop drilling)
- A data-fetching library (TanStack Query)
- React Navigation (once you're in React Native)

## Official docs

- [React documentation](https://react.dev/)
- [React Native documentation](https://reactnative.dev/)
- [Expo](https://docs.expo.dev/) — the easiest way to start a React Native app

← Back to [Home](/)
