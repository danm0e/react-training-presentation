# React Router
---
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
```js
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
---
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
