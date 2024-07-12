# Passing by reference & value
---
## What’s the difference?
- By reference = Points to the original object<!-- .element: class="fragment" --> 
- By val = Passed as a copy<!-- .element: class="fragment" --> 
Note: Pass by reference is when a reference to an original object in memory is given to a function.
Pass by value is when a value is passed to a function as a copy, not as a pointer to the original in memory value.

It’s important to know when something is created in memory vs when we’re acting on a reference as mutating an object that is passed by reference may impact other areas of your code and introduce bugs.
---
# Passing by reference

```js
const updateAge = (person) => {
 person.age = person.age + 1;
 return person;
};

const sandra = { name: 'sandra', age: 22 };
updateAge(sandra);

console.log(sandra);
> { name: 'sandra', age: 23 }
```
Note: In the example below, we can see that the change that the function makes to the object impacts the original object too. This is because it is passed by reference.
---
# By Value

```js
const reverseString = (str) => {
  str = str.split("").reverse().join("");
  return str;
};

const input = "hello";
console.log(reverseString(input));
> olleh

console.log(input);
> hello
```
Note: In this example, we can see that the original string and the output from the function are different. This is because it has been passed by value.