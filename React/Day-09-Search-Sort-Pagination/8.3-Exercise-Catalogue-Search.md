# Day 8 Task — Product Catalogue with Search, Filters, Sorting and Pagination

**Concepts practised:** Derived data pipeline, URL-driven controls, debouncing, pagination, responsive layout, CSS Modules (or Tailwind).

**Time:** 3 hours
**Marks:** 100

---

## 1. Problem Statement

Upgrade your Day 7 multi-page application so that the list page becomes a **full catalogue**. You may use the DummyJSON products API (`/products?limit=0` and `/products/category-list`) or another API that returns a few hundred items (for example DummyJSON recipes or REST Countries).

## 2. Required Features

### 2.1 Search

- [ ] Case-insensitive search by title (also search at least **one more field**, for example brand or tags).
- [ ] The text box updates immediately but the list/URL updates after a **debounce of 300–500 ms**.
- [ ] Search term is stored in the URL (`?search=`).

### 2.2 Filters

- [ ] Category dropdown loaded from the API.
- [ ] **Price range** filter (min and max inputs or a slider). Validate that min ≤ max.
- [ ] **Minimum rating** filter (Any / 3+ / 4+ / 4.5+).
- [ ] **In stock only** checkbox (use `stock > 0` or `availabilityStatus`).
- [ ] **Clear filters** button which also empties the search box.

### 2.3 Sorting

- [ ] Sort by: Default, Price low→high, Price high→low, Rating, Name A→Z.
- [ ] The sort must never mutate the original array.

### 2.4 Pagination

- [ ] 12 items per page.
- [ ] Reusable `Pagination` component with Previous / Next and page numbers (with `…` for long lists).
- [ ] Current page is stored in the URL (`?page=`), clamped to a valid range.
- [ ] The page resets to 1 whenever search, a filter or sort changes.
- [ ] Text such as *"Showing 13–24 of 87 products"*.

### 2.5 UI states

- [ ] Loading skeleton or loader.
- [ ] Error with retry.
- [ ] Empty state: *"No products match your filters"* with a **Clear filters** button.

## 3. Technical Requirements

- [ ] Raw data is fetched **once**, with `Promise.all` for products and categories.
- [ ] Filtered, sorted and visible lists are **derived**, never stored in state.
- [ ] A `useListParams` (or similar) helper centralises reading/updating URL params.
- [ ] A `useDebounce` hook in `src/hooks`.
- [ ] Controls (`search`, `category`, `minPrice`, `maxPrice`, `rating`, `inStock`, `sort`, `page`) live in the URL; opening a copied link in a new tab shows the identical view.
- [ ] All components are styled using CSS Modules (or Tailwind, consistently).
- [ ] The grid works from 320px to 1440px without horizontal scrolling.

## 4. Suggested Folder Structure

```text
src/
├── hooks/
│   ├── useDebounce.js
│   └── useListParams.js
├── utils/
│   ├── filterProducts.js     // pure functions: search, filter, sort, paginate
│   └── formatters.js         // formatCategory, formatPrice
├── components/
│   ├── SearchBox.jsx
│   ├── ProductFilters.jsx
│   ├── ProductCard.jsx / ProductCard.module.css
│   ├── Pagination.jsx / Pagination.module.css
│   └── ...
└── pages/
    └── ProductsPage.jsx
```

**Tip:** Put the pipeline into pure functions in `utils/filterProducts.js`, then test them using `console.log` before using them in React.

```js
export function applyFilters(products, { search, category, minPrice, maxPrice, rating, inStock }) { /* ... */ }
export function sortProducts(products, sort) { /* ... */ }
export function paginate(items, page, pageSize) { /* ... */ }
```

## 5. Testing Checklist

| # | Test | Pass? |
|---|---|---|
| 1 | Go to page 5, then type a search: page resets to 1 | |
| 2 | Open `?page=9999`, `?page=-1`, `?page=abc`: app shows a valid page | |
| 3 | Combine search + category + price range + sort: results correct | |
| 4 | Copy the URL, open in a new tab: same results | |
| 5 | Type quickly: URL changes only after a pause | |
| 6 | Browser Back button: goes to the previous filter state | |
| 7 | Sorting the same list twice never changes the "Default" order | |
| 8 | Narrow screen (375px): filters stack neatly, cards readable | |

## 6. Marking Rubric (100 marks)

| Criteria | Marks |
|---|---:|
| Search with debounce | 10 |
| Filters (category, price range, rating, stock) | 20 |
| Sorting without mutation | 10 |
| Pagination logic and component | 15 |
| URL as the source of truth (all controls) | 15 |
| Derived data and pure utility functions | 10 |
| Loading / error / empty states | 5 |
| Responsive design and CSS Modules | 10 |
| Code quality and README | 5 |
| **Total** | **100** |

## 7. Viva Questions

1. Which pieces are state and which are derived? Show them in your code.
2. Why does the page reset when the search changes?
3. What happens if the user opens `?page=500`?
4. How does your debounce work? What would happen without the cleanup?
5. Why is `[...list].sort()` used instead of `list.sort()`?
6. When would you switch from client-side to server-side pagination?

## 8. Stretch Goals

- Remember the **last used sort** in `localStorage` as the default when no `sort` param exists.
- Add a "grid / list" view toggle.
- Highlight the search term in the product title (hint: split the title with a regular expression and wrap matches in `<mark>`).
- Replace `eslint-disable` in `SearchBox` with a cleaner design using an `onChange` approach: call `onSearch` from a debounced callback or use a `key`.
- Implement **server-side** pagination for a second page using `?limit=12&skip=...` and compare the two approaches in your README.

## 9. Submission

1. Push to GitHub (branch `day-8`).
2. README: features, URL parameters table, and screenshots (desktop and mobile).
3. Share the repository link.
