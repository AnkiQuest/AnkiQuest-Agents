## This repository

AnkiQuest-Sync holds AnkiQuest's scheduled GitHub Actions jobs. Beyond the workflows and `watched.json`, it holds `art-consumers.json` (the repositories that pin AnkiQuest-Art releases) and `tools/art-pin`, the Rust tool behind the `art` job.

- **Jobs.** `sync` (`.github/workflows/sync.yml`): opens a pull request from upstream into each fork's `master`, one matrix entry per fork. `watch`: reports new commits or versions in the sources listed in `watched.json`. `agents` (`.github/workflows/agents.yml`): writes each repository's `AGENTS.md` from AnkiQuest-Agents and opens a pull request where it differs; its targets are the `TARGETS` map in that workflow. `art`: when AnkiQuest-Art publishes a release, writes its `ankiquest-art.json` into every repository that uses art and opens a pull request "Use AnkiQuest-Art <tag>".
- **Token.** Every job writes to other repositories with `FORK_SYNC_TOKEN`; `GITHUB_TOKEN` can't. Never print it. Its scopes are listed in the README; widen them there when a job needs a new repository.
- **Never force-push** or write a fork's `master` directly; everything goes through a pull request or an issue.
- **Shell.** Keep each step a few lines of glue. Logic that grows beyond that moves to a Rust tool in this repository.
- **Checks to run** before pushing: `nix develop -c actionlint` (the `check` workflow runs it too); run the job by hand (Run workflow) after merging.
