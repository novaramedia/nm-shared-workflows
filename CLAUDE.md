# nm-shared-workflows

Reusable GitHub Actions workflows (`on: workflow_call`) called from other Novara Media repos.

## Stack

- GitHub Actions YAML + bash/jq

## Rules

- **Public repo.** Never commit secrets, hostnames or internal URLs. Secrets are always passed in by the caller.
- Callers pin to `@v1`-style tags. Changing a workflow's inputs or behaviour incompatibly needs a new major tag; update CHANGELOG.md and the tags on every release.
- Untrusted input goes through `env:` + `jq --arg`, never inline `${{ }}` in `run:`. Third-party actions pinned to commit SHA.

## Structure

```
.github/workflows/  — one file per reusable workflow; header comment documents inputs + secrets
README.md           — workflow index + usage
CHANGELOG.md        — Keep a Changelog format
```

## Further Context

- Cross-project conventions: [nm-agents-shared/conventions.md](https://github.com/novaramedia/nm-agents-shared/blob/main/conventions.md)
