# Agent Operating Constraints

## Scope discipline

- Implement only what is explicitly requested.
- Do not add aesthetic styling, refactors, or extra structure unless explicitly requested.
- If request is ambiguous, ask one clarifying question before editing.

## Change minimization

- Prefer the smallest possible diff.
- Do not modify unrelated files.
- Do not create alternative plans unless asked.
- Do not introduce new patterns when existing project patterns already solve it.

## Styling policy

- Bootstrap first: use existing Bootstrap utilities/components.
- No custom CSS for visual styling unless explicitly requested.
- Custom CSS is allowed only for required layout mechanics not achievable with existing utilities.

## Validation and checkpoints

- Before edits, restate requested behavior in 3-5 bullets.
- After first pass, stop and ask for review before "improving" anything.
- Never do speculative polish.

## Workflow policy

- Work in current workspace/branch by default.
- Do not suggest or require worktrees unless explicitly requested.
