# Day 19 — Frontend Performance Exercise

**Suggested duration:** 3–4 hours

## Project: Performance Audit and Improvement

Choose a React app you built earlier in the course, or create a small catalogue with a searchable list and a detail route. The task is to diagnose, improve, and explain one or more measurable bottlenecks.

### Part A — Establish the Baseline

1. Build the app for production and run it using the documented preview or deployment flow.
2. Choose one route and one user task, such as searching and opening a product.
3. Record the viewport, browser, test conditions, and at least three repeated measurements.
4. Capture Lighthouse findings and a Network trace.
5. Use React DevTools Profiler for one meaningful interaction.
6. Identify the largest likely bottleneck and explain why it affects users.

### Part B — Make Focused Improvements

Choose at least three improvements that match the evidence. Possible options:

- Resize or convert an oversized image and reserve its layout dimensions.
- Avoid lazy-loading an above-the-fold LCP image; lazy-load below-the-fold imagery.
- Split a rarely visited route or heavy component.
- Reduce expensive repeated list work, and justify memoization with a profile.
- Break up or defer non-urgent UI updates that block input.
- Remove or replace an unnecessary large dependency.
- Fix a layout shift caused by late content or fonts.

Do not apply every option automatically. A change that does not target an observed problem is not a required improvement.

### Part C — Verify and Document

1. Repeat the same production tests after each change.
2. Compare results and note normal variation.
3. Confirm loading, error, empty, and success states still work.
4. Confirm keyboard access and reduced-motion behavior where relevant.
5. Explain any trade-off, such as a new loading fallback or additional maintenance.

## Report Template

```text
Route and user task:
Baseline environment:
Baseline LCP / INP / CLS (or explain unavailable metrics):
Baseline bundle or largest-resource observations:
Baseline React profile finding:
Changes made and the evidence for each:
Repeated results after changes:
Accessibility/functionality checks:
Remaining bottleneck or follow-up:
```

## Deliverables

- The improved application.
- Before/after report with measurement conditions.
- At least one browser trace or profiler observation described in the report.
- README updates explaining production build and test commands.

## Review Questions

1. What exact evidence identified your bottleneck?
2. Which change produced a measurable benefit, and how repeatable was it?
3. Why is FID not the current Core Web Vital for responsiveness?
4. How can image dimensions reduce CLS?
5. Why should memoization be based on evidence?
6. What user-facing behavior or accessibility check might an optimization accidentally break?
