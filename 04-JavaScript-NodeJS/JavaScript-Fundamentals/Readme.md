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

## 42. Hoisting

Variables and function declarations are moved to the top of their scope before code execution.

```js
console.log(a); // undefined
var a = 5;
```

## 43. IIFE (Immediately Invoked Function Expression)

Function that runs immediately after it's defined.

```js
(function() {
  console.log('Executed');
})();
```

## 44. Inheritance (Class-based, Prototype-based)

```js
class Animal {
  speak() { console.log('Animal speaks'); }
}
class Dog extends Animal {}
const d = new Dog();
d.speak();
```

## 45. Intersection Observer API

Used for observing element visibility.

```js
const observer = new IntersectionObserver(entries => {
  entries.forEach(entry => console.log(entry.isIntersecting));
});
observer.observe(document.querySelector('#target'));
```

## 46. JavaScript Memory Management (Garbage Collection)

Automatically allocates and frees memory. Use references wisely to avoid leaks.

## 47. JavaScript vs ECMAScript

* **JavaScript**: Implementation (browser/runtime)
* **ECMAScript**: Specification (language standard)

## 48. JSON (JavaScript Object Notation)

Data format used for data exchange.

```js
const json = JSON.stringify({ name: 'JS' });
const obj = JSON.parse(json);
```

## 49. Lazy Loading

Loading content only when needed.

```js
<img src="img.jpg" loading="lazy" />
```

## 50. Map and Set

```js
const map = new Map([[1, 'a']]);
const set = new Set([1, 2, 3]);
```

## 51. Memoization

Caching results to improve performance.

```js
const memo = {};
function fib(n) {
  if (memo[n]) return memo[n];
  if (n < 2) return n;
  return (memo[n] = fib(n - 1) + fib(n - 2));
}
```

## 52. Methods

Functions defined on objects.

```js
const obj = {
  greet() { return 'Hello'; }
};
```

## 53. Module Pattern

Encapsulation using closures.

```js
const Counter = (() => {
  let count = 0;
  return {
    increment: () => ++count,
    get: () => count
  };
})();
```

## 54. Modules (Import/Export)

```js
// file.js
export const x = 10;
// app.js
import { x } from './file.js';
```

## 55. MutationObserver

Observes DOM changes.

```js
const observer = new MutationObserver(mutations => {
  console.log(mutations);
});
observer.observe(document.body, { childList: true });
```

## 56. NaN (Not a Number)

Result of invalid number operation.

```js
console.log(NaN === NaN); // false
Number.isNaN(NaN); // true
```

## 57. Object

Collection of key-value pairs.

```js
const obj = { name: 'JS' };
```

## 58. Object Literal Shorthand

```js
const name = 'JS';
const obj = { name }; // same as { name: name }
```

## 59. Object.assign()

Copies values from source to target object.

```js
const target = {};
Object.assign(target, { a: 1 });
```

## 60. Performance Optimization

* Use lazy loading, debouncing, reduce DOM access
* Use web workers, pagination, caching

## 61. Polyfills

Code that adds support for features not supported in older browsers.

```js
if (!Array.prototype.includes) {
  Array.prototype.includes = function(el) {
    return this.indexOf(el) !== -1;
  };
}
```

## 62. Promise.all()

Resolves when all promises resolve.

```js
Promise.all([Promise.resolve(1), Promise.resolve(2)]).then(console.log);
```

## 63. Promises

Handle async code.

```js
new Promise((resolve, reject) => {
  resolve('Done');
}).then(console.log);
```

## 64. Prototypal Inheritance

Objects inherit from other objects.

```js
const a = { greet() { return 'Hello'; } };
const b = Object.create(a);
console.log(b.greet());
```

## 65. RegEx (Regular Expressions)

Used for pattern matching.

```js
const regex = /hello/i;
regex.test('Hello World');
```

## 66. Scope (Function vs Block Scope)

* `var`: function scoped
* `let`, `const`: block scoped

## 67. Service Workers

Scripts that run in background for caching/offline.

```js
navigator.serviceWorker.register('/sw.js');
```

## 68. Set and Map Iteration

```js
for (const val of new Set([1, 2, 3])) console.log(val);
for (const [k, v] of new Map([[1, 'a']])) console.log(k, v);
```

## 69. Set vs Map

* **Set**: unique values
* **Map**: key-value pairs

## 70. SetTimeout and SetInterval

```js
setTimeout(() => console.log('later'), 1000);
const intervalId = setInterval(() => console.log('repeat'), 1000);
```

## 71. Shadow DOM

Encapsulation for custom elements.

```js
const shadow = element.attachShadow({ mode: 'open' });
shadow.innerHTML = '<p>Shadow!</p>';
```

## 72. Template Literals

```js
const name = 'JS';
console.log(`Hello, ${name}`);
```

## 73. Shadowing

Inner variable with same name as outer.

```js
let a = 1;
function foo() {
  let a = 2;
  console.log(a); // 2
}
```

## 74. Spread & Rest Operators

```js
// Spread
const arr = [1, 2];
const copy = [...arr];

// Rest
function sum(...nums) {
  return nums.reduce((a, b) => a + b);
}
```

## 75. Strict Mode

Enables stricter parsing and error handling.

```js
'use strict';
```

## 76. SVG Manipulation

```js
const svg = document.querySelector('svg');
svg.setAttribute('width', '100');
```

## 77. Symbol

Unique identifier.

```js
const sym = Symbol('desc');
```

## 78. String Concatenation

```js
const full = 'Hello' + ' ' + 'World';
```

## 79. This Keyword

Refers to context object.

```js
const obj = {
  name: 'JS',
  greet() { return this.name; }
};
```

## 80. Test-Driven Development

Write tests before implementation.

```js
// Pseudo-code
it('adds correctly', () => expect(add(2, 3)).toBe(5));
```

## 81. Boolean Values

```js
const isTrue = true;
const isFalse = false;
```

## 82. let, var & const

* `let`: block-scoped, mutable
* `var`: function-scoped
* `const`: block-scoped, immutable reference

## 83. Type Coercion vs Type Conversion

* Coercion: implicit
* Conversion: explicit

```js
console.log('5' + 1); // '51'
console.log(Number('5') + 1); // 6
```

## 84. URL API (URLSearchParams, URL objects)

```js
const url = new URL('https://example.com?page=1');
const params = new URLSearchParams(url.search);
console.log(params.get('page'));
```

## 85. WeakMap & WeakSet

Only hold weak references, no iteration.

```js
const wm = new WeakMap();
const ws = new WeakSet();
```

## 86. Web Animations

```js
document.querySelector('div').animate([
  { transform: 'translateX(0)' },
  { transform: 'translateX(100px)' }
], {
  duration: 1000
});
```

## 87. localStorage & sessionStorage

```js
localStorage.setItem('key', 'value');
sessionStorage.setItem('key', 'value');
```

## 88. Web Workers & WebSockets

* **Web Workers**: Run JS in background thread.

```js
const worker = new Worker('worker.js');
```

* **WebSockets**: Bi-directional communication.

```js
const socket = new WebSocket('ws://example.com');
socket.onmessage = (e) => console.log(e.data);
```

---

