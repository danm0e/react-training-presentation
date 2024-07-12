
# Types 
---
### Primatives
Remember the 7 primatives?
- String type for strings <!-- .element: class="fragment" -->
- Number for numbers of any kind: integer or floating-point <!-- .element: class="fragment" -->
- Boolean for true/false <!-- .element: class="fragment" -->
- BigInt type for large numbers <!-- .element: class="fragment" -->
- Null for unknown values <!-- .element: class="fragment" -->
- Undefined for unassigned values – a standalone type that has a single value undefined <!-- .element: class="fragment" -->
- Symbol type for unique identifiers <!-- .element: class="fragment" -->
Note: That's it - that's all the primitives in Javascript.
---
### Special Types
Typescript has some additional types
- literal - a type that can only be one concrete thing <!-- .element: class="fragment" -->
- enum - a possible set of constants <!-- .element: class="fragment" -->
- void - when you want nothing  <!-- .element: class="fragment" -->
- any - a dynamic object <!-- .element: class="fragment" -->
- unknown - like any but you can't use it's properties <!-- .element: class="fragment" -->
- never - it won't continue  <!-- .element: class="fragment" -->

Note: 
- literal - a type that can only be one concrete thing
- enum - a possible set of constants
- void - the return type of a function that returns nothing or has no return statement
- any - makes a value behave like it would in regular Javascript. It is the default when you, or typescript, don’t assign a type. Avoid!
- unknown - when you really don’t know what a type could be. You should refine the type before using the value
- never - the return type of a function that never returns - eg it always throws an exception or terminates execution
---
# Type annotation & aliases
Note: Type annotation is a way to explicitly specify the type of a variable, parameter, or return value.
Type aliases allow you to create a new name for a type, making complex types more readable and reusable.
We’ve talked about different types of types and how they behave in some circumstances, how do we actually say something is a type?
### Type annotation

```js
let secondName: string;
// typeof string

function toLowercase(input: string) {}

const firstName = "Bill";
// typeof string
```
Note: Typescript can infer types where they are not explicitly specified. 
---
## Type aliases
```js
type Friends = string[]
// string array (alias)

type House = string | number
// union

type Location = {
    x: number;
    y: number;
}
// object literal
```
Note: Types can be declared in isolation. This is useful for documentation and when to make aliases for a specific shapes or structures.
---
### Union & Intersection
```js
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
```
Note: The union of two types is everything in one, the other, or both. The intersection is everything in both types.
---
### Pick & Partial
```js
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
```
Note: The union of two types is everything in one, the other, or both.The intersection is everything in both types.
---
### Type casting
```js
// We have a variable of type unknown
let userInput: unknown = “123”;

// We want to treat userInput as a string
let userInputString = userInput as string;
```
Note: Type casting is the process of explicitly changing the type of a variable from one type to another. Type casting is useful when working with dynamic data or when integrating with JavaScript libraries that don't provide type information. 

Typically you’ll only be doing this with unknown types, or as we say here, when working with untyped JS libraries. You may use a type alias and then cast to that type.
---
### Type generics
```js
function identity<Type>(arg: Type): Type {
  return arg;
}

let output = identity<string>("myString");
// pass type as argument to function with <>

let output = identity("myString");
// let typescript use type argument inference
```
Note: A quick note on type generic syntax. 
We won’t go into any depth on this but I’ll introduce the idea of type generics. 
Sometimes you want a function, or class, to be flexible on the type it works with without using any, unknown, or a large union type.

Just know that when you see this syntax you are looking at a generic! Don’t worry about this for now!
---

### Type safety
Note:
All of this adds up to give us Type safety.
That is, we use types to prevent programs from doing invalid things.
JavaScript on its own attempts to make the best of invalid situations which can lead to unexpected outcomes, Typescript helps avoid that.


Example

Let's have a look at some examples of type safety.
---
## Objects, Arrays, Tuples & Enums
Note: Our main types for representing data in JavaScript are Object, Array, Tuple, and Enum
Objects are used to represent a collection of key-value pairs and do not guarantee any specific order for their properties.
Arrays store a collection of values in a specific order.
Tuples are similar to arrays. They maintain the order of their elements but their length and types of elements are fixed and predefined. 
Enums are way of defining a set of named constants. They allow us to create a collection of related values represented by a specific name.
---
### Objects
```js[1|3-5|7]
let obj: object;

let obj: Object;

let obj: {};

let obj: { a: string };
```
Note: Object types can be declared in a few different ways in Typescript.

There are some different ways of saying what type an object will be in Typescript.

The first is to define an empty object and you don't care what fields it has, but can essentially behave a bit like any.

The second and third are equilivent. This is specifying an object with no parameters at all. Avoid this as you'll be creating an empty object and you arn't giving typescript (or your IDE) any information about what you are making.

The last one is Object Literal Notation. It creates an object and specifies the shape of the object. This is the best way to do it. Let's dive into more examples. 
---
### Object literal notation
```js
let obj: {
  a: number;
  b?: string;
  readonly c: string;
  [key: number]: boolean;
};
```
Note: Also known as a shape. Used when you know which fields an object could have. 
---
### Index Signatures
```js
type Booking = {
  [seatNumber: string]: string;
};
type Booking = Record<string, string>;
```

```js
let trainSeatBookings: Booking = {
  "32A": "Peter Parker",
  "34E": "Carol Danvers",
};
```
 <!-- .element: class="fragment" -->
Note: This lets you tell Typescript that a given object might have more keys.
You could also use Record to create an object with key:value pairs of strings. Why might you not want to do that, though? (Collisions, Less expressive, Harder to save in a structured database, trickier to iterate)
---
### Arrays
```js [1-2|4-5|7]
let horses: string[];
horses = ["Clydesdale", "Shire", "Unicorn"];

let horses: Array<string>;
horses = ["Clydesdale", "Shire", "Unicorn"];

let horses = ["Clydesdale", "Shire", "Unicorn"];
```
---
### Tuples

```js[1-2|4-5|7-8|9-10]
const coordinates1: [number, number] = [23, 48];
const coordinates2 = [23, 48];

console.log(coordinates1[0]);
> 23

coordinates1.push(1);
```
Note: Tuples act similarly to arrays but their length and types of elements are fixed and predefined. 
Generally you would use bracket notation to access them, like arrays.
---
### Readonly Tuples
```js[1-3|4|6-7|8|10-12|13]
let coordinates1: readonly[number, number];
coordinates1 = [23, 48];
coordinates1.push(1);
// Property 'push' does not exist on type 'readonly [number, number]'.

const coordinates2 = [23, 48] as const;
coordinates1.push(1);
// Property 'push' does not exist on type 'readonly [number, number]'.

let coordinates3: [number, number];
coordinates3 = [23, 48] as const;
coordinates3.push(1);
// ccoordinates3.length = 3
```

Note: You might like to define a tuple as readonly, too. This would prevent adding to the tuple. You can do this by specifying readonly

Or setting a varaible "as const'

But be warned if you've set a tuple type without readonly, and then assign it will not treat it as readonly.
---
### Enum
```js
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
```
Note: Similar to an object, enums have named properties and associated values. However, unlike an object, the values cannot be changed. 
You can access values using dot or bracket notation. Typically dot notation is used.


Generally you’d access an Array using the bracketed notation.
---
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
