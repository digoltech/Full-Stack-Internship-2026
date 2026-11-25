# Day 17 — UI Libraries Exercise

**Suggested duration:** 2–3 hours

## Project: Team Directory

Build a responsive team directory using **one** primary UI approach: Ant Design, MUI, React Bootstrap, Chakra UI, or a headless/source-owned approach. Pick one and briefly justify your choice in the README.

### Requirements

1. Show at least eight team members with name, role, email, and status.
2. Use a reusable member row or card component with props.
3. Add a search field that filters by name or role.
4. Add a status filter with at least two choices and an “All” option.
5. Show a useful empty state when no records match.
6. Add a form or dialog to invite a member. Validate required fields and email format.
7. After a successful local submission, add the new person to the list and clear the form.
8. Add an action to change a member's status or remove a member. Use immutable state updates.
9. Ensure controls have visible labels, keyboard focus, and accessible names.
10. Check the layout at narrow and wide viewport widths.

### Suggested Data Shape

```js
{
  id: 'member-1',
  name: 'Amina Yusuf',
  role: 'Frontend Developer',
  email: 'amina@example.com',
  status: 'Active'
}
```

Use stable IDs for list keys. Do not use the array index as the key when records can be added, filtered, or removed.

## Deliverables

- A working React page and reusable components.
- A short README explaining the library choice and how to run the project.
- A checklist of accessibility and responsive checks performed.
- At least three tests or documented manual test scenarios covering search, empty state, and form validation.

## Stretch Goals

- Add pagination or sorting.
- Persist data in `localStorage` with a clear explanation that it is demo-only persistence.
- Add a confirmation step before removing a member.
- Theme the library with a small, consistent set of design tokens.

## Review Questions

1. Which component behavior came from the library, and which behavior did you implement?
2. What would be the cost of switching libraries later?
3. How did you make validation errors understandable to keyboard and screen-reader users?
4. What changed at the narrow viewport?
5. What server-side validation would still be needed in a real app?
