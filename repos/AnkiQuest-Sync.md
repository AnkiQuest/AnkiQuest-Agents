## This repository

AnkiQuest-Sync holds AnkiQuest's scheduled GitHub Actions jobs. It has no code of its own beyond the workflows and `watched.json`.

- **Jobs.** `sync` (`.github/workflows/sync.yml`): keeps the forks up to date with upstream, mirror or pr mode, one matrix entry per fork. `watch`: reports new commits or versions in the sources listed in `watched.json`. `agents` (`.github/workflows/agents.yml`): writes each repository's `AGENTS.md` from AnkiQuest-Agents and opens a pull request where it differs; its targets are the `TARGETS` map in that workflow.
- **Token.** Every job writes to other repositories with `FORK_SYNC_TOKEN`; `GITHUB_TOKEN` can't. Never print it. Its scopes are listed in the README; widen them there when a job needs a new repository.
- **Never force-push** or write a fork's working branch directly; mirrors are fast-forwarded through GitHub's API, everything else goes through a pull request or an issue.
- **Shell.** Keep each step a few lines of glue. Logic that grows beyond that moves to a Rust tool in this repository.
- **Checks to run** before pushing: `actionlint` on the changed workflows; run the job by hand (Run workflow) after merging.
