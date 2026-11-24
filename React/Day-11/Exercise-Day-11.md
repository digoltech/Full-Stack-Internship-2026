# Day 11 Task — Final Project: Deployed React Application (Frontend Capstone)

**Concepts practised:** Everything from Days 1–11.

**Time:** 4–5 hours on the day (you may continue the polish afterwards before the review)
**Marks:** 100
**Exit requirement of the frontend phase:** *"Students should be able to build a React interface and consume an API independently."*

---

## 1. Problem Statement

Finish your multi-page application (the project you built from Days 7–10) as a **polished, deployed, portfolio-quality** frontend. You may keep the shop idea or change the domain (recipes, movies, jobs, courses, books...), as long as the API provides a **list, details, search/filter** and (preferably) **login**.

## 2. Mandatory Requirements

### 2.1 Routes (minimum 3, expect 6+)

| Route | Description |
|---|---|
| `/` | Landing/home page |
| `/items` | List with search, filter, sort and pagination (state in the URL) |
| `/items/:id` | Details page |
| `/login` | Login form with validation, server errors and redirect back |
| `/cart` or `/favourites` | Protected page using global state |
| `/profile` | Protected page showing the logged-in user |
| `*` | 404 page |

### 2.2 Features checklist

**Data and UI**

- [ ] Data fetched from an API using `useFetch` (or equivalent) with loading, error, empty and success states.
- [ ] Search with debounce, at least two filters, sorting, pagination. All stored in the URL.
- [ ] Details page with its own states and a "not found" case.
- [ ] Reusable components (`Button`, `Card`, `Loader`, `ErrorMessage`, `EmptyState`, `Pagination`...).

**State**

- [ ] Context + `useReducer` for the cart (or favourites).
- [ ] `AuthContext` with login/logout and a persisted session.
- [ ] Theme (light/dark) persisted.
- [ ] No duplicated state; derived data is calculated.

**Engineering**

- [ ] Services layer and `.env` / `.env.example`.
- [ ] At least **4 custom hooks**.
- [ ] `ErrorBoundary` in the layout.
- [ ] Lazy-loaded pages.
- [ ] `memo` / `useMemo` / `useCallback` used where **measured** to help (explain in README).
- [ ] ESLint passes (`npm run lint`) and `npm run build` works.

**Quality**

- [ ] Responsive from 320px to 1440px.
- [ ] Accessibility: semantic landmarks, labels, alt text, keyboard navigation, visible focus, contrast. Lighthouse Accessibility **≥ 90**.
- [ ] No `console.log` or commented-out code left.
- [ ] No secrets, tokens, or passwords committed.

**Delivery**

- [ ] Deployed to Vercel / Netlify / Cloudflare. Refreshing on `/items/5` works.
- [ ] Git history with **at least 15 meaningful commits** over several days and feature branches merged through pull requests (at least 2 PRs).
- [ ] Professional `README.md` (template in Day 11.1).

## 3. Suggested Schedule for the Day

| Time | Activity |
|---|---|
| 0:00–0:45 | Authentication (service, context, login page, protected routes) |
| 0:45–1:30 | Connect protected pages (cart/profile), navbar states, logout clears the cart |
| 1:30–2:30 | Accessibility pass and Lighthouse, responsive pass, remove dead code |
| 2:30–3:15 | README, `.env.example`, folder clean-up, lint |
| 3:15–4:00 | Deploy, fix the SPA rewrite, test on mobile |
| 4:00–4:30 | Prepare a 5-minute demo and the viva answers |

## 4. Project Review Process

### 4.1 Live demo (5 minutes)

1. Show the live URL.
2. Walk through the main user journey: browse → filter → details → add to cart → login → protected page → logout.
3. Show one error scenario (offline, wrong password, invalid URL).

### 4.2 Code walkthrough (10 minutes)

1. Open the folder structure and explain the choices.
2. Explain one custom hook and one reducer case.
3. Show the Profiler evidence for one optimisation.
4. Make a **small live change** requested by the reviewer (for example, add a new filter or a new reducer action).

### 4.3 Viva questions (examples)

1. Which state lives where, and why?
2. Walk me through what happens when I refresh on `/items/5` while logged in.
3. Why is your protected route not a security feature on its own?
4. What would you change to move from client-side to server-side pagination?
5. How does your `useFetch` avoid race conditions?
6. Why is `.env` not committed? Which values can safely live in `VITE_` variables?
7. What would break if you removed the `key` from your cart list?
8. Explain one accessibility issue Lighthouse found and how you fixed it.

### 4.4 "Debug the Broken App" test (30 minutes)

You receive a small React application with **8–10 intentional bugs** (mutation of state, missing dependency, missing key, wrong route, conditional hook, missing `response.ok`, unhandled error state, a stale closure, an accessibility problem, a leaked secret). Find, explain and fix as many as you can. Explain each fix in one sentence.

## 5. Marking Rubric (100 marks)

| Area | Marks |
|---|---:|
| **Functionality:** list, details, search/filter/sort/pagination, cart/favourites, login and protected routes | 25 |
| **React quality:** component design, state placement, derived data, reducer/context, custom hooks | 20 |
| **API and error handling:** services, states, cancellation, `.env`, error boundary | 10 |
| **UI/UX:** responsive design, consistent styling, polished states (loading, empty, error) | 10 |
| **Accessibility and semantics** (Lighthouse + manual keyboard test) | 5 |
| **Performance reasoning:** measured optimisation, lazy loading | 5 |
| **Git and README:** commit history, PRs, README quality, setup instructions | 10 |
| **Deployment:** live URL, deep-link refresh, env configuration | 5 |
| **Viva and live change** | 10 |
| **Total** | **100** |

### Grading bands

| Score | Meaning |
|---|---|
| 85–100 | Excellent: ready for backend integration and portfolio |
| 70–84 | Good: minor gaps; fix list given |
| 55–69 | Satisfactory: re-review of specific topics (see below) before the backend phase |
| < 55 | Needs repeat of the relevant days |

## 6. Checklist Before You Submit

- [ ] `npm run lint` passes.
- [ ] `npm run build` succeeds and `npm run preview` works.
- [ ] I opened the live URL on my phone.
- [ ] I tested login with a wrong password.
- [ ] I tested the app offline (error and retry).
- [ ] I pressed `Tab` through every page.
- [ ] I searched my project for `console.log`, `TODO`, `password` and `token`.
- [ ] README has live link, screenshots, setup, env table, features and architecture notes.
- [ ] The repository is public (or access was given to the reviewers).

## 7. What Comes Next

You are now ready for **Week 7: Node.js and Express fundamentals**. In the backend weeks you will:

- Replace DummyJSON with **your own REST API** (Express + MongoDB).
- Replace the demo login with **real authentication** (hashed passwords, JWT, HttpOnly cookies).
- Move authorisation and validation to the **server**, where security belongs.
- Connect this React frontend to your backend and deploy both.

## 8. Stretch Goals

- Add automated tests for `cartReducer` and `useDebounce` (Vitest).
- Add a checkout form with full validation and an order summary page.
- Add TypeScript types to the service layer (`.js` → `.ts` for one file).
- Add a PWA manifest so the app can be installed on a phone.
- Add an analytics-free feedback form posting to a free form service.

## 9. Submission

1. Repository link (with README, `.env.example`, screenshots).
2. Live URL.
3. A 2-minute screen recording of the main journey (optional but encouraged).
4. Bring your laptop for the review.
