
# Welcome<!--.element: class="r-fit-text" -->

---

# Dan Moe<!--.element: class="r-fit-text" -->
<p class="r-fit-text">Product Developer <span class="andlogo">AND</span> String Plucker</p>

---

- Session 1 - React: The Basics <span class="andlogo fragment">←</span> 
- Session 2 - React: Digging Deeper 

---

### Learning Agreement

- Stay focused, cameras on <!-- .element: class="fragment" -->
- We are going to be coding <!-- .element: class="fragment" -->
- No question is a silly question <!-- .element: class="fragment" -->

...so please ask a question whenever you like<!-- .element: class="fragment" -->

---

# So, why React?

---

- <a href="https://npmtrends.com/@angular/core-vs-jquery-vs-react-vs-svelte-vs-vue">React</a> is the most popular frontend library
- Developed by Facebook<!-- .element: class="fragment" -->
- Declarative, efficient and flexible<!-- .element: class="fragment" -->
- It has the most stars on github<!-- .element: class="fragment" -->
- The most questions on stackoverflow<!-- .element: class="fragment" -->
- The most job listings<!-- .element: class="fragment" -->
- Huge community<!-- .element: class="fragment" -->

Note: 
- For Facebook, React is used on over 100,000 components seen by billions of users every day
- Unopinionated - bare bones (routing, styling, state handling etc)
- Utilises a component based architecture meaning building blocks are highly reusable
- Relatively short learning curve
- Really good dev exp, meaning easier to maintain
- Skills are in high demand so a good investment of time to learn
- 80% of AND clients use React 

---

### Comparison

<img src="./assets/fe-frameworks.png" alt="Front end frameworks" />

---

### Features

- Virtual DOM<!-- .element: class="fragment" -->
- JSX<!-- .element: class="fragment" -->
- One-way Data Binding<!-- .element: class="fragment" -->
- Declarative Syntax<!-- .element: class="fragment" -->
- Component-Based Architecture<!-- .element: class="fragment" -->
- Extensibility<!-- .element: class="fragment" -->

Note: 
React sets itself apart with several key features:

- Virtual DOM: How react handles rendering for high performance - reducing unnecessary updates.
- JSX (Javascript Syntax Extension / Javascript XML) templating language enables you to write JS and HTML code alongside eachother which is both familiar and powerful
- One-Way Data binding: Is how the data flows from parent to child, so we can guarantee mutations don't disrupt the components
- Declarative Syntax: React makes code more readable and therefore less prone to bugs.
- Component-Based: The component-based architecture promotes reusability, maintainability, and scalability, making it an ideal choice for complex UI development.
- Extensibility: React has many extensions, you can use what comes out of the box or include a different option. (REdux, TanQuery etc)

It supports mobile app development:
React Native
Now supports server-side rendering and static site generation with NextJS. 

---

### Today's agenda

- Virtual DOM
- JSX
- Components
- Handling events
- Handling data (props and state)
- Hooks
- Exercise / Demo<!-- .element: class="fragment" -->

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
- It allows us to interact with the page and programmatically and alter it with JavaScript, 
- for example  buttons, links, images, etc, become nodes in the DOM.

React allows us to interact with the virtual DOM to render and update HTML elements on a web page. 
The virtual DOM is an in-memory copy of the real DOM, and is how React achieves the level of performance that it does.  

So, while HTML is text, the DOM is an in-memory representation of this text.

Now originally DOM trees were quite simple. As the web has evolved things have gotten far more complex, and need to update much more often. 

Think about how quickly websites update when you visit Facebook, Twitter or LinkedIn. 

The DOM aims to rerender content every 16ms. 

Imagine you wanted to completely rerender the entire Facebook page every 16ms... it would likely crash you computer. 

To avoid such issues, we need a better implementation to make these small changes more quickly, and more dynamically.

---

### Virtual DOM

<img src="./assets/virtual-dom.jpg" alt="The Virtual DOM" style="width:50%;" />

Note:
Imagine you have your web page, which is the Real DOM.

When you first load a React application, React creates a copy of the Real DOM in memory. This is the Virtual DOM.

Now, let's say something changes in your application – perhaps you click a button, or data updates. React doesn't immediately touch the Real DOM. Instead, it creates a new Virtual DOM.

Next, React compares the old Virtual DOM with the new Virtual DOM. This process is called "diffing." It efficiently figures out exactly what has changed.

Finally, React takes only those specific changes and updates the Real DOM. This is much faster than re-rendering the entire page, making your application feel very responsive!

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
- In this case we are adding html elements useing the createElement method from React
- Its not something that is advised, but it’s a good to know that it’s possible 
  - Harder to read, harder to maintain, can open you up to security issues such as Injection attacks so not something that's widely used 
- Instead of this syntax we use something called JSX.

---

### With JSX

```jsx
import React from 'react';
import ReactDOM from 'react-dom';

const WelcomeMessage = () => (
  <div className="welcomeMessage">
    Welcome to ReactJS
  </div>;
)

const App = () => <WelcomeMessage />
```

Note:
- Defines a function - which is a reusable component
- Components return JSX that looks like HTML
- <WelcomeMessage /> is how you use/call a component (self-closing tag syntax)
- This is much cleaner than calling React.createElement() multiple times!

JavaScript XML - serves as a syntax extension for JavaScript in React. It allows developers to write UI components using a syntax that resembles HTML but is ultimately transpiled to JavaScript. JSX enhances code readability and expressiveness, making it an integral part of React development.

While JSX bears a resemblance to HTML, it's crucial to understand the distinctions. JSX introduces the ability to embed dynamic content through JavaScript expressions enclosed in curly braces {}. This dynamic nature empowers developers to create highly interactive and data-driven React components, blending the best of both worlds.
JSX vs HTML

---

## Thinking in React

---

### Atomic Design

<img src="./assets/atomic-design.png" alt="Atomic Design" style="width:70%;" />

Note:
- Book called Atomic Design - Brad Frost 
- Championed this idea of creating design systems split in to (Atoms, Molecules, Organisms, Templates and Pages)
- Good way of stucturing your app in terms of house keeping

---

### Components

<div style="display: flex; gap: 60px; justify-content: center;">
  <img src="./assets/react-components-1.png" alt="React Components Plain" style="width:25%;" />
  <img src="./assets/react-components-2.png" alt="React Components Split" style="width:50%;" />
</div>

Note:
- Component on the left
- Breakdown on the right

<a href="https://react.dev/learn/thinking-in-react" target="_blank">React Docs</a>

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
Class components are the traditional way of creating React components. They extend the React.Component class and have access to lifecycle methods, allowing developers to manage state and perform actions at various stages of a component's lifecycle.

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
- Functional components are the building blocks of a React application. 
- They are concise, stateless, and focus solely on rendering UI. 
- Since the introduction of React Hooks, functional components can now also manage state and lifecycle events, blurring the line between functional and class-based components.
- Dumb/Smart components ... stateless/stateful

---

# Handling Events

Note: 
- React provides a straightforward way to handle events, such as clicks or input changes. 
- Event handlers are assigned as attributes in JSX, and they can invoke functions that update state or perform other actions
– This creates a responsive and interactive user experience.

---

### onClick 

```js
const handleClick = (event) => {
  console.log('Button clicked!', event.target);
};

<button onClick={handleClick}>Click me</button>
```

Note: 
The onClick event attribute is a common way to handle click events. 
- React supports a range of event attributes, such as onChange for input changes and onSubmit for form submissions. 
- Understanding these attributes is crucial for building interactive user interfaces.
- React uses camelCase for event names, such as onClick instead of onclick. 
- Event handlers receive synthetic events with properties like target and currentTarget.

---

# Handling data

---

## Props vs State
- Props (Properties): Think of props as arguments.<!-- .element: class="fragment" -->
- State: A component's internal memory.<!-- .element: class="fragment" -->

Note:
- Props - They are external, read-only data passed down from a parent component to a child component. (Think One-way Data Binding). A child component cannot change its props.
- State: It is managed and controlled within the component itself. State is mutable (can be changed) and changing it is what causes the component to re-render.

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
- In React, data can be passed from a parent component to a child component using props. 
- Props are essentially properties that a parent component passes down to its children. 
- In JS however, we have no way of telling what these are, so we use typescript

---

<!-- .slide: data-auto-animate="true" -->
### Props ...with types
```js
const User = ({ username }) => (
  <div>
    <h1>{username}</h1>
  </div>
);

type UserProps = { username : string };
```
<!-- .element: data-id="code-animation" -->

Note: 
- When using Typescript you can dynamically design the props being passed in by naming them.
- You can end up repeating yourself if you are designing your props in the component file
- But the real value is if you pull the props into it's own object, and then you can share it amongst multiple areas 
- Which also give your IDE more clues on what the object contains
- Better dev exp (itellisense, visual aids etc)

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
- While props are used to pass data between components, state is used to manage a component's internal data. 
- State allows components to react to user input, events, or changes in data, leading to dynamic and interactive user interfaces.

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

---

# Exercise

---

#### Follow along!
```
https://playcode.io/react
```

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

#### React Docs
```
https://react.dev/
```

#### Atomic Design
```
https://bradfrost.com/blog/post/atomic-web-design/
```
<!-- 
Note:
https://playcode.io/react -->