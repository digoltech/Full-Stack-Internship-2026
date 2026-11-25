# Day 18 — Frontend Libraries Exercise

**Suggested duration:** 3–4 hours

## Project: Workshop Registration Admin

Build a small page for viewing workshop registrations and inviting a participant. Use React Hook Form and Zod for the form, TanStack Query for remote data, and optional Motion/Lucide for feedback and controls.

### Part A — Registration Form

1. Create fields for name, email, and workshop selection.
2. Validate the fields with a Zod schema.
3. Display field-specific errors connected to their labels.
4. Disable or clearly label the submit action while it is submitting.
5. Show an accessible success message after a successful submission.
6. Handle and explain a server error without clearing the user's input.

### Part B — Registration List

1. Fetch registrations through a service function.
2. Check `response.ok` and throw for failed HTTP responses.
3. Use a query key that includes the selected workshop filter.
4. Show loading, error, empty, and success states.
5. After adding a registration, refresh or update the relevant cached query.
6. Use stable IDs as list keys.

### Part C — Polish

1. Add a search field or status filter.
2. Use an icon only when it improves recognition; label icon-only buttons accessibly.
3. Add a brief success or list-entry animation, and honor reduced-motion preferences.
4. Check the page with keyboard only and at a narrow viewport.

## Suggested API Contract

You may use a mock service or a local in-memory implementation. If using a real API, document its URL and expected response shape.

```js
// GET /api/registrations?workshop=react
[
  { "id": "reg-1", "name": "Amina Yusuf", "email": "amina@example.com", "workshop": "react" }
]

// POST /api/registrations
{
  "name": "Amina Yusuf",
  "email": "amina@example.com",
  "workshop": "react"
}
```

## Testing Scenarios

- An empty name and malformed email show understandable validation messages.
- A valid submission appears in the list or shows a success state.
- A failed list request shows an error and does not render fake success data.
- No registrations produces an empty state, not a loading spinner forever.
- Search/filter changes display the correct records.
- Keyboard users can reach and activate every control.

## Deliverables

- Working feature with components and service code organized clearly.
- README with installation and run instructions.
- At least five focused tests, including validation, request failure, and empty results.

## Stretch Goals

- Add pagination and include the page in the query key.
- Add optimistic insertion with rollback on error; document how rollback works.
- Add a retry control and a pending mutation state.
