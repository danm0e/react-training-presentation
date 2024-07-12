# Practical Functional JavaScript
- Variables: Intro to const, let and var.
- Function basics: Understanding the basics about functions
- Advanced function arguments: Using rest and spread to write cleaner, simpler functions.
- Passing by reference & value: How functions interact with in memory variables.
- Understanding Functional Scope: Functions and how they access parent scope.
---
# Variables 
In JavaScript, there are 3 ways to declare a variable, each with their own differences.
These are:
- var
- let
- const
---
The first difference between the 3 declarations is scoping.
`var` has function scope, meaning that any variable declarations using it are scoped to within the function that is currently executing.
`let` and `const` are block scoped, meaning that declarations are scoped to the block that they are in.
---
# Difference: Scoping
Here is an example of function and block scope:
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
# Difference: Immutability
---
A `var` and a `let` declaration can be overwritten
A `const` cannot. If you attempt to overwrite it, an error will be thrown.
---
```js
const NAME = "Louis";
let age = 12;

console.log(`${NAME} is ${age}`);

try {
 age = age + 1;
 NAME = "woo";
} catch (e) {
 console.log(e);
}

console.log(`${NAME} is ${age}`);

> Louis is 12
> TypeError: Assignment to constant variable.
> Louis is 13
```
---
Whilst you cannot update the value of a `const` itself, you can update the properties of an array or object assigned to a `const`.
```js
const NAMES = ["Mo", "Jo"];
NAMES.push("JoJo");

console.log(NAMES);

> [ 'Mo', 'Jo', 'JoJo' ]
```
---
If you don’t add a var, let or const keyword, the variable will be bound to the global scope. Generally you want to avoid this as it can easily cause issues.
```js
(function nameMyCat() {
 cat = "Reginald Meowington III";
})();

console.log(cat);
> Reginald Meowington III
```