# Welcome back!<!--.element: class="r-fit-text" -->
 
---

# Dan Moe<!--.element: class="r-fit-text" -->
<p class="r-fit-text">Product Developer <span class="andlogo">AND</span> String Plucker</p>

---

## Session 2
#### React: Digging deeper<!-- .element: class="fragment" -->

Note:
- Welcome to Session 2!
- Last time around we touched on some basics with React (Virtual DOM, components etc)
- Today we're diving deeper in to some of those concepts
- Particularly around re-rendering and practical optimisation techniques to prevent it from doing so
- Two hands-on exercises to put concepts into practice

---

### Today's agenda

- Why React re-renders
- React Fiber
- Component Lifecycle
- Hooks
- Memoisation
- **Exercise 1 & 2 - Optimisation**
- React Compiler
- Quiz?<!-- .element: class="fragment" -->

Note:
- Touched on rendering, now we discuss why it does it
- React Fiber - Rework on the reconciler algorithm (the process which updates the DOM)
- Component Lifecycle
- Hooks
- Memoisation
- 2 Exercises to go over some optimisation techniques
- React Compiler
- If we have time - Quiz

---

### Learning Agreement

- Stay focused, cameras on 🙏<!-- .element: class="fragment" -->
- We are going to be looking at code <!-- .element: class="fragment" -->
- No question is a silly question <!-- .element: class="fragment" -->

...so please ask a question whenever you like<!-- .element: class="fragment" -->

Note:
- Same expectations as Session 1
- Performance concepts can be abstract
- Exercises make concepts concrete
- Questions are encouraged!

---

## Re-rendering<!--.element: class="r-fit-text" -->
### ...yeah, but why?<!-- .element: class="fragment" -->

---

<!-- .slide: data-auto-animate="true" -->

### The Three Reasons

A component re-renders when:

- It's state changed<!-- .element: class="fragment" -->
- The context changed<!-- .element: class="fragment" -->
- It's parent re-rendered<!-- .element: class="fragment" -->
- It's props changed (if memoised)<!-- .element: class="hidden" -->

<!-- .element: data-id="code-animation" -->

Note:
- These are the ONLY reasons React re-renders
- State change: updates via the state hooks we'll go over shortly
- Context change: Any context value the component consumes
- Parent re-renders: By default, all children re-render too
- Understanding this is fundamental to optimisation

---

<!-- .slide: data-auto-animate="true" -->

### The Three Reasons

A component re-renders when:

- It's state changed
- The context changed
- ~~It's parent re-rendered~~
- It's props changed (if memoised)

<!-- .element: data-id="code-animation" -->

Note:
- The 3rd reason is replaced if we're using memoisation

---

## React's Rendering Cycle

---

#### There are three phases of a render

- Render<!-- .element: class="fragment" -->
- Commit<!-- .element: class="fragment" -->
- Cleanup<!-- .element: class="fragment" -->

Note:
- **Render** 
  - Calculate what changed, build virtual DOM, 
  - which we do in memory as it's faster than mutating the DOM and preventing repaints etc
  - once we've gone through the whole component tree we get to the commit phase
- **Commit** 
  - The virtual DOM has calculated all of the changes via diffing
  - and now we're going to actually apply those changes to real DOM 
- **Cleanup** 
  - Once we're done there...
  - Run any cleanup functions from effects
- --
- So from React 15 and earlier, the “virtual DOM” was essentially a tree of lightweight objects that mirrored the real DOM 
- Every render, React would build a fresh tree from your JSX, diff it against the previous one, and then compute a patch to apply to the actual DOM
- That whole process was synchronous and uninterruptible: once React started walking the tree, it had to finish before the browser could do anything else

---

# React Fiber

---

### What is React Fiber?

- **Core Re-implementation** \
Complete rewrite of React's rendering engine \
(React 16+)

- **Primary Goal** \
Drastically improve performance in complex applications

Note:
- Introduced in React 16
- Complete rewrite of the reconciler
- Changed how React processes component trees
- Foundation for concurrent features

---

### Key Features

- **Incremental Rendering:** Breaks work into smaller, manageable units
- **Non-Blocking:** Can pause, abort, or resume rendering work
- **Better UX:** Yields control to handle high-priority tasks like user input

Note:
- **Before Fiber**
  - React processed the entire tree in one go (blocking)
- **With Fiber**
- More like **multitasking** vs **single-threaded** execution
- Main thread stays responsive for animations and user input

---

### "Cooperatively Scheduled Rendering"

React Fiber helps prioritise DOM changes by:<!-- .element: class="fragment" -->
- Pausing current work<!-- .element: class="fragment" -->
- Checking for higher priority tasks<!-- .element: class="fragment" -->
- Resuming when appropriate<!-- .element: class="fragment" -->

Note:
- Can stop current work and handle more important tasks
- This cooperative scheduling is the secret sauce
- Enables React to keep UI responsive even during heavy computation
- **Example**
  - User typing in a search box (urgent) vs filtering a large list (can wait)

---

## Types of Re-render

---

### Necessary vs Unnecessary

**Two types of re-render in React:**

- **Necessary** 
  - State or props actually changed<!-- .element: class="fragment" -->
- **Unnecessary** 
  - Component re-renders but produces same output<!-- .element: class="fragment" -->

Note:
- **Necessary re-renders**: We can't avoid, but can prioritise
- **Unnecessary re-renders**: Nothing has changed, so this is where we might want to optimise

---

### Necessary re-renders come in two flavours

- **Urgent:** 
  - User input, animations<!-- .element: class="fragment" -->
- **Non-urgent:** 
  - Data fetching, background updates<!-- .element: class="fragment" -->

Note:
- **Urgent** ...anything that would require immediate feedback
- **Non-urgent** ...anything that could probably be deferred
- --
- Our ultimate goal for optimisation: 
  - ...eliminate unnecessary
  - ...prioritise necessary

---

# Hooks

---

### useState

```jsx
const [state, setState] = useState(initialValue);
```

Note:
- Already discussed this in session 1
- Foundation for all stateful logic
- Adds state to function components
- Returns current state and setter function
- Setter triggers re-render

---

### useReducer

```jsx
const [state, dispatch] = useReducer(reducer, initialState);

function reducer(state, action) {
  switch (action.type) {
    case 'INCREMENT':
      return { count: state.count + 1 };
    case 'DECREMENT':
      return { count: state.count - 1 };
    default:
      return state;
  }
}

// Usage
dispatch({ type: 'INCREMENT' });
```

Note:
- Expands upon useState for complex state management
- Better for state with multiple sub-values
- Better when next state depends on previous
- Dispatch function is stable (like setState)
- Redux-style pattern built into React

---

### useContext

```jsx
const ThemeContext = React.createContext('light');

function ThemedButton() {
  const theme = useContext(ThemeContext);
  return <button className={theme}>Button</button>;
}

// In parent
<ThemeContext.Provider value="dark">
  <ThemedButton />
</ThemeContext.Provider>

// ⚠️ Triggers re-renders on ALL components that consume it
```

Note:
- Removes need for prop drilling
- Access shared data across component tree
- Problem: All consumers re-render when context changes
- Even if they only use part of the context value
- --
- Lots of unnecessary renders
- Performance degradation
- Can be a problem if you have a big store
- Solution: Split into multiple contexts

---

## 🔥 👺 🔥

```jsx
  <AppContext.Provider>
    <FeatureFlag.Provider>
      <AuthContext.Provider>
        <Store.Provider>
          <LocalStorage.Provider>
            <NotificationContext.Provider>
              <ThemeContext.Provider value="dark">
                <ThemedButton />
              </ThemeContext.Provider>
            </NotificationContext.Provider>
          </LocalStorage.Provider>
        </Store.Provider>
      </AuthContext.Provider>
    </FeatureFlag.Provider>
  </AppContext.Provider>
```

Note:
- but then we get the nested provider doom tree from hell
- so you just really do need to be mindful of how you structure your app
- Context is convenient but has performance implications
- Every context value change re-renders ALL consumers
- Even if they only use one property
- Splitting contexts helps but creates nesting
- This is why Redux, Zustand, Jotai exist
- They solve the "only re-render what changed" problem

---

### useRef

```jsx
// Creates a mutable reference that persists across renders
const inputRef = useRef(null);

useEffect(() => {
  inputRef.current.focus();
}, []);

return <input ref={inputRef} type="text" />;
```

Note:
- Doesn't trigger re-render when changed
- Common uses: DOM element access, storing mutable values
- Persists for component lifetime
- Good for storing previous values, timers, etc.

---

### useEffect
```jsx [1-4|6-9|11-14]
// No dependency array
useEffect(() => {
  console.log('Runs every render')
});

// Empty dependency array
useEffect(() => {
  console.log('Runs once on mount')
}, []);

// Array with dependencies
useEffect(() => {
  console.log('Runs when dependencies change')
}, [dependency1, dependency2]);
```

Note:
- **No array**
  - useEffect runs after every render (usually not what you want)
  - should be used sparingly
  - only when you want to trigger a side effect after render
  - example being resizing an element's height with useRef
- **Empty array**: Run once when component mounts
  - e.g Data fetch
- **With dependencies**: Run when those values change

---

### useEffect Cleanup

```jsx
useEffect(() => {
  const timer = setInterval(() => {
    console.log('Tick');
  }, 1000);

  // Cleanup function
  return () => {
    clearInterval(timer);
    console.log('Timer cleaned up');
  };
}, []);
```

Note:
- Return a cleanup function to prevent memory leaks
- Runs before component unmounts
- Essential for timers, subscriptions, event listeners
- Forget cleanup = memory leaks

---

### useLayoutEffect

```jsx
useLayoutEffect(() => {
  console.log('Before Paint!');
}, []);
```

Note:
- useLayoutEffect fires synchronously after render but before paint
- Blocks the browser paint
- Use for DOM measurements or manipulations
- Examples: tooltips positioning, scroll position restoration
- 99% of the time you want useEffect (asynchronous)
- Only use useLayoutEffect when you need to read/write DOM before paint

---

## Component Lifecycle

Note:
- Previously class based components had a bunch of lifecycle methods that we could use for various stages of the component's lifecycle
- I don't want to talk about class components - as far as I'm concerned they're redundant, haven't used one in 6 years
- With hooks, we can do the same thing within functional components

---

<img src="./assets/react-lifecycle.png" alt="React lifecycle" />

Note:
- **Mounting** - Component creation, so when the component is being added to the DOM
- **Updating** - Component Re-render
- **Unmounting** - Component Removal - when the component is removed from the DOM, like navigating to a new page for example

---

```jsx [3|8|12]
// Before mounting
useLayoutEffect(() => {
  console.log('Me first!');
}, []);

// After mounting
useEffect(() => {
  console.log('...and then me!');

  // Before unmounting
  return () => {
    console.log('...me last!');
  }
}, []);
```

Note:
- Just to illustrate this flow in practice
- You can see here how this would work with hooks

---

### Common usage

```jsx
useEffect(() => {
  fetchData();
}, []);

// ⚠️ Triggers AFTER the component is rendered
```

Problem: You render the component, then are forced to re-render when data arrives<!-- .element: class="fragment" -->

Note:
- useEffect fires after the commit phase
- So you render a loading state first
- Then fetch data
- Then re-render with data
- That's two renders for one piece of content
- There is another way which I'll show you shortly

---

### useEffect vs use

```jsx
// Old way - useEffect
function Component() {
  const [data, setData] = useState(null);
  
  useEffect(() => {
    fetchData().then(setData);
  }, []);
  
  if (!data) return <Loading />;

  return <div>{data}</div>;
}
```

Note:
- You're probably used to seeing this sort of pattern within your components
- As I mentioned earlier, the problem we have here is that the data is only ever fetched after the component has finished rendering
- Which means the data changes, and does what?
- Causes a re-render

---

### use (with Suspense)

```jsx
// New way - use with Suspense (React 19)
function Component() {
  const data = use(fetchData());
  const theme = isThemed ? use(ThemeContext) : 'default';

  return(
    <Suspense fallback={<Loading />}>
      <SomeComponent data={data} theme={theme}/>
    </Suspense>
  )
}
```

Note:
- React 19
- New hook that can be called conditionally (breaks Hook rules!)
- works with both promises (async data) and context (for shared state)
- Works with Suspense for data fetching
- Starts fetching during render phase, not after
- Only one render needed when data arrives
- Suspense shows fallback while waiting
- Much cleaner than useEffect for data fetching
- -- 
- React will suspend the component until the promise resolves, then render with the resolved value.
- When you pass context, it’s effectively a more flexible version of useContext that can be called conditionally.

---

# Memoisation<!--.element: class="r-fit-text" -->

---

### Three ways to memoise in React

- **useCallback** = Memoises a function
- **useMemo** = Memoises a value
- **React.memo** = Memoises an entire component

Note:
- All about preventing unnecessary work
- Each has specific use cases
- All have overhead - use if performance is an issue

---

### useCallback

```jsx
// Memoises a function
const handleClick = useCallback(() => {
  doSomething(value);
}, [value]);
```

Note:
- Prevents creating new function on every render
- Useful when passing callbacks to optimised child components
- Child using React.memo won't re-render unnecessarily

---

### useMemo

```jsx
// Memoises a computed value
const sortedList = useMemo(() => {
  return items.sort((a, b) => a.value - b.value);
}, [items]);

// ⚠️ "Checking to see if we have it in memo" has a cost
```

Note:
- Caches the result of expensive calculations
- Only recalculates when dependencies change
- Trade-off: Can add overhead from checking if value is in cache
- Don't use for cheap calculations
- Profile before memoising

---

### React.memo
```jsx
import { memo } from 'React'

// Prevents re-render if all props are still the same
const ExpensiveComponent = memo(({ data }) => {
  // Expensive rendering logic
  return (
    <div>{/* Some component... */}</div>;
  )
});
```

Note:
- Higher-order component that wraps your component
- Does shallow comparison of props
- If props unchanged, skips render and reuses last result
- Great for expensive components that get same props often
- But the comparison itself has a cost

---

### Be mindful of the trade offs

**Rendering speed** vs **Increased memory**

Note:
- Memoisation trades memory for speed
- Storing cached values uses memory
- Checking cache uses CPU
- Sometimes faster to just re-render
- Profile to know which is better
- Which leads us to the golden rule...

---

### 🏆 The Golden Rule ⚖️ 

"Doing nothing is faster than doing something"

Note:
- Simple but profound
- All optimisation comes back to this
- Avoid work rather than optimise work
- Memoisation helps avoid work
- But memoisation itself is work

---

## Beware of premature optimisation

---

### The Browser's Frame Budget

The browser paints every 16ms<!-- .element: class="fragment" -->

If your renders complete under 16ms, there may not be a need to optimise<!-- .element: class="fragment" -->

Note:
- 60 frames per second = 16.67ms per frame
- If you're under that, users won't notice
- Don't optimise based on feeling
- Use React DevTools Profiler to measure
- Only optimise if you're dropping frames

---

# To recap

---

## When to optimise

<div class="container">
<div class="col fragment" markdown="1">

## ✅

- Renders are expensive<!-- .element: class="fragment" -->
- Props don't change<!-- .element: class="fragment" -->
- Prevent cascading<!-- .element: class="fragment" -->
- Passing complex data<!-- .element: class="fragment" -->

</div>
<div class="col fragment" markdown="1">

## ❌ 

- Simple components<!-- .element: class="fragment" -->
- Props change often<!-- .element: class="fragment" -->
- Without profiling<!-- .element: class="fragment" -->
- Updates are internal<!-- .element: class="fragment" -->

</div>
</div>

Note:
- ✅
- **Renders are Expensive**: Your component takes a long time to calculate its output (e.g., complex calculations, processing large lists).
- **Props Don't Change**: The component often re-renders, but its props are identical to the last render.
- **Preventing Cascade Renders**: The component is high in the tree, and its unnecessary re-render causes many complex children to re-render.
- **Passing Complex Data**: You pass objects or arrays as props, and you need to ensure the child doesn't update just because the reference changed (you must also use useCallback for functions).
- ❌
- **Components are Simple**: The component is cheap and fast to render (small UI, simple HTML). The overhead of checking memoisation is slower than just letting it re-render.
- **Props Change Often**: The component is highly dynamic (e.g., animations, frequently updated charts). The memo check will constantly fail.
- **Premature Optimisation**: You haven't yet measured a real performance problem
- **Updates are Internal**: The component is re-rendering because of its own state change; memoising it won't stop the self-initiated update.

---

# 🚀 Exercise 1
## State Placement

**You'll need:** <a href="https://react.dev/learn/react-developer-tools">React Dev Tools</a> browser extension

<!-- **Tasks:**
1. Open the deep-thoughts example
2. Observe component re-renders with highlighting
3. Identify unnecessary re-renders
4. Push state down to optimise
5. Compare before and after -->

**Time: 10 minutes**

Note:
- This demonstrates the power of state placement
- No memoisation needed - just smart architecture
- You'll see how moving state eliminates re-renders
- Golden rule in action: not doing stuff is faster
- This should be your first optimisation strategy

---

<!-- PLACEHOLDER: Exercise 1 Solution
Include before/after code examples:

Before: State too high
```jsx
function App() {
  const [input, setInput] = useState('');
  return (
    <div>
      <ExpensiveComponent />
      <input value={input} onChange={e => setInput(e.target.value)} />
    </div>
  );
}
```

After: State pushed down
```jsx
function App() {
  return (
    <div>
      <ExpensiveComponent />
      <InputComponent />
    </div>
  );
}

function InputComponent() {
  const [input, setInput] = useState('');
  return <input value={input} onChange={e => setInput(e.target.value)} />;
}
```

Screenshot showing DevTools with reduced re-render flashing

No te:
- Take 2-3 minutes for discussion
- Did everyone see the re-render reduction?
- This is architectural optimisation
- No memoisation needed
- Questions about state placement?

-->

# 🚀 Exercise 2
## Counter Optimisation

<!-- **Tasks:**
1. Build counter with increment/decrement
2. Show state change and children re-rendering
3. Minimise with useCallback and React.memo
4. Move logic to custom hook
5. Explain referential equality issue with return value
6. Show previous state pattern removing dependencies -->

**Time: 15 minutes**

Note:
- More complex exercise combining multiple techniques
- Progressive optimisation approach
- We'll measure impact with DevTools at each step
- Custom hook demonstrates referential equality gotcha
- Previous state pattern shows dependency elimination

---

<!-- PLACEHOLDER: Exercise 2 Solution
Progressive code examples:

1. Basic counter (no optimisation)
```jsx
function Counter() {
  const [count, setCount] = useState(0);
  return (
    <div>
      <Display count={count} />
      <Button onClick={() => setCount(count - 1)}>-</Button>
      <Button onClick={() => setCount(count + 1)}>+</Button>
    </div>
  );
}
```

2. With React.memo on Button
3. With useCallback for handlers
4. Extracted to useCounter hook
5. Memoised hook return value
6. Using previous state pattern

DevTools screenshots showing render count improvements at each step

No te:
- Take 5 minutes for discussion
- Which optimisations made the biggest difference?
- When is memoisation worth it vs not worth it?
- Questions about the techniques?
- This is real-world optimisation workflow

-->
#### ...with all that said
# 👀
## React Compiler<!-- .element: class="fragment" -->

---

### What is React Compiler?

**The future of React performance**<!-- .element: class="fragment" -->

Automatically analyses code and applies optimisations<!-- .element: class="fragment" -->

## 🤯<!-- .element: class="fragment" -->

Note:
- This is cutting-edge technology
- No manual use of: useMemo, useCallback or React.memo
- Instagram is using this in production now
- Compiler does optimisation work for you
- No more manually adding useCallback and useMemo
- Still experimental but very promising

---

### How it works

<!-- .slide: data-auto-animate="true" -->

- 🧙‍♀️ Witchcraft<!-- .element: class="fragment" -->
- Stores references in arrays<!-- .element: class="hidden" -->
- Performs simple value checks<!-- .element: class="hidden" -->
- Instead of calling functions and comparing objects<!-- .element: class="hidden" -->

**Much more efficient than manual React.memo**<!-- .element: class="hidden" -->

<!-- .element: data-id="code-animation" -->

Note:
- The only possible explanation...
- Anyone who knows anything about referential equality in JS knows it's a pain
- Much more efficient than manual React.memo
- Doesn't need comparison functions
- Just checks primitive values
- Can optimise things we can't manually
- Removes whole classes of memoisation bugs

---

### How it works

<!-- .slide: data-auto-animate="true" -->

- 🧙‍♀️ Witchcraft<!-- .element: class="fragment strike" -->
- Stores references in arrays<!-- .element: class="fragment" -->
- Performs simple value checks<!-- .element: class="fragment" -->
- Instead of calling functions and comparing objects<!-- .element: class="fragment" -->

**Much more efficient than manual React.memo**<!-- .element: class="fragment" -->

<!-- .element: data-id="code-animation" -->

Note:
- The only possible explanation...
- Anyone who knows anything about referential equality in JS knows it's a pain
- Much more efficient than manual React.memo
- Doesn't need comparison functions
- Just checks primitive values
- Can optimise things we can't manually
- Removes whole classes of memoisation bugs

---

### 🪄 The Magic of Abstraction

React Compiler abstracts away complexity

- Just like JSX hides React.createElement
- The compiler hides memoisation

--

#### You focus on features, tools handle optimisation<!-- .element: class="fragment" -->

Note:
- Remember React.createElement from Session 1?
- JSX made that disappear
- Compiler makes memoisation disappear
- Both are powerful abstractions
- Let tools handle the hard parts

---

### React Compiler Playground

```
https://playground.react.dev/
```

Note:
- You can try it online right now
- Paste your component code
- See what optimisations it applies
- Really helps understand what compiler does
- Play with it after this session!

---

### Current Status

React 17+ (Relies on the Fiber architecture) \
currently relies on an opt-in strategy

```jsx
'use compiler';
```

- Minimum version: React 17 or later
- Used in production by Instagram
- Still experimental
- Being actively developed

Note:
- Instagram has billions of users on this code
- That's a pretty good stress test!
- Still experimental means API might change
- But coming to stable React soon
- Worth learning about now
- Might change how you write React

---

# Key Takeaways

---

### Remember these principles

1. Not doing stuff is faster than doing stuff (The Golden Rule)<!-- .element: class="fragment" -->
2. Profile before optimising<!-- .element: class="fragment" -->
3. State placement > memoisation<!-- .element: class="fragment" -->
4. Clarity > premature optimisation<!-- .element: class="fragment" -->
5. Memoisation has a cost<!-- .element: class="fragment" -->

Note:
- These are your core principles
- Golden rule is most important
- Always measure before optimising
- Architecture fixes > memoisation
- Readable code is maintainable code
- Memoisation isn't free

---

<!-- ### The Optimisation Hierarchy

1. **Fix architecture** (state placement, component structure)
2. **Profile and measure**
3. **Eliminate unnecessary renders** (React.memo)
4. **Memoise expensive computations** (useMemo)
5. **Stabilise callbacks** (useCallback)
6. **Consider React Compiler**

No te:
- Work through this list in order
- Architecture gives biggest wins
- Always measure to confirm problems
- Don't skip to memoisation
- Each level has diminishing returns
- Compiler might automate most of this soon

--
 -->
### Useful Links

##### React Compiler
```
https://react.dev/learn/react-compiler
```
```
https://playground.react.dev/
```

##### React DevTools
```
https://react.dev/learn/react-developer-tools
```

##### React Performance Docs
```
https://react.dev/learn/render-and-commit
```

##### React Fiber Architecture
```
https://github.com/acdlite/react-fiber-architecture
```

Note:
- These are your reference materials
- Playground is great for learning compiler
- DevTools is essential for profiling
- React docs have excellent performance section
- Fiber architecture explanation is detailed

---

## Any questions?<!--.element: class="r-fit-text" -->

Note:
- Performance is deep - we've covered fundamentals

---

# Thank you!<!--.element: class="r-fit-text" -->

<!-- 

### See also...

- `useTransition` - Mark updates as non-urgent
- `useDeferredValue` - Defer updating expensive values
- `useOptimistic` - Show optimistic UI updates
- `useActionState` - Manage form actions

Note:
- These are advanced performance hooks
- **useTransition**: Keep UI responsive during heavy updates
- **useDeferredValue**: Show stale value while computing new one
- **useOptimistic**: Instagram "like" that shows immediately
- **useActionState**: Server actions with pending states
- -- 
- Great for search, filtering, form submissions
- Look into these for your next project!


-- NEW PAGE -

### State Setters Are Already Memoised

```jsx
const [count, setCount] = useState(0);
```

State setters use **useCallback** under the hood

They always maintain the same reference

**Argument:** You don't need to overuse useCallback

Note:
- React guarantees setState identity is stable
- This is why you can safely omit it from dependency arrays
- One less thing to memoise manually
- But functions you pass TO setState might need memoisation
- When small optimisations build up, they matter

-- NEW PAGE - 

### The Previous State Pattern

```jsx
// With closure (needs count in dependencies)
const increment = useCallback(() => {
  setCount(count + 1);
}, [count]);

// With function (no dependencies needed)
const increment = useCallback(() => {
  setCount(prev => prev + 1);
}, []);
```

**Passing a function prevents dependency issues**

Note:
- When setState uses a function, doesn't need current state in closure
- Gets latest state as argument to function
- Allows useCallback to have empty dependencies
- Function stays stable across renders
- Prevents stale closure bugs

-- NEW PAGE - 

### When NOT to Optimise

You CAN memoise everything in your app, but:

- There is always a cost attached
- You could introduce bugs
- Maintainability suffers

**Better:** Let rendering work naturally

**Optimise only when needed** based on profiling

Note:
- This is critical to understand
- Premature optimisation is the root of all evil
- Clear, working code > slightly faster broken code
- Use your judgment as a developer
- Profile first, optimise second
- Bugs are worse than minor performance issues

-->
