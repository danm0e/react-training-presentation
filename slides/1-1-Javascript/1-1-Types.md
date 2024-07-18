### Types - Primitive Values

A primitive is basically anything that’s not an object.

An object has properties / methods

---
### Primatives (7 in total)
- `String` for text <!-- .element: class="fragment" -->
- `Number` for integers or floating-points <!-- .element: class="fragment" -->
- `Boolean` for true/false <!-- .element: class="fragment" -->
- `BigInt` type for large numbers <!-- .element: class="fragment" -->
- `Undefined` for unassigned values <!-- .element: class="fragment" -->
- `Null` for intentional nothing <!-- .element: class="fragment" -->
- `Symbol` type for unique identifiers <!-- .element: class="fragment" -->
Note: That's it - that's all the primitives in Javascript.

---
### Types - Objects
In JavaScript, an Object is a collection of properties. Property values can be values of any type, including other objects, which enables building complex data structures.
Null is something that has a value and it's 
Undefined is somthing that has been declared but not yet assigned a value

---
### Types - Objects
Examples of built-in objects are:
 - Function
 - Error
 - Promise
 - Date
Note: 
---
### Types - Objects

Types are important when it comes to operators.

```js [1|2|3|4|5]
console.log(1 + 1)
console.log(1 + '1')
console.log(1 - '1')
console.log('one' + 1)
console.log('one' - 1)
```

Note: <https://carbon.now.sh/6qs8fxhBqgIlIFOdddoj>
Output is 2 - it's a number
Next is 11 - it turns the number into a string because + can attach text together so it converts the number to a string
Next is 0 - Minus cannot do anything on strings so it attempts to turn the string into a number
Next is one1 - String concatination
Next is NaN because minus can only work on numbers, it can't parse 'one' to a number so it say "Not a Number"
---
### Types - typeof operator
We can use the typeof operator to tell the difference between data types. This allows us to implement error handling and/or different behaviour dependent on type.

```js [1-6|7-8|5|9-10|3]
const myFunction = (value) => {
 if (typeof value != "string") {
   console.log("No, strings only!");
 }
 console.log("We good, we good");
};

myFunction("Hey");

myFunction(0);
```
Note: <https://carbon.now.sh/efCTijMM7DgtATJEWBOo> (Output is 'We good, we good', 'No, strings only!')
---
### Types - typeof discrepancies
Unfortunately, typeof might not always return what you expect
```js [1|2|3|4|5]
console.log(typeof []);
console.log(typeof null);
console.log(typeof Number);
console.log(typeof new Number(0));
console.log(typeof NaN);
```
Note: <https://carbon.now.sh/PKS92HMzYG8KsfARg0gA> (Output is object, object, function, object, number)
---
# Question
- Why does typeof [] return object?
- How do we type check an array then? <!-- .element: class="fragment" -->
Note: An array is a type of object.
To check for an array use Array.isArray()
---
<!-- .slide: data-auto-animate="true" -->
### Types - Type coercion
```js 
var str = 'hello';
var upper = str.toUpperCase();
console.log(upper);
```
<!-- .element: data-id="code-animation" -->
Note: <https://carbon.now.sh/QxszaT53n3TK8V200tZe> (As mentioned earlier, primitives have no properties or methods, but somehow "abc".length returns a value.)
---
<!-- .slide: data-auto-animate="true" -->
### Types - Type coercion
```js 
var str = 'hello';
var upper = (new String(str)).toUpperCase();
console.log(upper);
```
<!-- .element: data-id="code-animation" -->
Note: <https://carbon.now.sh/9VSsrbCeQdpr7mJEvD68> (This is because JavaScript wraps the primitive in a String object temporarily.)
