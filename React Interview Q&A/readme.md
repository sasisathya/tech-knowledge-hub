# React.js Interview Questions & Answers

A comprehensive guide covering **React**, **Hooks**, **Redux**, **Context API**, and **Advanced React** — ideal for cracking interviews at top tech companies. Each question includes definitions, examples, and interview-ready explanations.

---

## 🟢 Basic ReactJS Interview Questions

### 1. What is React?

**Answer:** React is an open-source JavaScript library developed by Facebook for building user interfaces, especially single-page applications (SPAs).

**Why it matters:** It allows for building reusable UI components and efficiently updates the UI using a virtual DOM.

```js
const element = <h1>Hello, world!</h1>;
```

---

### 2. What are components in React?

**Answer:** Components are independent, reusable pieces of UI. They can be functional or class-based.

```js
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}
```

---

### 3. Difference between functional and class components?

| Functional Component         | Class Component       |
| ---------------------------- | --------------------- |
| Uses functions               | Uses ES6 classes      |
| Uses Hooks for state/effects | Has lifecycle methods |

---

### 4. What is JSX?

**Answer:** JSX stands for JavaScript XML. It allows writing HTML inside JavaScript and placing them in the DOM without `createElement()`.

```js
const element = <h1>Hello JSX</h1>;
```

---

### 5. How does the Virtual DOM work?

**Answer:** Virtual DOM is a lightweight copy of the real DOM. React updates only the changed elements instead of re-rendering the entire DOM.

**Interview Tip:** Mention diffing algorithm and reconciliation.

---

### 6. What is the role of keys in lists?

**Answer:** Keys help React identify which items have changed, are added, or are removed.

```js
{items.map(item => <li key={item.id}>{item.name}</li>)}
```

---

### 7. What are props in React?

**Answer:** Props (short for properties) are read-only inputs to components. They are used to pass data.

```js
<Welcome name="Alice" />
```

---

### 8. What is state in React?

**Answer:** State is a built-in object used to contain data or information about the component.

```js
const [count, setCount] = useState(0);
```

---

### 9. Explain the React component lifecycle (for class components).

* **Mounting:** constructor, render, componentDidMount
* **Updating:** shouldComponentUpdate, componentDidUpdate
* **Unmounting:** componentWillUnmount

---

### 10. What is the difference between controlled and uncontrolled components?

* **Controlled:** React controls the form input (via state)
* **Uncontrolled:** DOM controls input (uses refs)

```js
<input value={value} onChange={handleChange} /> // controlled
<input ref={inputRef} />                         // uncontrolled
```

---

## 🔵 React Hooks Interview Questions

### 1. What are React Hooks?

**Answer:** Hooks are functions that let you use state and other React features in functional components.

---

### 2. useState vs useRef — differences?

* `useState`: Causes re-render when state changes.
* `useRef`: Holds mutable value that persists across renders without triggering re-render.

```js
const [count, setCount] = useState(0);
const timerRef = useRef(null);
```

---

### 3. Explain useEffect and its dependency array.

**Answer:** `useEffect` runs side effects (data fetching, subscriptions).

```js
useEffect(() => {
  fetchData();
}, [dependency]);
```

---

### 4. How to clean up side effects in useEffect?

Return a cleanup function inside `useEffect`:

```js
useEffect(() => {
  const id = setInterval(doSomething, 1000);
  return () => clearInterval(id);
}, []);
```

---

### 5. How does useCallback prevent unnecessary renders?

It memoizes a callback function to prevent recreation unless dependencies change.

```js
const memoizedCallback = useCallback(() => doSomething(a, b), [a, b]);
```

---

### 6. What is useMemo and when to use it?

Memoizes a computed value to avoid costly recalculations.

```js
const result = useMemo(() => expensiveFunction(a, b), [a, b]);
```

---

### 7. useLayoutEffect vs useEffect?

* `useEffect`: runs after paint
* `useLayoutEffect`: runs synchronously after DOM mutations, before paint

---

### 8. How to create custom hooks?

```js
function useLocalStorage(key, initialValue) {
  const [value, setValue] = useState(() => localStorage.getItem(key) || initialValue);
  useEffect(() => {
    localStorage.setItem(key, value);
  }, [key, value]);
  return [value, setValue];
}
```

---

### 9. How does useReducer work?

Used for complex state logic:

```js
const [state, dispatch] = useReducer(reducer, initialState);
```

---

### 10. useRef use cases?

* Accessing DOM elements
* Storing interval IDs or mutable values

---

## 🟠 Context API Interview Questions

### 1. What is React Context API?

**Answer:** Provides a way to pass data through component tree without props drilling.

---

### 2. When should you use Context instead of props?

Use Context when multiple nested components need access to the same data (e.g., theme, user, auth).

---

### 3. How to pass functions using Context API?

```js
const MyContext = React.createContext();
<MyContext.Provider value={{ value, updateValue }}>
```

---

### 4. Compare Redux and Context API.

| Feature     | Context API | Redux             |
| ----------- | ----------- | ----------------- |
| Scope       | App-level   | Global (anywhere) |
| Boilerplate | Minimal     | More              |
| Middleware  | No          | Yes               |

---

### 5. How to optimize Context to avoid unnecessary re-renders?

* Split context by feature
* Use `React.memo` and selectors
* Avoid frequent updates

---

## 🔴 Redux Interview Questions

### 1. What is Redux and why is it used?

A state management library that provides a single source of truth via a global store.

---

### 2. Core principles of Redux?

* Single source of truth
* State is read-only
* Changes via pure functions (reducers)

---

### 3. What is a reducer in Redux?

A pure function that returns the new state based on the action type.

---

### 4. Explain actions and action creators.

* **Action:** plain JS object `{ type: "ADD" }`
* **Action creator:** function returning action object

```js
const addItem = () => ({ type: "ADD_ITEM" });
```

---

### 5. What is the role of the store in Redux?

Holds application state, provides dispatch and subscribe functions.

---

### 6. Redux Thunk vs Redux Saga?

| Feature        | Thunk               | Saga                       |
| -------------- | ------------------- | -------------------------- |
| Type           | Function middleware | Generator-based middleware |
| Async Handling | Manual (promises)   | Declarative (effects)      |

---

### 7. How does middleware work in Redux?

Enhances `dispatch` by intercepting actions. Useful for logging, async calls, etc.

---

### 8. combineReducers() usage?

Breaks reducer logic into multiple reducers handling slices of state.

```js
const rootReducer = combineReducers({ auth, cart });
```

---

### 9. Connect React to Redux using hooks?

```js
const value = useSelector(state => state.value);
const dispatch = useDispatch();
```

---

### 10. How to use Redux Toolkit?

A modern abstraction over Redux with built-in best practices.

```js
const slice = createSlice({ name, initialState, reducers });
```

---

## 🟣 Advanced React Questions

### 1. What is React Fiber architecture?

A reimplementation of the React core algorithm for incremental rendering.

---

### 2. What is reconciliation in React?

The process React uses to update the DOM by comparing old and new virtual DOM trees.

---

### 3. Explain concurrent mode in React.

Allows React to interrupt rendering to prioritize urgent tasks for better responsiveness.

---

### 4. Lazy loading vs code splitting?

* **Lazy loading:** Load components only when needed
* **Code splitting:** Split bundle into chunks

---

### 5. How does Suspense and React.lazy work?

```js
const LazyComp = React.lazy(() => import('./Comp'));
<Suspense fallback={<div>Loading...</div>}>
  <LazyComp />
</Suspense>
```

---

### 6. Explain error boundaries.

Components that catch JS errors in child components.

```js
componentDidCatch(error, info) {}
```

---

### 7. What are portals in React and when to use them?

Allow rendering components outside the main DOM tree.

```js
ReactDOM.createPortal(<Modal />, document.getElementById('modal-root'));
```

---

### 8. What is prop drilling and how do you avoid it?

Passing props through many levels. Use Context or state management tools to avoid.

---

### 9. How to handle performance optimization in large React apps?

* Code splitting
* Memoization
* Lazy loading
* React.memo / useMemo / useCallback

---

### 10. SSR vs CSR vs ISR (in Next.js)?

| Rendering Type | Description                         |
| -------------- | ----------------------------------- |
| SSR            | Server-side on each request         |
| CSR            | Rendering in browser (client)       |
| ISR            | Static generation with revalidation |

---

# React.js Interview Questions & Answers

A comprehensive guide covering **React**, **Hooks**, **Redux**, **Context API**, **React 19**, and **Advanced React** — ideal for cracking interviews at top tech companies. Each question includes definitions, examples, and interview-ready explanations.

---

## 🟢 Basic ReactJS Interview Questions

... (previous content remains unchanged)

---

## 🔵 React 19 New Features Interview Questions

### 1. What’s new in React 19?

**Answer:** React 19 introduces several new features like the React Compiler, Actions, use() hook, improved SSR hydration/streaming, form actions, and better TypeScript support.

---

### 2. What is the React Compiler introduced in React 19?

**Answer:** The React Compiler is an optimizing compiler that analyzes and automatically memoizes components and hooks at build time, improving rendering performance without manual `useMemo()` or `React.memo()` calls.

---

### 3. How does the React Compiler optimize re-renders?

**Answer:** It automatically identifies components and values that don’t change and avoids recomputing them by tracking dependencies, eliminating unnecessary re-renders.

---

### 4. What are Actions in React 19? How are they different from event handlers?

**Answer:** Actions are server or client functions triggered by form submissions. Unlike traditional event handlers, they can run on the server, simplify data mutation logic, and integrate naturally with `<form>` elements.

```tsx
<form action={someAction}>...</form>
```

---

### 5. What is use() in React 19? When should you use it?

**Answer:** `use()` is a new hook that allows components to wait for a Promise (like a server function or data fetch) to resolve. It integrates with Suspense for declarative async rendering.

```js
const user = use(fetchUser());
```

---

### 6. Explain the new form actions and async form handling in React 19.

**Answer:** React 19 supports async form submissions where the `action` attribute of a `<form>` can point to an async function (server/client). Form state and result are handled without manual useEffect/useState code.

---

### 7. What is the new built-in <form> behavior with Actions in React 19?

**Answer:** Forms can now submit directly to server-defined actions without JavaScript glue code. React automatically handles serialization, validation, and redirection.

---

### 8. What are "Server Actions" in React 19 (Next.js)?

**Answer:** Server Actions allow you to define async functions in server components that can be triggered from client UI elements like forms or buttons, enabling server mutations with minimal client JS.

---

### 9. What’s the role of useFormStatus() and useFormState() in React 19?

* `useFormStatus()`: Gets the status of the current form submission (e.g., pending, error)
* `useFormState()`: Holds the result or response from the last form submission

---

### 10. How does React 19 improve hydration and streaming for SSR?

**Answer:** React 19 enhances Suspense, allowing better streaming and partial hydration. Server-rendered content loads faster and client JS is loaded in smaller chunks.

---

## 🟢 Advanced React 19 Questions

### 1. How is React Compiler different from memoization or useMemo()?

**Answer:** Unlike manual memoization, React Compiler analyzes and memoizes automatically at build time, reducing developer overhead and human error.

---

### 2. How do Actions replace traditional state mutation logic?

**Answer:** Actions allow mutations to occur on the server or client and are automatically tied to user input events like form submission — removing the need for manually managing state update logic.

---

### 3. What are the benefits of React Compiler over manual optimization?

* Eliminates need for `useMemo`, `useCallback`, `React.memo`
* Reduces boilerplate
* Ensures consistent optimization

---

### 4. Explain how the new use() hook integrates with Suspense and async rendering.

**Answer:** `use()` suspends rendering until a Promise resolves. It works within Suspense boundaries to make async logic declarative and simpler to read.

---

### 5. What are the limitations or caveats of Actions and the use() hook?

* Server Actions may require special handling for auth/security
* `use()` only works in certain React runtimes (Next.js App Router)
* Experimental as of React 19 (subject to change)

---

### 6. How does React 19 enable better DX (developer experience)?

* Less boilerplate (no `useMemo`, `useCallback`)
* Server-first logic reduces client JS size
* Simplified forms and async handling

---

### 7. What are the differences between React Server Components (RSC) and Actions?

| Feature       | React Server Components | Server Actions           |
| ------------- | ----------------------- | ------------------------ |
| Purpose       | Server-rendered views   | Server-side mutations    |
| Triggered By  | Routing or page load    | Form submissions/buttons |
| JS on Client? | No                      | Minimal                  |

---

### 8. How do you debug or log server actions in React 19 (Next.js)?

Use server console logs, Next.js instrumentation (e.g., `app/api/logging.ts`), and consider edge middleware to inspect requests/responses.

---

### 9. How does React 19 support better compatibility with TypeScript?

React 19 improves TypeScript inference for form actions and compiler analysis, reducing need for explicit typings.

---

> This document is your go-to reference for mastering React.js interviews. Practice with real projects, keep your concepts sharp, and be ready to explain with examples.
