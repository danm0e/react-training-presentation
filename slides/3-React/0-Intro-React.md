
# React 
---
- Server Components (RSC) 
- JSX
- State & Redux
- Hooks vs Classes
---

### Introduction to React

React was initially developed by Facebook; and is declarative, efficient and flexible. <!-- .element: class="fragment" -->

Note: React is a JavaScript / TypeScript framework that lets you build user interfaces out of individual pieces called components.

You can create components like Button, Thumbnail and others; then combine them into screens, pages and entire applications.
Introduction to React

It’s widely used in building single-page applications, utilises a component based architecture. What this means is that a UI is constructed from reusable building blocks.
---
### Advantages of using React

- Virtual DOM
- Declarative Syntax
- Component-Based
- Popular

Note: 
React distinguishes itself through several key features:

Virtual DOM: React's efficient Virtual DOM minimizes direct manipulation of the actual DOM, enhancing performance by reducing unnecessary updates.

Declarative Syntax: With a declarative syntax, React makes code more readable and less prone to bugs, enabling developers to focus on the "what" rather than the "how.

Component-Based: The component-based architecture promotes reusability, maintainability, and scalability, making it an ideal choice for complex UI development.

Popular: React is the highest used and loved frontend framework, used by 49% of all respondants, and beating Svelte as a language people would use again

---

### Basics of JSX

```tsx
function renderLogin({ prefilledEmail }) {
  return (
    <section>
      <input type="email" placeholder="email" value={prefilledEmail} />
      <input type="password" placeholder="password" />
      <button>Log In!</button>
    </section>
  );
}
```
Note: JSX (JavaScript XML) serves as a syntax extension for JavaScript in React. It allows developers to write UI components using a syntax that resembles HTML but is ultimately transpiled to JavaScript. JSX enhances code readability and expressiveness, making it an integral part of React development.
Understanding JSX Syntax

While JSX bears a resemblance to HTML, it's crucial to understand the distinctions. JSX introduces the ability to embed dynamic content through JavaScript expressions enclosed in curly braces {}. This dynamic nature empowers developers to create highly interactive and data-driven React components, blending the best of both worlds.
JSX vs HTML
---
### JSX Expressions & Embeddings
```ts
const App = () => {
  const textButton = 'Click Me';
  return (
    <div>
      {/* referencing javascript variables into JSX */}
      <button id="btn">
        {textButton}
      </button>
    </div>
  );
};
```
Note: JSX goes beyond static markup; it supports the embedding of JavaScript expressions directly within the markup. By enclosing expressions in curly braces {}, developers can inject variables, functions, or any valid JavaScript expression into JSX. This dynamic behavior is fundamental to creating responsive, interactive, and data-aware React components that adapt to varying conditions and user interactions.
JSX Expressions & Embedding

---


### Components in React
  <img data-src="assets/react-tree.png" />
Note: React applications are built using components, which are self-contained, reusable pieces of code responsible for a specific part of the user interface. Components can be functional or class-based, and they encapsulate both the UI and the logic associated with it.

---
### Class components
```js
class MyClassComponent extends React.Component {
  constructor(props) {
    super(props);
    // Component state initialization
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
Note: Class components are the traditional way of creating React components. They extend the React.Component class and have access to lifecycle methods, allowing developers to manage state and perform actions at various stages of a component's lifecycle.

---
### Functional components
```js
const MyFunctionalComponent = () => {
  // Component logic here
  return (
    <div>
      {/* JSX content */}
    </div>
  );
};
```
---
Note: Functional components are the building blocks of a React application. They are concise, stateless, and focus solely on rendering UI. With the advent of React Hooks, functional components can now also manage state and lifecycle events, blurring the line between functional and class-based components.

---

### Props and Prop Types
```js
const User = ({ username }) => {
    return <div><h1>{username}</h1></div>;
}
// Prop Types
User.propTypes = {
  username: PropTypes.string.isRequired,
};
```

Note: In React, data can be passed from a parent component to a child component using props. Props are essentially properties that a parent component passes down to its children. Additionally, specifying PropTypes helps enforce data types and ensures the correct usage of props.


---

### TSX
```js
const User = ({ username }) => {
    return <div><h1>{username}</h1></div>;
}
```

```ts
const User = ({ username } 
    : { username: string}) => {
    return <div><h1>{username}</h1></div>;
}
```
<!-- .element: class="fragment" -->
--
### TSX
```js
const User = ({ username }) => {
    return <div><h1>{username}</h1></div>;
}
// Prop Types
User.propTypes = {
  username: PropTypes.string.isRequired,
};
```

```ts
function User(props: UserProps ) {
    return <div><h1>{props.username}</h1></div>;
}
type UserProps = { username: string };
```
<!-- .element: class="fragment" -->
```ts
const User: React.FC<UserProps> = ({username}) => {
    return <div><h1>{username}</h1></div>;
};
type UserProps = { username: string};
```
<!-- .element: class="fragment" -->

Note: In javascript you can dynamically design the props being passed in by naming them.

In Typscript you end up repaeting yourself if you are desingin your props in the component file

But the real value is if you pull the props into it's own object, ans then you can share it amonst multiple areas as well as give your IDE more clues on what the object contains.

---
```ts
type UserProps = { username: string};
const User: React.FC<UserProps> = ({username, children}) => {
    return <div>
        <h1>{username}</h1>
        <div>{children}</div>
    </div>;
};
```
<!-- .element: class="fragment" -->
```ts
type UserProps = { 
    username: string, 
    children: React.ReactNode
};
const User({username, children}: UserProps) {
    return <div>
        <h1>{username}</h1>
        <div>{children}</div>
    </div>;
};
```
<!-- .element: class="fragment" -->

2 different ways you can include thingsm notice there's using React.FC (React Function Component), or you can use raw objetcs as props.
---
### State in class components
```js
class CounterClass extends React.Component {
  constructor(props) {
    super(props);
    this.state = { count: 0 };
  }

  increment = () => {
    this.setState({ count: this.state.count + 1 });
  };

  render() {
    return (
      <div>
        <p>Count: {this.state.count}</p>
        <button onClick={this.increment}>Increment</button>
      </div>
    );
  }
}
```
Note: Goign back to class components, it often makes sense why developers reach for them. Classes like to retain state, theresfor you get the beneifts of simplyfying the codebase because you can mutate objects.

In class components, state is managed using the setState method. Understanding how to correctly update state is crucial for React developers. It ensures that the UI reflects the latest data and triggers necessary re-renders.
---
### State in React
```js
const Counter = () => {
  const [count, setCount] = useState(0);

  const increment = () => {
    setCount(count + 1);
  };

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={increment}>Increment</button>
    </div>
  );
};
```
Note: While props are used to pass data between components, state is used to manage a component's internal data. State allows components to react to user input, events, or changes in data, leading to dynamic and interactive user interfaces.
---

### useState Hook
<!-- .slide: data-auto-animate="true" -->
```js
const [state, setState] = useState(initialState);
```
<!-- .element: data-id="code-animation" -->
Note: Introduced in React Hooks, the useState hook is a powerful tool for managing state in functional components. It allows functional components to have stateful logic without the need for class components. The hook returns the current state and a function to update it.
---
<!-- .slide: data-auto-animate="true" -->
### useState Hook
```js
const [state, setState] = useState<number>(initialState);
```
<!-- .element: data-id="code-animation" -->
---
<!-- .slide: data-auto-animate="true" -->
### useState Hook
```js
const [state, setState] = useState<string>(initialState);
```
<!-- .element: data-id="code-animation" -->
---
<!-- .slide: data-auto-animate="true" -->
### useState Hook
```js
const [state, setState] = useState<MyType>(initialState);
interface MyType {
    age: number;
    name: string;
}
```
<!-- .element: data-id="code-animation" -->
---
## Handling Events

Note: React provides a straightforward way to handle events, such as clicks or input changes. Event handlers are assigned as attributes in JSX, and they can invoke functions that update state or perform other actions, creating a responsive and interactive user experience.
---

### onClick & Others

```js
const handleClick = (event) => {
  console.log('Button clicked!', event.target);
};

<button onClick={handleClick}>Click me</button>
```

Note: The onClick event attribute is a common way to handle click events. React supports a range of event attributes, such as onChange for input changes and onSubmit for form submissions. Understanding these attributes is crucial for building interactive user interfaces.

React uses camelCase for event names, such as onClick instead of onclick. Event handlers receive synthetic events with properties like target and currentTarget.
---
### Conditional Rendering

Note: Conditional rendering allows components to display different content based on certain conditions. This flexibility is essential for creating dynamic and interactive user interfaces.
Conditional Rendering
---
<!-- .slide: data-auto-animate="true" -->
### Conditional Rendering Basics
```js
const ConditionalComponent = ({ isLoggedIn }) => {
  if (isLoggedIn) {
    return (
      <div>
        <p>Welcome, User!</p>
      </div>
    );
  }
};
```
<!-- .element: data-id="code-animation" -->
Note: In React, conditional rendering is achieved using JavaScript expressions within JSX. This enables components to adapt their output based on the current state or props.


While JSX doesn't support traditional if statements, you can use ternary operators or logical && operators for conditional rendering.
---
<!-- .slide: data-auto-animate="true" -->
### Conditional Rendering Basics
```js
const ConditionalComponent = ({ isLoggedIn }) => {
  return (
    <div>
      {isLoggedIn && 
        <p>Welcome, User!</p>}

    </div>
  );
};
```
<!-- .element: data-id="code-animation" -->
Note: You can move the logic inline by using a logical and. Here it checks a boolean on the left and then if it's there it will render the Welcome user message.
---
<!-- .slide: data-auto-animate="true" -->
### Conditional Rendering Basics
```js
const ConditionalComponent = ({ isLoggedIn }) => {
  return (
    <div>
      {isLoggedIn ? 
        <p>Welcome, User!</p> :
        <p>Please log in.</p>}
    </div>
  );
};
```
<!-- .element: data-id="code-animation" -->
Note: Ternary operators are commonly used for concise conditional rendering. Choose the approach that fits the readability of your code. This one adds an alternative else statement.
---
<!-- .slide: data-auto-animate="true" -->
### Conditional Rendering Basics
```js
const ConditionalComponent = ({ username }) => {
  return (
    <div>
      {!!username ? 
        <p>Welcome, {username}!</p> :
        <p>Please log in.</p>}
    </div>
  );
};
```
Note: Now consider it's a username if it's logged in (or blank if it's not logged in). You can use the truthy comparison to ensure the name matches and display a personalised welcome message.
<!-- .element: data-id="code-animation" -->
---

## Lists & Keys

Note: Lists are a fundamental part of many user interfaces. React provides efficient ways to render lists and a mechanism called keys to optimize the performance of list updates.
Lists and Keys

---
### Rendering Lists
```js
const MyList = ({ items }) => {
  return (
    <ul>
      {items.map((item) => (
        <li key={item.id}>{item.name}</li>
      ))}
    </ul>
  );
};
```
Note: React enables dynamic rendering of lists by mapping over an array of data. This approach ensures that the UI updates automatically when the underlying data changes.


Keys are special attributes that provide a unique identity to list items. They help React identify which items have changed, been added, or removed, facilitating efficient updates.
Keys in React Lists
---
### Dynamic Lists and Methods

```js
const FilteredList = ({ items, filterTerm }) => {
  const filteredItems = items.filter((item) =>
    item.name.toLowerCase().includes(filterTerm.toLowerCase())
  );

  return (
    <ul>
      {filteredItems.map((item) => (
        <li key={item.id}>{item.name}</li>
      ))}
    </ul>
  );
};
```
Note: JavaScript array methods like map(), filter(), and reduce() play a crucial role in working with dynamic lists in React. Understanding these methods enhances your ability to manipulate and render data.
---
### Fragments in React
```js
const MyComponent = () => {
  return (
    <>
      <p>First paragraph</p>
      <p>Second paragraph</p>
    </>
  );
};
```
Note: Fragments are a way to group multiple elements without introducing an additional parent element to the DOM. They help keep the HTML structure clean when rendering multiple components.
Fragments in React

Styling in React

Styling is an essential aspect of creating visually appealing React applications. React supports various styling approaches, including inline styles, class-based styling, and CSS modules.
Styling in React
---
### Inline Styles in React
```js
const MyComponent = ({ isHighlighted }) => {
  const styles = {
    color: isHighlighted ? 'red' : 'black',
    fontSize: '16px',
  };

  return <div style={styles}>Styled Content</div>;
};
```
Note: React allows the use of inline styles directly within the JSX. This approach is convenient for small-scale styling and dynamic style changes based on component state or props.



---
### Class Based Styling
styles.module.css
```css
.myComponent {
  color: blue;
  font-size: 18px;
}
```
MyComponent.jsx
```js
import styles from './styles.module.css';

const MyComponent = () => {
  return <div className={styles.myComponent}>Styled Content</div>;
};
```

Note: For larger applications, organizing styles into separate CSS files and using class-based styling or CSS modules becomes beneficial. This promotes better maintainability and separation of concerns.

--
## Functional Components

Functional components, introduced in React with Hooks, provide a more concise and expressive way to write components. Hooks, such as useState and useEffect, enable stateful logic in functional components.

---
### Functional Benefits
Functional components are easier to read, write, and test. They encourage a functional programming style and make it simpler to reason about the component's behavior.

```js
const MyFunctionalComponent = () => {
  const [count, setCount] = useState(0);

  useEffect(() => {
    // Effect to run after each render
  }, [count]);

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
};
```
---
### useState Hook
```js
const [count, setCount] = useState(0);
```
Returns a 2 length tuple with
- The current state value
- A function that allows you to update the state

Note: The useState hook is used to introduce state in functional components. It returns an array with two elements:
The current state value.
A function that allows you to update the state.
---
```js
//useEffect
useEffect(() => {
  // Effect to run after each render
  return () => {
    // Cleanup function (optional)
  };
}, [dependencies]);
```
Note: The useEffect hook is employed for handling side effects in functional components. It runs after every render and replaces lifecycle methods like componentDidMount and componentDidUpdate in traditional class components.

Dependencies Array: The second parameter, an array of dependencies, controls when the effect runs. If dependencies change, the effect runs again.
Cleanup Function: The optional cleanup function runs before the next effect or when the component unmounts.
useEffect Hook

---
```js
//User function component
const [userID, setUserID] = useState("");
const [userProfile, setUserProfile] = useState({});

(async function getUserProfile() => {
  const res = await fetch(`/user/${userID}`, {signal});
  setUserProfile(res.profile));
})();
```
```js
const [userID, setUserID] = useState("");
const [userProfile, setUserProfile] = useState({});

useEffect(() => {

  (async function getUserProfile() => {
    const res = await fetch(`/user/${userID}`);
    setUserProfile(res.profile));
  })();

}, [userID]);
```

```js
const [userID, setUserID] = useState("");
const [userProfile, setUserProfile] = useState({});
useEffect(() => {
  const controller = new AbortController();
  const signal = controller.signal;

  (async function getUserProfile() => {
    const res = await fetch(`/user/${userID}`, {signal});
    setUserProfile(res.profile));
  })();

  return () => {
    controller.abort();
  }
}, [userID]);
```
---
### useRef Hook
```js
import { useRef, useEffect } from 'react';

const MyComponent = () => {
  const inputRef = useRef(null);

  useEffect(() => {
    // Focus on the input element after render
    inputRef.current.focus();
  }, []);

  return <input ref={inputRef} />;
};
```
Note: The useRef hook creates a mutable object called a "ref object" that persists across renders. It's commonly used to access and interact with DOM elements or to persist values without triggering re-renders.

In general - useState if you want to re-render the component when it changes, otherwise use useRef. IE - storing a value that must not re-render the component, or something that should remain constant.
---
### useContent Hook
```js
const MyComponent = () => {
  const contextValue = useContext(MyContext);

  // Access contextValue and render component logic
};
```
Note: The useContext hook is used to consume values from the React context. It provides a way to share values (like themes, user data, etc.) between components without passing props manually.
Key Points:
useContext simplifies context consumption in functional components.
It's particularly useful for avoiding prop drilling in deeply nested components.
---
### useContext Hook

Key Points:
- createContext creates a context object.
- Provider component wraps the part of the tree where the context is available.
- useContext hooks into the context within functional components.
```js
const MyContext = React.createContext();
```
```js
const MyProvider = ({ children }) => {
  const contextValue = // some value;
  return (
    <MyContext.Provider value={contextValue}>
      {children}
    </MyContext.Provider>
  );
};
```
```js
const MyComponent = () => {
  const contextValue = useContext(MyContext);
  // Access contextValue and render component logic
};
```
---

## React Router

React Router is a popular library for handling navigation and routing in React applications. It enables the creation of single-page applications with multiple views.
---


### Intro to React Router

```js
import { BrowserRouter as Router, Route } from 'react-router-dom';

const App = () => {
  return (
    <Router>
      <Route path="/home" component={Home} />
      <Route path="/about" component={About} />
    </Router>
  );
};
```
Note: React Router provides a <BrowserRouter> component and <Route> components to define different views for different paths. This enables seamless navigation without a page refresh.

Defining routes involves mapping paths to specific components. The Route component renders the specified component when the path matches.
---
### Parameters and Query
```
import { BrowserRouter as Router, Route } from 'react-router-dom';

const UserProfile = ({ match }) => {
  const userId = match.params.userId;
  // Access userId and render user profile
};

const App = () => {
  return (
    <Router>
      <Route path="/user/:userId" component={UserProfile} />
    </Router>
  );
};
```
Note: React Router allows the use of parameters in the URL and accessing them within components. Additionally, query strings can be utilized for dynamic data.

### Navigation and Linking
```js
import { Link } from 'react-router-dom';

const Navigation = () => {
  return (
    <nav>
      <Link to="/">Home</Link>
      <Link to="/about">About</Link>
      <Link to="/contact">Contact</Link>
    </nav>
  );
};
```
Note: React Router provides the <Link> component to create links between different views. This ensures a smooth and consistent user experience without full page reloads.

