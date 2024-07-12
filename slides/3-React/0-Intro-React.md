
React Server Components (RSC) overview
Most of us will be familiar with NextJS’s getServerSideProps function.
GetServerSideProps is a NextJS function that can be used to fetch data and render the contents of a page at request time.
RSC’s replace and enhance this concept by allowing you to fetch from the data layer directly from any given RSC. 
This is extremely powerful as it:
Reduces boilerplate
Guarantees type safety
Allows you to directly fetch from the data layer from (nearly) anywhere in the React Component Tree
This has gone too deep too soon
Now that we have our full infrastructure set up, we’ll start developing our Next JS app.
To do that we need to understand one of the fundamental features Next 14 provides which are “React Server Components”
In prior versions of Next to fetch from the data layer server side, you would use getServerSideProps.
RSC’s essentially replace that and allow you to do this in the same function as your HTML response.
This reduces boilerplate, guarantees type safety and allows you to perform server operations from nearly anywhere in the React Component Tree rather than only at the top of your page.

Objectives
Understand the fundamentals of React.
Build a solid foundation for advanced concepts.
Develop practical skills through exercises.

Day One: Fundamentals
Day Two: Advanced Theory & Coding
Day Three: React Challenge





In this file, you’ll see all the instructions for what you need to implement. Add your code and run the jest command to have it run the tests.

Introduction to React

React is a JavaScript / TypeScript framework that lets you build user interfaces out of individual pieces called components.

You can create components like Button, Thumbnail and others; then combine them into screens, pages and entire applications.
Introduction to React

It’s widely used in building single-page applications, utilises a component based architecture. What this means is that a UI is constructed from reusable building blocks.
Introduction to React
React was initially developed by Facebook; and is declarative, efficient and flexible.

Advantages of using React

React distinguishes itself through several key features:
Virtual DOM: React's efficient Virtual DOM minimizes direct manipulation of the actual DOM, enhancing performance by reducing unnecessary updates.

Declarative Syntax: With a declarative syntax, React makes code more readable and less prone to bugs, enabling developers to focus on the "what" rather than the "how."

Component-Based: The component-based architecture promotes reusability, maintainability, and scalability, making it an ideal choice for complex UI development.

Advantages of using React

Basics of JSX
Have a live codable example where people can play

JSX (JavaScript XML) serves as a syntax extension for JavaScript in React. It allows developers to write UI components using a syntax that resembles HTML but is ultimately transpiled to JavaScript. JSX enhances code readability and expressiveness, making it an integral part of React development.
Understanding JSX Syntax

While JSX bears a resemblance to HTML, it's crucial to understand the distinctions. JSX introduces the ability to embed dynamic content through JavaScript expressions enclosed in curly braces {}. This dynamic nature empowers developers to create highly interactive and data-driven React components, blending the best of both worlds.
JSX vs HTML

JSX goes beyond static markup; it supports the embedding of JavaScript expressions directly within the markup. By enclosing expressions in curly braces {}, developers can inject variables, functions, or any valid JavaScript expression into JSX. This dynamic behavior is fundamental to creating responsive, interactive, and data-aware React components that adapt to varying conditions and user interactions.
JSX Expressions & Embedding

5 Minute Break

Components in React

React applications are built using components, which are self-contained, reusable pieces of code responsible for a specific part of the user interface. Components can be functional or class-based, and they encapsulate both the UI and the logic associated with it.
Components in React

Class components are the traditional way of creating React components. They extend the React.Component class and have access to lifecycle methods, allowing developers to manage state and perform actions at various stages of a component's lifecycle.
Class Components

Functional components are the building blocks of a React application. They are concise, stateless, and focus solely on rendering UI. With the advent of React Hooks, functional components can now also manage state and lifecycle events, blurring the line between functional and class-based components.
Functional Components

In React, data can be passed from a parent component to a child component using props. Props are essentially properties that a parent component passes down to its children. Additionally, specifying PropTypes helps enforce data types and ensures the correct usage of props.
Props and Prop Types

State in React

While props are used to pass data between components, state is used to manage a component's internal data. State allows components to react to user input, events, or changes in data, leading to dynamic and interactive user interfaces.
Introduction to State

Introduced in React Hooks, the useState hook is a powerful tool for managing state in functional components. It allows functional components to have stateful logic without the need for class components. The hook returns the current state and a function to update it.
useState Hook

In class components, state is managed using the setState method. Understanding how to correctly update state is crucial for React developers. It ensures that the UI reflects the latest data and triggers necessary re-renders.
State in Class Components

5 Minute Break

Handling Events

React provides a straightforward way to handle events, such as clicks or input changes. Event handlers are assigned as attributes in JSX, and they can invoke functions that update state or perform other actions, creating a responsive and interactive user experience.
Handling Events

The onClick event attribute is a common way to handle click events. React supports a range of event attributes, such as onChange for input changes and onSubmit for form submissions. Understanding these attributes is crucial for building interactive user interfaces.
onClick & Others

React uses camelCase for event names, such as onClick instead of onclick. Event handlers receive synthetic events with properties like target and currentTarget.
Binding Event Handlers

Conditional Rendering

Conditional rendering allows components to display different content based on certain conditions. This flexibility is essential for creating dynamic and interactive user interfaces.
Conditional Rendering

In React, conditional rendering is achieved using JavaScript expressions within JSX. This enables components to adapt their output based on the current state or props.
Conditional Rendering Basics

While JSX doesn't support traditional if statements, you can use ternary operators or logical && operators for conditional rendering.
If Statements in JSX

Ternary operators and logical && operators are commonly used for concise conditional rendering. Choose the approach that fits the readability of your code.
Conditional Operators

Lists & Keys

Lists are a fundamental part of many user interfaces. React provides efficient ways to render lists and a mechanism called keys to optimize the performance of list updates.
Lists and Keys

React enables dynamic rendering of lists by mapping over an array of data. This approach ensures that the UI updates automatically when the underlying data changes.
Rendering Lists

Keys are special attributes that provide a unique identity to list items. They help React identify which items have changed, been added, or removed, facilitating efficient updates.
Keys in React Lists

JavaScript array methods like map(), filter(), and reduce() play a crucial role in working with dynamic lists in React. Understanding these methods enhances your ability to manipulate and render data.
Dynamic Lists and Methods

5 Minute Break

Fragments in React

Fragments are a way to group multiple elements without introducing an additional parent element to the DOM. They help keep the HTML structure clean when rendering multiple components.
Fragments in React

Styling in React

Styling is an essential aspect of creating visually appealing React applications. React supports various styling approaches, including inline styles, class-based styling, and CSS modules.
Styling in React

React allows the use of inline styles directly within the JSX. This approach is convenient for small-scale styling and dynamic style changes based on component state or props.
Inline Styles in React

For larger applications, organizing styles into separate CSS files and using class-based styling or CSS modules becomes beneficial. This promotes better maintainability and separation of concerns.
Class Based Styling

Functional Components

Functional components, introduced in React with Hooks, provide a more concise and expressive way to write components. Hooks, such as useState and useEffect, enable stateful logic in functional components.
Functional Components

Functional components are easier to read, write, and test. They encourage a functional programming style and make it simpler to reason about the component's behavior.
Functional Benefits

The useState hook is used to introduce state in functional components. It returns an array with two elements:
The current state value.
A function that allows you to update the state.
useState Hook

The useEffect hook is employed for handling side effects in functional components. It runs after every render and replaces lifecycle methods like componentDidMount and componentDidUpdate in traditional class components.
Dependencies Array: The second parameter, an array of dependencies, controls when the effect runs. If dependencies change, the effect runs again.
Cleanup Function: The optional cleanup function runs before the next effect or when the component unmounts.
useEffect Hook

The useRef hook creates a mutable object called a "ref object" that persists across renders. It's commonly used to access and interact with DOM elements or to persist values without triggering re-renders.
useRef Hook

The useContext hook is used to consume values from the React context. It provides a way to share values (like themes, user data, etc.) between components without passing props manually.
Key Points:
useContext simplifies context consumption in functional components.
It's particularly useful for avoiding prop drilling in deeply nested components.

useContext Hook

Key Points:
createContext creates a context object.
Provider component wraps the part of the tree where the context is available.
useContext hooks into the context within functional components.
Creating & Using Context

5 Minute Break

React Router

React Router is a popular library for handling navigation and routing in React applications. It enables the creation of single-page applications with multiple views.
React Router

React Router provides a <BrowserRouter> component and <Route> components to define different views for different paths. This enables seamless navigation without a page refresh.
Intro to React Router

Defining routes involves mapping paths to specific components. The Route component renders the specified component when the path matches.
Setting up Routes

React Router allows the use of parameters in the URL and accessing them within components. Additionally, query strings can be utilized for dynamic data.
Parameters and Query

React Router provides the <Link> component to create links between different views. This ensures a smooth and consistent user experience without full page reloads.
Navigation and Linking

User Interface Best Practices
From ISOS coding standards

Component Structure and Organization 
a. Use a modular component-based architecture to promote code reusability and maintainability. 
b. Group related components together in separate directories or folders. We are following a "feature-first" approach for folder structure to improve maintainability and scalability. Folder structure of the application will look like below. 
c. Split larger components into smaller, reusable components for easier maintenance and testing. 
d. Follow naming conventions that reflect component functionality and purpose. 
e. We have organized our project structure logically by separating components, styles, and utility functions. Follow single responsibility principle.
e. We have organized our project structure logically by separating components, styles, and utility functions. Follow single responsibility principle.

Micro frontends 
a. We are following micro frontend architecture. screens are divided based on features.
b. All micro frontends related to the features will be wrapped inside container frontend (i.e. messages and message-preview micro frontend will be wrapped inside messages-container and will be hosted on S3 and CloudFront. This will keep micro frontends loosely coupled.

Functional Components
a. We prefer using functional components over class components. b. Functional components are simpler, easier to read, and promote better performance.

State Management
a. We are utilizing a state management library redux-toolkit and redux-saga for managing centralized application state.
b. Normalize and organize the state structure to ensure a predictable and efficient data flow.
c. Try to avoid unnecessary or excessive use of global state; prefer local component state when applicable.
d. We are using re-select library for memorization techniques to optimize state updates which will eventually enhance the performance of our application to a significant amount by reducing unnecessary re-renders on the DOM.


TypeScript
a. We are using TypeScript for type-checking and static typing in the project.
b. TypeScript helps catch potential errors early and improves code reliability and maintainability


Performance Optimization
a. Leverage techniques like React.memo to avoid unnecessary re-renders and enhance performance.
b. Optimize performance by leveraging techniques like lazy loading and code splitting.
c. Use progressive web app-Workbook.
d. Verification of Core web vitals.

Code Formatting and Styling
a. For consistent code formatting and indentation, we are using Prettier and eslint.
b. Use meaningful and descriptive variable and function names to enhance code readability.
c. We have adopted a CSS-in-JS solution like styled-components which offers several benefits like Component-based Styling,
Elimination of Class Name Collisions, Dynamic and Responsive Styling and Better Performance.
d. pre-commit hooks have been added. Don’t use ignore rules while committing code.
e. We are using MaterialUI library for the components (like button, label etc), theme and styling.

Data Fetching and APIs
a. Encapsulate data fetching logic within separate service or utility functions to promote reusability and separation of concerns.
b. Use async/await or Promise based syntax for handling asynchronous operations.
c. Handle API errors gracefully and provide appropriate feedback to users.
d. Cache API responses, when possible, to reduce unnecessary network requests using React-Query.


Error Handling
a. Implement error boundaries to catch and handle errors in component trees, preventing the application from crashing.
b. Provide meaningful error messages or fallback UI to guide users in case of failures.


Testing
a. Write comprehensive unit tests using frameworks like Jest and React Testing Library.
b. Test component rendering, user interactions, and data visible on the DOM.
c. Aim for high test coverage to ensure stability and prevent regressions.


Accessibility
a. Follow accessibility guidelines and standards (e.g., WCAG (Web Content Accessibility Guidelines) 2.1 AA) when developing UI
components. More details here.
b. Use proper semantic HTML elements to enhance accessibility.
c. Test for keyboard navigation and ensure screen reader compatibility.
d. Provide alternative text for images and captions for multimedia content.

12. Tooling
a. We are using webpack to bundle the application.
b. We are creating micro frontends using module federation plugin of webpack.
c. We are using storybook to document the components.