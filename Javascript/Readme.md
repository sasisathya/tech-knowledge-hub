# 📘 Every Developer Should Know These JavaScript Concepts

As developers, it’s essential to have a solid understanding of JavaScript fundamentals and advanced topics. Whether you’re just starting or refining your expertise, this guide provides in-depth explanations and examples for 88 key JavaScript concepts.

---

## 🧠 Core Concepts (1–20)

### 1. **Array Buffer & Typed Arrays**

ArrayBuffer is a fixed-length binary buffer. Typed arrays (e.g., `Uint8Array`, `Float32Array`) allow reading/writing of binary data efficiently.

```js
const buffer = new ArrayBuffer(16);
const view = new Uint8Array(buffer);
view[0] = 255;
```

### 2. **Array Destructuring**

Allows unpacking values from arrays into variables.

```js
const [a, b] = [10, 20];
```

### 3. **Array Methods (map, filter, etc.)**

These are higher-order functions on arrays.

```js
[1, 2, 3].map(x => x * 2); // [2, 4, 6]
[1, 2, 3].filter(x => x > 1); // [2, 3]
```

### 4. **Arrow Functions vs Regular Functions**

Arrow functions do not have their own `this`, `arguments`, or `super`.

```js
const add = (a, b) => a + b;
```

### 5. **Async / Await**

Syntactic sugar over Promises.

```js
async function getData() {
  const res = await fetch('https://api.example.com');
  const data = await res.json();
  console.log(data);
}
```

### 6. **Bitwise Operators**

Used to manipulate binary representations.

```js
const a = 5 & 1; // 1 (0101 & 0001)
```

### 7. **call(), apply(), bind()**

Control `this` in functions.

```js
const obj = { name: 'JS' };
function greet() { console.log(this.name); }
greet.call(obj); // JS
```

### 8. **Callbacks**

A function passed as an argument.

```js
function greet(name, cb) {
  cb(`Hello ${name}`);
}
greet('Dev', console.log);
```

### 9. **Canvas API**

Used for rendering graphics.

```js
const canvas = document.getElementById('myCanvas');
const ctx = canvas.getContext('2d');
ctx.fillRect(10, 10, 100, 100);
```

### 10. **Clean Code Practices**

Readable, maintainable code: meaningful names, small functions, avoid duplication.

```js
// Bad
function x(a){return a*2}

// Good
function double(number) { return number * 2; }
```

### 11. **Client-Side Routing**

Controls URL changes in SPAs without reloading pages.

```js
history.pushState({}, '', '/dashboard');
```

### 12. **Closures**

A function remembers variables from its lexical scope.

```js
function outer() {
  let count = 0;
  return function inner() {
    count++;
    return count;
  }
}
const counter = outer();
counter(); // 1
```

### 13. **Code Splitting**

Break code into smaller bundles.

```js
// webpack or dynamic import
import('./module.js').then(mod => mod.init());
```

### 14. **Cross-Browser Compatibility**

Ensure code runs on different browsers using polyfills, transpilers, and feature detection.

### 15. **Cross-Origin Resource Sharing (CORS)**

A browser security feature that controls resource sharing between different origins.

### 16. **Currying**

Transforms a function with multiple arguments into a series of unary functions.

```js
const multiply = a => b => a * b;
```

### 17. **Custom Events**

Allows you to define your own events.

```js
const event = new CustomEvent('hello', { detail: 'world' });
document.dispatchEvent(event);
```

### 18. **Debounce vs Throttle**

* **Debounce**: delays execution until after a pause.
* **Throttle**: ensures execution at fixed intervals.

### 19. **Debouncing and Throttling**

```js
function debounce(fn, delay) {
  let timeout;
  return function(...args) {
    clearTimeout(timeout);
    timeout = setTimeout(() => fn.apply(this, args), delay);
  }
}
```

### 20. **Deep vs. Shallow Copy**

* Shallow: only top-level copied
* Deep: all levels copied

```js
const shallow = {...obj};
const deep = JSON.parse(JSON.stringify(obj));
```

# JavaScript Concepts Comprehensive Guide

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

---

**\[Due to size constraints, this is a partial preview.]**

Would you like me to continue documenting the remaining concepts (11 to 88) in the same format?



