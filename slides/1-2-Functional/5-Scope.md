# Understanding <!--.element: class="r-fit-text" -->
# Functional Scope <!--.element: class="r-fit-text" -->
---
### Closures

```js [1-5|6-8|9-10|11-13]
const add = function (a) {
 return function (b) {
   return a + b;
 };
};
const addOne = add(1);
console.log(addOne(2));
> 3
console.log(addOne(5));
> 6
const addFour = add(4);
console.log(addFour(3));
> 7
```
Note: A closure is the combination of a function bundled together with references to its surrounding state. In other words, a closure gives you access to an outer function's scope from an inner function. In JavaScript, closures are created every time a function is created, at function creation time.
This can allow us to create private/inaccessible scope, or allow us to have functions with some parameters pre-set.
---
### Advanced closure example 

```js [1-7|9|11-12|14-15]
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