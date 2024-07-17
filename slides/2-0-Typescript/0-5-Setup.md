### The Setup
We will step through some activites to setup TypeScript in a brand new project.
---
### Initializing a New Project
```
npm init
```
<div markdown=1>
Answer the questions until...

```
entry point: (index.js) index.ts
```
</div>
<!-- .element: class="fragment" -->

<div markdown=1>
Did you spot the new file?

```bash
package.json
```
</div>
<!-- .element: class="fragment" -->

Note: Open your terminal in the folder you want to create a project in. You will be asked with a few questions. This command initializes a new Node.js project and creates a package.json file for you.

For the entry point question please change it to `index.ts`

This will have generated a single file in the directory called `package.json`. The contents will contain the answers you just provided, You can edit this at any time.
---
### Install Typescript

```
npm install typescript --save-dev
```

<div markdown=1>
This added a new folder

```bash
node_modules
```
</div>
<!-- .element: class="fragment" -->

Note: Now we want to install Typescript. You can do this using this command. This calls NPM (Sometimes mistakenly refrerred to as Node Package Manager) and asks it to install "Typescript" in the project. The Save-Dev bit means it should be treated as a dveelopment library not something that gets downloaded to the user.

If you check the package.json you'll see it now references the library and you'll also see a node_moduels folder has appeared.

Node Modules is like DLL library. You can normally delete it and run `npm i` to get everything re-installed. 
---
### Setup Typescript

Go into `package.json` and add a reference to the typescript compiler.

```
  "scripts": {
    "tsc:init": "tsc --init",
    "tsc": "tsc"
  },
```
<div markdown=1>

Now in the terminal run 

```
npm run tsc:init
```
</div>
<!-- .element: class="fragment" -->

Note: We need to add some scripts to the package.json. These are basically commandline shortcuts.

What they will do is allow us to use the command `npm run...` and it will run a binary file that sits in /node_modules/bin

Go have a look in there, you'll see a binary called "tsc". This is an application that compiles typescript into javascript. (TypeScript Compiler)

Go ahead and run tsc:init - you'll see a new file called tsconfig.json get configuered. This is the default typescript setup and it allows us to make a custom comilation rules for typescript.
---
### Finetune the compiler
Change the following settings on tsconfig.json
```
{
  ...
  "compilerOptions": {
    ...
    "target": "ESNext",
    ...
  },
  "rootDir": "./src",
  "outDir": "./dist",
  ...
}
```
Note: We want to have a separate directory from the source and the output info.

We also want to use the very latest language features.
---
### Create a typescript file
In Visual Studio Code create a new file called 

```
src/index.ts
```
<div markdown=1>
Add the following

```
const message:string = 'Welcome from AND!'
export function getMessage(): string {
    return message;
}
console.log(getMessage())
```
</div>
<!-- .element: class="fragment" -->


Note: The src/ autmatically creates the source file.
Now create a folder named src and inside, create a file index.ts inside the src folder with the following code:
const message: string = 'Welcome from AND'.
---
### Compile typescript

```
npm run tsc
```
<div markdown=1>

Check the `src` directory and see a new file `index.js`

```
"use strict";
Object.defineProperty(exports, "__esModule", { value: true });
exports.getMessage = getMessage;
const message = 'Welcome from AND!';
function getMessage() {
    return message;
}
console.log(getMessage());
```

What do you notice?
</div>
<!-- .element: class="fragment" -->



Note: 
You should notice that the new file is almost identical to the TS file. It doesn't have the typing. It also has a semicolon `;` and "use strict" at the top.

These are all little javascript language fetaures to be strict (and performant) javascript.

It also has created a module.

---
### Run a node application

```
node dist/index.js
```
<div markdown=1>

The terminal says
```
"Welcome from AND"
```
</div>
<!-- .element: class="fragment" -->
Note: Node is a backend server that allows you to run node applications written in Javascript. You can run this application.

This is fine, but it requires us to compile the javascript and then re-run the application. What if we could auotmate this?
---
### Install a typescript server

```
npm install ts-node --save-dev
```

<div markdown=1>

Now edit `package.config`

```
"scripts": {
  ...
  "tsnode": "ts-node src/index.ts"
}
```
</div>
<!-- .element: class="fragment" -->

<div markdown=1>
Run the app directly from typescript

```
npm run tsnode
```
</div>
<!-- .element: class="fragment" -->

Note:
Node is a backend server that allows you to run node applications written in Javascript. 

TS-Node is an execution engine for typescript. It JIT tansforms TS to JS, enabling you to directly execute Typescript on Node without pre-compiling.

You can even delete the output directory - it's just using the source files now!

Try chaning the message in typescript and the re-running the command.
---
### Auto-run on change


```
npm install nodemon --save-dev
```

<div markdown=1>

Then create a new file `nodemon.json`

```
{
  "execMap": {
    "ts": "ts-node"
  }
}
```
</div>
<!-- .element: class="fragment" -->

<div markdown=1>

Next edit `package.json`

```
"scripts": {
  "dev": "nodemon src/index.ts"
}
```
</div>
<!-- .element: class="fragment" -->

<div markdown=1>
Finally run it

```
npm run dev
```
</div>
<!-- .element: class="fragment" -->
Note: Go and play with index.ts
---
### ESLint

```
npm install eslint @typescript-eslint/parser @typescript-eslint/eslint-plugin --save-dev
```

<div markdown=1>

Create an `.eslintrc.js` file and add

```
/* eslint-env node */
module.exports = {
  env: {
    node: true,
  },
  extends: ['plugin:@typescript-eslint/recommended', 'eslint:recommended'],
  parser: '@typescript-eslint/parser',
  plugins: ['@typescript-eslint'],
  root: true,
}
```
</div>
<!-- .element: class="fragment" -->


<div markdown=1>

Finally add to `package.json`

```
    "scripts": {
        ...,
        "lint": "eslint ./src/**/.ts"
    }
```

</div>
<!-- .element: class="fragment" -->

Note: Setting up ESLint for TypeScript
Linting is essential for maintaining code quality. Install ESLint and its TypeScript parser
You may want to ignore the dist folder because your editor's ESLint plugin may still be highligthing errors from it. For that, create an .eslintignore file and add the entry dist to it.
It's worth mentioning you can also install the ESLint extension in VSCode which is from Microsoft and will honour yout `eslintrc` file.
---
### Testing Setup

```
npm install jest ts-jest @types/jest --save-dev
npx ts-jest config:init
```
<div markdown=1>

Also edit `.eslintrc.js`

```
module.exports = {
  env: {
    node: true,
    jest: true, // <-- Add this
  },
```
</div>
<!-- .element: class="fragment" -->

Note: Integrating Jest for Testing
Jest is fantastic for testing TypeScript projects. Install it by running
Create a jest configuration by running the following command:
The above command allows Jest to work with TypeScript.

---
### Testing Code

```
//src/index.test.ts
import { getMessage } from './index'

describe('getMessage()', () => {
  it('should return the correct message when called', () => {
    expect(getMessage()).toBe('Welcome from AND!')
  })
})
```

<div markdown=1>

Finally update the `package.json`

```
 "scripts": {
    ...,
    "test": "jest",
    "test:watch": "jest --watchAll"
  }
```

</div>
<!-- .element: class="fragment" -->   

<div markdown=1>
And run it

```
npm run test:watch
```

</div>
<!-- .element: class="fragment" -->  
Note:

Create a file named `index.test.ts` inside the src folder. Add the following code to it:


--watch is not supported without git/hg, please use --watchAll - it needs to be git or you need watchall.

---

### Debugging in VSCode
Create a `launch.json` to allow debugging from VSCode
```
{
  "version": "0.2.0",
  "configurations": [
    {
      "name": "dev",
      "request": "launch",
      "runtimeArgs": ["run", "dev"],
      "runtimeExecutable": "npm",
      "skipFiles": ["<node_internals>/**"],
      "type": "node"
    },
    {
      "name": "test",
      "request": "launch",
      "runtimeArgs": ["run", "test:watch"],
      "runtimeExecutable": "npm",
      "skipFiles": ["<node_internals>/**"],
      "type": "node"
    }
  ]
}
```
Note:
Debugging TypeScript in VSCode is straightforward. Just hit F5 after configuring your launch.json appropriately. You can go in the debugging panel to edit the launch.json. Or create a new folder named .vscode in the project. And inside the .vscode folder, create a launch.json file with the following content:

---
# Phew!
