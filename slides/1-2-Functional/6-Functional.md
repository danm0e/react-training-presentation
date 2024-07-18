# Functional Methods
---
### Array methods
- .map<!-- .element: class="fragment" --> 
- .filter<!-- .element: class="fragment" --> 
- .reduce<!-- .element: class="fragment" --> 
Note:Functional methods allow us to write code where inputs aren’t mutated. This is useful in cases where we pass a array to a function and want to do things with that array without changing the original array.
There are 3 main functional methods on arrays in JavaScript, but there are many more that you should [take time to understand](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array#:~:text=non%2Dmutating%20alternative%3A-,Mutating,-method).

---
### Map

```js [1|3-4|6-7]
const numbers = [1, 2, 3];

console.log(numbers)
> [ 1, 2, 3 ]

console.log(numbers.map((number) => number * 3))
> [ 3, 6, 9 ]
```
Note: The map method iterates over all of the items in a collection and runs a function on them and then returns a new collection with the results.
This is useful for things like manipulating a set of data into a format that you need, or doing repeated calculations.
---
### Filter

```js [1|3-4|6-12]
const numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];

console.log(numbers)
> [ 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 ]

console.log(numbers.filter((number) => {
 if (number % 2 === 0) {
   return true;
 }
 return false;
});)
> [ 2, 4, 6, 8, 10 ]
```
Note: The filter method iterates over all of the items in a collection and runs a function on them to decide whether or not that item should be included in the returned collection. 
---

# Reduce

```js 
const numbers = [10, 2, 73, 1, 0, 19, 210, 3, 47, 18];

console.log(numbers.reduce((highest, number) => {
 if (number > highest) {
   return number;
 }
 return highest;
}, 0))
> 210
```

Note: The reduce method runs a function on each element in the collection, passing it the result from running the function on the previous element. The final result is a single value
---
### Exercise 2: Implement lodash
- Re-implement some lodash methods.
- Add your code to: `exercises/2-functional.js`
- Run this to have the tests run as you save:
```
npm run exercise::functional
```






