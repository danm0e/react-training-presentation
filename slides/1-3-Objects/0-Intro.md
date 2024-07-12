


Object Oriented JavaScript
3

3 - Object Oriented JavaScript
Using Objects As Modules: Design patterns and pseudo-private variables 
Object Constructor: How we create objects in JavaScript.
Prototypal Inheritance: How JS does inheritance and why your arrays have a .map
Classes: A class is just a function ... but how!?
Dynamic Scoping: How JavaScript gives contexts dynamic scope with "this"

Using Objects As Modules
3.1

3.1 - Using Objects As Modules
Modules
A module is simply a way of organizing code and using them can be helpful for grouping together related code.
You can utilise the various module systems such as native modules and node modules. But you can also create them in your code using objects.

3.1 - Using Objects As Modules
Basic module
A basic module is just an object with properties applied. These properties can be functions or other types and they can be accessed both within the module and outside of the module.

const databaseSeed = {
 patchQuery: "INSERT into USERS ...",
 init: function () {
   return this.runQuery(this.patchQuery);
 },
 runQuery(query) {
   return `Running query: ${query}`;
 },
};

console.log(databaseSeed.init());
> Running query: INSERT into USERS...
console.log(databaseSeed.patchQuery);
> INSERT into USERS ...

3.1 - Using Objects As Modules
Revealing module pattern
A common pattern in JavaScript modules is the revealing module pattern. This is where you use a function call to return an object that contains only some of the methods and properties used by the module, so you can have pseudo-private methods and properties
const databaseSeed = function() {
 const patchQuery = "INSERT into USERS ...";
 const init = () => runQuery(patchQuery);
 const runQuery = (query) => `Running: ${query}`;
 return {
   init
 }
};

console.log(databaseSeed().init());
> Running: INSERT into USERS ...
console.log(databaseSeed().patchQuery);
> undefined

Object Constructor
3.2

A constructor is function with a set of instructions used when creating an object. This can useful for things like defining instance values or storing any passed configuration.
When a function is called using the new keyword, it is run as a constructor.



3.2 - Object Constructor
Constructors

3.2 - Object Constructor
The new keyword
To run a function as a constructor, we need to use the new keyword. When we do this, the following happens:
A new JavaScript object is created. Let’s call it newInstance
The prototype of newInstance is set to the prototype of the constructor 
The this value of the constructor is set to newInstance and the constructor is executed.
If the constructor returns a non-primitive value, then this becomes the result of the entire new expression. Otherwise, newInstance is returned

3.2 - Object Constructor
The new keyword
The below example shows a constructor being called with a value passed to it, which is then stored on the object being created.
You can also see that this is the same as the object that is created. So any updates made to this will be reflected in the object that is returned.
function Cheese(name) {
   this.name = name;
   console.log(this);
}

console.log(new Cheese("Brie"));
> Cheese {name: 'Brie'}
> Cheese {name: 'Brie'}

Prototypal Inheritance
3.3

3.3 - Prototypal Inheritance
Prototypes
A prototype is how javascript allows shared functionality. Every object in javascript has a prototype “link” (this can be seen as __proto__ or [[prototype]] in your browser)
These __proto__ links eventually end up back at the parent Object type.



3.3 - Prototypal Inheritance
Classes vs Prototypes
Classes are inert, they don’t really do anything and can’t be modified.
This is where prototypal inheritance differs, in prototypal inheritance we have objects that are chained together and it is possible to mutate any member of the prototype chain or even swap out the prototype at runtime.
Therefore, prototypal inheritance can be seen as a sort of dynamic inheritance, inheritance that can be modified/changed.



3.3 - Prototypal Inheritance
Inheritance
Using constructors in JavaScript allows us to do inheritance, but it’s a two step process:
Create a constructor for the new object we’re creating 
Tell it which prototype to inherit from by assigning the function a prototype object


function MyArray() {
   this.myarray = true;
}
Object.setPrototypeOf(MyArray.prototype, Array.prototype);

const myArrayInstance = new MyArray();
console.log(myArrayInstance.myarray)
> true
console.log(myArrayInstance instanceof Array)
> true

3.3 - Prototypal Inheritance
Prototype mutation
Since prototypes are references to an object, if you mutate the object instance that is the parent of your object, you’ll dynamically update the prototype.

function Speech() {}
Speech.prototype.greeting = (name) => `Hello ${name}!`;

function Human() {}
Object.setPrototypeOf(Human.prototype, Speech.prototype);

const Dave = new Human();
console.log(Dave.greeting("Geraldine"));
> Hello Geraldine!

Speech.prototype.greeting = (name) => `Go away ${name}!`;
console.log(Dave.greeting("Geraldine"));
> Go away Geraldine!

3.3 - Prototypal Inheritance
Built-in object prototype mutation
Because changes to the prototype impact any objects that use that prototype, we should avoid modifying the prototypes of any of the built-in objects as this can cause unintended impacts elsewhere in the codebase.
Object.prototype.toString = function() {
return "Not what you're expecting!";
};

console.log({test: 1}.toString());
> Not what you're expecting!

console.log(Intl.toString());
> Not what you're expecting!

Classes
3.4

3.4 - Classes
Classes vs constructor & prototype
In JavaScript, a class is mainly a clearer way of defining a constructor and prototype. The below two examples are equivalent to each other.
function Box(value) {
 this.value = value;
}

Box.prototype.getValue = function () {
 return this.value;
};
class Box {
 constructor(value) {
   this.value = value;
 }

 getValue() {
   return this.value;
 }
}


3.4 - Classes
Static methods
As we have already talked about, a function is an object in JavaScript. Because a function is an object it can have properties and if we assign functions to these properties, they become the function’s “static” methods.
They’re called static methods, because you don’t have to create a new instance of the object like a prototype method. An example of a static method on one of the built-in objects is Array.isArray().
When writing code with constructors, defining static methods can make our code cluttered, but when we’re writing code with classes, it becomes much cleaner.



3.4 - Classes
Static methods
In the below example, we’re creating a static method on a constructor and then calling it. You can see that it looks a little cluttered.
function constructorExample() {
 // Constructor code goes here
}

constructorExample.staticMethod = () => {
 return 'static constructor';
}

console.log(constructorExample.staticMethod());
> static constructor

3.4 - Classes
Static methods
Here you can see the equivalent code written as a class. It is far more concise than the constructor example and is easier to understand.
class ClassExample {
 static staticMethod() {
   return 'static class';
 }
}

console.log(ClassExample.staticMethod());
> static class

Dynamic Scoping
3.5

3.4 - Dynamic Scoping
This
this in Javascript is dynamic scoping.
Dynamic scoping is code that can be understood only when the code runs, not when it is written.
Lexical scope is the scope we can see whereas dynamic scope might change, dependent on how a function is executed.
Dynamic scoping creates impurity in our code as our function acts on data (objects) outside of its own scope.


3.4 - Dynamic Scoping
This
Every function within JavaScript has a value of this
You can either tell JavaScript what you want a value of this to be explicitly, or you can leave it up to JavaScript to try and work out what you wanted it to do.
this can be set implicitly, or you can set it explicitly by invoking the function with one of either: call, apply or bind.
This means, in total that there are 4 ways to set the value of this.



3.4 - Dynamic Scoping
Implicit binding
If you call a call a function without having explicitly set this, it will be automatically given a value. This value is assigned to the object that the function is called on.
If the function is not part of an object, this will be set to the global object. However if the function is part of an object (e.g as part of a class or prototype), this will be the object that the function is part of.

function whatIsThis() {
 return this;
}
const contextualWrapper = { whatIsThis };

console.log(whatIsThis());
> global { global: global, clearInterval: ƒ, … }

console.log(contextualWrapper.whatIsThis());
> { whatIsThis: ƒ }

3.4 - Dynamic Scoping
Explicit binding
We can use call, apply or bind to explicitly set the value of this.
call and apply will both execute a function, the key difference between them is that call accepts a list of arguments specified individually,  whereas apply accepts them as an array.
bind returns a function with a scope and any arguments bound to it that then needs to be called.


3.4 - Dynamic Scoping
Explicit binding
const argA = "Hello";
const argB = "World";

function whatIsThis(a, b) {
 return this;
}

console.log(whatIsThis.call({ hello: true }, argA, argB));
> { hello: true }

console.log(whatIsThis.apply({ hello: true }, [argA, argB]));
> { hello: true }

const boundWhatIsThis = whatIsThis.bind({ hello: true }, argA)
console.log(boundWhatIsThis(argB));
> { hello: true }


Exercise 3: Implement A Calculator
Implement a Calculator with a module, constructor and a Class.

Add your code to: exercises/3-objectOriented.test.js

Run this to have the tests run as you save:
npm run exercise::object-oriented
Now we have our first exercise, we’re going to re-implement some lodash methods.

In this file, you’ll see all the instructions for what you need to implement. Add your code and run the jest command to have it run the tests.
