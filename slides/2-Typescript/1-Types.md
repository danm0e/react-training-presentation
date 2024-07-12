
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

Generally we use dot notation to access enum values.

They offer improved readability for related constants. Often uses to represent a set of fixed options or choices, like directions.
### BitWise Enums
```js
enum FileAccess {
  // constant members
  None,
  Read = 1 << 0,
  Write = 1 << 1,
  Execute = 1 << 2,
  ReadWrite = Read | Write,
}
```
Note: Very nice for efficient representation of compond properties. For example you can capture the state of 3 parameters using 3 bits. What's lovely about Bitwise style is you can also have permeatations of those different values in athe minimum data footprint, with type safety