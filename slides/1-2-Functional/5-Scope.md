# Understanding Functional Scope
---
### Closures

```js
const add = function (a) {
 return function (b) {
   return a + b;
 };
};
const parent = add(1);
console.log(parent(2));
> 3
console.log(parent(5));
> 6
```
Note: A closure is the combination of a function bundled together with references to its surrounding state. In other words, a closure gives you access to an outer function's scope from an inner function. In JavaScript, closures are created every time a function is created, at function creation time.
This can allow us to create private/inaccessible scope, or allow us to have functions with some parameters pre-set.
---
### Advanced closure example 

```js
const getFunctions = function () {
 let funcs = [];
 for (let i = 0; i < 3; i++) {
   funcs[i] = () => `I am index ${i}!`;
 }
 return funcs;
};

const funcs = getFunctions();

console.log(funcs[0]());
> I am index 0

console.log(funcs[2]());
> I am index 2
```
Note: As a function stores its closure when it’s created, we can do things like the following