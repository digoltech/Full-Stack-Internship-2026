# Day 19: Frontend Performance & Optimization

Building a functional app is easy; building a **fast** app is where the professional difference lies. This guide covers how to optimize a React application for maximum performance.

## 1. Rendering Optimization (React Specific)
React re-renders components when state or props change. Too many re-renders lead to "laggy" UIs.

### Memoization
- **`React.memo`**: Prevents a component from re-rendering if its props haven't changed.
- **`useMemo`**: Memoizes the result of an expensive calculation.
- **`useCallback`**: Memoizes a function definition to prevent child components from re-rendering when a function is passed as a prop.

### Code Splitting & Lazy Loading
Don't load the entire app at once. Load only what the user needs.
- **`React.lazy` & `Suspense`**: Load components only when they are rendered.
- **Dynamic Imports**: Use `import()` for libraries that are only needed in specific sections.

**Example:**
```jsx
import React, { Suspense, lazy } from 'react';

const HeavyChart = lazy(() => import('./components/HeavyChart'));

function Dashboard() {
  return (
    <Suspense fallback={<div>Loading Chart...</div>}>
      <HeavyChart />
    </Suspense>
  );
}
```

## 2. Asset Optimization
Images and fonts are usually the biggest cause of slow page loads.

### Image Optimization
- **WebP Format**: Use `.webp` instead of `.jpg` or `.png` for better compression.
- **Responsive Images**: Use `srcset` to serve smaller images to mobile users.
- **Lazy Loading**: Use the `loading="lazy"` attribute on `<img>` tags.
- **CDN**: Serve images from a Content Delivery Network (Cloudinary, Imgix).

### Font Optimization
- **Self-host fonts**: Avoid multiple requests to Google Fonts.
- **`font-display: swap`**: Ensures text is visible immediately using a system font until the custom font loads.

## 3. Network & Bundle Optimization
Reducing the amount of JavaScript sent to the browser.

### Tree Shaking
Removing unused code from the final bundle. Ensure you use ES Modules (`import/export`) so the bundler (Vite/Webpack) can identify dead code.

### Dependency Audit
- Avoid large libraries if a small one exists (e.g., use `date-fns` or `dayjs` instead of `moment.js`).
- Use **Bundle Analyzer** to see which libraries are taking up the most space.

## 4. Core Web Vitals (Measuring Performance)
Google uses these metrics to rank websites. You should monitor them using **Lighthouse** (Chrome DevTools).

- **LCP (Largest Contentful Paint)**: How long it takes for the main content to load. (Target: < 2.5s)
- **FID (First Input Delay)**: Time from first user interaction to browser response. (Target: < 100ms)
- **CLS (Cumulative Layout Shift)**: How much the page "jumps" during loading. (Target: < 0.1)

## 5. Performance Checklist for Production

- [ ] **Enable Gzip/Brotli Compression** on the server.
- [ ] **Minify CSS and JS** (Vite does this by default).
- [ ] **Implement Caching** (Cache-Control headers).
- [ ] **Use a CDN** for static assets.
- [ ] **Optimize Images** (Compress and use WebP).
- [ ] **Lazy Load** routes and heavy components.
- [ ] **Audit Bundle Size** using `rollup-plugin-visualizer`.
