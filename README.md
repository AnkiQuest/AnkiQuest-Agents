# AnkiQuest-Agents

The source of the agent instructions (`AGENTS.md`) in every AnkiQuest repository.

- `shared.md`: the rules for all repositories.
- `repos/<repository>.md`: one repository's `## This repository` section, named after the repository (`repos/AnkiQuest-Android.md` for AnkiQuest/AnkiQuest-Android).

## Changing a rule

Open a pull request here; it merges under the shared rules. Never edit `AGENTS.md` in another repository: the next distribution overwrites it.

## Generation

AnkiQuest-Sync's `agents` job runs daily, on demand, and when this repository's `master` changes (a `repository_dispatch` of type `agents-changed`, sent by `.github/workflows/agents.yml`). For each repository in its `TARGETS` map it writes:

- `AGENTS.md` = `shared.md`, a blank line, `repos/<repository>.md`. In a fork, an "Upstream guidance" section follows: upstream's own `CLAUDE.md` and `AGENTS.md`, verbatim, at the upstream commit the fork last merged (pointer files such as `@AGENTS.md` and duplicates left out).
- `CLAUDE.md` = `@AGENTS.md`.

If either differs from the repository's branch, the job pushes branch `agents-sync` there and opens or updates one pull request, `chore(agents): update AGENTS.md from AnkiQuest-Agents`. When upstream changes its guidance, the fork's sync pull request (`sync/<owner>/<repo>`) brings the new text, regenerated in the merge.

To generate one by hand:

```sh
{ cat shared.md; echo; cat repos/AnkiQuest-Android.md; } > AGENTS.md
```

AnkiQuest-Sync's `tools/fork-sync agents` does the same and adds the upstream guidance.

## Adding a repository

Add `repos/<repository>.md` here and the repository to `TARGETS` in AnkiQuest-Sync's `.github/workflows/agents.yml`.

## Secrets

`FORK_SYNC_TOKEN`: an organization secret shared with AnkiQuest-Sync, which distributes with it; sending the dispatch needs its Contents read and write on AnkiQuest/AnkiQuest-Sync.
