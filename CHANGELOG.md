# Changelog

All notable changes to this project are documented here. Format: [Keep a Changelog](https://keepachangelog.com/en/1.1.0/). Versioning: [SemVer](https://semver.org/).

## [Unreleased]

## [1.0.0] - 2026-11-24

### Added

- `slack-post.yml`: reusable workflow posting a Block Kit message to Slack via a bot token. Status header using team emoji (success :feelsgood:, ok :coffee:, approved, received :inbox_tray:, info, warning, failure) with an `icon` override, standard-markdown body so changelog `###` headings and links render, optional CHANGELOG section extraction from the caller repo, up to 5 link buttons, failure mention by Slack ID, footer linking the run (optional via `show_footer`), threading via `thread_ts` input and `ts` output. A failed post warns instead of failing the run.
- `test-slack-post.yml`: manual self-test posting a sample message and a threaded reply.
