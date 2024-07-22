#  Best Practices
## From ISOS coding standards
---
### Component Structure and Organization 

- Use a modular component-based architecture to promote code reusability and maintainability. 
-  Group related components together in separate directories or folders. We are following a "feature-first" approach for folder structure to improve maintainability and scalability. <!-- .element: class="fragment" -->
- Split larger components into smaller, reusable components for easier maintenance and testing. <!-- .element: class="fragment" -->
- Follow naming conventions that reflect component functionality and purpose. <!-- .element: class="fragment" -->
- We have organized our project structure logically by separating components, styles, and utility functions. Follow single responsibility principle.<!-- .element: class="fragment" -->

---
![alt text](/assets/structure.png)
---

### Micro frontends 
- We are following micro frontend architecture. screens are divided based on features.
- All micro frontends related to the features will be wrapped inside container frontend (i.e. messages and message-preview micro frontend will be wrapped inside messages-container and will be hosted on S3 and CloudFront. This will keep micro frontends loosely coupled.

---
### Functional Components
- We prefer using functional components over class components. 
- Functional components are simpler, easier to read, and promote better performance.
---
### State Management
- We are utilizing a state management library redux-toolkit and redux-saga for managing centralized application state.
- Normalize and organize the state structure to ensure a predictable and efficient data flow.
- Try to avoid unnecessary or excessive use of global state; prefer local component state when applicable.
---
### TypeScript
- We are using TypeScript for type-checking and static typing in the project.
- TypeScript helps catch potential errors early and improves code reliability and maintainability
---
### Performance Optimization
- Leverage techniques like React.memo to avoid unnecessary re-renders and enhance performance.
- Optimize performance by leveraging techniques like lazy loading and code splitting.
- Use progressive web app-Workbook.
- Verification of Core web vitals.
---
### Code Formatting and Styling
- For consistent code formatting and indentation, we are using Prettier and eslint.
- Use meaningful and descriptive variable and function names to enhance code readability.
- We have adopted a CSS-in-JS solution like styled-components which offers several benefits like Component-based Styling,
Elimination of Class Name Collisions, Dynamic and Responsive Styling and Better Performance.
- pre-commit hooks have been added. Don’t use ignore rules while committing code.
- We are using MaterialUI library for the components (like button, label etc), theme and styling.
---
### Data Fetching and APIs
- Encapsulate data fetching logic within separate service or utility functions to promote reusability and separation of concerns.
- Use async/await or Promise based syntax for handling asynchronous operations.
- Handle API errors gracefully and provide appropriate feedback to users.
- Cache API responses, when possible, to reduce unnecessary network requests using React-Query.
---
### Error Handling
- Implement error boundaries to catch and handle errors in component trees, preventing the application from crashing.
- Provide meaningful error messages or fallback UI to guide users in case of failures.

---
### Testing
- Write comprehensive unit tests using frameworks like Jest and React Testing Library.
- Test component rendering, user interactions, and data visible on the DOM.
- Aim for high test coverage to ensure stability and prevent regressions.
---

### Accessibility
- Follow accessibility guidelines and standards (e.g., WCAG (Web Content Accessibility Guidelines) 2.1 AA) when developing UI
components. More details here.
- Use proper semantic HTML elements to enhance accessibility.
- Test for keyboard navigation and ensure screen reader compatibility.
- Provide alternative text for images and captions for multimedia content.
---
### Tooling
- We are using webpack to bundle the application.
- We are creating micro frontends using module federation plugin of webpack.
- We are using storybook to document the components.





