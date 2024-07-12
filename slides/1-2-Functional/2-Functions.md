# Function characteristics
A function is the encapsulation of behaviours. Here are some of the characteristics of functions in JavaScript:
Functions can take an infinite number of arguments
A function implicitly returns undefined
A function is a first-class object
A function is an object, with behaviour

---
# Function Signatures
A function signature is the pattern the function expects you to implement, its inputs and outputs.
When thinking about a function, it’s important to consider the function signature carefully as it can help you write more readable and extendable code.
The function signature of the below example is:
- Expects a single parameter
- If no parameter is passed, the assumed default value for the cat is Miggins
- Returns an object with the key “name”

```js 
const getAllTheCats = function (name = "Miggins") {
 return {
   name,
 };
};
```
---
# Hoisting
Hoisting in JavaScript refers to the process whereby the interpreter appears to move the declaration of functions to the top of their scope, prior to execution of the code.
Hoisting allows functions to be safely used in code before they are declared.
Variables are also hoisted, but only their declarations. They are not initialized with any value. Additionally, an exception will be thrown if a variable declared with let or const is read before it is initialized.
---
The example on the below gets hoisted
Additionally, an error will be thrown because funcExp has been accessed before it has been initialized.

```
try {
 console.log(funcDec);
 console.log(funcExp);
} catch (e) {
 console.log(e);
}
function funcDec() {}
const funcExp = () => {};
```
Additionally, an error will be thrown because funcExp has been accessed before it has been initialized.
```
function funcDec() {}
try {
 console.log(funcDec);
 console.log(funcExp);
} catch (e) {
 console.log(e);
}
const funcExp = () => {};
```
---
Hoisting happens because of how our code is interpreted and executed by the JavaScript interpreter.
During run time, javascript code is interpreted in a minimum of 2 cycles:
- 1st run: the interpreter goes through the code line by line while looking only for functions or variable declarations. Wherever it encounters a declaration, it moves it to the top.
- 2nd run: the interpreter starts compiling the code from the previous run. i.e. assigning values, executing function calls, reassignment of values, etc.
---
# Function Returning

If a function doesn’t have a return keyword, it will return undefined by default. The exception to this is an arrow function using the concise body syntax.

```js
function undefinedReturn1() {}
function explicitReturn1() { return "hello";}
const undefinedReturn2 = () => {};
const implicitReturn = () => "hello";
const explicitReturn2 = () => { return "hello";}

console.log(undefinedReturn1());  // undefined
console.log(explicitReturn1());   // hello
console.log(undefinedReturn2());  // undefined
console.log(implicitReturn());    // hello
console.log(explicitReturn2());   // hello
```
