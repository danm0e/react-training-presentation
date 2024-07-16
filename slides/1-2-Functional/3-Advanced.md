# Advanced Function Arguments
---
### Helpful syntax
- Default parameters<!-- .element: class="fragment" --> 
- Rest parameters<!-- .element: class="fragment" --> 
- Spread operator<!-- .element: class="fragment" --> 
- Destructuring<!-- .element: class="fragment" --> 
Note: There are a few things that we can use with function arguments that can help us write more readable code and help us avoid some error scenarios. These are:
- Default parameters
- Rest parameters
- Spread operator
- Destructuring
---
# Default parameters

```js[1|1,2-3|1,4-5|1,6-7]
const multiply = (a, b = 1) => a * b;
multiply(5, 2);
> 10
multiply(5);
> 5
multiply(5, undefined);
> 5
```
Note: By default a function parameter is assigned undefined if no value is passed, however it is often useful to set a different default value. With default parameters we can do this.
In the below example, we set the default value of b to 1 so we’ll have a value returned if only one argument is passed.
---
# Rest parameters
```js
const sum = (name, ...args) => {
  return name + ":" + args.reduce((agg, curr) => agg + curr);
};
console.log(sum("Bob", 1, 2, 3, 4));
> "Bob:10"
```
Note: The rest operator allows you to define the last parameter of a function definition to be an array containing any remaining arguments. This means that a function can accept an indefinite number of arguments.
In the below example, we use the rest operator to create an array of all the arguments and then use the Array.reduce method to iterate through all of the items in the array and return the sum.
---
# Spread operator
```js
const getOptions = (params) => {
 const defaultOptions = { color: "red", height: 10 };
 return { ...defaultOptions, ...params};
};

console.log(getOptions({ color: "blue" }));
> { color: "blue", height: 10 }
```
Note: The spread operator allows iterable objects (such as arrays or strings) and object literals to be expanded where zero or more arguments or elements are expected.
In the below example, we have a function that returns a set of options. There is a default set of options and the user can provide a set with their own values. We use the spread operator to merge these together.
---
# Spread copies
<!-- .slide: data-auto-animate="true" -->
```js [1-2|4|6-7|8-9]
const objHello = { nested: { greeting: "hello" } };
const objBye = { ...objHello };

objBye.nested.greeting = "goodbye";

console.log(objBye);
> { nested: { greeting: "goodbye" } }
console.log(objHello);
> { nested: { greeting: "goodbye" } }
```
<!-- .element: data-id="code-animation" -->
Note: One thing to be aware of with the spread operator is that it only creates a new copy of the top level object. Any nested objects will still refer to the same object and will be impacted by modifications.
In the example below, we create an object with a nested object within it. We then use the spread operator to copy this into a new object. When we modify the nested object within objB, it also modifies the object within objA as well. This behaviour can cause unexpected issues.
---
# Deep copies

```js [2|4|6-7|8-9]
const objHello = { nested: { greeting: "hello" } };
const objBye = structuredClone(objHello);

objBye.nested.greeting = "goodbye";

console.log(objBye);
> { nested: { greeting: "goodbye" } }
console.log(objHello);
> { nested: { greeting: "hello" } }
```
Note: One thing to be aware of with the spread operator is that it only creates a new copy of the top level object. Any nested objects will still refer to the same object and will be impacted by modifications.
In the example below, we create an object with a nested object within it. We then use the spread operator to copy this into a new object. When we modify the nested object within objB, it also modifies the object within objA as well. This behaviour can cause unexpected issues.
---
# Destructuring
```js
const addFirstTwo = ([a, b]) => a + b;
console.log(addFirstTwo([35, 7, 999999]));
> 42

const getCar = ({ make, model }) => `${make} ${model}`;
console.log(getCar({
  make: "Ford",
  model: "Mustang",
  color: "Blue"
}));
> Ford Mustang
```
Note: Destructuring allows us to unpack values from arrays or objects into distinct variables. In the context of function arguments, this is useful as we can have a variable scoped to our function and not have to traverse the object or array.
---
# Destructuring
```js
const getCar = (props) => {
const  { make, model: { modelName: name, year } } = props;
 return `${year} ${make} ${name}`;
}
console.log(
 getCar({
   make: "Ford",
   model: {
     modelName: "Mustang",
     year: "1975",
   },
   color: "Blue",
 })
);
> 1975 Ford Mustang
```
Note: We can destructure within objects, to save us having to traverse deeper into the object.
We can also rename a variable that we destructure. In the below example we rename modelName to name.