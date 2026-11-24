# Day 5 Task — Task Manager Pro

**Concepts practised:** Lifting state up, immutable updates, derived data, `localStorage`, `useRef`.

**Time:** 2.5–3 hours
**Marks:** 100
**Rule:** Build it yourself. You may read the Day 5.1 notes, but do **not** copy the sample Task Manager. Your app must be different (different name, design, and at least two extra features).

---

## 1. Problem Statement

Build a **Task Manager** that a real person could use every day. Tasks must survive a page refresh.

## 2. Required Features

### 2.1 Core

- [ ] Add a task (title is required, trim spaces, no duplicates ignoring case).
- [ ] Mark a task as completed or active.
- [ ] Edit a task title.
- [ ] Delete a task.
- [ ] Filter: **All / Active / Completed**.
- [ ] Show the counts: total, completed, remaining (**derived, not stored in state**).
- [ ] **Clear completed** button (visible only when something is completed).
- [ ] Empty state message for every filter (different message for each).

### 2.2 Persistence

- [ ] Tasks are saved to `localStorage` and loaded using a lazy initialiser.
- [ ] Corrupted `localStorage` data must not crash the app (use `try/catch`).
- [ ] The selected filter is also remembered after refresh.

### 2.3 Extra features (choose **at least 2**)

- [ ] Priority (Low / Medium / High) with a coloured badge and a sort-by-priority option.
- [ ] Due date; overdue tasks are highlighted (derived).
- [ ] Search box (case-insensitive).
- [ ] Drag-free reordering with Move up / Move down buttons (immutable).
- [ ] Undo the last delete (hint: keep the last deleted task in state).
- [ ] Categories (Study / Work / Personal) with a category filter.

### 2.4 `useRef`

- [ ] The input receives focus when the page loads and after adding a task.
- [ ] When editing, the edit input receives focus automatically.

## 3. Technical Requirements

- [ ] All state for tasks lives in **`App`** (lifted state).
- [ ] At least **five** components, each in its own file.
- [ ] No mutation of state anywhere (`push`, `splice`, direct assignment).
- [ ] Each task has a unique `id` generated when the task is created.
- [ ] No `index` used as a key.
- [ ] No duplicated state (for example, no `filteredTasks` state).
- [ ] Event handlers use the callback form `setTasks((prev) => ...)` when updating from previous state.
- [ ] Meaningful names and short comments where logic is not obvious.

## 4. Suggested Folder Structure

```text
src/
├── App.jsx
├── index.css
├── components/
│   ├── TaskForm.jsx
│   ├── TaskFilter.jsx
│   ├── TaskStats.jsx
│   ├── TaskList.jsx
│   └── TaskItem.jsx
└── utils/
    └── storage.js        // loadFromStorage(key, fallback), saveToStorage(key, value)
```

A good `storage.js` makes your code cleaner:

```js
export function loadFromStorage(key, fallback) {
  try {
    const saved = localStorage.getItem(key);
    return saved ? JSON.parse(saved) : fallback;
  } catch {
    return fallback;
  }
}

export function saveToStorage(key, value) {
  localStorage.setItem(key, JSON.stringify(value));
}
```

## 5. Testing Checklist (do this before you submit)

| # | Test | Pass? |
|---|---|---|
| 1 | Add three tasks, refresh the page: tasks are still there | |
| 2 | Open DevTools → Application → Local Storage, change the value to `abc` and refresh: app does not crash | |
| 3 | Try to add an empty task and a task with only spaces | |
| 4 | Edit a task, press `Escape`: the old title returns | |
| 5 | Complete two tasks, switch filters: lists and counts are correct | |
| 6 | Delete a task while a filter is active | |
| 7 | Open React DevTools: is there any state that could be calculated instead? | |

## 6. Marking Rubric (100 marks)

| Criteria | Marks |
|---|---:|
| Core features working | 25 |
| Lifted state and component structure | 15 |
| Immutable updates and unique keys | 15 |
| Derived data (no duplicated state) | 10 |
| `localStorage` persistence and error handling | 10 |
| `useRef` usage | 5 |
| Extra features (2 × 5) | 10 |
| UI quality and responsiveness | 5 |
| Code readability and naming | 5 |
| **Total** | **100** |

## 7. Viva Questions (be ready)

1. Which component owns the tasks and why?
2. Show me where data flows down and where events flow up.
3. Which values in your app are derived? Show the code.
4. What happens if you replace `setTasks((prev) => prev.filter(...))` with `tasks.splice(...)`?
5. Why is `useState(loadTasks)` better than `useState(loadTasks())`?
6. What would break if two tasks had the same id?

## 8. Stretch Goals

- Add keyboard shortcuts (`/` focuses the search box).
- Export tasks as a JSON file and import them again.
- Move the `localStorage` logic into a reusable function and use it for two different keys (you will convert it to a hook on Day 10).

## 9. Submission

1. Push your project to your own GitHub repository (branch `day-5`).
2. The repository must include a `README.md` with: project description, features, how to run it, and 2 screenshots.
3. Share the repository link.
