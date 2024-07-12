
# Typescript
---
### Agenda
- Types: What goes on top of what we've learnt?
- Objects & Arrays: Creating, managing and structuring your data objects.
- Truthy/Fasley Values: What resolves to true and what resolves to false
- Errors & Throwing: How and when to create, throw and handle errors.
---
In this file, you’ll see all the instructions for what you need to implement. Add your code and run the jest command to have it run the tests.

The Basics
1
Look at Javascript and Typescript chapters and merge into the best of both

1 - The Basics
Variables: How do we declare values?
Types: What are types and why do we care?
Objects, Arrays, Tuples & Enums: Creating, managing and structuring your data objects.
Truthy/Falsey Values: What resolves to true and what resolves to false
Errors & Throwing: How and when to create, throw and handle errors.
In this section we’ll be covering:
Variables - declaration, reassignment
Types, what they are and why we care
Objects and arrays
What resolves to true and false
Creating, throwing and handling errors

Variables
1.0

1.0 - Variables
Variable declarations
In Typescript, there are 3 ways to declare a variable, each with their own differences.
These are:
var
let
const

1.0 - Variables
Difference: Scoping
The first difference between the 3 declarations is scoping.
var has function scope, meaning that any variable declarations using it are scoped to within the function that is currently executing.
let and const are block scoped, meaning that declarations are scoped to the block that they are in.

1.0 - Variables
Difference: Scoping
Here is an example of function and block scope:
var _var = 1;
let _let = 2;
const _const = 3;

if (true) {
  var _var = 4;
  let _let = 5;
  const _const = 6;
  console.log("Block scope: ", _var, _let, _const);
}

console.log("Function scope: ", _var, _let, _const);

// Block scope:  4 5 6
// Function scope:  4 2 3

1.0 - Variables
Difference: Immutability
A var and a let value can be reassigned.
A const cannot. If you attempt to overwrite it, an error will be thrown.
const NAME: string = "Louis";
let age: number = 12;

age = age + 1
NAME = "Harold" // Cannot reassign to 'NAME' because it is a constant.

1.0 - Variables
Difference: Immutability
Whilst you cannot update the value of a const itself, you can update the properties of an array or object assigned to a const.
const NAMES = ["Mo", "Jo"];
NAMES.push("JoJo");

console.log(NAMES);

> [ 'Mo', 'Jo', 'JoJo' ]

1.0 - Variables
Difference: Declaration
You can redeclare a var, but not a let or const

Example

examples/variables.ipynb


Types
1.1
Right, lets really jump in
Types are metadata for values, in that types tell us something about the value we’re operating on.
This is one of the defining traits of typescript and how it differs from standard JS

1.1 - Types	
Primitive Values
A primitive is basically anything that’s not an object. These all exist in standard Javascript.The following are not objects (and therefore don’t have properties / methods).
boolean for true/false.
number for numbers of any kind: integer or floating-point.
string for strings.
null for the absence of a value.
undefined for unassigned values.
bigInt for large numbers.
symbol for unique identifiers.

In most normal usage you won’t come across bigint or symbols.



1.1 - Types
Special types
Typescript also has some unique types.
any - makes a value behave like it would in regular Javascript. It is the default when you, or typescript, don’t assign a type. Avoid!
unknown - when you really don’t know what a type could be. You should refine the type before using the value
void - the return type of a function that returns nothing or has no return statement
never - the return type of a function that never returns



1.1 - Types
object type
Apart from primitives, the most common sort of type we work with are objects. This refers to any value with properties, which is almost all of them! 
Examples of built-in objects are:
Function
Error
Promise
Date
More on objects later - it is a bit more complex than this!
In JavaScript an object is a collection of properties.
Values can be of any type, including other objects, meaning complex data structures can be built
Examples are:
Function
Error
Promise
Date

1.1 - Types
The typeof operator
We can use the typeof operator to tell the difference between data types. This allows us to implement error handling and/or different behaviour dependent on type.

const myFunction = (value: unknown) => {
  if (typeof value != "string") {
    console.log("No, strings only!");
  } else {
    console.log("We good, we good");
  }
};

myFunction("Hey");
> We good, we good

myFunction(0);
> No, strings only!
Using the typeof operator, we can tell the difference between data types
We can use this to handle errors or different behaviour for different types
Example prints message on strings, different message on anything else.


1.1 - Types
typeof discrepancies
Unfortunately, typeof might not always return what you expect
console.log(typeof []);
> object

console.log(typeof null);
> object

console.log(typeof Number);
> function

console.log(typeof new Number(0));
> object

console.log(typeof NaN);
> number
Sometimes typeof might not return what you expect

Here are a few examples

Typeof null is an object for legacy reasons

Question
typeof doesn’t always behave how you might expect! 

What do these return?



 


typeof []
typeof {}
typeof null
typeof undefined
typeof 'test'
typeof true
typeof 0
typeof Number
typeof new Number(0)
If you like, play along with these examples

typeof null is actually a bug!

value === null

This is the preferred way of checking a value is null

Question
Why does typeof [] return object?

How do we type check an array then?
Question:
Why does typeof [] return object?

How do we type check an array then?

Answer:
Arrays are a child of the object prototype, but with methods overwritten.

We can use Array.isArray() to check if something is an array.

1.1 - Types	
Type differences
Types are important when it comes to operators.
console.log('1' + '1');
> 11

console.log('1' + 1);
> 11

console.log(1 + 1);
> 2
Types are important when we’re trying to do things with values
Adding a string of 1 to a string of 1 joins them together and gives us 11
Similarly, adding a string of 1 and the number 1 also joins them together
But adding 1 and 1 as numbers gives us 2, as we’d expect

1.1 - Types
Type coercion
As mentioned earlier, primitives have no properties or methods, but somehow "myString".toUppercase() exists?!
This is because the primitive gets wrapped in a String object temporarily.

let str = 'hello';
let upper = str.toUpperCase();
console.log(upper);
> HELLO
let str = 'hello';
let upper = (new String(str)).toUpperCase();
console.log(upper);
> HELLO
Mentioned earlier that primitives have no properties or methods, but .length returns a value

This is because the primitive gets wrapped in a String object temporarily

These 2 snippets are equivalent, just the second one explicitly creates the String object.

1.1 - Types
Type coercion
"1" + 1 returns 11. This is also down to type coercion.
JavaScript engines will try calling the toString and valueOf methods to attempt to get a primitive. In this case, the engine prefers to coerce the number into a string.
If no primitive can be found, an error will be thrown.
Also mentioned earlier that a string of 1 and the number 1 returns a string of 11

This is also because of type coercion.

Engines will call the toString and valueOf methods to try and get a primitive to work with.

In this case, it can be coerced to a string.

1.1 - Types
Type annotation & aliases
Type annotation is a way to explicitly specify the type of a variable, parameter, or return value.
Type aliases allow you to create a new name for a type, making complex types more readable and reusable.
We’ve talked about different types of types and how they behave in some circumstances, how do we actually say something is a type?

1.1 - Types
Type annotation
Typescript can infer types where they are not explicitly specified. 
let secondName: string;
// typeof string

function toLowercase(input: string) {}

const firstName = "Bill";
// typeof string

1.1 - Types
Type aliases
Types can be declared in isolation. This is useful for documentation and when to make aliases for a specific shapes or structures.
type Friends = string[]
// string array (alias)

type House = string | number
// union


type Location = {
    x: number;
    y: number;
}
// object literal

1.1 - Types
Union & Intersection
The union of two types is everything in one, the other, or both.The intersection is everything in both types.
type Cat = { name: string; purrs: boolean };
type Dog = { name: string; barks: boolean; wags: boolean };
type CatOrDogOrBoth = Cat | Dog;
type CatAndDog = Cat & Dog;

let dog: CatOrDogOrBoth = {
  name: "pooch",
  barks: true,
  purrs: true,
};

let dogcat: CatAndDog = {
  name: "pooch",
  barks: true,
  purrs: true,
  wags: true,
};

1.1 - Types
Pick & Partial
The union of two types is everything in one, the other, or both.The intersection is everything in both types.
type Cat = { name: string; purrs: boolean };
type Dog = { name: string; barks: boolean; wags: boolean };
type CatOrDogOrBoth = Cat | Dog;
type CatAndDog = Cat & Dog;

let animal: CatOrDogOrBoth = {
  name: "pooch",
  barks: true,
  purrs: true,
};

let animal2: CatAndDog = {
  name: "pooch",
  barks: true,
  purrs: true,
  wags: true,
};

1.1 - Types
Type casting
Type casting is the process of explicitly changing the type of a variable from one type to another. Type casting is useful when working with dynamic data or when integrating with JavaScript libraries that don't provide type information. 

// We have a variable of type unknown
let userInput: unknown = “123”;

// We want to treat userInput as a string
let userInputString = userInput as string;
Typically you’ll only be doing this with unknown types, or as we say here, when working with untyped JS libraries. You may use a type alias and then cast to that type.

1.1 - Types
Type generics
A quick note on type generic syntax. 

function identity<Type>(arg: Type): Type {
  return arg;
}

let output = identity<string>("myString");
// pass type as argument to function with <>

let output = identity("myString");
// let typescript use type argument inference
We won’t go into any depth on this but I’ll introduce the idea of type generics. Sometimes you want a function, or class, to be flexible on the type it works with without using any, unknown, or a large union type.

Just know that when you see this syntax you are looking at a generic!Don’t worry about this for now!

1.1 - Types
Type safety
All of this adds up to give us Type safety.
That is, we use types to prevent programs from doing invalid things.
Javascript on its own attempts to make the best of invalid situations which can lead to unexpected outcomes, Typescript helps avoid that.


Example

Let's have a look at some examples of type safety.



 



Break
☕️

Objects, Arrays, Tuples & Enums
1.2	

1.2 - Objects, Arrays, Tuples & Enums
Our main types for representing data in JavaScript are Object, Array, Tuple, and Enum
Objects are used to represent a collection of key-value pairs and do not guarantee any specific order for their properties.
Arrays store a collection of values in a specific order.
Tuples are similar to arrays. They maintain the order of their elements but their length and types of elements are fixed and predefined. 
Enums are way of defining a set of named constants. They allow us to create a collection of related values represented by a specific name.

1.2 - Objects, Arrays, Tuples & Enums

Objects
Object types can be declared in a few different ways in Typescript.

let obj: { a: string };

let obj: {};

let obj: object;

let obj: Object;
There are some different ways of saying what type an object will be in Typescript.

A couple of these we should always try to avoid.

1.2 - Objects, Arrays, Tuples & Enums

object and Object
object is used where we just want an object and don’t care what fields it has. 
Object is effectively the same as {} (empty object notation) and should be avoided.

1.2 - Objects, Arrays, Tuples & Enums

Object literal notation
Also known as a shape. Used when you know which fields an object could have. 

let obj: {
  a: number;
  b?: string;
  readonly c: string;
  [key: number]: boolean;
};

let obj: {} // Don’t do this!

1.2 - Objects, Arrays, Tuples & Enums

Index Signatures
This lets you tell Typescript that a given object might have more keys.
You could also use Record to create an object with key:value pairs of strings. Why might you not want to do that, though?

type Booking = {
  [seatNumber: string]: string;
};
type Booking = Record<string, string>;

let trainSeatBookings: Booking = {
  "32A": "Peter Parker",
  "34E": "Carol Danvers",
};

1.2 - Objects, Arrays, Tuples & Enums

Objects
To access and set properties in an Object, we can use dot notation or bracketed notation

let assignToMe: { [key: string]: string };
// allow assignment of any property

assignToMe.name = "I'm a dot assignment";
assignToMe["name" + 1] = "I'm a bracket assignment";

console.log(assignToMe);
> {
    name: "I'm a dot assignment",
    name1: "I'm a bracket assignment"
  }
We can use either dots or brackets to access and set properties in an object
Brackets are especially useful if you want use a variable or something computed as a key

As mentioned in the last section, Arrays are actually implemented as types of object. The main difference is that Arrays ensure their order.
Generally you’d access an Array using the bracketed notation.
const horses = ["Clydesdale", "Shire", "Unicorn"];

console.log(horses[1]);
> Shire

console.log(horses[2]);
> Unicorn
1.2 - Objects, Arrays, Tuples & Enums

Arrays
Generally we use bracketed notation to access an array, and an array’s numbering starts from zero

You can see this in the example

Bonus fact: the national animal of Scotland is the Unicorn. True fact

Tuples act similarly to arrays but their length and types of elements are fixed and predefined. 
Generally you would use bracket notation to access them, like arrays.


Generally you’d access an Array using the bracketed notation.
const coordinates: [number, number] = [23, 48];

console.log(coordinates[0]);
> 23

console.log(coordinates[1]);
> 48
1.2 - Objects, Arrays, Tuples & Enums

Tuples
Generally we use bracketed notation to access an tuples too, and indexing starts from 0 like arrays

You can see this in the example

Tuples offer some advantages over objects, They can offer improved performance. You might like to define a tuple as readonly, too. This would prevent adding and redf

Similar to an object, enums have named properties and associated values. However, unlike an object, the values cannot be changed. 
You can access values using dot or bracket notation. Typically dot notation is used.


Generally you’d access an Array using the bracketed notation.
enum Direction {
  Up = "UP",
  Down = "DOWN",
  Left = "LEFT",
  Right = "RIGHT",
}

Direction.Down;
> DOWN

Direction["Up"];
> UP
1.2 - Objects, Arrays, Tuples & Enums

Enums
Generally we use dot notation to access enum values.

They offer improved readability for related constants. Often uses to represent a set of fixed options or choices, like directions.

Very nice for usage with switching logic. E.g. switch statements!


Truthy / Falsey Values
1.3	

1.3 - Truthy / Falsey  Values
Truthy & Falsey


Truthy and falsey refer to whether or not a value can be converted to true or false. If a value can be converted to true, it is truthy and if a value can be converted to false, it is falsey.
In JavaScript, all values are truthy unless they are falsey. The values that are considered falsey are the following:
false
0
-0
0n
null
undefined
NaN
“”


1.3 - Truthy / Falsey Values
The !! operator
In JavaScript, ! is a logical NOT operator. When it’s used with a non-boolean value, the value is converted to a boolean using the principles mentioned in the previous slide and then returns the inverse of that.
For example as 1 is truthy, !1 is false.
But if we use two logical NOT operators (!!), we can explicitly force the value to be converted to a boolean based on the truthyness or falseyness of the value.

console.log(!!1);
> true

console.log(!!0);
> false

Question
What do you think the truthyness of these are?


!!{}
!![]
!!'true'
!!'false'
!!'0'
!!1
!!new Boolean(false)
!!false
!!undefined
!!-1
!!null
!!''
!!0

Question
What is the difference between == and ===?

Which should you use?
0 == '0'
0 === '0'
Question
What is the difference between double equals and triple equals?
Which should you use?

Answer
Double equals is looser about type checking
You should almost always use triple equals to ensure strict equality. Explicitly convert the types if necessary.

1.3 - Truthy / Falsey Values
Loose & Strict Equality
We can use both == and === for comparisons, however == will perform type coercion on the values. This means that if the two values are of a different type but the same value, the comparison will return true.
To avoid this, we can use  === and the comparison will return false if the types are different.
console.log("1" == 1);
> true

console.log("1" === 1);
> false

Break
☕️

Errors & Throwing
1.4

1.4 - Errors & Throwing
Errors
An error is where a computer program has reached a state of execution that is unexpected and the resolution is not explicitly known.
Which is why we have errors, and error handling.
You should try and handle all errors in your code, throw an explicit error for all errors you might “expect”.
What type is an Error?

1.4 - Errors & Throwing
Error Objects
The Error object is one of the built-in objects in JavaScript.
Any runtime errors in your code will cause an Error object to be created and thrown by the JavaScript engine.
We can also create our own Error objects
const result = new Error("Oops!");

console.log(result);
> Error: Oops!

1.4 - Errors & Throwing
Throwing
By using the throw keyword, we can halt the current execution when an error occurs. It then traverses up the call stack to the nearest try/catch block.
throw accepts an argument, which can be of any type, and this is passed to the catch block.
It’s preferred to use the built-in error object for consistency.
try {
 throw "Just a string...";
} catch (e) {
 console.log(e);
}
> Error: Just a string...

Question
How can we only catch some errors?


What if you know a certain condition could throw a particular error - how might you go about catching just that error?

You can’t, you have to catch all and then rethrow



What have we learnt?

Types and how to use them
(Nearly) Everything is an object
What makes something true
Errors and how to handle them
Variables and their scope

Exercise Implement a test assertion library
Implement a jest inspired API assertion library.

Add your code to: exercises/assert.ts

Run this to have the tests run as you save:
npm run exercise::assert
Now we have our first exercise, we’re going to implement an assertion library inspired by jest

In this file, you’ll see all the instructions for what you need to implement. Add your code and run the jest command to have it run the tests.

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

Object Oriented Typescript
3

3 - Object Oriented TypeScript
Using Objects As Modules: Design patterns and pseudo-private variables
ES6 Modules: A modern approach to modules
Classes: Fancy objects
Interfaces: Defining the shape of an object or class


Using Objects As Modules
3.1

3.1 - Using Objects As Modules
Modules
A module is simply a way of organizing code and using them can be helpful for grouping together related code.
You can utilise the various module systems such as native modules and node modules. But you can also create them in your code using objects.

3.1 - Using Objects As Modules
Basic module
A basic module is just an object with properties applied. These properties can be functions or other types and they can be accessed both within the module and outside of the module.

const databaseSeed = {
  patchQuery: "INSERT into USERS ...",
  init: function () {
    return this.runQuery(this.patchQuery);
  },
  runQuery(query: string) {
    return `Running query: ${query}`;
  },
};

console.log(databaseSeed.init());
console.log(databaseSeed.patchQuery);

3.1 - Using Objects As Modules
Revealing module pattern
A common pattern in basic modules is the revealing module pattern. This is where you use a function call to return an object that contains only some of the methods and properties used by the module, so you can have pseudo-private methods and properties.
const databaseSeed = function () {
  const patchQuery = "INSERT into USERS ...";
  const init = () => runQuery(patchQuery);
  const runQuery = (query: string) => `Running: ${query}`;
  return {
    init,
    runQuery,
  };
};

console.log(databaseSeed().init());
console.log(databaseSeed().patchQuery);
// Property 'patchQuery' does not exist on type....

ES6 Modules
3.2

3.2 - ES6 Modules
ES6 modules
ES6 modules are similar to objects as modules but offer some advantages.
// databaseSeed.ts
const patchQuery = "INSERT into USERS ...";

const init = () => {
  return runQuery(patchQuery);
};

const runQuery = (query) => {
  return `Running query: ${query}`;
};

export { patchQuery, init, runQuery };

// app.ts (for TypeScript)
import { patchQuery, init, runQuery } from './databaseSeed';

console.log(patchQuery);
console.log(init());
console.log(runQuery('SELECT * FROM USERS'));

3.2 - ES6 Modules
Why use ES6 modules?
ES6 modules are natively supported in modern browsers and Node.js environments, providing great tooling integration and performance
Explicit dependencies make it easier to manage and reason about module dependencies.
They provide encapsulation by default, as variables and functions are private to the module unless explicitly exported.

Classes
3.3

3.3 - Classes
Classes vs objects
A class is a clearer way of defining an object with a constructor
const person = (firstName: string, surname: string) => {
  const fullName = `${firstName} ${surname}`;

  const greeting = () => {
    console.log(`Hello, ${fullName}!`);
  };

  return {
    fullName,
    greeting,
  };
};

3.3 - Classes
Classes vs objects
A class is a clearer way of defining an object with a constructor
class Person {
  fullName: string;

  constructor(firstName: string, surname: string) {
    this.fullName = `${firstName} ${surname}`;
  }

  greeting() {
    console.log(`Hello, ${this.fullName}!`);
  }
}
Start with class

Define some properties

Define a constructor

In the constructor assign the instance properties

That is what this is

Define some 

3.4 - Classes
Static methods
As we have already talked about, a function is an object in JavaScript. Because a function is an object it can have properties and if we assign functions to these properties, they become the function’s “static” methods.
They’re called static methods, because you don’t have to create a new instance of the object like a prototype method. An example of a static method on one of the built-in objects is Array.isArray().
When writing code with constructors, defining static methods can make our code cluttered, but when we’re writing code with classes, it becomes much cleaner.



Static Members
3.4

3.4 - Static Members
static
A static member is a method or property that is defined on the class itself, rather than on instances of the class. 

class Circle {
  static pi: number = 3.14;

  static calculateArea(radius: number) {
    return this.pi * radius * radius;
  }
}

Circle.pi; // 3.14
Circle.calculateArea(3); // 28.26
Accessibility: Static methods can be called directly on the class itself, without creating an instance of the class. For example, MyClass.staticMethod().

Instance Independence: Static methods do not have access to instance properties or methods. They can only access and operate on static properties and methods of the class.

Inheritance: Static methods are inherited by subclasses, but they are not overridden. If a subclass defines a static method with the same name as a static method in the parent class, the subclass method will hide the parent class method for that subclass.

Use Cases: Static methods are commonly used for utility or helper functions that operate on data without requiring an instance of the class. They are also used for creating instances of the class (factory methods) or for providing functionality related to the class itself, rather than its instances.

3.4 - Static Members
readonly
You might also pair static with readonly.

class Circle {
  static readonly pi: number = 3.14;

  static calculateArea(radius: number) {
    return this.pi * radius * radius;
  }
}

Circle.pi = 314; 
// Cannot assign to 'pi' because it is a read-only property.

Accessibility: Static methods can be called directly on the class itself, without creating an instance of the class. For example, MyClass.staticMethod().

Instance Independence: Static methods do not have access to instance properties or methods. They can only access and operate on static properties and methods of the class.

Inheritance: Static methods are inherited by subclasses, but they are not overridden. If a subclass defines a static method with the same name as a static method in the parent class, the subclass method will hide the parent class method for that subclass.

Use Cases: Static methods are commonly used for utility or helper functions that operate on data without requiring an instance of the class. They are also used for creating instances of the class (factory methods) or for providing functionality related to the class itself, rather than its instances.

Access Modifiers
3.5

3.5 - Access Modifiers
Access modifiers
An access modifier is a keyword that specifies the accessibility or visibility of a class member (properties, methods, or constructors) from other parts of the code. Access modifiers control how and where class members can be accessed or referenced.
public - accessible from anywhere (the default)
private - only accessible in the class that defined them
protected - accessible in the class that defined then and any subclasses.

3.5 - Access Modifiers
public
class Example {
  public property: string;
  public someFunction() {}

  constructor() {
    this.property = "Example";
  }
}
// equivalent to...
class Example {
  property: string;
  someFunction() {}

  constructor() {
    this.property = "Example";
  }
}
This is the default and you don’t necessarily need to specify that something is public.

3.5 - Access Modifiers
private
class Example {
  private property: string;
  private someFunction(arg: string) {}

  constructor() {
    this.property = "Example";
  }

  anotherFunction() {
    this.someFunction(this.property);
  }
}

const myExample = new Example();

myExample.someFunction();
// Property 'someFunction' is private and only accessible within class 'Example'
Worth noting that the constructor cannot be private, that wouldn’t be very helpful!

A use case for this is some helper methods within the class that are then called by public functions

Worth noting there is some sneaky ECMA script syntax that can be used in place of private - the #

I would caution against this as it isn’t widely used and private is more explicit and marrys up to other OOO language syntax.

3.5 - Access Modifiers
protected
class Animal {
  protected name: string;

  constructor(name: string) {
    this.name = name;
  }

  protected makeSound(): void {
    console.log(`${this.name} makes a sound.`);
  }
}

class Dog extends Animal {
  bark(): void {
    this.makeSound();
    console.log(`${this.name} barks.`);
  }
}
Protected members can be accessed within the class and any sub classes.



3.4 - Classes
Automatic this assignment
class Animal {
  constructor(public name: string, public sound: string) {}

  protected makeSound(): void {
    console.log(`${this.name} ${this.sound}.`);
  }
}

Setting the access modifier in the constructor automatically assigns the parameter to this. A handy shortcut!
Protected members can be accessed within the class and any sub classes.



Getters & Setters
3.3

3.4 - Getters & Setters
get and set
Getters and Setters are special methods that allow you to control the access and manipulation of a class's properties. They offer some benefits over interacting with properties directly.
Data Validation - Validate the data being assigned to a property,
Computed Properties - Compute and return a value based on other properties or calculations.
Logging & Debugging - Log or debug the access and modification of properties.

3.4 - Getters & Setters
class Example {
  private _property: number = 1;

  get property() {
    return this._property;
  }
  set property(value: number) {
    this._property = value;
  }
}
const example = new Example();

example.property = 2;
console.log(example.property);
// 2
This is a basic example 

shows how you would use a private property that is only accessible within the class 

Then use getter and setter methods to interact with it.

In this example it is more verbose and not really worthwhile but demonstrates the syntax



3.4 - Getters & Setters
class Person {
  private _name: string;

  constructor(name: string) {
    this._name = name;
  }

  get name() {
    console.log("Getting name");
    return this._name.toUpperCase();
  }

  set name(value: string) {
    if (value.length > 20) {
      throw new Error("Name is too long");
    }
    console.log("Setting name");
    this._name = value;
  }
}
This is a more complete and realistic use case for getters and setters.

We do some logging (which could be to a logging service)

We modify the property as it is retrieved

We validate that the value fits requirements

Inheritance
3.3

3.4 - Inheritance
Inheritance is a mechanism that allows a new class to inherit properties and methods from an existing class. This gives some great advantages over many classes.
Code Reuse - Keep it DRY
Hierarchical Classification - Specialized classes can be derived from more general base classes for better organization and classification of objects.
Testability - Common functionality can be tested once in a base class then relied upon for children classes.

3.4 - Inheritance
Base Class
Here we define a base class - Animal with two public members, a property and a method.
class Animal {
  public name: string;

  constructor(name: string) {
    this.name = name;
  }

  public makeSound(): void {
    console.log(`${this.name} makes a sound.`);
  }
}

3.4 - Inheritance
Child Class
This class extends Animal.
Note the extends keyword and super() method.
class Dog extends Animal {
  public breed: string;

  constructor(name: string, breed: string) {
    super(name);	
    this.breed = breed;
  }

  public bark(): void {
    this.makeSound();
    console.log(`${this.name} barks.`);
  }
}
This class has its own property - breed

And its own method bark()

In the constructor we call super()

This calls the constructor of the parent class

In bark() we can call this.makeSound because makeSound is part of this class because it extends Animal.

This can be layered and layered.

3.4 - Inheritance
abstract Classes
Abstract classes allow defining a common class in situations you don't want to instantiate the base class itself. They provide a way to enforce behaviors or properties that derived classes must implement

abstract class Animal {
  public name: string;
  protected abstract sound: string;

  constructor(name: string) {
    this.name = name;
  }

  public abstract makeSound(): void;
}
This class has its own property - breed

And its own method bark()

In the constructor we call super()

This calls the constructor of the parent class

In bark() we can call this.makeSound because makeSound is part of this class because it extends Animal.

This can be layered and layered.

3.4 - Inheritance
Extending abstract Classes
Extending abstract classes is similar to standard classes but with the requirement of implementing abstract properties and methods. 

abstract class Animal {
  public name: string;

  constructor(name: string) {
    this.name = name;
  }

  public abstract makeSound(): void
}

class Dog extends Animal {
  public breed: string;
  protected sound: string = "barks";

  constructor(name: string, breed: string) {
    super(name);
    this.breed = breed;
  }

  public makeSound(): void {
    console.log(`${this.name} ${this.sound}.`);
  }
}
This class has its own property - breed

And its own method bark()

In the constructor we call super()

This calls the constructor of the parent class

In bark() we can call this.makeSound because makeSound is part of this class because it extends Animal.

This can be layered and layered.

Interfaces
3.5

3.5 - Interfaces
interface
An interface is a structural contract that defines the shape of an object, including its properties and methods. It serves as a blueprint or a set of rules that classes, objects, or functions must adhere to.

interface Animal {
  name: string;
  makeSound(): void;
}

3.5 - Interfaces
interface
The Dog class implements the Animal interface, ensuring that it adheres to the contract defined by the interface. It provides an implementation for the makeSound() method and includes an additional breed property.

class Dog implements Animal {
  name: string;
  breed: string;

  constructor(name: string, breed: string) {
    this.name = name;
    this.breed = breed;
  }

  makeSound(): void {
    console.log(`${this.name} barks.`);
  }
}
Optional Properties: Interfaces can define optional properties by using the ? syntax, allowing objects to have a flexible structure while still providing type safety.

Readonly Properties: Interfaces can define readonly properties using the readonly keyword, ensuring that these properties cannot be modified after an object is created.

Quite similar to types!

Interfaces are primarily used for defining the structure of object literals and classes.

Interfaces can extend other interfaces, allowing for inheritance and code reuse.

Interfaces are automatically merged when they have the same name, which can be useful for modular development.

Class Patterns
3.6

3.6 - Class Patterns
Factory Pattern
With interfaces (or types!) and classes we can use the Factory Pattern. This is a way to create objects of some type, leaving the decision of which concrete type to create to the factory.

interface Shoe {
  purpose: string;
}

class BalletFlat implements Shoe {
  purpose = "dancing";
}

class Sneaker implements Shoe {
  purpose = "running";
}

class Boot implements Shoe {
  purpose = "hiking";
}

3.6 - Class Patterns
Factory Pattern
The factory class with a static method is responsible for creating the 

class ShoeFactory {
  static createShoe(type: "ballet" | "sneaker" | "boot"): Shoe {
    switch (type) {
      case "ballet":
        return new BalletFlat();
      case "sneaker":
        return new Sneaker();
      case "boot":
        return new Boot();
    }
  }
}

const balletShoe = ShoeFactory.createShoe("ballet");
console.log(balletShoe.purpose);
// dancing
This class has its own property - breed

And its own method bark()

In the constructor we call super()

This calls the constructor of the parent class

In bark() we can call this.makeSound because makeSound is part of this class because it extends Animal.

This can be layered and layered.

3.6 - Class Patterns
Returning this
class RequestBuilder {
  private method: "get" | "post" | null = null;
  private url: string | null = null;

  public setMethod(method: "get" | "post"): this {
    this.method = method;
    return this;
  }

  public setUrl(url: string): this {
    this.url = url;
    return this;
  }
}
You can also return this and create chains of functions acting on the same object instances. 
Protected members can be accessed within the class and any sub classes.



3.6 - Class Patterns
Builder Pattern
class RequestBuilder {
  private method: "GET" | "POST" | null = null;
  private url: string | null = null;
  private data: object | null = null;

  // other methods...

  public send(): void {
    // do send
  }
}

new RequestBuilder()
  .setMethod("POST")
  .setUrl("https://example.com")
  .setData({ key: "value" })
  .send();

This is called the builder pattern. 
Protected members can be accessed within the class and any sub classes.



3.4 - Interfaces
abstract & interface
You can also combine and interface and abstract classes!

interface Animal {
  name: string;
  makeSound(): void;
}

abstract class Mammal {
  public breathesAir: boolean = true;
}
This class has its own property - breed

And its own method bark()

In the constructor we call super()

This calls the constructor of the parent class

In bark() we can call this.makeSound because makeSound is part of this class because it extends Animal.

This can be layered and layered.

3.4 - Interfaces
abstract & interface

class Dog extends Mammal implements Animal {
  name: string;

  constructor(name: string) {
    super();
    this.name = name;
  }

  makeSound(): void {
    console.log(`${this.name} barks.`);
  }
}

const dog = new Dog("Fluffy");
dog.breathesAir; // true

This class has its own property - breed

And its own method bark()

In the constructor we call super()

This calls the constructor of the parent class

In bark() we can call this.makeSound because makeSound is part of this class because it extends Animal.

This can be layered and layered.

Decorators
3.3

3.4 - Interfaces
@decorator
A decorator in TypeScript is a special kind of function that allows you to modify or extend the behavior of a class, method, property, or parameter. It is a way to add metadata or additional functionality to your code without directly modifying the original code.

class Dog implements Animal {
  name: string;
  breed: string;

  constructor(name: string, breed: string) {
    this.name = name;
    this.breed = breed;
  }

  makeSound(): void {
    console.log(`${this.name} barks.`);
  }
}
This class has its own property - breed

And its own method bark()

In the constructor we call super()

This calls the constructor of the parent class

In bark() we can call this.makeSound because makeSound is part of this class because it extends Animal.

This can be layered and layered.

Generic Types
4

4.1 - Generics
Functions
A generic type is a way to write code that can work with different types of data. Instead of writing separate code for each data type, you can write one piece of code that can handle multiple types. 

function wrapStringInArray(string: string): string[] {
  return [string];
}

function wrapNumberInArray(number: number): number[] {
  return [number];
}

//generic
function wrapValueInArray<T>(value: T): T[] {
  return [value];
}
This class has its own property - breed

And its own method bark()

In the constructor we call super()

This calls the constructor of the parent class

In bark() we can call this.makeSound because makeSound is part of this class because it extends Animal.

This can be layered and layered.

4.1 - Generics
Classes
Generics can also be used with classes!

class ValueHolder<T> {
  constructor(private _value: T) {}

  get value(): T {
    return this._value;
  }
}

const num = new ValueHolder(1);
console.log(num.value);

const str = new ValueHolder('string');
console.log(str.value);

This class has its own property - breed

And its own method bark()

In the constructor we call super()

This calls the constructor of the parent class

In bark() we can call this.makeSound because makeSound is part of this class because it extends Animal.

This can be layered and layered.

4.1 - Generics
Types
Type aliases can also use generics!

type ValueBox<T> = {
  value: T;
};

const myStringValue: ValueBox<string> = { value: "hello" };
const myNumberValue: ValueBox<number> = { value: 5 };

type ValueConverterFunction<T, U> = (value: T) => U;

const stringToNumber: ValueConverterFunction<string, number> = function (
  value
) {
  return Number(value);
};

This class has its own property - breed

And its own method bark()

In the constructor we call super()

This calls the constructor of the parent class

In bark() we can call this.makeSound because makeSound is part of this class because it extends Animal.

This can be layered and layered.

Exercise 2: Implement lodash
Re-implement some lodash methods.

Add your code to: exercises/2-functional.test.js

Run this to have the tests run as you save:
npm run exercise::functional
Now we have our first exercise, we’re going to re-implement some lodash methods.

In this file, you’ll see all the instructions for what you need to implement. Add your code and run the jest command to have it run the tests.

Exercise 3: Implement A Calculator
Implement a Calculator with an interface,  module and a Class.

Add your code to: exercises/3-objectOriented.test.js

Run this to have the tests run as you save:
npm run exercise::object-oriented
Now we have our first exercise, we’re going to re-implement some lodash methods.

In this file, you’ll see all the instructions for what you need to implement. Add your code and run the jest command to have it run the tests.

End of Day 2
🎉

Asynchronous JavaScript
4

4 - Asynchronous JavaScript
The Event Loop: Why we need async anyway, and how JS handles async.
Callbacks: Passing functions around for later execution
Promises: Understanding the promise object and using it.
Async / Await: Taking Promises one step further with async/await.

The Event Loop
4.1

4.1 - The Event Loop
JavaScript is a single threaded language, but it uses some clever data structures and a runtime model called the event loop to allow us to have asynchronous tasks.

The call stack is responsible for keeping track of all the operations in line to be executed. Whenever a new function is executed it is pushed onto the stack and when it is finished, it is popped from the stack.
4.1 - The Event Loop
The call stack
function greeting() {
 const message = sayHi();
 console.log(message);
}
function sayHi() {
 return "Hi!";
}

greeting();
Call stack

The call stack is responsible for keeping track of all the operations in line to be executed. Whenever a new function is executed it is pushed onto the stack and when it is finished, it is popped from the stack.
4.1 - The Event Loop
The call stack
function greeting() {
 const message = sayHi();
 console.log(message);
}
function sayHi() {
 return "Hi!";
}

greeting();
Call stack
Script

The call stack is responsible for keeping track of all the operations in line to be executed. Whenever a new function is executed it is pushed onto the stack and when it is finished, it is popped from the stack.
4.1 - The Event Loop
The call stack
function greeting() {
 const message = sayHi();
 console.log(message);
}
function sayHi() {
 return "Hi!";
}

greeting();
Call stack
Script

The call stack is responsible for keeping track of all the operations in line to be executed. Whenever a new function is executed it is pushed onto the stack and when it is finished, it is popped from the stack.
4.1 - The Event Loop
The call stack
function greeting() {
 const message = sayHi();
 console.log(message);
}
function sayHi() {
 return "Hi!";
}

greeting();
Call stack
Script
greeting()

The call stack is responsible for keeping track of all the operations in line to be executed. Whenever a new function is executed it is pushed onto the stack and when it is finished, it is popped from the stack.
4.1 - The Event Loop
The call stack
function greeting() {
 const message = sayHi();
 console.log(message);
}
function sayHi() {
 return "Hi!";
}

greeting();
Call stack
Script
greeting()
sayHi()

The call stack is responsible for keeping track of all the operations in line to be executed. Whenever a new function is executed it is pushed onto the stack and when it is finished, it is popped from the stack.
4.1 - The Event Loop
The call stack
function greeting() {
 const message = sayHi();
 console.log(message);
}
function sayHi() {
 return "Hi!";
}

greeting();
Call stack
Script
greeting()

The call stack is responsible for keeping track of all the operations in line to be executed. Whenever a new function is executed it is pushed onto the stack and when it is finished, it is popped from the stack.
4.1 - The Event Loop
The call stack
function greeting() {
 const message = sayHi();
 console.log(message);
}
function sayHi() {
 return "Hi!";
}

greeting();
Call stack
Script
greeting()
console.log()

The call stack is responsible for keeping track of all the operations in line to be executed. Whenever a new function is executed it is pushed onto the stack and when it is finished, it is popped from the stack.
4.1 - The Event Loop
The call stack
function greeting() {
 const message = sayHi();
 console.log(message);
}
function sayHi() {
 return "Hi!";
}

greeting();
Call stack
Script
greeting()

The call stack is responsible for keeping track of all the operations in line to be executed. Whenever a new function is executed it is pushed onto the stack and when it is finished, it is popped from the stack.
4.1 - The Event Loop
The call stack
function greeting() {
 const message = sayHi();
 console.log(message);
}
function sayHi() {
 return "Hi!";
}

greeting();
Call stack
Script

The call stack is responsible for keeping track of all the operations in line to be executed. Whenever a new function is executed it is pushed onto the stack and when it is finished, it is popped from the stack.
4.1 - The Event Loop
The call stack
function greeting() {
 const message = sayHi();
 console.log(message);
}
function sayHi() {
 return "Hi!";
}

greeting();
Call stack

4.1 - The Event Loop
Environment APIs
Environment APIs aren’t part of the JavaScript engine itself, but are part of the environment that the engine runs in. These environment APIs allow us to do things that JavaScript itself can’t do, such as network requests or interacting with the DOM.
Because these environment APIs aren’t part of the JavaScript engine itself, they don’t halt the execution of the JavaScript code and the script can continue executing after the call has been made.
This allows us to have some form of concurrency in JavaScript.


The task queue is a list of any functions to be processed after the current call stack has emptied. When the current call stack is empty, the event loop takes the first item off of the task queue and executes it.

4.1 - The Event Loop
console.log("Hello");

setTimeout(function cb{
 console.log("from")
}, 5000);

console.log("AND");
The task queue
Call stack
Runtime APIs
Task Queue
Console
Script

The task queue is a list of any functions to be processed after the current call stack has emptied. When the current call stack is empty, the event loop takes the first item off of the task queue and executes it.

4.1 - The Event Loop
console.log("Hello");

setTimeout(function cb{
 console.log("from")
}, 5000);

console.log("AND");
The task queue
Call stack
Runtime APIs
Task Queue
Console
Script

The task queue is a list of any functions to be processed after the current call stack has emptied. When the current call stack is empty, the event loop takes the first item off of the task queue and executes it.

4.1 - The Event Loop
The task queue
console.log("Hello");

setTimeout(function cb{
 console.log("from")
}, 5000);

console.log("AND");
Call stack
Runtime APIs
Task Queue
Console
> Hello
Script
console.log()

The task queue is a list of any functions to be processed after the current call stack has emptied. When the current call stack is empty, the event loop takes the first item off of the task queue and executes it.

4.1 - The Event Loop
The task queue
console.log("Hello");

setTimeout(function cb{
 console.log("from")
}, 5000);

console.log("AND");
Call stack
Runtime APIs
Task Queue
Console
> Hello
Script
setTimeout(cb)

The task queue is a list of any functions to be processed after the current call stack has emptied. When the current call stack is empty, the event loop takes the first item off of the task queue and executes it.

4.1 - The Event Loop
The task queue
console.log("Hello");

setTimeout(function cb{
 console.log("from")
}, 5000);

console.log("AND");
Call stack
Runtime APIs
Task Queue
Console
> Hello
Script
setTimeout(cb)
timer
cb

The task queue is a list of any functions to be processed after the current call stack has emptied. When the current call stack is empty, the event loop takes the first item off of the task queue and executes it.

4.1 - The Event Loop
The task queue
console.log("Hello");

setTimeout(function cb{
 console.log("from")
}, 5000);

console.log("AND");
Call stack
Runtime APIs
Task Queue
Console
> Hello
> AND
Script
console.log()
timer
cb

The task queue is a list of any functions to be processed after the current call stack has emptied. When the current call stack is empty, the event loop takes the first item off of the task queue and executes it.

4.1 - The Event Loop
The task queue
console.log("Hello");

setTimeout(function cb{
 console.log("from")
}, 5000);

console.log("AND");
Call stack
Runtime APIs
Task Queue
Console
> Hello
> AND
Script
timer
cb

The task queue is a list of any functions to be processed after the current call stack has emptied. When the current call stack is empty, the event loop takes the first item off of the task queue and executes it.

4.1 - The Event Loop
The task queue
console.log("Hello");

setTimeout(function cb{
 console.log("from")
}, 5000);

console.log("AND");
Call stack
Runtime APIs
Task Queue
Console
> Hello
> AND
timer
cb

The task queue is a list of any functions to be processed after the current call stack has emptied. When the current call stack is empty, the event loop takes the first item off of the task queue and executes it.

4.1 - The Event Loop
The task queue
console.log("Hello");

setTimeout(function cb{
 console.log("from")
}, 5000);

console.log("AND");
Call stack
Runtime APIs
Task Queue
Console
> Hello
> AND
cb

The task queue is a list of any functions to be processed after the current call stack has emptied. When the current call stack is empty, the event loop takes the first item off of the task queue and executes it.

4.1 - The Event Loop
The task queue
console.log("Hello");

setTimeout(function cb{
 console.log("from")
}, 5000);

console.log("AND");
Call stack
Runtime APIs
Task Queue
Console
> Hello
> AND
cb()

The task queue is a list of any functions to be processed after the current call stack has emptied. When the current call stack is empty, the event loop takes the first item off of the task queue and executes it.

4.1 - The Event Loop
The task queue
console.log("Hello");

setTimeout(function cb{
 console.log("from")
}, 5000);

console.log("AND");
Call stack
Runtime APIs
Task Queue
Console
> Hello
> AND
> from
cb()
console.log()

The task queue is a list of any functions to be processed after the current call stack has emptied. When the current call stack is empty, the event loop takes the first item off of the task queue and executes it.

4.1 - The Event Loop
The task queue
console.log("Hello");

setTimeout(function cb{
 console.log("from")
}, 5000);

console.log("AND");
Call stack
Runtime APIs
Task Queue
Console
> Hello
> AND
> from
cb()

The task queue is a list of any functions to be processed after the current call stack has emptied. When the current call stack is empty, the event loop takes the first item off of the task queue and executes it.

4.1 - The Event Loop
The task queue
console.log("Hello");

setTimeout(function cb{
 console.log("from")
}, 5000);

console.log("AND");
Call stack
Runtime APIs
Task Queue
Console
> Hello
> AND
> from

4.1 - The Event Loop
The event loop
The event loop is essentially an infinite loop that checks the task queue for work to be done.
When it finds work, it processes it until the stack is empty and then continues the loop.


Callbacks
4.2

4.2 - Callbacks
A callback function is a function that is passed into another function as an argument to be called later, for example after some other code has executed.
Callbacks can be used in both synchronous and asynchronous code, and a number of methods on built-in objects accept a callback function.
Examples of this are:
Array.prototype.sort
setTimeout
String.prototype.replaceAll

An example of a synchronous callback is the one passed to Array.prototype.map
The callback that is passed is called for each element in the array and is called with the current item in the array, the index of that item and the original array.
Once it has completed executing the function on every element, it will then return a the new array and execute the next line of code.
4.2 - Callbacks
Synchronous callbacks
const numbers = [1, 2, 3, 4, 5];

const multiplied = numbers.map((number, index) => {
 return number * index;
});

console.log(multiplied);
> [ 0, 2, 6, 12, 20 ]

An example of an asynchronous callback is the one passed to setTimeout
As mentioned in the previous section, this callback is only called after the specified time, but it doesn’t halt execution of any other code. This means that if we need to do anything once the timeout has completed, it must be done inside the callback.
4.2 - Callbacks
Asynchronous callbacks
console.log("Hello");
setTimeout(function cb(){
 console.log("from")
}, 5000);
console.log("AND");

> Hello
> AND
> from

Callback hell is when you have callbacks nested within callbacks, multiple layers deep. This can make code very difficult to read and understand. This can be avoided by structuring our code differently
4.2 - Callbacks
Callback hell
getProfile("1234", (profile) => {
 getPosts(profile, (posts) => {
   getPostComments(posts[0],(comments) => {
     console.log(comments)
   })
 })
})
function profileCb(profile) {
 getPosts(profile, postsCb);
}
function postsCb(posts) {
 getPostComments(posts, commentsCb);
}
function commentsCb(comments) {
 console.log(comments);
}

getProfile("1234", profileCb);

Promises
4.3

4.3 - Promises
Promises are a way to handle asynchronous behaviour in JavaScript. 
Promises themselves are constructor functions, so they’re just an object, but they have specific control flow that makes them useful.
Understanding Promises is a precursor to understanding async/await.


4.3 - Promises
Creating a promise
A promise can be created in two ways:
Long hand, using the constructor.
Shorthand, using the Promise.resolve and Promise.reject static methods

4.3 - Promises
Promise constructor
The promise constructor is passed a function with two parameters that are functions, resolve and reject. When resolve is called, the promise is resolved When reject is called, the promise is rejected.
const clash = new Promise(function(resolve, reject) {
 if (Math.random() > 0.5) {
   resolve('Should I stay or should I go now?');
 } else {
   reject('If I go there will be trouble');
 }
});

4.3 - Promises
Promise static methods
You can also use the Promise.resolve and Promise.reject static methods to create a promise that is immediately resolved or rejected.
Unless you have a .catch chained on to the end of your promise, a rejected promise will throw an error.
const clash = Promise.resolve('If stay it will be double');
try {
 const clash = Promise.reject('So you’ve got to let me know');
} catch (e) {
 console.log(e);
}

4.3 - Promises
Then

The only way to get a resolved value out of a promise is to chain a .then onto it. A .then call takes a function that can only have one parameter, which is the value returned from the promise.


const getGitHubData = () => Promise.resolve([
 { commit: '123csj43', author: '@1337c0d3r },
 { commit: '123csj44', author: '@1337c0d3r }
]);

getGitHubData().then(data => {
 console.log(data);
});
> [{commit ... }]

4.3 - Promises
Return values

Promises work heavily with return values, this is a very common gotcha
A consuming function must have access to the Promise in order to understand when it is returned.
The below example will probably only work intermittently, as jest doesn’t know that there is a promise inside it.


test('Calls the server', () => {
 fetch('/users/:123').then(data => {
   expect(data.user).toEqual('Trevor');
 });
});

4.3 - Promises
Catch
Errors that are thrown in a Promise will go down the Promise chain. If no .catch is provided the Promise usually throws an unhandled exception.
It is generally best practice to always add a .catch to your promises.


fetch('/users/:123').then(data => {
 console.log(data);
}).catch(error => {
 console.log("Who unplugged the internet?")
});

Exercise 4: Practicing Promises
Apply what you’ve learned about promises in the exercise

Add your code to: exercises/4-promises.test.js

Run this to have the tests run as you save:
npm run exercise::promises


In this file, you’ll see all the instructions for what you need to implement. Add your code and run the jest command to have it run the tests.

Async/Await
4.4

4.4 - Async/Await
Async / Await is simply a different way of writing Promises
If you understand Promises, async/await is much easier to understand, so it’s important to understand Promises well first.



Any function that uses await inside it, must have the async keyword applied to it. This fundamentally changes the behaviour of the function and now the async function by returns a promise.
Any time you want to make an asynchronous call that returns a promise you add the await keyword. This makes promise-returning functions behave as though they're synchronous by suspending execution until the returned promise is fulfilled or rejected
The resolved value of the promise is treated as the return value of the await.

4.4 - Async/Await
Anatomy of async/await
const getFacebookUser = async () => {
 const user = await facebook.getUser();

 return user;
};

4.4 - Async/Await
async/await and try..catch
With async/await, any rejected promises are thrown as an error. The below example would throw an exception and potentially break our application.
const exampleWithUnhandledError = async () => {
 const user = await Promise.reject('Nope.');
 return user;
};

await exampleWithUnhandledError();


4.4 - Async/Await
async/await and try..catch
Whereas we can use try/catch to catch that error and return something from our function
const exampleWithHandledError = async () => {
   try {
     return await Promise.reject('Nope');
   } catch (e) {
     return null;
   }
};

await exampleWithHandledError();


Exercise 5: async/await refactoring
Apply what you now know to refactor your code from exercise 4 to use async/await

Refactor your code in: exercises/4-promises.test.js

Run this to have the tests run as you save:
npm run exercise::promises