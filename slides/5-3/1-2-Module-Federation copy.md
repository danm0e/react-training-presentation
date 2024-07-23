# Module Federation
---
### What is Module Federation?

- Share code across javascript applications at runtime<!-- .element: class="fragment" -->
- Allows Microfrontends<!-- .element: class="fragment" -->
Note:
- Allows different JavaScript applications to dynamically share code with each other at runtime.
- enables the creation of a micro-frontend architecture, where multiple independent frontend applications can be composed into a single cohesive user experience.

---

![alt text](./assets/module-federation.png)


---

# [Example](https://stackblitz.com/~/github.com/digiguru/module-federation-example?file=aboutusapp/src/App.js)<!-- .element: target="_blank" -->
Note: Do we have other examples?
---

<div class="container">
<div class="col" markdown="1">

### 😄 Nice

- Team autonomy<!-- .element: class="fragment" -->
- Progressive refactoring<!-- .element: class="fragment" -->
- Distributed approach<!-- .element: class="fragment" -->
- Clearer boundaries<!-- .element: class="fragment" -->
- Better code reuse<!-- .element: class="fragment" -->
- Smaller bundle sizes<!-- .element: class="fragment" -->
- Faster load times<!-- .element: class="fragment" -->
- Independant releases<!-- .element: class="fragment" -->
- Feature flagging<!-- .element: class="fragment" -->
- Enable diversity in the tech-stack<!-- .element: class="fragment" -->

</div>
<div class="col" markdown="1">

### 🤯 Nasty

- Architecture Overhead<!-- .element: class="fragment" -->
- Requires CI/CD<!-- .element: class="fragment" -->
- Resource Duplication<!-- .element: class="fragment" -->
- Inter-Microfrontend Communication<!-- .element: class="fragment" -->
- UI/UX Consistency<!-- .element: class="fragment" -->
- Learning Curve<!-- .element: class="fragment" -->
- Premature Decoupling<!-- .element: class="fragment" -->

</div>
</div>


Note:
- Tries to solve the challenge of building and maintaining large, complex frontend applications.
- Frontend monoliths can become difficult to scale and maintain as they grow in size and complexity.
- Module federation allows for a more modular and distributed approach, where different parts of an application can be developed and deployed independently.
