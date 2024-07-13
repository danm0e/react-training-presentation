# ES6 modules
```js
// databaseSeed.ts
const patchQuery = "INSERT into USERS ...";

const init = () => {
  return runQuery(patchQuery);
};

const runQuery = (query) => {
  return `Running query: ${query}`;
};

export { patchQuery, init, runQuery };
```
```js
// app.ts (for TypeScript)
import { patchQuery, init, runQuery } from './databaseSeed';

console.log(patchQuery);
console.log(init());
console.log(runQuery('SELECT * FROM USERS'));
```
Note: ES6 modules are similar to objects as modules but offer some advantages.
---
### Why use ES6 modules?
Note:
ES6 modules are natively supported in modern browsers and Node.js environments, providing great tooling integration and performance
Explicit dependencies make it easier to manage and reason about module dependencies.
They provide encapsulation by default, as variables and functions are private to the module unless explicitly exported.
---
<!-- .slide: data-auto-animate="true" -->
### Classes vs objects
```js
const person = (firstName: string, surname: string) => {
  const fullName = `${firstName} ${surname}`;

  const greeting = () => {
    console.log(`Hello, ${fullName}!`);
  };

  return {
    fullName,
    greeting,
  };
};
```
<!-- .element: data-id="code-animation" -->
---
<!-- .slide: data-auto-animate="true" -->
### Classes vs objects
```js
class Person {
  fullName: string;

  constructor(firstName: string, surname: string) {
    this.fullName = `${firstName} ${surname}`;
  }

  greeting() {
    console.log(`Hello, ${this.fullName}!`);
  }
}
```
<!-- .element: data-id="code-animation" -->

Note: A class is a clearer way of defining an object with a constructor

Start with class

Define some properties

Define a constructor

In the constructor assign the instance properties

That is what this is

Define some 
---

### Static methods

```js
class Circle {
  static pi: number = 3.14;

  static calculateArea(radius: number) {
    return this.pi * radius * radius;
  }
}
Circle.pi; // 3.14
Circle.calculateArea(3); // 28.26
```
Note: As we have already talked about, a function is an object in JavaScript. Because a function is an object it can have properties and if we assign functions to these properties, they become the function’s “static” methods.
They’re called static methods, because you don’t have to create a new instance of the object like a prototype method. An example of a static method on one of the built-in objects is Array.isArray().
When writing code with constructors, defining static methods can make our code cluttered, but when we’re writing code with classes, it becomes much cleaner.

Accessibility: Static methods can be called directly on the class itself, without creating an instance of the class. For example, MyClass.staticMethod().

Instance Independence: Static methods do not have access to instance properties or methods. They can only access and operate on static properties and methods of the class.

Inheritance: Static methods are inherited by subclasses, but they are not overridden. If a subclass defines a static method with the same name as a static method in the parent class, the subclass method will hide the parent class method for that subclass.

Use Cases: Static methods are commonly used for utility or helper functions that operate on data without requiring an instance of the class. They are also used for creating instances of the class (factory methods) or for providing functionality related to the class itself, rather than its instances.

Can you name a static method? Array.isArray()
---
### readonly
```js
class Circle {
  static readonly pi: number = 3.14;

  static calculateArea(radius: number) {
    return this.pi * radius * radius;
  }
}

Circle.pi = 314; 
// Cannot assign to 'pi' because it is a read-only property.
```
Note: You might also pair static with readonly.
---
### Access modifiers
The three Ps
- public <!-- .element: class="fragment" -->
- private <!-- .element: class="fragment" -->
- protected <!-- .element: class="fragment" -->
Note: An access modifier is a keyword that specifies the accessibility or visibility of a class member (properties, methods, or constructors) from other parts of the code. Access modifiers control how and where class members can be accessed or referenced.
public - accessible from anywhere (the default)
private - only accessible in the class that defined them
protected - accessible in the class that defined then and any subclasses.
---
<!-- .slide: data-auto-animate="true" -->
### public
```js
class Example {
  public property: string;
  public someFunction() {}

  constructor() {
    this.property = "Example";
  }
}
```
<!-- .element: data-id="code-animation" -->
---
### public
<!-- .slide: data-auto-animate="true" -->
```js
class Example {
  property: string;
  someFunction() {}

  constructor() {
    this.property = "Example";
  }
}
```
<!-- .element: data-id="code-animation" -->
Note: This is the default and you don’t necessarily need to specify that something is public.
---
<!-- .slide: data-auto-animate="true" -->
### private
```js
class Example {
  private property: string;
  private someFunction(arg: string) {}

  constructor() {
    this.property = "Example";
  }
}
```
<!-- .element: data-id="code-animation" -->
```js
const myExample = new Example();

myExample.someFunction();
// Property 'someFunction' is private and only accessible within class 'Example'
```
<!-- .element: class="fragment" -->
Note:
Worth noting that the constructor cannot be private, that wouldn’t be very helpful!

A use case for this is some helper methods within the class that are then called by public functions

Worth noting there is some sneaky ECMA script syntax that can be used in place of private - the Hash symbol #

I would caution against this as it isn’t widely used and private is more explicit and marrys up to other OOO language syntax.
---
### protected
```js
class Animal {
  protected name: string;

  constructor(name: string) {
    this.name = name;
  }

  protected makeSound(): void {
    console.log(`${this.name} makes a sound.`);
  }
}
```
```js
class Dog extends Animal {
  bark(): void {
    this.makeSound();
    console.log(`${this.name} barks.`);
  }
}
```
<!-- .element: class="fragment" -->
Note: Protected members can be accessed within the class and any sub classes.
---
<!-- .slide: data-auto-animate="true" -->
### Automatic assignment
```js
class Animal {
    private name: string;
    private sound: string;
    constructor( animalName: string, animalSound: string) {
        this.name = animalName;
        this.sound = animalSound;
    }

    public makeSound(): void {
        console.log(`The ${this.name} says ${this.sound}.`);
    }
}
let d = new Animal("dog","Woof!")
console.log(d.makeSound());
```
<!-- .element: data-id="code-animation" -->
Note: You can automatically assign properties rather than assinging them in the constructor.
---
<!-- .slide: data-auto-animate="true" -->
### Automatic assignment
```js
class Animal {


    constructor(private name: string, private sound: string) {}




    public makeSound(): void {
        console.log(`The ${this.name} says ${this.sound}.`);
    }
}
let d = new Animal("dog","Woof!")
console.log(d.makeSound());
```
<!-- .element: data-id="code-animation" -->
Note: Setting the access modifier in the constructor automatically assigns the parameter to this. A handy shortcut!
Protected members can be accessed within the class and any sub classes.

---
## Getters & Setters

Note: Getters and Setters are special methods that allow you to control the access and manipulation of a class's properties. They offer some benefits over interacting with properties directly.
---
### get and set
- Data Validation
- Computed Properties
- Logging & Debugging
Note:
- Data Validation - Validate the data being assigned to a property,
- Computed Properties - Compute and return a value based on other properties or calculations.
- Logging & Debugging - Log or debug the access and modification of properties.
---
### Getters & Setters
```js
class Example {
  private _property: number = 1;

  get property() {
    return this._property;
  }
  set property(value: number) {
    this._property = value;
  }
}
const example = new Example();

example.property = 2;
console.log(example.property);
// 2
```
Note: This is a basic example 

shows how you would use a private property that is only accessible within the class 

Then use getter and setter methods to interact with it.

In this example it is more verbose and not really worthwhile but demonstrates the syntax
---
3.4 - Getters & Setters
class Person {
  private _name: string;

  constructor(name: string) {
    this._name = name;
  }

  get name() {
    console.log("Getting name");
    return this._name.toUpperCase();
  }

  set name(value: string) {
    if (value.length > 20) {
      throw new Error("Name is too long");
    }
    console.log("Setting name");
    this._name = value;
  }
}
This is a more complete and realistic use case for getters and setters.

We do some logging (which could be to a logging service)

We modify the property as it is retrieved

We validate that the value fits requirements

Inheritance
3.3

3.4 - Inheritance
Inheritance is a mechanism that allows a new class to inherit properties and methods from an existing class. This gives some great advantages over many classes.
Code Reuse - Keep it DRY
Hierarchical Classification - Specialized classes can be derived from more general base classes for better organization and classification of objects.
Testability - Common functionality can be tested once in a base class then relied upon for children classes.

3.4 - Inheritance
Base Class
Here we define a base class - Animal with two public members, a property and a method.
class Animal {
  public name: string;

  constructor(name: string) {
    this.name = name;
  }

  public makeSound(): void {
    console.log(`${this.name} makes a sound.`);
  }
}

3.4 - Inheritance
Child Class
This class extends Animal.
Note the extends keyword and super() method.
class Dog extends Animal {
  public breed: string;

  constructor(name: string, breed: string) {
    super(name);	
    this.breed = breed;
  }

  public bark(): void {
    this.makeSound();
    console.log(`${this.name} barks.`);
  }
}
This class has its own property - breed

And its own method bark()

In the constructor we call super()

This calls the constructor of the parent class

In bark() we can call this.makeSound because makeSound is part of this class because it extends Animal.

This can be layered and layered.

3.4 - Inheritance
abstract Classes
Abstract classes allow defining a common class in situations you don't want to instantiate the base class itself. They provide a way to enforce behaviors or properties that derived classes must implement

abstract class Animal {
  public name: string;
  protected abstract sound: string;

  constructor(name: string) {
    this.name = name;
  }

  public abstract makeSound(): void;
}
This class has its own property - breed

And its own method bark()

In the constructor we call super()

This calls the constructor of the parent class

In bark() we can call this.makeSound because makeSound is part of this class because it extends Animal.

This can be layered and layered.

3.4 - Inheritance
Extending abstract Classes
Extending abstract classes is similar to standard classes but with the requirement of implementing abstract properties and methods. 

abstract class Animal {
  public name: string;

  constructor(name: string) {
    this.name = name;
  }

  public abstract makeSound(): void
}

class Dog extends Animal {
  public breed: string;
  protected sound: string = "barks";

  constructor(name: string, breed: string) {
    super(name);
    this.breed = breed;
  }

  public makeSound(): void {
    console.log(`${this.name} ${this.sound}.`);
  }
}
This class has its own property - breed

And its own method bark()

In the constructor we call super()

This calls the constructor of the parent class

In bark() we can call this.makeSound because makeSound is part of this class because it extends Animal.

This can be layered and layered.

Interfaces
3.5

3.5 - Interfaces
interface
An interface is a structural contract that defines the shape of an object, including its properties and methods. It serves as a blueprint or a set of rules that classes, objects, or functions must adhere to.

interface Animal {
  name: string;
  makeSound(): void;
}

3.5 - Interfaces
interface
The Dog class implements the Animal interface, ensuring that it adheres to the contract defined by the interface. It provides an implementation for the makeSound() method and includes an additional breed property.

class Dog implements Animal {
  name: string;
  breed: string;

  constructor(name: string, breed: string) {
    this.name = name;
    this.breed = breed;
  }

  makeSound(): void {
    console.log(`${this.name} barks.`);
  }
}
Optional Properties: Interfaces can define optional properties by using the ? syntax, allowing objects to have a flexible structure while still providing type safety.

Readonly Properties: Interfaces can define readonly properties using the readonly keyword, ensuring that these properties cannot be modified after an object is created.

Quite similar to types!

Interfaces are primarily used for defining the structure of object literals and classes.

Interfaces can extend other interfaces, allowing for inheritance and code reuse.

Interfaces are automatically merged when they have the same name, which can be useful for modular development.

Class Patterns
3.6

3.6 - Class Patterns
Factory Pattern
With interfaces (or types!) and classes we can use the Factory Pattern. This is a way to create objects of some type, leaving the decision of which concrete type to create to the factory.

interface Shoe {
  purpose: string;
}

class BalletFlat implements Shoe {
  purpose = "dancing";
}

class Sneaker implements Shoe {
  purpose = "running";
}

class Boot implements Shoe {
  purpose = "hiking";
}

3.6 - Class Patterns
Factory Pattern
The factory class with a static method is responsible for creating the 

class ShoeFactory {
  static createShoe(type: "ballet" | "sneaker" | "boot"): Shoe {
    switch (type) {
      case "ballet":
        return new BalletFlat();
      case "sneaker":
        return new Sneaker();
      case "boot":
        return new Boot();
    }
  }
}

const balletShoe = ShoeFactory.createShoe("ballet");
console.log(balletShoe.purpose);
// dancing
This class has its own property - breed

And its own method bark()

In the constructor we call super()

This calls the constructor of the parent class

In bark() we can call this.makeSound because makeSound is part of this class because it extends Animal.

This can be layered and layered.

3.6 - Class Patterns
Returning this
class RequestBuilder {
  private method: "get" | "post" | null = null;
  private url: string | null = null;

  public setMethod(method: "get" | "post"): this {
    this.method = method;
    return this;
  }

  public setUrl(url: string): this {
    this.url = url;
    return this;
  }
}
You can also return this and create chains of functions acting on the same object instances. 
Protected members can be accessed within the class and any sub classes.



3.6 - Class Patterns
Builder Pattern
class RequestBuilder {
  private method: "GET" | "POST" | null = null;
  private url: string | null = null;
  private data: object | null = null;

  // other methods...

  public send(): void {
    // do send
  }
}

new RequestBuilder()
  .setMethod("POST")
  .setUrl("https://example.com")
  .setData({ key: "value" })
  .send();

This is called the builder pattern. 
Protected members can be accessed within the class and any sub classes.



3.4 - Interfaces
abstract & interface
You can also combine and interface and abstract classes!

interface Animal {
  name: string;
  makeSound(): void;
}

abstract class Mammal {
  public breathesAir: boolean = true;
}
This class has its own property - breed

And its own method bark()

In the constructor we call super()

This calls the constructor of the parent class

In bark() we can call this.makeSound because makeSound is part of this class because it extends Animal.

This can be layered and layered.

3.4 - Interfaces
abstract & interface

class Dog extends Mammal implements Animal {
  name: string;

  constructor(name: string) {
    super();
    this.name = name;
  }

  makeSound(): void {
    console.log(`${this.name} barks.`);
  }
}

const dog = new Dog("Fluffy");
dog.breathesAir; // true

This class has its own property - breed

And its own method bark()

In the constructor we call super()

This calls the constructor of the parent class

In bark() we can call this.makeSound because makeSound is part of this class because it extends Animal.

This can be layered and layered.

Decorators
3.3

3.4 - Interfaces
@decorator
A decorator in TypeScript is a special kind of function that allows you to modify or extend the behavior of a class, method, property, or parameter. It is a way to add metadata or additional functionality to your code without directly modifying the original code.

class Dog implements Animal {
  name: string;
  breed: string;

  constructor(name: string, breed: string) {
    this.name = name;
    this.breed = breed;
  }

  makeSound(): void {
    console.log(`${this.name} barks.`);
  }
}
This class has its own property - breed

And its own method bark()

In the constructor we call super()

This calls the constructor of the parent class

In bark() we can call this.makeSound because makeSound is part of this class because it extends Animal.

This can be layered and layered.

Generic Types
4

4.1 - Generics
Functions
A generic type is a way to write code that can work with different types of data. Instead of writing separate code for each data type, you can write one piece of code that can handle multiple types. 

function wrapStringInArray(string: string): string[] {
  return [string];
}

function wrapNumberInArray(number: number): number[] {
  return [number];
}

//generic
function wrapValueInArray<T>(value: T): T[] {
  return [value];
}
This class has its own property - breed

And its own method bark()

In the constructor we call super()

This calls the constructor of the parent class

In bark() we can call this.makeSound because makeSound is part of this class because it extends Animal.

This can be layered and layered.

4.1 - Generics
Classes
Generics can also be used with classes!

class ValueHolder<T> {
  constructor(private _value: T) {}

  get value(): T {
    return this._value;
  }
}

const num = new ValueHolder(1);
console.log(num.value);

const str = new ValueHolder('string');
console.log(str.value);

This class has its own property - breed

And its own method bark()

In the constructor we call super()

This calls the constructor of the parent class

In bark() we can call this.makeSound because makeSound is part of this class because it extends Animal.

This can be layered and layered.

4.1 - Generics
Types
Type aliases can also use generics!

type ValueBox<T> = {
  value: T;
};

const myStringValue: ValueBox<string> = { value: "hello" };
const myNumberValue: ValueBox<number> = { value: 5 };

type ValueConverterFunction<T, U> = (value: T) => U;

const stringToNumber: ValueConverterFunction<string, number> = function (
  value
) {
  return Number(value);
};

This class has its own property - breed

And its own method bark()

In the constructor we call super()

This calls the constructor of the parent class

In bark() we can call this.makeSound because makeSound is part of this class because it extends Animal.

This can be layered and layered.

Exercise 2: Implement lodash
Re-implement some lodash methods.

Add your code to: exercises/2-functional.test.js

Run this to have the tests run as you save:
npm run exercise::functional
Now we have our first exercise, we’re going to re-implement some lodash methods.

In this file, you’ll see all the instructions for what you need to implement. Add your code and run the jest command to have it run the tests.

Exercise 3: Implement A Calculator
Implement a Calculator with an interface,  module and a Class.

Add your code to: exercises/3-objectOriented.test.js

Run this to have the tests run as you save:
npm run exercise::object-oriented
Now we have our first exercise, we’re going to re-implement some lodash methods.

In this file, you’ll see all the instructions for what you need to implement. Add your code and run the jest command to have it run the tests.
