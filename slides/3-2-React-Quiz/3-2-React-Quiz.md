# Quiz Time!

---

### Question 1

What are the three reasons a \
React component re-renders?

1. State changed<!-- .element: class="fragment" -->
2. Context changed<!-- .element: class="fragment" -->
3. Parent re-rendered<!-- .element: class="fragment" --> \
(Or props changed if memoised)<!-- .element: class="fragment" -->

Note:
- These are the ONLY reasons React re-renders
- Understanding this is fundamental to optimisation
- If using memoisation, third reason is replaced with "props changed"

---

### Question 2

What is React Fiber?

A complete rewrite of React's rendering engine that enables incremental, non-blocking rendering<!-- .element: class="fragment" -->

Note:
- Introduced in React 16
- Can pause, abort, or resume rendering work
- Enables cooperative scheduling
- Foundation for concurrent features

---

### Question 3

What's the difference between necessary and unnecessary re-renders?

Necessary: State or props actually changed<!-- .element: class="fragment" -->

Unnecessary: Component re-renders but produces same output<!-- .element: class="fragment" -->

Note:
- Necessary re-renders we can't avoid, but can prioritise
- Unnecessary re-renders are where we optimise

---

### Question 4

How does the dependency array in useEffect control when it runs?

- No array = runs every render<!-- .element: class="fragment" -->
- Empty array = runs once on mount<!-- .element: class="fragment" -->
- With dependencies = runs when the values change<!-- .element: class="fragment" -->

Note:
- No array: Usually not what you want
- Empty array: Common for data fetching
- With dependencies: Most common pattern

---

### Question 5

What's the key advantage of using "use()" with Suspense over useEffect for data fetching?

"use()" starts fetching during render phase, requiring only one render when data arrives<!-- .element: class="fragment" -->

useEffect fetches after render, requiring two renders (loading state + data)<!-- .element: class="fragment" -->

Note:
- useEffect: Render loading → fetch → re-render with data
- use: Start fetch during render → one render when ready
- Much more efficient pattern

---

### Question 6

What do these three memoisation techniques do?

useCallback, useMemo, React.memo<!-- .element: class="fragment" -->

- useCallback = Memoises a function<!-- .element: class="fragment" -->
- useMemo = Memoises a value<!-- .element: class="fragment" -->
- React.memo = Memoises an entire component<!-- .element: class="fragment" -->

Note:
- Each has specific use cases
- All have overhead - only use when needed
- Profile before memoising

---

### Question 7

What is the golden rule of \
React performance optimisation?

"Doing nothing is faster than doing something"<!-- .element: class="fragment" -->

Note:
- Simple but profound
- All optimisation comes back to this
- Avoid work rather than optimise work
- Foundation of all performance work

---

### Question 8

What's the browser's frame budget, and why does it matter for optimisation?

The browser paints every 16ms<!-- .element: class="fragment" -->

If renders complete under 16ms, there may be no need to optimise<!-- .element: class="fragment" -->

Note:
- 60 frames per second = 16.67ms per frame
- Users won't notice if you're under that threshold
- Always profile before optimising
- Don't optimise based on feeling

---

### Question 9

When should you optimise vs not optimise?

✅ Optimise when: Renders are expensive, props don't change often, preventing cascade renders<!-- .element: class="fragment" -->

❌ Don't optimise: Simple components, props change often, without profiling first<!-- .element: class="fragment" -->

Note:
- Premature optimisation is evil
- Profile first to find real issues
- Simple components are faster to just re-render
- Complexity can introduce bugs

---

### Question 10

What is React Compiler and \
what problem does it solve?

Automatically analyses code and applies optimisations<!-- .element: class="fragment" -->

Removes need for manual useMemo, useCallback, and React.memo<!-- .element: class="fragment" -->

Note:
- The future of React performance
- Instagram using in production
- Still experimental but promising
- Requires React 17+ (Fiber architecture)
- Use 'use compiler' directive to opt in
