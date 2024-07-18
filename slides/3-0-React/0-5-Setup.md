### The Setup
We will step through some activities to setup TypeScript in a brand new project.
---
### Initializing a New Project
Go into the parent directory for a brand new project and run this...

```
npx create-react-app@latest react-learning --template typescript
```

<div markdown=1>

This will setup a good bare-bones template. 

[Other ones](https://react.dev/learn/start-a-new-react-project) are available

</div> <!-- .element: class="fragment" -->

Note: Remeber all that stuff we did last time? Well React is a bit nicer. First we use NPX - this was a tool we used last time to create one of the config files. Can anyone remeber what NPX does?

It's Node Package eXecute. It allows dves to execute packages on the NPM registery without even installing it.

---
### Observe

What do you notice about this file?

```bash
package.json
```

Note: Now let's go into the package.json. What do you notice?

Quite nice - 4 scripts in there. Some packages, some typings.

What about Node Modules?

870 items? The last one was 273!

Wow.
---
![Heaviest objects in the universe](./assets/node_modules.png)
---
### Test the project
---
```
npm run test
```

<div markdown=1>

# OH NO!

```
  console.error
    Warning: `ReactDOMTestUtils.act` is deprecated in favor of `React.act`. Import `act` from `react` instead of `react-dom/test-utils`. See https://react.dev/warnings/react-dom-test-utils for more info.
```

</div> <!-- .element: class="fragment" -->
---

### Update modules (interactive)

```
npx npm-check-updates -i
```
<div markdown=1>

Find these modules

```
@testing-library/jest-dom
@testing-library/react
@testing-library/user-event
@types/jest
```

</div>

---
### Test the project (again)
---

```
npm run test
```

---
# ALRIGHT!
---
### Run the application

```
npm run start
```
---
### Edit the page
---
# Challenge

Can you make the logo spin the other way?