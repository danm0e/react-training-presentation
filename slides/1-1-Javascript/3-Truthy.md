## Truthy / Falsey
- `Truthy` and `falsey` refer to whether or not a value can be converted to true or false. 
- If a value can be converted to true, it is truthy and if a value can be converted to false, it is falsey.<!-- .element: class="fragment" -->
---
### Falsey
- `false`<!-- .element: class="fragment" -->
- `0`<!-- .element: class="fragment" -->
- `-0`<!-- .element: class="fragment" -->
- `0n`<!-- .element: class="fragment" -->
- `null`<!-- .element: class="fragment" -->
- `undefined`<!-- .element: class="fragment" -->
- `NaN`<!-- .element: class="fragment" -->
- `Empty strings`<!-- .element: class="fragment" -->

Note: Everything else is a Turthy. 0n is  BigInt zero
---
### The !! operator
- ! is a logical NOT operator <!-- .element: class="fragment" -->
- Converts non-Booleans to the opposite boolean value <!-- .element: class="fragment" -->
- !! Will swap it back to the original object but as a boolean <!-- .element: class="fragment" -->
```js
console.log(!!1);
> true
```
<!-- .element: class="fragment" -->
```js
console.log(!!0);
> false
```
<!-- .element: class="fragment" -->
---
### What about these?
```js[1|2|3|4|5]
console.log(!!false);
console.log(!!NaN);
console.log(!!"yes");
console.log(!!42);
console.log(!!"false");
```
Note: all of these seem logical apart from the last one. It is a string so javascript returns true, despite the fact we might think it's false
---
# Question
What is the difference between == and ===? <!-- .element: class="fragment" -->

Which should you use?<!-- .element: class="fragment" -->
Note: Answer
Double equals is looser about type checking
You should almost always use triple equals to ensure strict equality. Explicitly convert the types if necessary.
---
### Loose & Strict Equality

```js [1|2]
console.log("1" == 1);
console.log("1" === 1);
```
Note: In JavaScript, we can use both == and === for comparisons, however == will perform type coercion on the values. This means that if the two values are of a different type but the same value, the comparison will return true.
To avoid this, we can use  === and the comparison will return false if the types are different.

