

# Asynchronous JavaScript
---
### Agenda
- The Event Loop: Why we need async anyway, and how JS handles async.
- Callbacks: Passing functions around for later execution
- Promises: Understanding the promise object and using it.
- Async / Await: Taking Promises one step further with async/await.
---
### The Event Loop
```js
function greeting() {
 const message = sayHi();
 console.log(message);
}
function sayHi() {
 return "Hi!";
}

greeting();
```
Note: JavaScript is a single threaded language, but it uses some clever data structures and a runtime model called the event loop to allow us to have asynchronous tasks.

The call stack is responsible for keeping track of all the operations in line to be executed. Whenever a new function is executed it is pushed onto the stack and when it is finished, it is popped from the stack.

The call stack is responsible for keeping track of all the operations in line to be executed. Whenever a new function is executed it is pushed onto the stack and when it is finished, it is popped from the stack.
---
# The call stack
```js
function greeting() {
 const message = sayHi();
 console.log(message);
}
function sayHi() {
 return "Hi!";
}

greeting();
```
Note: JavaScript is a single threaded language, but it uses some clever data structures and a runtime model called the event loop to allow us to have asynchronous tasks.

The call stack is responsible for keeping track of all the operations in line to be executed. Whenever a new function is executed it is pushed onto the stack and when it is finished, it is popped from the stack.
---
### Environment APIs

Note: Environment APIs aren’t part of the JavaScript engine itself, but are part of the environment that the engine runs in. These environment APIs allow us to do things that JavaScript itself can’t do, such as network requests or interacting with the DOM.
Because these environment APIs aren’t part of the JavaScript engine itself, they don’t halt the execution of the JavaScript code and the script can continue executing after the call has been made.
This allows us to have some form of concurrency in JavaScript.

### Task queue
```js
console.log("Hello");

setTimeout(function cb{
 console.log("from")
}, 5000);

console.log("AND");
```
Note: The task queue is a list of any functions to be processed after the current call stack has emptied. When the current call stack is empty, the event loop takes the first item off of the task queue and executes it.

---
### The event loop
Note: The event loop is essentially an infinite loop that checks the task queue for work to be done.
When it finds work, it processes it until the stack is empty and then continues the loop.
----
### Callbacks
Some built in objects accept a callback. For example:
- Array.prototype.sort
- setTimeout
- String.prototype.replaceAll

Note: A callback function is a function that is passed into another function as an argument to be called later, for example after some other code has executed.
Callbacks can be used in both synchronous and asynchronous code, and a number of methods on built-in objects accept a callback function.
Examples of this are:
- Array.prototype.sort
- setTimeout
- String.prototype.replaceAll
An example of a synchronous callback is the one passed to Array.prototype.map
The callback that is passed is called for each element in the array and is called with the current item in the array, the index of that item and the original array.
Once it has completed executing the function on every element, it will then return a the new array and execute the next line of code.
---
### Synchronous callbacks
```js
const numbers = [1, 2, 3, 4, 5];

const multiplied = numbers.map((number, index) => {
 return number * index;
});

console.log(multiplied);
> [ 0, 2, 6, 12, 20 ]
```

Note: An example of an asynchronous callback is the one passed to setTimeout

---
### Asynchronous callbacks

```js
console.log("Hello");
setTimeout(function cb(){
 console.log("from")
}, 5000);
console.log("AND");

> Hello
> AND
> from
```
Note: 
As mentioned in the previous section, this callback is only called after the specified time, but it doesn’t halt execution of any other code. This means that if we need to do anything once the timeout has completed, it must be done inside the callback.
---
### Callback hell
```js
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
```
Note: Callback hell is when you have callbacks nested within callbacks, multiple layers deep. This can make code very difficult to read and understand. This can be avoided by structuring our code differently

---
### Promises
Note: Promises are a way to handle asynchronous behaviour in JavaScript. 
Promises themselves are constructor functions, so they’re just an object, but they have specific control flow that makes them useful.
Understanding Promises is a precursor to understanding async/await.
---
### Creating a promise
There are 2 ways:
- Long hand (using the constructor).<!-- .element: class="fragment" --> 
- Short hand (using the Promise.resolve static methods)<!-- .element: class="fragment" --> 
---
### Promise constructor
```js
const clash = new Promise(function(resolve, reject) {
 if (Math.random() > 0.5) {
   resolve('Should I stay or should I go now?');
 } else {
   reject('If I go there will be trouble');
 }
});
```
Note: The promise constructor is passed a function with two parameters that are functions, resolve and reject. When resolve is called, the promise is resolved When reject is called, the promise is rejected.
---
### Promise static methods
```js
const clash = Promise.resolve('If stay it will be double');
try {
 const clash = Promise.reject('So you’ve got to let me know');
} catch (e) {
 console.log(e);
}
```
Note: You can also use the Promise.resolve and Promise.reject static methods to create a promise that is immediately resolved or rejected.
Unless you have a .catch chained on to the end of your promise, a rejected promise will throw an error.
---
### Then


```js
const getGitHubData = () => Promise.resolve([
 { commit: '123csj43', author: '@1337c0d3r' },
 { commit: '123csj44', author: '@1337c0d3r' }
]);

getGitHubData().then(data => {
 console.log(data);
});
> [{commit ... }]
```
Note: The only way to get a resolved value out of a promise is to chain a .then onto it. A .then call takes a function that can only have one parameter, which is the value returned from the promise.

---
### Return values

```js
test('Calls the server', () => {
 fetch('/users/:123').then(data => {
   expect(data.user).toEqual('Trevor');
 });
});
```
Note: Promises work heavily with return values, this is a very common gotcha
A consuming function must have access to the Promise in order to understand when it is returned.
The below example will probably only work intermittently, as jest doesn’t know that there is a promise inside it.
---
### Catch

```js
fetch('/users/:123').then(data => {
 console.log(data);
}).catch(error => {
 console.log("Who unplugged the internet?")
});
```
Note: Errors that are thrown in a Promise will go down the Promise chain. If no .catch is provided the Promise usually throws an unhandled exception.
It is generally best practice to always add a .catch to your promises.
---

### Exercise 4: Practicing Promises
- Apply what you’ve learned about promises in the exercise
- Add your code to: exercises/4-promises.test.js
- Run this to have the tests run as you save:
```
npm run exercise::promises
```

Note: In this file, you’ll see all the instructions for what you need to implement. Add your code and run the jest command to have it run the tests.
---
### Async/Await
Note: Async / Await is simply a different way of writing Promises
If you understand Promises, async/await is much easier to understand, so it’s important to understand Promises well first.
Any function that uses await inside it, must have the async keyword applied to it. This fundamentally changes the behaviour of the function and now the async function by returns a promise.
Any time you want to make an asynchronous call that returns a promise you add the await keyword. This makes promise-returning functions behave as though they're synchronous by suspending execution until the returned promise is fulfilled or rejected
The resolved value of the promise is treated as the return value of the await.
---
### Anatomy of async/await
```js
const getFacebookUser = async () => {
 const user = await facebook.getUser();

 return user;
};
```
### async/await and try..catch
```js
const exampleWithUnhandledError = async () => {
 const user = await Promise.reject('Nope.');
 return user;
};

await exampleWithUnhandledError();
```
Note: With async/await, any rejected promises are thrown as an error. The below example would throw an exception and potentially break our application.
---
### async/await and try..catch
```js
const exampleWithHandledError = async () => {
   try {
     return await Promise.reject('Nope');
   } catch (e) {
     return null;
   }
};
await exampleWithHandledError();
```
Note: Whereas we can use try/catch to catch that error and return something from our function

---
### Exercise 5: async/await refactoring
- Apply what you now know to refactor your code from exercise 4 to use async/await
- Refactor your code in: exercises/4-promises.test.js
- Run this to have the tests run as you save:
```js
npm run exercise::promises
```