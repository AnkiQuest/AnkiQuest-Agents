## This repository

AnkiQuest-Sync holds AnkiQuest's scheduled GitHub Actions jobs and the Rust tools they run (`tools/`).

- **Jobs.** `sync` (`.github/workflows/sync.yml`): merges upstream into branch `sync/<owner>/<repo>` of each fork, regenerates `AGENTS.md` there, and opens or updates one pull request from it into `master`, one matrix entry per fork; the logic is `tools/fork-sync`. `watch`: reports new commits or versions in the sources listed in `watched.json`. `agents` (`.github/workflows/agents.yml`): writes each repository's `AGENTS.md` from AnkiQuest-Agents and opens a pull request where it differs; its targets are the `TARGETS` map in that workflow. `art`: when AnkiQuest-Art publishes a release, writes its `ankiquest-art.json` into every repository that uses art and opens a pull request `chore(art): use AnkiQuest-Art <tag>`.
- **Token.** Every job writes to other repositories with `FORK_SYNC_TOKEN`; `GITHUB_TOKEN` can't. Never print it. Its scopes are listed in the README; widen them there when a job needs a new repository.
- **Never force-push** or write a fork's `master` directly; everything goes through a pull request or an issue. The jobs only add commits to their own branches (`sync/*`, `agents-sync`, `art-release`), so people can push fixes there.
- **Shell.** Keep each step a few lines of glue. Logic that grows beyond that moves to a Rust tool in this repository.
- **Checks to run** before pushing: `nix develop -c actionlint` (the `check` workflow runs it too), and `cargo fmt --check`, `cargo clippy --all-targets -- -D warnings` and `cargo test` in each tool you changed; run the job by hand (Run workflow) after merging.
