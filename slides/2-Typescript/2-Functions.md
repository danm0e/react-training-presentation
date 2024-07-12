
Practical Functional Typescript
2

2 - Practical Functional TypeScript
Function basics: Understanding the basics about functions
Advanced function arguments: Using rest and spread to write cleaner, simpler functions.
Passing by reference & value: How functions interact with in memory variables.
Understanding Functional Scope: Functions and how they access parent scope.

Function Type
2.0

2.0 - Function Type
Declaring function types
The type signature of a function specifies the types of the parameters that a function accepts and the type of the value that it returns.
Common use cases for this are functions in object literals and callbacks in other functions.
type myFunction = (arg: string, arg2: number) => string;
type myType = {
  func: (arg: string) => void;
};

function doesSomething(arg: number, callback: (arg: number) => void): void {
  // do something...
  callback(arg);
}

2.0 - Function Type
Function
The Function type represents the type of all function values. It is a very general type that doesn't provide any information about the function's parameters or return type. 
Effectively it is shorthand for (...args: any[]) => anyAvoid using it!
function add(a: number, b: number): number {
  return a + b;
}

let addFunction: Function = add
let addFunction2: (...args: any[]) => any = add

Function Basics
2.1

2.1 - Function Basics
Function characteristics
A function is the encapsulation of behaviours. Here are some of the characteristics of functions in Typescript:
Functions can take an infinite number of arguments
A function implicitly returns undefined
A function is a first-class object
A function is an object, with behaviour



2.1 - Function Basics
Function Signatures
A function signature is the pattern the function expects you to implement, its inputs and outputs.
The function signature of the below example is:
Expects a single parameter
If no parameter is passed, the assumed default value for the name is Lisa
Returns a string

function greeting(name: string = "Lisa"): string {
  return "hello " + name;
}

2.1 - Function Basics
Function declaration


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


Question
What is the difference between the different types of declaration?
Hoisting: Named functions are hoisted to the top of their scope (either the global scope or the function scope), while function expressions are not hoisted. This means you can call a named function before it is defined in the code, but you cannot do the same with function expressions.

Name and Self-Reference: Named functions have a name that can be used for recursion or debugging purposes. Function expressions can also have a name (named function expressions), but this name is primarily used for debugging and cannot be used for recursion or self-reference within the function.

2.1 - Function Basics
Hoisting
Hoisting in JS/TS refers to the process whereby the interpreter appears to move the declaration of functions to the top of their scope, prior to execution of the code.
Hoisting allows functions to be safely used in code before they are declared.
Variables are also hoisted, but only their declarations. They are not initialized with any value, except for var which gets initialized with undefined.. Additionally, an exception will be thrown if a variable (or function) declared with let or const is read before it is initialized.


2.1 - Function Basics
Hoisting
The example on the left below gets hoisted to behave like the example on the right.
Additionally, an error will be thrown:
Block-scoped variable 'funcExp' used before its declaration.
funcDec()
funcExp()

function funcDec() {
  console.log("declaration");
}

const funcExp = () => {
  console.log("expression")
};
function funcDec() {
  console.log("declaration");
}

funcDec()
funcExp()

const funcExp = () => {
  console.log("expression")
};

2.1 - Function Basics
Hoisting
Hoisting happens because of how our code is interpreted and executed by the JavaScript interpreter.
During run time, javascript code is interpreted in a minimum of 2 cycles:
1st run: the interpreter goes through the code line by line while looking only for functions or variable declarations. Wherever it encounters a declaration, it moves it to the top.
2nd run: the interpreter starts compiling the code from the previous run. i.e. assigning values, executing function calls, reassignment of values, etc.

2.1 - Function Basics
Function Returning
If a function doesn’t have a return keyword, it will return undefined by default. The exception to this is an arrow function using the concise body syntax.

function undefinedReturn1() {}
function explicitReturn1() { return "hello";}
const undefinedReturn2 = () => {};
const implicitReturn = () => "hello";
const explicitReturn2 = () => { return "hello";}

undefinedReturn1();  // undefined
explicitReturn1();   // hello
undefinedReturn2();  // undefined
implicitReturn();    // hello
explicitReturn2();   // hello

Advanced Function Arguments
2.2

2.2 - Advanced Function Arguments
There are a few things that we can use with function arguments that can help us write more readable code and help us avoid some error scenarios. These are:
Default parameters
Optional parameters
Rest parameters
Spread operator
Destructuring

2.2 - Advanced Function Arguments
Default parameters
By default with Typescript function parameters must always be provided, however it is often useful to set a default value. With default parameters we can do this and also infer the type.
In the below example, we set the default value of b to 1 so we’ll have a value returned if only one argument is passed.

const multiply = (a: number, b = 2) => a * b;

multiply(5, 2);
// 10

multiply(5);
// 5

multiply(5, undefined);
// 5

2.2 - Advanced Function Arguments
Optional parameters
The optional operator allows parameters to be optionally provided as arguments when calling the function.
In the below example, we set the argument b as optional so where it is not provided, it will undefined (and falsey!)

function greetUser(name: string, greeting?: string): string {
  // If a greeting is provided, use it. 
  // Otherwise, use the default greeting.
  const greetingMessage = greeting ? greeting : "Hello";

  return `${greetingMessage}, ${name}!`;
}

2.2 - Advanced Function Arguments
Rest parameters
The rest operator allows you to define the last parameter of a function definition to be an array containing any remaining arguments. This means that a function can accept an indefinite number of arguments.
In the below example the function takes any number of arguments of type number and sums them together. Note the array type of the parameter.

function sumNumbers(...numbers: number[]): number {
  let sum = 0;
  for (const num of numbers) {
    sum += num;
  }
  return sum;
}

2.2 - Advanced Function Arguments
Spread operator
The spread operator allows iterable objects (such as arrays or strings) to be expanded or updated where zero or more arguments or elements are expected.
In the below example, we have a function that returns a set of options. There is a default set of options and the user can provide a set with their own values. We use the spread operator to merge these together.
const getOptions = (params) => {
 const defaultOptions = { color: "red", height: 10 };
 return { ...defaultOptions, ...params};
};

console.log(getOptions({ color: "blue", width: 5 }));
// { color: "blue", height: 10, width: 5 }

2.2 - Advanced Function Arguments
Spread operator
The spread operator only creates a new copy of the top level object - a shallow copy. Any nested objects still reference the original object and will be impacted by modifications
In the example below, we create an object with a nested object within it. We then use the spread operator to copy this into a new object. When we modify the nested object within objB, it also modifies the object within objA as well. This behaviour can cause unexpected issues.
const obj1 = { a: 1, b: { c: 2 } };
const obj2 = { ...obj1 };
obj2.b.c = 3;
console.log(obj1); // Output: { a: 1, b: { c: 3 } }
console.log(obj2); // Output: { a: 1, b: { c: 3 } }

2.2 - Advanced Function Arguments
Destructuring
Destructuring allows us to unpack values from arrays or objects into distinct variables. In the context of function arguments, this is useful as we can have a variable scoped to our function and not have to traverse the object or array.

const addFirstTwo = ([a, b]: number[]) => a + b;
console.log(addFirstTwo([35, 7, 999999]));
// 42

type Car = { make: string; model: string; color: string };
const getCar = ({ make, model }: Car) => `${make} ${model}`;

console.log(
  getCar({
    make: "Ford",
    model: "Mustang",
    color: "Blue",
  })
);
// Ford Mustang

2.2 - Advanced Function Arguments
Destructuring
We can destructure within objects, to save us having to traverse deeper into the object. We can also rename variables.
type Person = {
  name: string;
  age: number;
  address: {
    street: string;
    city: string;
  };
};

function display Person({ name, age, address: { city: location } }: Person) {
  console.log(`Name: ${name} Age: ${age} City: ${location}`);
}

displayPerson({
  name: "Gareth",
  age: 44,
  address: { street: "Forest Road", city: "Big City" },
});

// Name: Gareth Age: 44 City: Big City

Passing by reference & value
2.3

2.3 - Passing by reference & value
What’s the difference?
Pass by reference is when a reference to an original object in memory is given to a function.
Pass by value is when a value is passed to a function as a copy, not as a pointer to the original in memory value.It’s important to know when something is created in memory vs when we’re acting on a reference as mutating an object that is passed by reference may impact other areas of your code and introduce bugs.

Javascript is a bit confusing in this regard - technically everything is passed as a value, but some values might be references. A little confusing!

2.3 - Passing by reference & value
Passing by reference
In the example below, we can see that the change that the function makes to the object impacts the original object too. This is because the value that is passed is a reference.
const updateAge = (person: Person) => {
  person.age = person.age + 1;
  return person;
};

const sandra: Person = { name: "sandra", age: 22 };
const updatedSandra = updateAge(sandra);

console.log(sandra);
console.log(updatedSandra);
// { name: "sandra", age: 23 }

2.3 - Passing by reference & value
Passing by value
In this example, we can see that the original string and the output from the function are different. This is because it has been passed by value.
const reverseString = (str: string) => {
  str = str.split("").reverse().join("");
  return str;
};

const input = "hello";
console.log(reverseString(input));
// olleh

console.log(input);
// hello

Understanding Functional Scope
2.4

2.4 - Understanding Functional Scope
Closures
A closure is the combination of a function bundled together with references to its surrounding state. In other words, a closure gives you access to an outer function's scope from an inner function. In JavaScript, closures are created every time a function is created, at function creation time.
This can allow us to create private/inaccessible scope, or allow us to have functions with some parameters pre-set.
function outerFunction(outerParam: string): () => string {
  const outerVar = 'Hello, ';

  function innerFunction(): string {
    return outerVar + outerParam;
  }

  return innerFunction;
}

const greetingFunction = outerFunction('World!');
console.log(greetingFunction()); 
// Output: Hello, World!

2.4 - Understanding Functional Scope
Advanced closure example 
As a function stores its closure when it’s created, we can do things like the following:
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

Dynamic Scoping
2.5

2.5 - Dynamic Scoping
this
this in Javascript is dynamic scoping.
Dynamic scoping is code that can be understood only when the code runs, not when it is written.
Lexical scope is the scope we can see whereas dynamic scope might change, dependent on how a function is executed.
Dynamic scoping creates impurity in our code as our function acts on data (objects) outside of its own scope.


2.5 - Dynamic Scoping
this
Every function within JavaScript has a value of this
You can either tell JavaScript what you want a value of this to be explicitly, or you can leave it up to JavaScript to try and work out what you wanted it to do.
this can be set implicitly, or you can set it explicitly by invoking the function with one of either: call, apply or bind.
This means, in total that there are 4 ways to set the value of this.



2.5 - Dynamic Scoping
Implicit binding
If you call a call a function without having explicitly set this, it will be automatically given a value. This value is assigned to the object that the function is called on.
If the function is not part of an object, this will be set to the global object. However if the function is part of an object (e.g as part of a class or prototype), this will be the object that the function is part of.

function whatIsThis() {
 return this;
}
const contextualWrapper = { whatIsThis };

console.log(whatIsThis());
// global { global: global, clearInterval: ƒ, … }

console.log(contextualWrapper.whatIsThis());
// { whatIsThis: ƒ }
In typescript, you may find that `this` isn’t actually the global object, it may be undefined.

2.5 - Dynamic Scoping
Explicit binding
We can use call, apply or bind to explicitly set the value of this.
call and apply will both execute a function, the key difference between them is that call accepts a list of arguments specified individually,  whereas apply accepts them as an array.
bind returns a function with a scope and any arguments bound to it that then needs to be called.


2.5 - Dynamic Scoping
Explicit binding
const argA = "Hello";
const argB = "World";

function whatIsThis(a, b) {
 return this;
}

console.log(whatIsThis.call({ hello: true }, argA, argB));
// { hello: true }

console.log(whatIsThis.apply({ hello: true }, [argA, argB]));
// { hello: true }

const boundWhatIsThis = whatIsThis.bind({ hello: true }, argA)
console.log(boundWhatIsThis(argB));
// { hello: true }
Call and apply are very similar,

Apply just needs the parameters passed as an array

Bind creates a new version of that function with this already bound

Question
When do need to bind this explicitly?

Functional Methods
2.6

2.6 - Functional Methods
Collection functional methods
Functional methods allow us to write code where inputs aren’t mutated. This is useful in cases where we pass a collection to a function and want to do things with that collection without changing the original collection.
There are 3 main functional methods on collections in JavaScript:
.map
.filter
.reduce

2.6 - Functional Methods
map
The map method iterates over all of the items in a collection and runs a function on them and then returns a new collection with the results.
This is useful for things like manipulating a set of data into a format that you need, or doing repeated calculations.



const numbers = [1, 2, 3];

const tripledNumbers = numbers.map((number) => {
 return number * 3;
});

console.log(numbers)
// [ 1, 2, 3 ]
console.log(tripledNumbers)
// [ 3, 6, 9 ]

2.6 - Functional Methods
filter
The filter method iterates over all of the items in a collection and runs a function on them to decide whether or not that item should be included in the returned collection. 



const numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];

const evenNumbers = numbers.filter((number) => {
  return number % 2 === 0;
});

console.log(numbers);
// [ 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 ]
console.log(evenNumbers);
// [ 2, 4, 6, 8, 10 ]

2.6 - Functional Methods
reduce
The reduce method runs a function on each element in the collection, passing it the result from running the function on the previous element. The final result is a single value



const numbers = [10, 2, 73, 1, 0, 19, 210, 3, 47, 18];

const highestNumber = numbers.reduce((previous, current) => {
  if (current > previous) {
    return current;
  }
  return previous;
}, 0);

console.log(highestNumber);
// 210

Break
☕️
