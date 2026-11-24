# nm-shared-workflows

Reusable GitHub Actions workflows shared across Novara Media repos.

This repo is public so that public repos (e.g. the novaramedia.com theme) can call it. Nothing sensitive lives here: every secret belongs to the calling repo and is passed in at call time.

## Workflows

| Workflow | What it does |
|---|---|
| [`slack-post.yml`](.github/workflows/slack-post.yml) | Posts a Block Kit message to Slack via a bot token: status header with team emoji, markdown body (optionally the caller's CHANGELOG section), link buttons, failure mention, footer, threading. Inputs documented in the file header. Self-test: run **Test slack-post** from the Actions tab (needs a `SLACK_BOT_TOKEN` repo secret). Follows the [Slack Messages conventions](https://github.com/novaramedia/nm-agents-shared/blob/main/conventions.md#slack-messages). |

## Using a workflow

Call it as a job, pinned to a release tag:

```yaml
jobs:
  notify:
    needs: deploy
    if: ${{ !cancelled() }}
    uses: novaramedia/nm-shared-workflows/.github/workflows/slack-post.yml@v1
    with:
      channel: '#team-digital-public'
      status: ${{ needs.deploy.result == 'success' && 'success' || 'failure' }}
      title: Example site ${{ github.ref_name }} deployed
      changelog_version: ${{ github.ref_name }}
      buttons: |
        View site | https://example.com/
        Release notes | ${{ github.event.release.html_url }}
      mention_on_failure: U0123456789
    secrets:
      slack_bot_token: ${{ secrets.SLACK_BOT_TOKEN }}
```

Each workflow file documents its inputs and secrets in its header comment.

## Versioning

Tags cover the whole repo, not individual files. `v1` is a moving major tag that callers pin to; each release also gets an exact tag (`v1.0.0`). Breaking changes to any workflow's inputs or behaviour mean a new major (`v2`), so existing callers keep working until they opt in. See [CHANGELOG.md](CHANGELOG.md).

## Adding a workflow

- One file per workflow in `.github/workflows/` (GitHub doesn't allow subfolders for reusable workflows).
- Trigger with `on: workflow_call` only.
- Pin third-party actions to a commit SHA.
- Pass untrusted input (release notes, PR titles) through `env:`, never inline `${{ }}` in `run:`.
