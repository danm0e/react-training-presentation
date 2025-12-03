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
- Particularly around re-rendering and practical optimisation techniques
- Exercise/Demo to put these concepts into practice

---

### Today's agenda

- Why React re-renders
- React Fiber
- Hooks
- Memoisation
- Exercise - Optimising
- React Compiler
- Quiz?<!-- .element: class="fragment" -->

Note:
- Previously touched on rendering, today we discuss why
- React Fiber 
  - Rework to the process which updates the virtual DOM
- Most common Hooks
- Memoisation which is how we can manually control a components render
- Exercise to some examples of optimising our components
- React Compiler
- If we have time - Quiz

---

### Learning Agreement

- Stay focused, cameras on 🙏<!-- .element: class="fragment" -->
- We are going to be looking at code <!-- .element: class="fragment" -->
- No question is a silly question <!-- .element: class="fragment" -->

...so please ask a question whenever you like<!-- .element: class="fragment" -->

Note:
- As per last time, I have a couple of asks...
- It really does help me!
- We'll be going deeper this time, so definitely more technical

---

## Re-rendering<!--.element: class="r-fit-text" -->
### ...yeah, but why?<!-- .element: class="fragment" -->

---

<!-- .slide: data-auto-animate="true" -->

### The three reasons

A component re-renders when:

- It's state changed<!-- .element: class="fragment" -->
- The context changed<!-- .element: class="fragment" -->
- It's parent has re-rendered<!-- .element: class="fragment" -->
- It's props changed (if memoised)<!-- .element: class="hidden" -->

<!-- .element: data-id="code-animation" -->

Note:
- These are the ONLY reasons React will re-render
- **State change**: any updates via the state hooks we'll go over shortly causes a render
- **Context change**: Any context value the component consumes
- **Parent re-renders**: If a component re-renders, then by default all it's children will re-render too
- Understanding this is fundamental to how we plan our optimisation

---

<!-- .slide: data-auto-animate="true" -->

### The three reasons

A component re-renders when:

- It's state changed
- The context changed
- ~~It's parent has re-rendered~~
- It's props changed (if memoised)

<!-- .element: data-id="code-animation" -->

Note:
- There is a slight caveat to this however
- If the component is memoised, the 3rd reason is replaced by if it's props changed

---

## React's Rendering Cycle

---

### There are three phases
### of a render

- Render<!-- .element: class="fragment" -->
- Commit<!-- .element: class="fragment" -->
- Cleanup<!-- .element: class="fragment" -->

Note:
- **Render** 
  - Calculate what changed, so we can rebuild virtual DOM 
  - Which we do in memory as it's faster than mutating the DOM and preventing repaints etc
  - Once we've gone through the whole component tree we get to the commit phase
- **Commit** 
  - The virtual DOM has calculated all of the changes
  - We know what needs to be updated
  - And now we're going to actually apply those changes to real DOM 
  - Think of it like a git commit
- **Cleanup** 
  - Once we're done there...
  - Run any cleanup functions from effects
- --
- So from React 15 and earlier, the “virtual DOM” was essentially a tree of lightweight objects that mirrored the real DOM 
- Every render, React would build a fresh tree from your JSX, diff it against the previous one, and then compute a patch to apply to the actual DOM
- That whole process was synchronous and uninterruptible: 
- So it was blocking by nature, much like the javascript call stack
- Once React started traversing the tree, it **had** to finish before the browser could do anything else
- So this was a problem right? 
- Is there a better way?

---

# React Fiber

---

### What is React Fiber?

- Core Re-implementation<!-- .element: class="fragment" -->
  - Complete rewrite of React's rendering engine (React 16+)<!-- .element: class="fragment" -->
- Primary Goal<!-- .element: class="fragment" -->
  - Drastically improve performance in complex applications<!-- .element: class="fragment" -->

Note:
- Complete rewrite of React's rendering engine
- Introduced in React 16
- Complete rewrite of the reconciler
- Changed how React processes component trees
- It is the foundation for concurrent features

---

### Key Features

- Incremental Rendering <!-- .element: class="fragment" --> 
  - Breaks work into smaller, manageable units<!-- .element: class="fragment" -->
- Non-Blocking <!-- .element: class="fragment" --> 
  - Can pause, abort, or resume rendering work<!-- .element: class="fragment" -->
- Better UX <!-- .element: class="fragment" --> 
  - Yields control to handle high-priority tasks like user input<!-- .element: class="fragment" -->

Note:
- **Before Fiber**
  - React processed the entire tree in one go (blocking)
- **With Fiber**
- More like **multitasking** vs **single-threaded** execution
- Main thread stays responsive for animations and user input
- **Example**
  - User typing in a search box (urgent) vs filtering a large list (can wait)

---

## Types of Re-render

Note:
- There are two types of render

---

### Necessary vs Unnecessary

**Two types of re-render in React:**

- **Necessary** 
  - State or props actually changed<!-- .element: class="fragment" -->
- **Unnecessary** 
  - Component re-renders but produces the same output<!-- .element: class="fragment" -->

Note:
- **Necessary re-renders**: We can't avoid, but can prioritise
- **Unnecessary re-renders**: Nothing has changed, but the component still re-renders
- This is where we might want to optimise

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
  - ...eliminate unnecessary renders
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
- Returns the current state along with a setter function
- These setters will trigger a re-render

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
- Better in a case where you may have multiple sub-values
- When next state depends on the previous
- Dispatch function is stable (like setState)
- If you've used any of the other state management packages before
- It's more like a Redux-style pattern built into React
- Which I believe if you dig in to the source code of Redux, is using reducer under the hood

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
- So we declare a global state or context
- We then consume that via the hook
- Then wrap all components that need it within a provider 
- This then removes need for prop drilling
- Access shared data across component tree
- Problem: 
  - All consumers re-render when context changes, this can be a lot
  - Even if they only use part of the context value
  - You can imagine, lots of component re-rendering would mean performance degradation
  - Can be a problem if you have a big store
- Solution: 
  - Split into multiple contexts

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
- But then we get the nested provider doom tree from hell
- So you just really do need to be mindful of how you structure your app
- Context is convenient but has performance implications
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
- Creates a mutable reference that persists across renders
- Doesn't trigger re-render when changed
- Common uses: DOM element access, storing mutable values
- Persists for component lifetime
- Good for storing previous values, timers, etc.

---

### useLayoutEffect

```jsx
useLayoutEffect(() => {
  console.log('Before Paint!');
}, []);
```

Note:
- useLayoutEffect also fires after render but before paint and is synchronous
- Blocks the browser paint
- Use for DOM measurements or manipulations
- Examples: tooltips positioning, scroll position restoration
- 99% of the time you want useEffect (asynchronous)

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
- useEffect lets you perform side effects (like data fetching, subscriptions, or manually changing the DOM) 
- Triggers after the component is rendered
- There are a couple of ways that you can use it
- **No array**
  - useEffect runs after every render (usually not what you want)
  - should be used sparingly
  - only when you want to trigger a side effect after render
  - example being get the new height of an element that has been stored in a useRef
- **Empty array**: Run once when component mounts
  - e.g common pattern is a data fetch
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
- Return a function, which runs before component unmounts
- Known as a cleanup function to prevent memory leaks
- Essential for timers, subscriptions, event listeners
- Forget cleanup = memory leaks

---

### Common pattern

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

Problem: You render the component, then are forced to re-render when data arrives<!-- .element: class="fragment" -->

Note:
- You're probably used to seeing this sort of pattern within your components
- The problem we have here is that the data is only ever fetched after the component has finished rendering
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
- As of React 19 we have a new way
- New **use** hook and **Suspense** component that handles this for us
- Starts fetching during render phase, not after
- Only one render needed once data arrives
- Handles the loading state while waiting
- Much cleaner than useEffect for data fetching
- And is als works with both promises and context
- It can also be called conditionally which you can't usually do with hooks
- -- 
Key point:
- React will suspend the component until the promise resolves, then render with the resolved value.
- When you pass context, it’s effectively a more flexible version of useContext that can be called conditionally.

---

# Memoisation<!--.element: class="r-fit-text" -->

---

### Three ways to memoise 
### in React

- useCallback = Memoises a function<!-- .element: class="fragment" -->
- useMemo = Memoises a value<!-- .element: class="fragment" -->
- React.memo = Memoises an entire component<!-- .element: class="fragment" -->

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

### 🏆 The Golden Rule 🏆 

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

### The browser's frame budget

The browser paints every 16ms<!-- .element: class="fragment" -->

If your renders complete under 16ms, there may not be a need to optimise<!-- .element: class="fragment" -->

Note:
- 60 frames per second = 16.67ms per frame
- If you're under that, users won't notice
- Don't optimise based on feeling
- Use React DevTools Profiler to measure
- Only optimise if you need to
- It's usually only a problem if it's a problem

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

# 🚀 Exercise
## Putting it all together

**You'll need:** <a href="https://react.dev/learn/react-developer-tools">React Dev Tools</a> browser extension

```jsx
https://github.com/danm0e/react-training-exercise
```

Note:
1. Open the example
2. Observe component re-renders with highlighting
3. Identify unnecessary re-renders
4. All state is currently in the top level (Application file)
4. Push state down to optimise
5. Compare before and after (Use profiling tool - check the render time)
6. Discuss methods are being defined new everytime
7. Add useCallback to each method
8. Previous state pattern shows dependency elimination
9. Custom useCounter hook demonstrates referential equality gotcha
10. Add useMemo to return object for referential equality
11. Show how changing the text widget re-renders the color widget
12. Add React.memo to color widget to fix
13. Observe how this now prevents widget from re-rendering
- --
Summary:
- This demonstrates the power of state placement
- Priciple rule of state: Keep state as high as you need it and as low as you can get away with
- No tricks needed - just smart architecture
- Golden rule in action: not doing stuff is faster
- This should be your first optimisation strategy

---

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
#### 🪄 The magic of abstraction 🪄

React Compiler abstracts away complexity

- Just like JSX hides React.createElement
- The compiler hides memoisation

--

#### You focus on features, tools handle optimisation<!-- .element: class="fragment" -->

Note:
- You can try it out right now but is currently opt in only
- Minimum version: React 17 or later
- Used in production by Instagram
- Still experimental
- Being actively developed

---

# Key takeaways

---

### Remember these principles

1. Not doing stuff is faster than doing stuff \
(The Golden Rule)<!-- .element: class="fragment" -->
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

---

# Thank you!<!--.element: class="r-fit-text" -->
