# Frontend Development Theoretical Assessment

## 1. HTML5 Semantics

**Q: What is Semantic HTML and why is it important?**
*Answer:*
Semantic HTML refers to the use of HTML tags that inherently convey the meaning—or semantics—of the content contained within them, rather than just its presentation. Examples include `<article>`, `<nav>`, `<header>`, `<footer>`, and `<section>` instead of using generic `<div>` or `<span>` tags.

*Importance:*
1. **Accessibility:** Screen readers and assistive technologies rely on semantic tags to interpret page structures and navigate effectively, providing a better experience for users with disabilities.
2. **SEO (Search Engine Optimization):** Search crawler bots use semantic tags to understand the structure and hierarchy of content, which can improve page ranking and visibility in search results.
3. **Maintainability:** Code is significantly easier for developers to read and understand, making collaboration and maintenance simpler.

***

## 2. CSS3 Layouts and Responsiveness

**Q: Compare and contrast Flexbox and CSS Grid. When would you use each?**
*Answer:*
* **Flexbox (Flexible Box Layout):** A one-dimensional layout model primarily used for laying out items in a single row or a single column. It excels at distributing space, alignments, and reordering content along a single axis.
  * *Use cases:* Navigation bars, aligning items within a card component, centering elements, vertically or horizontally aligning a list of items.
* **CSS Grid:** A two-dimensional layout model designed for laying out items in both rows and columns simultaneously. It provides fine-grained control over complex web page structures.
  * *Use cases:* Overall page layouts (header, sidebar, main content, footer), masonry layouts, or complex image galleries.
* *Summary:* Use Flexbox for component-level layouts along a single axis, and Grid for page-level or complex two-dimensional layouts.

**Q: Explain the concepts of responsive web design and the mobile-first approach.**
*Answer:*
**Responsive web design (RWD)** ensures a web application functions well and looks good on all devices (desktops, tablets, phones) by dynamically adapting its layout using CSS media queries, flexible grids, and responsive images.

A **mobile-first approach** is a responsive design strategy where you build properties for the mobile layout first (the default CSS logic without media queries) and then use `min-width` media queries to progressively enhance the layout for larger screens (tablets, desktops).
* *Implications:* Mobile-first ensures the core experience is optimized for smaller screens in terms of performance and usability, and prevents mobile devices from needlessly downloading heavy desktop assets overriding mobile rules.

***

## 3. JavaScript (ES6+) Concepts

**Q: Explain the differences between `var`, `let`, and `const`.**
*Answer:*
* `var`: Function-scoped. Can be redeclared and updated. It's hoisted to the top of its scope and initialized with `undefined`, which can lead to unpredictable bugs and scope leakage.
* `let`: Block-scoped (contained within `{}`). Can be updated but not redeclared in the same scope. It is hoisted but not initialized (temporal dead zone), making it safer than `var`.
* `const`: Block-scoped. Cannot be updated or redeclared. It requires an initial value. However, for objects and arrays declared with `const`, their properties/elements can still be mutated; only the variable's reference is strictly constant.
* *Best practice:* Default to `const`. Use `let` only when you know the variable's value needs to change (like counters in loops). Avoid `var` in modern JavaScript.

**Q: What are Promises and how do Async/Await improve asynchronous code?**
*Answer:*
A **Promise** is an object representing the eventual completion (or failure) of an asynchronous operation and its resulting value. It exists in three states: *pending*, *fulfilled*, and *rejected*. Promises solve the problem of deeply nested callbacks ("callback hell").

**Async/Await** (introduced in ES8) is syntactic sugar built on top of Promises.
* `async` transforms a function to inherently return a Promise.
* `await` pauses the execution of the `async` function until the Promise is settled.
* *Improvement:* They make asynchronous code look and behave more like synchronous code. This makes it significantly easier to read, write, and debug utilizing standard `try/catch` blocks instead of long `.then()` and `.catch()` chains.

***

## 4. React.js/Vue.js Fundamentals

**Q: Describe the Virtual DOM and why it improves performance in frameworks like React or Vue.**
*Answer:*
The Virtual DOM (VDOM) is a lightweight JavaScript representation of the actual DOM in memory.
* *Mechanism:* When an application's state changes, the framework creates a new Virtual DOM tree. It then compares this new tree with the previous Virtual DOM tree (a process called "diffing"). It calculates the absolute minimal set of changes (mutations) needed to update the real DOM to match the new state. This synchronization process is called "reconciliation".
* *Performance:* Directly manipulating the real browser DOM is slow and expensive. The VDOM batches updates and minimizes reflows and repaints in the browser, significantly boosting performance for dynamic applications.

**Q: What are component lifecycles, and how are they handled in modern React or Vue?**
*Answer:*
Lifecycles represent the phases a UI component goes through: creation (mounting), updating, and destruction (unmounting).
* **React Hooks:** Primarily handled via `useEffect`.
  * *Mounting:* `useEffect(() => { ... }, [])` (runs once using empty dependency array).
  * *Updating:* `useEffect(() => { ... }, [dependency])` (runs when the specific dependency changes).
  * *Unmounting:* Return a cleanup function inside `useEffect`.
* **Vue Composition API:** Uses explicit lifecycle hooks imported from Vue, like `onMounted`, `onUpdated`, and `onUnmounted`.
* *Implications:* Moving from class-based lifecycles to modern hooks/composition functions enables grouping related logic together (separation of concerns by feature rather than lifecycle phase) and vastly improves logic reusability.

***

## 5. State Management

**Q: Compare local component state with global state management. When is a tool like Redux, Zustand, or Vuex necessary?**
*Answer:*
* **Local State:** Managed within a single component file (e.g., `useState` in React, `ref` or `reactive` in Vue). You should use this for state that only affects the component itself, such as a dropdown open/closed status, modal toggles, or controlled form input values.
* **Global State:** State that is accessible and modifiable by any component in the application, regardless of its position in the component tree.
* *When to use global state:* When multiple non-adjacent components need to share or update the exact same data points (e.g., user authentication credentials, shopping cart contents, system theme preferences). Using local state becomes inefficient because passing props down many component layers ("prop drilling") is unmaintainable. Tools like Redux, Zustand (React), or Pinia/Vuex (Vue) provide a centralized store, predictable state updates, and better debugging capabilities.

***

## 6. Performance Optimization

**Q: List three strategies for optimizing frontend performance.**
*Answer:*
1. **Code Splitting & Lazy Loading:** Break down large JavaScript bundles into smaller chunks. Load only the code necessary for the initial route rendering, and lazy-load other components/routes asynchronously on-demand. This heavily reduces the initial payload and Time to Interactive (TTI).
2. **Image Optimization:** Compress heavy images, use modern WebP/AVIF formats, and explicitly serve sizing utilizing the `<picture>` tag or `srcset` attributes. Implement lazy loading for images below the fold so they only fetch when scrolled into view.
3. **Memoization & Caching:** Minimize unnecessary component re-renders. In React, utilize `useMemo`, `useCallback`, and `React.memo` to cache expensive calculations and prevent re-rendering when props haven't structurally changed. On the network side, leverage standard HTTP caching headers (Cache-Control).

***

## 7. Accessibility (a11y)

**Q: What is ARIA, and what are some essential practices to ensure a web application is accessible?**
*Answer:*
**ARIA (Accessible Rich Internet Applications)** is a set of HTML attributes that define ways to make web content and applications more accessible to people with disabilities, especially when native semantic HTML is insufficient (e.g., implementing custom complex UI components like comboboxes or custom tab panels).
* *Essential Practices:*
  * Prefer semantic HTML elements first. Only apply ARIA when pure semantic HTML falls short.
  * Provide descriptive `alt` text for all meaningful images.
  * Ensure sufficient color contrast between text and background elements.
  * Validate that all interactive and actionable elements are focusable and functional entirely via keyboard navigation (Tab-key compatibility).

***

## 8. Git Workflow

**Q: Describe a standard Git workflow for a team environment (e.g., Feature Branch Workflow).**
*Answer:*
1. **Main Branch:** The `main` (or `master`) branch represents the stable, production-ready state. Directly committing here is strictly prohibited.
2. **Branching:** When starting a new specific ticket or feature, developers create a dedicated feature branch radiating from `main` (e.g., `feat/user-auth` or `bugfix/header-overlap`).
3. **Committing:** Developers iterate locally, creating logical commits with descriptive, conventional messages on their feature branch.
4. **Pull Requests (PR):** Upon completion, a PR is opened against `main`. Automated CI/CD pipelines trigger formatting checks and tests. Peers review the code for architecture and logic.
5. **Merging:** After peer approval and green tests, the feature branch is merged into `main` (often squashed) to keep the central history linear and clean.

***

## 9. TypeScript Benefits

**Q: How does TypeScript improve frontend development compared to vanilla JavaScript?**
*Answer:*
TypeScript, a syntactic superset of JS, introduces static typing.
1. **Early Error Detection:** Type errors are caught during compilation time inside the IDE rather than blindly executing and crashing at runtime in the browser GUI.
2. **Enhanced IDE Support:** Explicit typing provides rich autocompletion, intelligent code refactoring, and inline documentation, vastly boosting developer velocity.
3. **Confident Refactoring:** Changing an entity model or function signature safely flags all consuming areas in the codebase that require a structural update.
4. **Self-Documenting Code:** Explicit type definitions naturally document what exact data structures a function or component expects and returns, making onboarding significantly easier.

***

## 10. Basic Frontend Architecture Considerations

**Q: What factors should you consider when designing the architecture of a large-scale frontend application?**
*Answer:*
1. **Component Reusability Ecosystem:** Designing a consistent UI library using atomic design principles (atoms, molecules, organisms) to ensure design system consistency and speed of continuous UI development.
2. **Data Fetching and Server State:** Differentiating local state from server state using dedicated tools (React Query/SWR/Apollo) that implicitly handle caching, retries, and background refetching.
3. **Routing and Module Boundaries:** Architecting routing for massive apps by employing robust lazy-loading principles to enforce minimal bundle delivery bounds.
4. **Testing Layers Structure:** Emphasizing testing boundaries—Unit testing (atomic utility functions), Integration testing (component integration), and overarching End-to-End browser testing (vital user scenarios).
5. **Separation of Concerns:** Deeply decoupling presentation layers (UI components) from business logic, data fetching rules, and third-party interactions utilizing custom hooks, pure functions, or distinct service layers.
