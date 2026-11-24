# Day 9 Task — Shopping Cart, Favourites and Theme with Context + `useReducer`

**Concepts practised:** `createContext`, Provider, custom hooks, `useReducer`, global state, persistence, derived totals.

**Time:** 3 hours
**Marks:** 100

---

## 1. Problem Statement

Extend your Day 8 catalogue into a small e-commerce front end with a **cart**, **favourites** and a **dark mode**. All three must use the Context pattern from the notes. The cart must use `useReducer`.

## 2. Required Features

### 2.1 Cart (`CartProvider` + `useCart`)

- [ ] **Add to cart** button on every product card and on the details page.
- [ ] If the product is already in the cart, increase the quantity (no duplicates).
- [ ] Navbar cart link with a **badge** showing the total quantity.
- [ ] `/cart` page that lists items with image, title, unit price, quantity controls (− / +), line total and **Remove**.
- [ ] Decreasing quantity to 0 removes the item.
- [ ] Order summary: subtotal, a simple discount rule (see 2.4), **total**.
- [ ] **Clear cart** button.
- [ ] Empty cart state with a link back to the products.
- [ ] Cart survives refresh (`localStorage` with a safe loader).

### 2.2 Favourites (`FavouritesProvider` + `useFavourites`)

- [ ] Heart button toggles favourite on cards and on the details page.
- [ ] Navbar link with favourites count.
- [ ] `/favourites` page with the saved products and a way to remove them.
- [ ] Persisted in `localStorage`.

### 2.3 Theme (`ThemeProvider` + `useTheme`)

- [ ] Light / dark toggle in the navbar.
- [ ] Uses CSS variables and `data-theme` on `<html>`.
- [ ] Remembers the choice; also uses the user's system preference (`window.matchMedia("(prefers-color-scheme: dark)").matches`) as the **first-visit** default.

### 2.4 Business rules inside the reducer / derived data

- [ ] Maximum quantity per item is **10**. Adding more is ignored and a message is shown (hint: handle in the reducer by not changing state, and compare in the UI with `quantity >= 10` to disable **+**).
- [ ] If the subtotal is above **$500**, apply a **10% discount** (derived value, not stored).
- [ ] Prices are shown with two decimals.

## 3. Technical Requirements

- [ ] `cartReducer` is a **pure function in its own file** (`context/cartReducer.js`) and does not mutate state.
- [ ] Reducer actions: `ADD_ITEM`, `REMOVE_ITEM`, `INCREASE`, `DECREASE`, `CLEAR`.
- [ ] Context values expose **friendly functions** (`addItem`, `removeItem`...) rather than raw `dispatch`.
- [ ] Each custom hook throws a clear error when used outside its Provider.
- [ ] Totals (`totalItems`, `subtotal`, `discount`, `total`) are **derived**, not stored.
- [ ] Providers are composed in `main.jsx` in a sensible order.
- [ ] Reducer tests: a file `cartReducer.test-notes.md` (or console script) with at least **8** scenarios and expected results. (You will write automated tests later in the course; for now, write the scenarios and verify them manually with `console.log`.)

## 4. Suggested Folder Structure

```text
src/
├── context/
│   ├── CartContext.jsx
│   ├── cartReducer.js
│   ├── FavouritesContext.jsx
│   └── ThemeContext.jsx
├── pages/
│   ├── CartPage.jsx
│   └── FavouritesPage.jsx
└── components/
    ├── CartLink.jsx
    ├── AddToCartButton.jsx
    ├── FavouriteButton.jsx
    └── ThemeToggle.jsx
```

## 5. Reducer Scenarios to Verify

| # | Starting state | Action | Expected result |
|---|---|---|---|
| 1 | empty | `ADD_ITEM` product 1 | 1 line, quantity 1 |
| 2 | product 1 qty 1 | `ADD_ITEM` product 1 | 1 line, quantity 2 |
| 3 | product 1 qty 2 | `DECREASE` 1 | quantity 1 |
| 4 | product 1 qty 1 | `DECREASE` 1 | cart empty |
| 5 | product 1 qty 10 | `INCREASE` 1 | still 10 |
| 6 | two products | `REMOVE_ITEM` first | only second remains |
| 7 | any | `CLEAR` | empty |
| 8 | any | unknown action | throws an error |

## 6. Testing Checklist

| # | Test | Pass? |
|---|---|---|
| 1 | Add the same product 3 times from different pages: one line with quantity 3 | |
| 2 | Refresh the page: cart and favourites remain | |
| 3 | Break the stored data in DevTools (`localStorage` value `{{{`): app still loads | |
| 4 | Remove the `CartProvider` temporarily: you see your clear error message | |
| 5 | Open React DevTools: do you see the providers in the tree? | |
| 6 | Toggle theme: all pages, including cart, follow it | |
| 7 | Subtotal $499.99 → no discount; $500.01 → 10% discount | |

## 7. Marking Rubric (100 marks)

| Criteria | Marks |
|---|---:|
| Cart context + reducer (pure, immutable, all actions) | 25 |
| Cart page and navbar badge | 15 |
| Favourites context and page | 15 |
| Theme context | 10 |
| Business rules (max quantity, discount) as derived data | 10 |
| Persistence and safe loading | 5 |
| Custom hooks with guard errors | 5 |
| Reducer scenarios verified and documented | 5 |
| UI quality and accessibility (labels on icon buttons) | 5 |
| README and code quality | 5 |
| **Total** | **100** |

## 8. Viva Questions

1. Why did you choose `useReducer` for the cart but maybe `useState` for the theme?
2. Why can't the reducer write to `localStorage`?
3. Which components re-render when an item is added? How can you see this in React DevTools?
4. What happens if two Providers are in the wrong order (for example, a Provider that uses another Provider's hook)?
5. Why is `total` not stored in the reducer state?
6. How would you test your reducer without a browser?

## 9. Stretch Goals

- Add a `CartDrawer` (slide-in mini cart) that is controlled by a `UIContext` (`isCartOpen`).
- Create a **"Move to favourites"** button on a cart row.
- Add a coupon code field (`SAVE10`) handled by a new reducer action `APPLY_COUPON`.
- Use a Context `value` memoised with `useMemo` (preview of Day 10) and compare the number of renders with the React DevTools Profiler.

## 10. Submission

1. Push to GitHub (branch `day-9`).
2. README: features, context/reducer design diagram (a simple text diagram is fine), reducer scenarios table, screenshots.
3. Share the repository link.
