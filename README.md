# AnkiQuest-Agents

The source of the agent instructions (`AGENTS.md`) in every AnkiQuest repository.

- `shared.md`: the rules for all repositories.
- `repos/<repository>.md`: one repository's `## This repository` section, named after the repository (`repos/AnkiQuest-Android.md` for AnkiQuest/AnkiQuest-Android).

## Changing a rule

Open a pull request here; it merges under the shared rules. Never edit `AGENTS.md` in another repository: the next distribution overwrites it.

## Generation

AnkiQuest-Sync's `agents` job runs daily, on demand, and when this repository's `master` changes (a `repository_dispatch` of type `agents-changed`, sent by `.github/workflows/agents.yml`). For each repository in its `TARGETS` map it writes:

- `AGENTS.md` = `shared.md`, a blank line, `repos/<repository>.md`.
- `CLAUDE.md` = `@AGENTS.md`. A fork whose upstream has its own `CLAUDE.md` keeps it, with `@AGENTS.md` added as its first line.

If either differs from the repository's branch, the job pushes branch `agents-sync` there and opens or updates one pull request, "Update AGENTS.md from AnkiQuest-Agents".

To generate one by hand:

```sh
{ cat shared.md; echo; cat repos/AnkiQuest-Android.md; } > AGENTS.md
```

## Adding a repository

Add `repos/<repository>.md` here and the repository to `TARGETS` in AnkiQuest-Sync's `.github/workflows/agents.yml`.

## Secrets

`SYNC_DISPATCH_TOKEN`: a fine-grained token with Contents read and write on AnkiQuest/AnkiQuest-Sync, used only to send the dispatch.
