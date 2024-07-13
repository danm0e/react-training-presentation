
### Declaring function types
```js
type myFunction = (arg: string, arg2: number) => string;
type myType = {
  func: (arg: string) => void;
};

function doesSomething(arg: number, callback: (arg: number) => void): void {
  // do something...
  callback(arg);
}
```
Note:
The type signature of a function specifies the types of the parameters that a function accepts and the type of the value that it returns.
Common use cases for this are functions in object literals and callbacks in other functions.
---
### Function
```js
function add(a: number, b: number): number {
  return a + b;
}

let addFunction: Function = add
let addFunction2: (...args: any[]) => any = add
```
Note: The Function type represents the type of all function values. It is a very general type that doesn't provide any information about the function's parameters or return type. 
Effectively it is shorthand for (...args: any[]) => anyAvoid using it!
---
### Function Signatures
```js
function greeting(name: string = "Lisa"): string {
  return "hello " + name;
}
// named function
function greeting(name: string): string {
  return "hello " + name;
}

// function expression
const greeting = function (name: string): string {
  return "hello " + name;
};

// arrow function expression
const greeting = (name: string): string => {
  return "hello " + name;
};

// shorthand arrow function expression
const greeting = (name: string): string => "hello" + name;

// function constructor - don't do this!
const greeting = new Function("name", 'return "hello " + name');

```
Note: A function signature is the pattern the function expects you to implement, its inputs and outputs.
The function signature of the below example is:
Expects a single parameter
If no parameter is passed, the assumed default value for the name is Lisa
Returns a string
---
# Question
What is the difference between the different types of declaration?
