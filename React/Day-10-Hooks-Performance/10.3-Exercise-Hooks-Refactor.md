# Day 10 Task — Refactor to Custom Hooks, Measure Performance and Add Error Handling

**Concepts practised:** Custom hooks, Rules of Hooks, `useMemo`, `useCallback`, `React.memo`, React Profiler, Error Boundaries, `React.lazy`.

**Time:** 3 hours
**Marks:** 100

---

## 1. Problem Statement

Take your Day 9 application and **improve its engineering quality without adding new visible features**. This is a **refactoring** day. At the end the app should behave the same, but the code should be shorter, more reusable, measurably faster in at least one place, and safer when something fails.

## 2. Required Work

### 2.1 Custom hooks (create in `src/hooks/`)

- [ ] `useFetch(path, { skip })` returning `{ data, loading, error, refetch }` with `AbortController`.
- [ ] `useLocalStorage(key, initialValue)`.
- [ ] `useDebounce(value, delay)`.
- [ ] `useToggle(initial)`.
- [ ] One **extra hook of your choice** (for example `useOnClickOutside`, `useWindowWidth`, `useDocumentTitle`, `useMediaQuery`).

### 2.2 Refactor the app to use them

- [ ] **At least 3 pages/components** that previously contained `useState + useEffect` fetching now use `useFetch`.
- [ ] Theme, favourites or the cart use `useLocalStorage` where suitable. (If `useReducer` makes this awkward, explain why in your README.)
- [ ] The search box uses `useDebounce`.
- [ ] Show in the README a **before/after line count** for one refactored file.

### 2.3 Performance (measure first!)

- [ ] Install React DevTools. Record a Profiler session while typing in the search box on the list page.
- [ ] Save **screenshots (before)** and note which components re-render and how long it takes.
- [ ] Apply the right fix: `memo` for `ProductCard`, `useCallback` for handlers passed to it, `useMemo` for the filtered/sorted list and for the Cart Provider `value`.
- [ ] Record again. Save **screenshots (after)** and write 5–8 lines: what changed, what you measured, and whether it was worth it.
- [ ] Add **one place where you decided NOT to optimise** and explain why.

### 2.4 Error handling

- [ ] `ErrorBoundary` class component around `<Outlet />` in the layout, resettable on route change (use `key={location.pathname}`).
- [ ] A hidden test page (`/debug-crash`) that throws on render so you can prove the boundary works. Remove or hide it for the final submission.
- [ ] A **second** boundary around one risky widget (for example product reviews) with its own smaller fallback.

### 2.5 Lazy loading

- [ ] Convert at least **3 pages** to `React.lazy` with a single `Suspense` fallback.
- [ ] Run `npm run build` and note in the README how many JavaScript chunks were produced and their sizes (the build prints them).

## 3. Technical Rules

- Hooks follow the Rules of Hooks, and the ESLint plugin shows **no hook warnings**. Do not use `eslint-disable` for hook rules without a written explanation.
- Each custom hook has a short comment describing its parameters and return value.
- No hook has more than one responsibility.
- Keep the app working after each refactoring step. Commit after every step (at least **6 commits** with meaningful messages).

## 4. Suggested Folder Structure

```text
src/
├── hooks/
│   ├── useFetch.js
│   ├── useLocalStorage.js
│   ├── useDebounce.js
│   ├── useToggle.js
│   └── useOnClickOutside.js
├── components/
│   ├── ErrorBoundary.jsx
│   └── ...
└── docs/
    ├── profiler-before.png
    └── profiler-after.png
```

## 5. Testing Checklist

| # | Test | Pass? |
|---|---|---|
| 1 | Every screen still works as it did on Day 9 | |
| 2 | Turn the network offline: error + retry still work through `useFetch` | |
| 3 | Open `/debug-crash`: fallback UI appears; navbar still works; navigating away resets the boundary | |
| 4 | Profiler "after" shows fewer or faster renders than "before" | |
| 5 | Network tab shows separate chunks being loaded when opening a lazy page for the first time | |
| 6 | `npm run lint` has no errors | |
| 7 | `npm run build` succeeds | |

## 6. Marking Rubric (100 marks)

| Criteria | Marks |
|---|---:|
| Quality of the custom hooks (API design, cleanup, comments) | 25 |
| Refactoring: hooks actually used, less duplication | 15 |
| Performance: measured before and after, correct use of memo / useMemo / useCallback | 20 |
| Error boundaries (global + local) and reset behaviour | 15 |
| Lazy loading and Suspense | 10 |
| Lint-clean code, commits and README analysis | 10 |
| "Where I did not optimise" reasoning | 5 |
| **Total** | **100** |

## 7. Viva Questions

1. What is the difference between sharing logic and sharing state? Which did you use for `useLocalStorage`?
2. Why does `useFetch` depend on `path` and not on an options object?
3. What did the Profiler show before your changes? What was the cause?
4. Why did you wrap the Cart Provider's value in `useMemo`? What does it prevent?
5. Which errors will your boundary not catch? How do you handle them?
6. What would happen if you remove `Suspense` from the lazy-loaded routes?

## 8. Stretch Goals

- Add `useMediaQuery("(max-width: 600px)")` and use it to switch the navbar to a mobile menu.
- Add a `useEventListener(eventName, handler)` hook and use it to close the cart drawer when pressing `Escape`.
- Write a `useAsync(fn)` hook for event-triggered requests (for example, form submissions) with `{ run, loading, error }`.
- Prefetch a lazy page when the user hovers over its link (`onMouseEnter={() => import("./pages/CartPage")}`).

## 9. Submission

1. Push to GitHub (branch `day-10`) with at least 6 commits.
2. README sections: *Hooks created*, *Before/After code*, *Performance analysis with screenshots*, *Error handling*, *Build output*.
3. Share the repository link.
