
# JavaScript Function Types – Complete Reference

## 📘 1. Function Declaration
```js
function greet(name) {
  return `Hello, ${name}`;
}
console.log(greet("Sasi"));
```
Hoisted; used for reusable functions and utilities.

---

## 📗 2. Function Expression
```js
const greet = function(name) {
  return `Hello, ${name}`;
};
console.log(greet("Kumar"));
```
Not hoisted; often used for anonymous or callback functions.

---

## 📙 3. Arrow Function (ES6)
```js
const add = (a, b) => a + b;
const square = n => n * n;
const greet = () => console.log("Hi!");
```
Lexical `this`, concise syntax, great for callbacks.

---

## 📒 4. Anonymous Function
```js
setTimeout(function() {
  console.log("Executed after delay");
}, 1000);
```
Used inline as callback or event handler.

---

## 📕 5. IIFE (Immediately Invoked Function Expression)
```js
(function() {
  console.log("IIFE executed!");
})();
(() => console.log("Arrow IIFE"))();
```
Executes immediately; creates private scope.

---

## 📔 6. Higher-Order Function
```js
function multiplier(factor) {
  return function(num) {
    return num * factor;
  };
}
const double = multiplier(2);
console.log(double(5)); // 10
```
Accepts or returns functions; foundation for functional JS.

---

## 📘 7. Callback Function
```js
function processUser(name, callback) {
  console.log("User:", name);
  callback();
}
processUser("Sasi", () => console.log("Callback executed"));
```

---

## 📗 8. Constructor Function
```js
function Person(name, age) {
  this.name = name;
  this.age = age;
}
const user = new Person("Sasi", 28);
console.log(user);
```

---

## 📙 9. Generator Function
```js
function* counter() {
  yield 1; yield 2; yield 3;
}
const gen = counter();
console.log(gen.next().value);
```
Used for lazy evaluation, async iteration.

---

## 📒 10. Async Function
```js
async function fetchUser() {
  const data = await fetch("https://jsonplaceholder.typicode.com/users/1");
  return data.json();
}
```

---

## 📕 11. Recursive Function
```js
function factorial(n) {
  return n <= 1 ? 1 : n * factorial(n - 1);
}
console.log(factorial(5));
```

---

## 📔 12. Method (Object Function)
```js
const user = {
  name: "Sasi",
  greet() { console.log(`Hi, ${this.name}`); }
};
user.greet();
```

---

## 📘 13. Class Method
```js
class Car {
  start() { console.log("Car started"); }
}
const c = new Car();
c.start();
```

---

## 📗 14. Array Method Callbacks
```js
const nums = [1, 2, 3, 4, 5];
nums.forEach(n => console.log(n));
const squares = nums.map(n => n * n);
const evens = nums.filter(n => n % 2 === 0);
const sum = nums.reduce((a,b) => a + b, 0);
```

---

## 📙 15. Rest Parameter Function
```js
function sum(...nums) {
  return nums.reduce((a,b) => a+b, 0);
}
console.log(sum(1,2,3,4)); // 10
```

---

## 📒 16. Default Parameter Function
```js
function greet(name = "Guest") {
  console.log(`Hello, ${name}`);
}
greet();
```

---

## 📕 17. Function Returning Function (Closure)
```js
function counter() {
  let count = 0;
  return () => ++count;
}
const c = counter();
console.log(c()); // 1
console.log(c()); // 2
```

---

## 📔 18. Function as Property
```js
const obj = {
  name: "Sasi",
  greet: () => console.log("Hello from arrow!")
};
obj.greet();
```

---

## 📘 19. Dynamic Function (Function Constructor)
```js
const sum = new Function("a", "b", "return a + b");
console.log(sum(2, 3)); // 5
```

---

## 🧠 Summary Table
| Type | Example Keyword | Key Trait |
|------|------------------|-----------|
| Function Declaration | `function` | Hoisted |
| Function Expression | `const f = function(){}` | Not hoisted |
| Arrow Function | `()=>{}` | Lexical `this` |
| IIFE | `(() => {})()` | Runs immediately |
| Constructor | `function Person(){}` + `new` | Creates instances |
| Async | `async function` | Awaits Promises |
| Generator | `function*` | Yields values |
| Method | `obj.method(){}` | Object context |
| Class Method | `class { method(){} }` | OOP style |
| Callback / HOF | `(fn)=>fn()` | Pass or return function |
| Recursive | `f(){ f() }` | Calls itself |
| Rest / Default | `(...args)` / `param=default` | Flexible args |
| Dynamic | `new Function()` | Build functions dynamically |

---

## 🧭 Function Family Tree Diagram
![JavaScript Function Family Tree](A_diagram_titled_"JavaScript_Function_Family_Tree".png)

---
