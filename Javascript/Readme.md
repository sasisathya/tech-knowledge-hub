# 📘 Every Developer Should Know These JavaScript Concepts

As developers, it’s essential to have a solid understanding of JavaScript fundamentals and advanced topics. Whether you’re just starting or refining your expertise, this guide provides in-depth explanations and examples for 88 key JavaScript concepts.

## JavaScript Concepts Comprehensive Guide

This document provides detailed explanations and examples of essential JavaScript concepts useful for beginners to advanced developers. Organized alphabetically for clarity.

---

## 1. Array Buffer & Typed Arrays

**ArrayBuffer** represents a generic, fixed-length binary data buffer. **Typed Arrays** provide a way to read and write to an ArrayBuffer using specific types.

```js
const buffer = new ArrayBuffer(8); // 8 bytes
const view = new Uint8Array(buffer);
view[0] = 255;
console.log(view[0]); // 255
```

## 2. Array Destructuring

Destructures values from an array into variables.

```js
const [a, b] = [1, 2];
console.log(a); // 1
```

## 3. Array Methods (map, filter & more)

* `map`: Transform array
* `filter`: Filter array based on condition
* `reduce`: Accumulate value

```js
const nums = [1, 2, 3];
console.log(nums.map(x => x * 2)); // [2, 4, 6]
```

## 4. Arrow Functions vs Regular Functions

* Arrow functions do not bind their own `this`.

```js
const obj = {
  name: 'JS',
  arrow: () => console.log(this.name),
  regular() { console.log(this.name); }
};
obj.arrow(); // undefined
obj.regular(); // 'JS'
```

## 5. Async / Await

Simplifies promise handling in asynchronous code.

```js
async function fetchData() {
  const res = await fetch('/api');
  const data = await res.json();
  console.log(data);
}
```

## 6. Bitwise Operators

Used for manipulating bits.

```js
console.log(5 & 1); // 1
console.log(5 | 1); // 5
console.log(5 ^ 1); // 4
```

## 7. call(), apply(), bind()

Used to change the context of `this`.

```js
function greet() { console.log(this.name); }
const obj = { name: 'JS' };
greet.call(obj);
greet.apply(obj);
const bound = greet.bind(obj);
bound();
```

## 8. Callbacks

Functions passed into other functions as arguments.

```js
function greet(name, cb) {
  cb(`Hello, ${name}`);
}
greet('JS', console.log);
```

## 9. Canvas API

Used for drawing graphics.

```html
<canvas id="myCanvas" width="200" height="100"></canvas>
<script>
const ctx = document.getElementById('myCanvas').getContext('2d');
ctx.fillStyle = 'red';
ctx.fillRect(10, 10, 150, 75);
</script>
```

## 10. Clean Code Practices in JavaScript

* Use meaningful names
* Avoid deep nesting
* DRY (Don’t Repeat Yourself)
* Keep functions small and focused

```js
// Bad
function doSomething(a, b) { return a + b; }

// Good
function calculateSum(x, y) { return x + y; }
```

## 11. Client-Side Routing

Handles navigation without full page reloads (e.g., SPA frameworks).

```js
// In React Router
<Route path="/about" element={<About />} />
```

## 12. Closures

Function with preserved scope chain.

```js
function outer() {
  let count = 0;
  return function inner() {
    count++;
    console.log(count);
  }
}
const counter = outer();
counter(); // 1
```

## 13. Code Splitting

Breaks code into smaller bundles for faster load.

```js
// React lazy loading
const Home = React.lazy(() => import('./Home'));
```

## 14. Cross-Browser Compatibility

Ensuring consistent functionality across browsers.

* Use Babel for transpiling
* Test with BrowserStack

## 15. Cross-Origin Resource Sharing (CORS)

Allows/denies access to resources from different origins.

```js
// Node.js Express example
app.use((req, res, next) => {
  res.setHeader('Access-Control-Allow-Origin', '*');
  next();
});
```

## 16. Currying

Transforms a function with multiple arguments into nested functions.

```js
function multiply(a) {
  return function(b) {
    return a * b;
  }
}
const double = multiply(2);
console.log(double(3)); // 6
```

## 17. Custom Events

Allows creating and dispatching custom events.

```js
const event = new CustomEvent('myEvent', { detail: { msg: 'Hello' } });
document.dispatchEvent(event);
```

## 18. Debounce vs Throttle

**Debounce** delays execution until after a pause. **Throttle** limits function calls over time.

## 19. Debouncing and Throttling

```js
// Debounce
function debounce(fn, delay) {
  let timeout;
  return (...args) => {
    clearTimeout(timeout);
    timeout = setTimeout(() => fn(...args), delay);
  };
}

// Throttle
function throttle(fn, limit) {
  let lastCall = 0;
  return (...args) => {
    const now = new Date().getTime();
    if (now - lastCall >= limit) {
      lastCall = now;
      fn(...args);
    }
  };
}
```

## 20. Deep vs. Shallow Copy

* Shallow copy: One level deep
* Deep copy: Full object copy

```js
// Shallow
const a = { x: 1 };
const b = Object.assign({}, a);

// Deep
const c = JSON.parse(JSON.stringify(a));
```

## 21. Design Patterns (Observer, Singleton, Factory)

* **Singleton** ensures one instance:

```js
const Singleton = (function() {
  let instance;
  return function() {
    if (!instance) instance = this;
    return instance;
  }
})();
```

* **Observer** pattern reacts to state change
* **Factory** creates objects without `new`

## 22. Destructuring

Extracting properties from objects/arrays.

```js
const { name } = { name: 'JS' };
```

## 23. Destructuring Assignment

Assign variables using object/array structure.

```js
const person = { name: 'JS', age: 25 };
const { name, age } = person;
```

## 24. Destructuring Nested Objects/Arrays

```js
const obj = { a: { b: { c: 1 } } };
const { a: { b: { c } } } = obj;
```

## 25. DOM Manipulation

Modifying HTML content or style using JavaScript.

```js
document.getElementById('demo').innerText = 'Hello';
```

## 26. Dynamic Imports

Importing modules at runtime.

```js
import('./module.js').then(module => module.doStuff());
```

## 27. Dynamic Typing

Variables can hold multiple types over time.

```js
let x = 5;
x = 'Hello'; // valid in JS
```

## 28. Equality Operators (== vs ===)

* `==` checks value (with coercion)
* `===` checks value and type

```js
console.log(2 == '2'); // true
console.log(2 === '2'); // false
```

## 29. Error Boundaries (in React.js)

Catch rendering errors in components.

```js
class ErrorBoundary extends React.Component {
  componentDidCatch(error, info) {
    // Log error
  }
  render() {
    return this.props.children;
  }
}
```

## 30. Error Handling (Try/Catch/Throw)

```js
try {
  throw new Error('Oops');
} catch (e) {
  console.error(e.message);
}
```

## 31. ES6 Features (Arrow Functions, Classes, Modules, Destructuring)

* Arrow functions
* let/const
* Classes
* Default + Rest Parameters
* Promises

```js
const sum = (a, b) => a + b;
class Person { constructor(name) { this.name = name; } }
```

## 32. Event Bubbling and Capturing

* Bubbling: from child to parent
* Capturing: from parent to child

```js
div.addEventListener('click', handler, true); // capture phase
```

## 33. Event Delegation

Attach one listener to parent for child events.

```js
document.getElementById('parent').addEventListener('click', e => {
  if (e.target.matches('button')) console.log('Clicked', e.target);
});
```

## 34. Event Handling (addEventListener)

```js
document.getElementById('btn').addEventListener('click', () => alert('Clicked'));
```

## 35. Event Loop

Handles async operations via micro/macrotasks.

```js
console.log('start');
setTimeout(() => console.log('timeout'));
Promise.resolve().then(() => console.log('promise'));
console.log('end');
// Output: start, end, promise, timeout
```

## 36. Fetch API

Used for making HTTP requests.

```js
fetch('https://api.example.com')
  .then(res => res.json())
  .then(data => console.log(data));
```

## 37. Functions

Reusable code blocks.

```js
function greet(name) { return `Hello, ${name}`; }
```

## 38. Generator Functions

Function that can pause and resume.

```js
function* gen() {
  yield 1;
  yield 2;
}
const it = gen();
console.log(it.next().value); // 1
```

## 39. Geolocation API

Access geographic location of user.

```js
navigator.geolocation.getCurrentPosition(pos => {
  console.log(pos.coords.latitude);
});
```

## 40. Geolocation vs Location Services

* Geolocation: Web API
* Location Services: OS-level, hardware-backed services (e.g., GPS)

## 41. Global and Local Object (window, globalThis)

```js
console.log(window === globalThis); // true in browser
```

Would you like me to continue from concept 42 onwards?
