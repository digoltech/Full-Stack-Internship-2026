# Exercise Day 12 — File Upload and Optimistic UI

Build one small feature in the course project that uploads a file and one feature that uses optimistic UI.

## Required Features

- [ ] Add a file input that validates type and size.
- [ ] Send the file using `FormData`.
- [ ] Display upload progress or a loading state.
- [ ] Show success and error states.
- [ ] Prevent duplicate submissions.
- [ ] Revoke object URLs used for previews.
- [ ] Add one optimistic state update.
- [ ] Snapshot and restore previous state on request failure.
- [ ] Avoid direct mutation of state.
- [ ] Document both patterns in the project README.

## Viva Questions

1. Why should `Content-Type` not be set manually for `FormData`?
2. Why is a snapshot needed before an optimistic update?
3. Which operations are unsafe to implement optimistically?
4. How can an object URL leak browser memory?
5. Where should final file validation happen?
