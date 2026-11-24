# Day 7 Task — Multi-Page Catalogue with React Router

**Concepts practised:** `BrowserRouter`, layout routes, `Outlet`, `NavLink`, dynamic routes, `useParams`, `useSearchParams`, `useNavigate`, 404 page.

**Time:** 2.5–3 hours
**Marks:** 100

---

## 1. Problem Statement

Convert your Day 6 explorer into a proper **multi-page application** (or build a new one with the same API). It must have a navigation bar, a list page, a details page, and several static pages.

## 2. Pages and Routes

| Route | Page | Requirements |
|---|---|---|
| `/` | Home | Short welcome, 4 featured items (fetched), button linking to the list |
| `/items` *(rename to your topic: `/products`, `/recipes`, `/movies`...)* | List | Grid of cards; search stored in the URL |
| `/items/:id` | Details | Fetch by id; loading, error and **not found** state |
| `/about` | About | Static content about the project |
| `/contact` | Contact | A controlled form (name, email, message) with validation; after success, `navigate("/")` and show a message |
| `*` | 404 | Friendly message and link home |

## 3. Required Features

### 3.1 Layout and navigation

- [ ] One `MainLayout` with `Navbar`, `<Outlet />` and `Footer`.
- [ ] `NavLink` with a clearly highlighted active link. The Home link uses `end`.
- [ ] Scroll to top when the route changes (`ScrollToTop`).
- [ ] The navbar is responsive (it must not overflow on a 375px wide screen).

### 3.2 List page

- [ ] Search input stored in the URL (`?search=`), restored on refresh.
- [ ] Each card links to its details page with `Link`.
- [ ] Back button of the browser returns to the same search result.

### 3.3 Details page

- [ ] The id is read from `useParams`.
- [ ] Fetch with `AbortController`; effect depends on the id.
- [ ] Shows **Not found** if the API returns 404 (try `/items/99999`).
- [ ] **Back to list** link that preserves the previous search (hint: `navigate(-1)`).
- [ ] **Previous / Next** buttons that move to `id - 1` and `id + 1` (disable *Previous* when `id` is 1).

### 3.3.1 Extra

- [ ] Set the browser tab title to the item's title (`document.title`) using `useEffect`, and restore the original title in the cleanup.

### 3.4 Contact page

- [ ] Fields: name, email, message. Show validation errors.
- [ ] On valid submit, redirect to `/` using `useNavigate`, passing a success message through route `state` and display it on the Home page.

## 4. Technical Rules

- Use **relative** child paths inside the layout route.
- No `<a href>` for internal links.
- Pages live in `src/pages`, reusable components in `src/components`, layout in `src/layouts`.
- Reuse `Loader`, `ErrorMessage` and the service layer from Day 6.
- No duplicated fetching code: create at least one helper or component to avoid repetition.

## 5. Suggested Folder Structure

```text
src/
├── main.jsx
├── App.jsx
├── layouts/MainLayout.jsx
├── pages/
│   ├── HomePage.jsx
│   ├── ListPage.jsx
│   ├── DetailsPage.jsx
│   ├── AboutPage.jsx
│   ├── ContactPage.jsx
│   └── NotFoundPage.jsx
├── components/
│   ├── Navbar.jsx
│   ├── Footer.jsx
│   ├── ScrollToTop.jsx
│   ├── ItemCard.jsx
│   ├── Loader.jsx
│   └── ErrorMessage.jsx
└── services/
    ├── apiClient.js
    └── itemService.js
```

## 6. Testing Checklist

| # | Test | Pass? |
|---|---|---|
| 1 | Click through every nav link: page does not reload (watch the Network tab) | |
| 2 | Refresh while on `/items/5`: details page still works | |
| 3 | Type a search, open an item, press browser Back: search restored | |
| 4 | Open `/something-random`: 404 page appears | |
| 5 | Open `/items/99999`: friendly not-found message | |
| 6 | Use Previous and Next quickly on the details page: no wrong data | |
| 7 | Narrow the browser to mobile width: layout still usable | |

## 7. Marking Rubric (100 marks)

| Criteria | Marks |
|---|---:|
| Routes configured correctly (layout, index, relative paths, 404) | 20 |
| Navigation (`Link`, `NavLink`, `useNavigate`) | 10 |
| Dynamic details page with correct dependencies and states | 20 |
| Search in URL (`useSearchParams`) | 15 |
| Contact form and redirect | 10 |
| Previous / Next and `document.title` | 5 |
| Code organisation and reuse | 10 |
| Responsive UI and accessibility | 5 |
| README and screenshots | 5 |
| **Total** | **100** |

## 8. Viva Questions

1. Explain what happens between clicking a `Link` and seeing the next page.
2. What is `Outlet`? Where did you use it?
3. Why does your details page re-fetch when you click Next?
4. Why is the search in the URL and not in `useState`?
5. What is the difference between `/items/5` and `/items?id=5`? Which one is better here?
6. What will happen on a production server if you refresh on `/items/5`? (Preview answer for Day 11.)

## 9. Stretch Goals

- Add pagination parameters (`?page=2`) now; Day 8 will improve them.
- Add breadcrumbs (`Home / Items / Item name`) using `useLocation`.
- Animate page transitions with CSS classes.

## 10. Submission

1. Push to GitHub (branch `day-7`).
2. README with route table, features and screenshots of the list, details and 404 pages.
3. Share the repository link.
