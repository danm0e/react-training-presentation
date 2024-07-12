# Truthy / Falsey

Truthy and falsey refer to whether or not a value can be converted to true or false. If a value can be converted to true, it is truthy and if a value can be converted to false, it is falsey.
In JavaScript, all values are truthy unless they are falsey. The values that are considered falsey are the following:
- false
- 0
- -0
- 0n (BigInt zero)
- null
- undefined
- NaN
- Empty strings
---
# The !! operator
In JavaScript, ! is a logical NOT operator. When it’s used with a non-Boolean value, the value is converted to a boolean using the principles mentioned in the previous slide and then returns the inverse of that.
For example as 1 is truthy, !1 is false.
But if we use two logical NOT operators (!!), we can explicitly force the value to be converted to a boolean based on the truthyness or falseyness of the value.
```js
console.log(!!1);
> true

console.log(!!0);
> false
```
---
# Question
What is the difference between == and ===?

Which should you use?
---
# Loose & Strict Equality

In JavaScript, we can use both == and === for comparisons, however == will perform type coercion on the values. This means that if the two values are of a different type but the same value, the comparison will return true.
To avoid this, we can use  === and the comparison will return false if the types are different.

```js
console.log("1" == 1);
> true

console.log("1" === 1);
> false
```
---

