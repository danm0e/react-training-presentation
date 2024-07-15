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






### Server Components (RSC) overview

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