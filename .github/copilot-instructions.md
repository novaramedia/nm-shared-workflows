# Copilot Instructions

See `CLAUDE.md` for project structure, stack, and context.
See `CHANGELOG.md` for release history format reference.

## Code Review

Flag these in every PR:

- **Changelog missing** — `CHANGELOG.md` must have an entry under `[Unreleased]` (Keep a Changelog format). One entry per meaningful change, not per commit.
- **PR title format** — must be `<Type>: <Short description>`. Valid types: `Fix`, `Feature`, `Release`, `Refactor`, `Chore`, `Content`, `Docs`.
- **Debug artifacts** — no `console.log`, `var_dump`, `dd()`, or similar left in production code.
- **TODO without issue ref** — any TODO comment must reference a GitHub issue: `TODO(#123): ...`
- **TypeScript `any`** — flag implicit or unjustified `any`. A comment explaining why is acceptable.
- **New dependency** — flag any new package/import not already in the project. PR description should justify it.
- **Frontend CSS** — flag custom CSS that duplicates nm-stylus-library utility classes. Use the library.
- **Pattern deviation** — flag code that diverges from existing patterns in the same file or module without explanation.

Don't suggest architectural changes in review — raise a new issue instead.

## Generating Code from Issues

Before generating:

1. Read the full issue including all comments.
2. Check for linked issues or PRs — understand prior attempts.
3. Read the files most likely to be affected before writing anything.

When generating:

- Match existing file structure, naming conventions, and abstractions.
- Prefer extending existing patterns over introducing new ones.
- Match the project's stack — check `CLAUDE.md` before assuming TypeScript, PHP, etc.
- For any frontend work, use nm-stylus-library utility classes.
- Don't add error handling or validation beyond what the issue describes.

After generating:

- Update `CHANGELOG.md` under `[Unreleased]`.
- Ensure PR title follows format above.
