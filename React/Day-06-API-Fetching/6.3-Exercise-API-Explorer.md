# Day 6 Task — Movie / Product / User Explorer with a Real API

**Concepts practised:** `fetch`, `useEffect`, loading / error / empty / success states, `AbortController`, service layer, `.env`.

**Time:** 2.5–3 hours
**Marks:** 100

---

## 1. Problem Statement

Build a data explorer using **one** public API of your choice. Pick a different API from the sample in the notes.

| API | Base URL | Notes |
|---|---|---|
| DummyJSON products | `https://dummyjson.com/products` | Good for shop-like apps |
| DummyJSON recipes | `https://dummyjson.com/recipes` | Images, ingredients, ratings |
| Rick and Morty | `https://rickandmortyapi.com/api/character` | Pagination, search by `?name=` |
| PokeAPI | `https://pokeapi.co/api/v2/pokemon?limit=20` | List, then detail URLs |
| REST Countries | `https://restcountries.com/v3.1/all?fields=name,flags,region,population,capital` | Filtering by region |
| JSONPlaceholder | `https://jsonplaceholder.typicode.com/users` | Users, posts, comments |

*(Public APIs can change or go offline. If your API fails, inspect the response in the browser, check the API documentation, or switch to DummyJSON.)*

## 2. Required Features

### 2.1 Listing

- [ ] Fetch and show at least **12** items as cards in a responsive grid.
- [ ] Each card shows an image, a title and at least two other fields.
- [ ] **Loading** state with a spinner or skeleton cards.
- [ ] **Error** state with a clear message and a **Retry** button that really retries.
- [ ] **Empty** state when a search has no results.

### 2.2 Search

- [ ] A search input that re-fetches (or filters) when the user types.
- [ ] Outdated requests are cancelled with `AbortController`.
- [ ] No "flash" of old results after a newer search (race condition handled).

### 2.3 Details

- [ ] Clicking a card shows a details section (a modal, side panel or below the list). Fetch the details from the API using the item's id. (Real routing comes on Day 7.)
- [ ] The details panel has its own loading and error state.
- [ ] A **Close** button.

### 2.4 Code organisation

- [ ] `services/apiClient.js` with a shared `request()` function that checks `response.ok`.
- [ ] `services/<name>Service.js` with functions such as `getItems`, `getItemById`, `searchItems`.
- [ ] The API base URL is stored in `.env` as `VITE_API_URL`, and `.env.example` is committed.
- [ ] Reusable `Loader`, `ErrorMessage`, `EmptyState` components.
- [ ] No component contains `fetch(` directly.

## 3. Technical Rules

- Use `async/await` with `try/catch/finally`.
- Never call `fetch` in the component body.
- The dependency arrays must be correct (no missing dependencies).
- Handle `AbortError` without showing an error message.
- Do **not** commit secrets. (This task needs none.)
- Alt text on every image and a `<label>` or `aria-label` for the search input.

## 4. Suggested Folder Structure

```text
src/
├── App.jsx
├── index.css
├── components/
│   ├── Loader.jsx
│   ├── ErrorMessage.jsx
│   ├── EmptyState.jsx
│   ├── ItemCard.jsx
│   ├── ItemGrid.jsx
│   ├── SearchBar.jsx
│   └── ItemDetails.jsx
└── services/
    ├── apiClient.js
    └── itemService.js
.env
.env.example
```

## 5. Testing Checklist

| # | Test | Pass? |
|---|---|---|
| 1 | Throttle the network to **Slow 3G** in DevTools: is the loader shown? | |
| 2 | Switch DevTools to **Offline** and refresh: error + Retry works after going online | |
| 3 | Change the URL to a wrong path (for example `/productz`): friendly error, no crash | |
| 4 | Type a search word that has no results | |
| 5 | Type quickly: only the last search result is displayed | |
| 6 | Open details for item A, then quickly for item B: details show B, never A | |
| 7 | In the Network tab, are cancelled requests shown as `(canceled)`? | |

## 5.1 Mini Challenge

Without using any library, add a **"Last updated at HH:MM:SS"** line below the list that updates every time data is successfully loaded.

## 6. Marking Rubric (100 marks)

| Criteria | Marks |
|---|---:|
| Correct data fetching inside `useEffect` | 15 |
| Loading / error / empty / success states | 20 |
| Search with cancellation (no race conditions) | 15 |
| Details fetch with its own states | 10 |
| Service layer and `.env` | 15 |
| Component structure and reusability | 10 |
| UI quality, responsiveness, accessibility | 10 |
| Code readability and README | 5 |
| **Total** | **100** |

## 7. Viva Questions

1. Why can't `fetch` run in the component body?
2. What happens if you remove `controller.abort()` from the cleanup?
3. Why do we check `response.ok`?
4. Why is the base URL in `.env`? Can we hide a secret key there? Why not?
5. What would happen if you forget `[query]` in the dependency array?
6. Show me where the four UI states are handled.

## 8. Stretch Goals

- Cache results in a `useRef` map so going back to a previous search does not re-fetch.
- Add a "Load more" button using `limit` and `skip` (or the API's page parameter).
- Show skeleton cards instead of a text loader.

## 9. Submission

1. Push to your GitHub repository (branch `day-6`).
2. `README.md` with: API used, features, how to run, `.env.example` explanation, screenshots of loading, error and success states.
3. Share the repository link.
