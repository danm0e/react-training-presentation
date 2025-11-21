
# Welcome!<!--.element: class="r-fit-text" -->

---

# Dan Moe<!--.element: class="r-fit-text" -->
<p class="r-fit-text">Product Developer <span class="andlogo">AND</span> String Plucker</p>

---

## Session 1
#### React: The Basics<!-- .element: class="fragment" -->

Note:
- This is session 1 of 2 parts
- We're going to cover some basics of the whats and the whys
- As well as going over some of the key mechanics of how React works under the hood

---

### Today's agenda

- Why React?
- Virtual DOM
- Components
- JSX
- Handling events
- Handling data (props and state)
- Hooks
- Exercise / Demo (Live coding)<!-- .element: class="fragment" -->

---

### Learning Agreement

- Stay focused, cameras on <!-- .element: class="fragment" -->
- We are going to be looking at code <!-- .element: class="fragment" -->
- No question is a silly question <!-- .element: class="fragment" -->

...so please ask a question whenever you like<!-- .element: class="fragment" -->

Note:
 - Helps me know I'm not alone
 - I understand there maybe some people here that do not code, so please...
 - If there is any point where I have gone to fast or you would like some clarity on something, please ask
 - There will also hopefully be some time at the end for a bit of a Q&A

---

# So, why React?

---

- <a href="https://npmtrends.com/@angular/core-vs-jquery-vs-react-vs-svelte-vs-vue">React</a> is the most popular frontend library
- Developed and used by Meta (Facebook) <!-- .element: class="fragment" -->
- Declarative, efficient and flexible<!-- .element: class="fragment" -->
- Huge community<!-- .element: class="fragment" -->
- It has the most stars on github<!-- .element: class="fragment" -->
- The most questions on stackoverflow<!-- .element: class="fragment" -->
- The most job listings<!-- .element: class="fragment" -->

Note: 
- Facebook: So they have over 100,000 components used by billions of users every day
- Declarative: Really good developer experience
  - Relatively short learning curve
  - ...Meaning easier to maintain and debug
- Efficient: It's fast... 
- Flexible: Unopinionated - bare bones library for building UI (routing, styling, state handling etc)
- Community: Lots of good reference for AI
- Skills are in high demand so a good investment of time to learn
- 80% of AND clients use React 

---

### Comparison

<img src="./assets/fe-frameworks.png" alt="Front end frameworks" />

---

### Features

- Virtual DOM<!-- .element: class="fragment" -->
- Component-Based Architecture<!-- .element: class="fragment" -->
- JSX<!-- .element: class="fragment" -->
- One-way Data Binding<!-- .element: class="fragment" -->
- Declarative Syntax<!-- .element: class="fragment" -->
- Extensibility<!-- .element: class="fragment" -->

Note: 
React sets itself apart with several key features:

- Virtual DOM: How react handles rendering for high performance
- Component-Based: Promotes reusability, maintainability, and scalability, making it an ideal choice for complex UI development
- JSX (Javascript Syntax Extension / Javascript XML) templating language enables you to write JS and HTML code alongside eachother
- One-Way Data binding: So how the data flows from parent to child, so we can guarantee mutations don't disrupt the components
- Declarative Syntax: React makes code more readable and therefore less prone to bugs
- Extensibility: React has many packages (extensions), you can use what comes out of the box or include a different option
- If you think Lego... you can follow the instructions or build your own (Redux, TanstackQuery, Zustand etc)
- --
- It supports mobile app development with React Native
- Now supports server-side rendering and static site generation with NextJS

---

# Virtual DOM

---

### The DOM

The DOM (Document Object Model) is a programming interface for the web. 

```
<html>
  <body>
    <h1>My web page</h1>
    <button>Click me</button>
  </body>
</html>
```

Note:
- It’s a data structure that represents the HTML on a page
- While HTML is text, the DOM is an in-memory representation of this text
- It allows us to interact with the page programmatically with JavaScript
- So buttons, links, images, etc, are all nodes in the DOM
- Now originally DOM trees were quite simple (think static brochure style websites)
- As the web has evolved things have gotten far more complex and need to update much more often 
- Think about how quickly websites update when you visit Facebook, Twitter or LinkedIn.
- The DOM aims to rerender content every 16ms 
- Imagine you wanted to completely rerender the entire Facebook page every 16ms... it would likely crash your computer.
- To avoid this, we need a better implementation

---

### Virtual DOM

<img src="./assets/virtual-dom.png" alt="The Virtual DOM" style="width:50%;" />

Note:
- Imagine you have your web page, which is the Real DOM
- When you first load a React application, React creates a copy of the Real DOM in memory. This is the Virtual DOM
- Now, let's say something changes in your application – perhaps you click a button, or data updates 
- React doesn't immediately touch the Real DOM. Instead, it creates a new copy of the Virtual DOM with the new changes
- Next, React compares the old Virtual DOM with the new Virtual DOM. 
- This process is called "diffing." It efficiently figures out exactly what has changed, like a snapshot
- Finally, React takes only those specific changes and updates the Real DOM. 
- This is much faster than re-rendering the entire page

---

## Thinking in React

---

### Atomic Design

<img src="./assets/atomic-design.png" alt="Atomic Design" style="width:70%;" />

Note:
- Brad Frost - Atomic Design
- Championed this idea of creating design systems split in to (Atoms, Molecules, Organisms, Templates and Pages)
- Good way of designing your app for reusability
- Good way of stucturing your app in terms of house keeping

---

### Components

<div style="display: flex; gap: 60px; justify-content: center;">
  <img src="./assets/react-components-1.png" alt="React Components Plain" style="width:25%;" />
  <img src="./assets/react-components-2.png" alt="React Components Split" style="width:50%;" />
</div>

Note:
- Overall component on the left which would represent a page such as a shopping cart
- Then an example of how we'd break that down on the right
  - organism being the filter/product table
  - and then the molecules that build the table rows
  - and then labels and prices making up the individual atoms  
---

### Class components

```jsx
class MyClassComponent extends React.Component {
  constructor(props) {
    super(props);
    // Component state initialisation
  }

  render() {
    return (
      <div>
        {/* JSX content */}
      </div>
    );
  }
}
```
Note:
- Class components are the traditional way of creating React components. 
- They extend the React.Component class and have access to lifecycle methods
- This allows developers to manage state and perform actions at various stages of a component's lifecycle.
- Think when the component is 
  - mounted - so when a page is loaded
  - updated - when an event has taking place (button click or data change)
  - unmounted - when the user leaves a page

---

### Functional components

```jsx
const MyFunctionalComponent = () => {
  // Component logic here
  return (
    <div>
      {/* JSX content */}
    </div>
  );
};
```
Note:
- Functional components are the building blocks of a React application
- This example is concise, stateless, and focus solely on rendering UI 
- Since the introduction of React Hooks, functional components can now also manage state and lifecycle events
  - blurring the line between functional and class-based components
- Dumb/Smart components ... stateless/stateful

---

# 🐾

Note:
- I'm aware there maybe some non coding folk who may not want to delve deeper
- The rest of the demo is code heavy so wanted to give you an chance to drop off

---

# JSX

---

### Without JSX

```jsx
import React from 'react';
import ReactDOM from 'react-dom';

// Example div containing welcome message
React.createElement( 'div', { className: "welcomeMessage" }, "Welcome to ReactJS")

// Rendering to the DOM
ReactDOM.render (<App />, document.getElementById("root")) ;
```

Note:
- As you can see these are some javascript functions, and you CAN use React this way
- In this case we are adding html elements using the createElement method from React
- Its not something that is advised, but it’s a good to know that it’s possible 
- Hard to read, hard to maintain, can open you up to security issues such as Injection attacks so not something that's widely used 
- Instead of this syntax we use something called JSX.

---

### With JSX

<!-- .slide: data-auto-animate="true" -->
```jsx
const WelcomeMessage = () => (
  <div className="welcomeMessage">
    Welcome to ReactJS
  </div>
)
```
<!-- .element: data-id="code-animation" -->

Note:
- JSX - is a syntax extension for JavaScript in React (known as syntactic sugar). 
- It enhances readability and expressiveness of our code, and is an integral part of React development.
- We define a function - which becomes a reusable component
- Components return JSX that looks like HTML
- This is much cleaner than calling React.createElement() multiple times!

---

### With JSX

<!-- .slide: data-auto-animate="true" -->
```jsx
const WelcomeMessage = () => (
  <div className="welcomeMessage">
    {welcomeText}
  </div>
)

const welcomeText = 'Welcome to ReactJS';
```
<!-- .element: data-id="code-animation" -->

Note:
- It also has ability to embed dynamic content through JavaScript expressions enclosed in curly braces
- So we can create data-driven React components, blending the best of both worlds

Key takeaway:
- While JSX looks like HTML, it's crucial to understand the distinctions
- Whilst what we have here is something that resembles HTML, it's ultimately transpiled to JavaScript via the createElement method under the hood

---

<!-- .slide: data-auto-animate="true" -->
### JSX Gotchas
```js
const MyComponent = () => (
  <p>First paragraph</p>
  <p>Second paragraph</p>
)
```
<!-- .element: data-id="code-animation" -->

Note: 
- Now with everything, there are a couple of gotchas with JSX
- Some rules that need to be followed
- Can anybody tell me what is wrong with this code?
- It would error... (next slide)

---

<!-- .slide: data-auto-animate="true" -->
### JSX Gotchas
```js
const MyComponent = () => (
  <p>First paragraph</p>
  <p>Second paragraph</p>
)

!⛔️JSX expressions must have one parent element.ts(2657)
```
<!-- .element: data-id="code-animation" -->

Note: 
- JSX rule is that there can only be one element in a component
- So what can we do here? 
- Maybe wrap these paragraphs with a div right?

---

<!-- .slide: data-auto-animate="true" -->
### JSX Fragments
```js
import { Fragment } from 'react';

const MyComponent = () => (
  <Fragment>
    <p>First paragraph</p>
    <p>Second paragraph</p>
  </Fragment>
)
```
<!-- .element: data-id="code-animation" -->

Note: 
- React exports something known as a Fragment
- Fragments are a way to group multiple elements without introducing an unnecessary element to the DOM
- They help keep the HTML structure clean when rendering multiple components
- Think performance at scale

---
<!-- .slide: data-auto-animate="true" -->
### JSX Fragments
```js
const MyComponent = () => (
  <>
    <p>First paragraph</p>
    <p>Second paragraph</p>
  </>
);
```
<!-- .element: data-id="code-animation" -->
Note: 
- There's a short hand way of using them - an empty tag
- So it's more descriptive and you don't have to import the Fragment, React just understands this as a Fragment
- There's also a gotcha here too with a key requirement when looping through data but we'll not get in to that now

---

# Handling Events

Note: 
- React provides a straightforward way to handle events, such as clicks or input changes 
- Event handlers are assigned as attributes in JSX, and they can invoke functions that update state or perform other actions
- This creates a responsive and interactive user experience.

---

### onClick 

```js
const handleClick = (event) => {
  console.log('Button clicked!', event.target);
};

<button onClick={handleClick}>Click me</button>
```

Note: 
The onClick event attribute is a common way to handle click events 
- React supports a range of event attributes, such as onChange and onSubmit for input changes and form submissions
- It's really important to understand these for building interactive user interfaces
- The camelCase convention is used for event names, such as onClick instead of onclick
- Event handlers receive synthetic events with properties like target and currentTarget

---

# Handling data

---

## Props vs State
- Props (Properties): Think of props as arguments.<!-- .element: class="fragment" -->
- State: A component's internal memory.<!-- .element: class="fragment" -->

Note:
- Props - They are external, read-only data passed down from a parent component to a child component
- (Think One-way Data Binding) 
- A child component cannot change its props
- --
- State: It is managed and controlled within the component itself
- State is mutable (can be changed) and changing it is what causes the component to re-render

---

### Props
<!-- .slide: data-auto-animate="true" -->
```js
const User = ({ username }) => (
  <div>
    <h1>{username}</h1>
  </div>
);
```
<!-- .element: data-id="code-animation" -->

Note: 
- Props are essentially properties that a parent component passes down to its children 
- In JS however, we have no way of telling what these are, so we use typescript

---

<!-- .slide: data-auto-animate="true" -->
### Props ...with types
```js
const User = ({ username }: UserProps) => (
  <div>
    <h1>{username}</h1>
  </div>
);

type UserProps = { username : string };
```
<!-- .element: data-id="code-animation" -->

Note: 
- When using Typescript you can design the data type being passed in as the prop
- Which also give your IDE more clues on what the object contains
- Better dev exp (itellisense, visual aids etc)
- -- 
- You can end up repeating yourself if you are designing your props in the component file
- But the real value is if you pull the props into it's own object, and then you can share it amongst multiple areas 

---

### State
```js
const Counter = () => {
  const [message, setMessage] = useState("I'm set on page load");

  setTimeout(() => {
    setMessage("I've been updated a few seconds later");
  }, 5000);

  return (
    <MessageComponent message={message} />
  );
};
```

Note: 
- While props are used to pass data between components, state is used to manage a component's internal data
- State can also be passed down as a prop 
- State allows components to react to user input, events, or changes in data
- This leads to dynamic and interactive user interfaces
- --
Question: state changes cause what in React?
Answer... Re-renders.

---

# Hooks

---

### useState Hook
<!-- .slide: data-auto-animate="true" -->
```js
const [state, setState] = useState(initialState);
```
<!-- .element: data-id="code-animation" -->

Note: 
- Introduced in React Hooks, the useState hook is a powerful tool for managing state in functional components. 
- It allows functional components to have stateful logic without the need for class components. 
- The hook returns the current state and a function to update it.

---

<!-- .slide: data-auto-animate="true" -->
### useState Hook

```tsx
const [state, setState] = useState<number>(initialState);
```
<!-- .element: data-id="code-animation" -->

---

<!-- .slide: data-auto-animate="true" -->
### useState Hook

```tsx
const [state, setState] = useState<string>(initialState);
```
<!-- .element: data-id="code-animation" -->

---

<!-- .slide: data-auto-animate="true" -->
### useState Hook
```tsx
const [state, setState] = useState<MyType>(initialState);

interface MyType {
  age: number;
  name: string;
}
```
<!-- .element: data-id="code-animation" -->

Note:
- Other hooks - e.g to manage rerendering (useMemo, useCallback)
- Custom hooks (useAuthentication)
- Garbage collection, a way to keep business logic out of your components and keep it reusable

---

# ✋

---

# Exercise

---

#### Follow along!
```
https://playcode.io/react
```

Note: 
- Walk through example of building a simple counter
- When the user clicks the button, React captures the beginning of this event handler.
- React sees the three state updates (setCount).
- Instead of triggering a re-render after Update 1, then Update 2, and finally Update 3
- React puts all three updates into a queue (the "batch").
- Once the event handler function (handleClick) has finished executing, React processes the entire queue at once.
- It calculates the final, resulting state based on all the updates.
- Finally, React triggers a single re-render of the component with the new state values.
- -- 
- Key takeaway: State setters are asynchronous and do not immediately change the state or trigger a re-render. They merely queue the change for React to process later.

---

## Any questions?<!--.element: class="r-fit-text" -->

---

### Useful links

<!-- #### Exercise - Follow along!
```
https://playcode.io/react
``` -->

<!-- #### Follow along session 2
```
https://codesandbox.io/p/sandbox/d9dw8v?file=%2Fsrc%2FApp.tsx%3A11%2C1
``` -->

##### React Docs
```
https://react.dev/
```

##### Thinking in React
```
https://react.dev/learn/thinking-in-react
```

##### Atomic Design
```
https://bradfrost.com/blog/post/atomic-web-design/
```

---

# Thank you!<!--.element: class="r-fit-text" -->
