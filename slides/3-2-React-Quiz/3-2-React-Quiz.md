# Quiz Time!

---

### Question 1

What are the two broad categories of performance issues in React applications?

Big bottlenecks and small accumulated issues<!-- .element: class="fragment" -->

Note:
- Let them think before revealing answer
- Big bottlenecks: Easy to find and fix
- Small issues: More insidious

---

### Question 2

Why are accumulated small performance issues considered more insidious than single large bottlenecks?

They accumulate gradually and become difficult to refactor<!-- .element: class="fragment" -->

Note:
- Single bottleneck: Profiler finds it, you fix it
- Small issues: Creep in over time
- By the time you notice, they're everywhere
- Refactoring becomes expensive and risky

---

### Question 3

What is the golden rule of performance optimisation?

Not doing stuff is faster than doing stuff<!-- .element: class="fragment" -->

Note:
- The foundation of all optimisation
- Avoid work rather than optimise work
- All our techniques come back to this

---

### Question 4

Why is showing a loading indicator better than showing nothing during a long-running operation?

It provides user feedback that the application is working rather than being frozen - "Perceived performance"<!-- .element: class="fragment" -->

Note:
- User perception matters
- Loading indicator communicates "I'm working on it"
- Without it, users think app is frozen
- Perceived performance vs actual performance

---

### Question 5

What is one of the main risks of overusing React.memo and memoisation?

Cache invalidation bugs can be extremely difficult to debug<!-- .element: class="fragment" -->

Note:
- Phil Karlton quote about cache invalidation
- Memoisation IS caching
- Wrong cache = stale data shown to users
- These bugs are subtle and hard to reproduce

---

### Question 6

Why is 'feeling fast' considered almost as valuable as actually being fast?

Preloading and optimistic UI updates improve perceived performance without actual speed gains<!-- .element: class="fragment" -->

And why is this important?

It provides immediate feedback to users, making the application feel responsive even during slow network conditions<!-- .element: class="fragment" -->

Note:
- User perception > actual milliseconds
- Preloading: Fetch before user clicks
- Optimistic updates: Show result immediately
- Makes app feel instant even when it's not
- Instagram and Twitter use this heavily

---

### Question 7

What problem do React's useTransition and similar hooks primarily solve?

They provide the ability to prioritise urgent updates over less important ones<!-- .element: class="fragment" -->

Note:
- Not all updates are equally important
- Typing: Urgent, needs immediate feedback
- Filtering large list: Can wait a frame
- useTransition marks updates as "transitions"
- Keeps UI responsive

---

### Question 8

What is React Fiber? (React 17+)

A cooperatively scheduled rendering engine (helps React prioritise DOM changes, pausing and rechecking vs starting at the top and processing the entire component tree in a blocking manner)<!-- .element: class="fragment" -->

i.e. It can stop current work and handle the more important task<!-- .element: class="fragment" -->

Note:
- Complete rewrite of React's core
- Can pause, check for urgent work, resume
- Like cooperative multitasking
- Foundation for concurrent features

---

### Question 9

In React's original architecture, what was the primary purpose of the virtual DOM?

To perform DOM manipulations in memory before applying changes to the actual DOM, avoiding expensive browser recalculations<!-- .element: class="fragment" -->

Note:
- DOM operations are slow
- Virtual DOM is just JavaScript objects - fast
- Do work in memory first
- Apply minimum necessary changes to real DOM
- Revolutionary when React launched

---

### Question 10

What is the key difference between the render phase and commit phase in React Fiber?

The render phase updates the virtual DOM and can be interrupted, while the commit phase updates the actual DOM and cannot be interrupted<!-- .element: class="fragment" -->

Note:
- Render phase: Pure computation, safe to pause
- Commit phase: Actually updating DOM, must complete
- Two-phase approach enables Fiber's scheduling
- Understanding this helps debug lifecycle issues

---

### Question 11

What is a key benefit of React Fiber's architecture for handling long-running operations?

It can interrupt low-priority work to handle high-priority user interactions immediately<!-- .element: class="fragment" -->

Note:
- Example: Heavy list filtering happening
- User starts typing in search box
- Fiber pauses filtering, handles typing
- Resumes filtering after
- Keeps UI responsive

---

### Question 12

Why is using useEffect with an empty dependency array for API calls considered less optimal than using Suspense?

Because useEffect is called after the entire DOM has been rendered, requiring a second render when data arrives, whereas Suspense fires API calls during the initial render<!-- .element: class="fragment" -->

Note:
- useEffect: Render loading state, fetch, re-render with data
- That's two renders
- Suspense: Start fetching during render
- Only one render when data arrives
- More efficient

---

### Question 13

How does React Suspense handle promises during the render phase?

It pauses rendering at the promise location and shows a loading component until the promise resolves<!-- .element: class="fragment" -->

Note:
- Component "suspends" when it hits promise
- React shows nearest Suspense fallback
- Continues rendering when promise resolves
- Enables elegant data fetching patterns
- Works with the new "use" hook

---

### Question 14

What is the primary principle for managing state placement in React applications?

Keep state as high as you need it and as low as you can get away with<!-- .element: class="fragment" -->

Note:
- State too high: Unnecessary re-renders
- State too low: Prop drilling or duplication
- Find lowest common ancestor
- This is "lifting state up"
- We practiced this in Exercise 1

---

### Question 15

Why does defining event handler functions inside a component cause unnecessary re-renders?

Functions are defined as brand new objects on every render, causing referential inequality<!-- .element: class="fragment" -->

Note:
- In JavaScript, functions are objects
- Every render creates new function instance
- Child components see them as "new props"
- If child uses React.memo, still re-renders
- This is where useCallback helps

---

### Question 16

What is the primary tradeoff to consider when trying to avoid unnecessary re-renders using complex techniques?

The complexity cost and maintainability can lead to bugs, which is worse than minor performance issues<!-- .element: class="fragment" -->

Note:
- This is CRITICAL
- Premature optimisation is evil
- Complex code is hard to maintain
- Can introduce bugs
- Bugs > minor performance issues
- Profile first, optimise only when needed

---

### Question 17

What is the primary purpose of the useCallback hook in React?

To memoise a function so that if its dependencies haven't changed, React reuses the same function instance instead of creating a new one<!-- .element: class="fragment" -->

Note:
- Returns same function reference between renders
- Only creates new function if dependencies change
- Useful with optimised child components
- Child with React.memo won't re-render unnecessarily

---

### Question 18

What is the main difference between useMemo and useCallback?

useMemo memoises the result of a computation, while useCallback memoises the function itself<!-- .element: class="fragment" -->

Note:
- useMemo: Cache computed value
- useCallback: Cache function
- useCallback is technically useMemo(() => fn)
- Both have overhead, use judiciously

---

### Question 19

What problem can occur when returning an object from a custom hook that contains both state values and memoised functions?

The object itself is a new reference on each render, even if its members are memoised, potentially breaking downstream memoisation<!-- .element: class="fragment" -->

Note:
- Subtle gotcha
- Object literal creates new reference
- Even though properties are memoised
- Components see "new props"
- Solution: Wrap return object in useMemo
- Or return array instead

---

### Question 20

When profiling a React application, what does it indicate if props like onUpdate and onDelete are shown as changed even though their logic hasn't changed?

New function instances are being created on each render, causing referential inequality<!-- .element: class="fragment" -->

Note:
- This is your debugging workflow
- Profiler shows which props changed
- Functions showing as changed? Need useCallback
- Objects showing as changed? Need useMemo
- DevTools Profiler is your friend

---

### Question 21

What is the primary purpose of wrapping a component with React.memo?

To prevent re-rendering when props haven't changed<!-- .element: class="fragment" -->

Note:
- Higher-order component
- Does shallow comparison of props
- If props same, skip render, reuse last result
- Great for expensive components
- But comparison itself has cost

---

### Question 22

Why can't React.memo be applied everywhere by default in React applications?

Memoising a component can prevent necessary updates to its children down the component tree<!-- .element: class="fragment" -->

Note:
- Interesting edge case
- If parent is memoised but children need updates
- Updates might not propagate correctly
- Also: Comparison overhead
- React can't make this decision automatically
- Developer must choose when to memoise

---

### Question 23

When using setState with a function instead of a direct value, what advantage does this provide in terms of dependencies?

It allows access to the previous state value without needing the current state in closure scope<!-- .element: class="fragment" -->

Note:
- Function form: prev => prev + 1
- Gets latest state as argument
- Doesn't need current state in closure
- Allows useCallback with empty dependencies
- Prevents stale closure bugs

---

### Question 24

What does passing an empty array as the dependency array to useCallback indicate?

The callback has no dependencies and will remain static<!-- .element: class="fragment" -->

Note:
- Empty array = no dependencies
- Function never changes
- Same reference across all renders
- Only possible with previous state pattern
- Or if function truly has no dependencies

---

### Question 25

When a component is wrapped with React.memo and receives the same props, what happens during re-renders?

The component skips rendering entirely<!-- .element: class="fragment" -->

Note:
- React doesn't call component function at all
- Just reuses previous render output
- Saves creating virtual DOM
- This is where real performance gains come from
- But only if props actually stay the same

---

### Question 26

What is the primary purpose of React Compiler?

To automatically analyse code and apply memoisation optimisations without manual use of useMemo, useCallback, and React.memo<!-- .element: class="fragment" -->

Note:
- Removes need for manual optimisation
- Automatically applies best practices
- Instagram using in production
- Still experimental but promising
- The future of React performance

---

### Question 27

What is the minimum React version required to use React Compiler?

React 17 or later, as it relies on the Fiber architecture<!-- .element: class="fragment" -->

Note:
- Requires modern rendering engine
- Fiber architecture enables optimisations
- React 17+ includes Fiber
- Most projects already on React 18
- If on older version, need to upgrade

---

### Question 28

How does React Compiler optimise component rendering compared to manually using React.memo?

It stores references in arrays and performs simple value checks instead of calling functions and comparing objects<!-- .element: class="fragment" -->

Note:
- More efficient approach
- No comparison function calls needed
- Just primitive value checks
- Can optimise things we can't manually
- Removes memoisation bug classes

---

### Question 29

What is the recommended approach for adopting React Compiler in an existing legacy codebase?

Use an incremental approach, opting in components progressively using the 'use compiler' directive<!-- .element: class="fragment" -->

Note:
- Don't compile everything at once
- Start with new components
- Gradually opt in existing ones
- Use directive for control
- Safe migration path
- Remove manual memoisation as you go
