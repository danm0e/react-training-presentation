# Variables 
In JavaScript, there are 3 different ways to declare a variable.

These are:
- `var   ` Function Scope <!-- .element: class="fragment" --> 
- `let   ` Block Scope<!-- .element: class="fragment" -->
- `const`   Immutable Block Scope<!-- .element: class="fragment" -->
Note: The first difference between the 3 declarations is scoping.
`var` has function scope, meaning that any variable declarations using it are scoped to within the function that is currently executing.
`let` and `const` are block scoped, meaning that declarations are scoped to the block that they are in.
---
### Difference: Scoping

```js
var $var = 1;
let $let = 2;
const $const = 3;

if (true) {
 var $var = true;
 let $let = true;
 const $const = true;
 console.log("Block scope:", $var, $let, $const);
}

console.log("Function scope:", $var, $let, $const);
> Block scope: true true true
> Function scope: true 2 3
```
Note: Here is an example of function and block scope:
---
### Difference: Immutability

```js
const NAME = "Louis";
let age = 12;

console.log(`${NAME} is ${age}`);

try {
 age = age + 1;
 NAME = "Joe";
} catch (e) {
 console.log(e);
}

console.log(`${NAME} is ${age}`);

> Louis is 12
> TypeError: Assignment to constant variable.
> Louis is 13
```
Note: A `var` and a `let` declaration can be overwritten
A `const` cannot. If you attempt to overwrite it, an error will be thrown.
---
### Difference: Immutability

```js
const NAMES = ["Mo", "Jo"];
NAMES.push("JoJo");

console.log(NAMES);

> [ 'Mo', 'Jo', 'JoJo' ]
```
Note: Whilst you cannot update the value of a `const` itself, you can update the properties of an array or object assigned to a `const`.
---
### Global
```js
(function nameMyCat() {
 cat = "Reginald Meowington III";
})();

console.log(cat);
> Reginald Meowington III
```
Note: If you don’t add a var, let or const keyword, the variable will be bound to the global scope. Generally you want to avoid this as it can easily cause issues.