# Functions
---
### Function characteristics

- Can take an infinite number of arguments
- Implicitly returns undefined<!-- .element: class="fragment" --> 
- Is a first-class object<!-- .element: class="fragment" --> 
- Functions can be called<!-- .element: class="fragment" --> 
Note: In JavaScript, functions are first-class objects, because they can be passed to other functions, returned from functions, and assigned to variables and properties. They can also have properties and methods just like any other object. What distinguishes them from other objects is that functions can be called.
---
### Function Signatures


```js 
const getAllTheCats = function (name = "Miggins") {
 return {
   name,
 };
};
```
The function above:
- Expects a single parameter<!-- .element: class="fragment" --> 
- If no parameter is passed, the assumed default value for the cat is Miggins<!-- .element: class="fragment" --> 
- Returns an object with the key “name”<!-- .element: class="fragment" --> 

Note: A function signature is the pattern the function expects you to implement, its inputs and outputs.
When thinking about a function, it’s important to consider the function signature carefully as it can help you write more readable and extendable code.
---
### Hoisting
Note: Hoisting in JavaScript refers to the process whereby the interpreter appears to move the declaration of functions to the top of their scope, prior to execution of the code.
Hoisting allows functions to be safely used in code before they are declared.
Variables are also hoisted, but only their declarations. They are not initialized with any value. Additionally, an exception will be thrown if a variable declared with let or const is read before it is initialized.
---
### Hoisting

```js[1-8|2-3|2,7|3,8]
try {
 console.log(funcDec);
 console.log(funcExp);
} catch (e) {
 console.log(e);
}
function funcDec() {}
const funcExp = () => {};
```
Note: The example on the here gets hoisted
Additionally, an error will be thrown because funcExp has been accessed before it has been initialized.
Hoisting happens because of how our code is interpreted and executed by the JavaScript interpreter.
---
### Runtime
Javascript takes a minimum of 2 cycles
- 1st run: Move variables declarations to the top<!-- .element: class="fragment" --> 
- 2nd run: Assigning values, executing function calls, reassignment of values, etc.<!-- .element: class="fragment" --> 

Note: During run time, javascript code is interpreted in a minimum of 2 cycles:
- 1st run: the interpreter goes through the code line by line while looking only for functions or variable declarations. Wherever it encounters a declaration, it moves it to the top.
- 2nd run: the interpreter starts compiling the code from the previous run. i.e. assigning values, executing function calls, reassignment of values, etc.
---
### Function Returning

If a function doesn’t have a return keyword, it will return undefined by default. The exception to this is an arrow function using the concise body syntax.

```js[1,7|2,8|3,9|4,10|5,11]
function undefinedReturn1() {}
function explicitReturn1() { return "hello";}
const undefinedReturn2 = () => {};
const implicitReturn = () => "hello";
const explicitReturn2 = () => { return "hello";}

console.log(undefinedReturn1());  > undefined
console.log(explicitReturn1());   > hello
console.log(undefinedReturn2());  > undefined
console.log(implicitReturn());    > hello
console.log(explicitReturn2());   > hello
```
