# Errors & Throwing
An error is where a computer program has reached a state of execution that is unexpected and the resolution is not explicitly known.
Which is why we have errors, and error handling.
You should try and handle all errors in your code, throw an explicit error for all errors you might “expect”
---
# Errors
The Error object is one of the built-in objects in JavaScript.
Any runtime errors in your code will cause an Error object to be created and thrown by the JavaScript engine.
We can also create our own Error objects
```js
const result = new Error("Oops!");

console.log(result);
> Error: Oops!
```
---
# Throwing
By using the throw keyword, we can halt the current execution when an error occurs. It then traverses up the call stack to the nearest try/catch block.
throw accepts an argument, which can be of any type, and this is passed to the catch block.
It’s preferred to use the built-in error object for consistency.
```js
try {
 throw "I throw an error";
 console.log("I never get called");
} catch (e) {
 console.log(e);
}
> Error: I throw an error
```
---
npm run exercise::basics
brew install node@18

git clone https://github.com/and-digital/and-workshop-corejs.git

cd and-workshop-corejs
npm install
---
# Exercise 1: Implement a test assertion library
Implement a jest inspired API assertion library.

Add your code to: `exercises/1-theBasics.test.js`

Run this to have the tests run as you save:

```
npm run exercise::basics
```
---
# Solution
```js
toBeTruthy: () => {
    return !!actualValue == true;
},
toBeUndefined: () => {
    return actualValue === undefined;
},
toBeArray: () => {
    return Array.isArray(actualValue);
},
toBe: (expectedValue) => {
    return actualValue === expectedValue;
},
toThrow: () => {
    try {
        actualValue()
        return false;
    } catch (x) {
        return true;
    }
},
```
