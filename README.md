# AnkiQuest-Agents

The source of the agent instructions (`AGENTS.md`) in every AnkiQuest repository.

- `shared.md`: the rules for all repositories.
- `repos/<repository>.md`: one repository's `## This repository` section, named after the repository (`repos/AnkiQuest-Android.md` for AnkiQuest/AnkiQuest-Android).
- `upstream.md`: the introduction of a fork's "Upstream guidance" section; `{upstream}` stands for the upstream's `owner/repo`.

## Changing a rule

Open a pull request here; it merges under the shared rules. Never edit `AGENTS.md` in another repository: the next distribution overwrites it.

## Generation

AnkiQuest-Sync's `agents` job runs daily, on demand, and when this repository's `master` changes (a `repository_dispatch` of type `agents-changed`, sent by `.github/workflows/agents.yml`). For each repository in its `TARGETS` map it writes:

- `AGENTS.md` = `shared.md`, a blank line, `repos/<repository>.md`. In a fork (a repository in AnkiQuest-Sync's `forks.json`), an "Upstream guidance" section follows: `upstream.md`, then upstream's own `CLAUDE.md` and `AGENTS.md`, verbatim, at the newest upstream commit the fork's branch has merged (pointer files such as `@AGENTS.md` and duplicates left out). Our rules come first and override upstream's.
- `CLAUDE.md` = `@AGENTS.md`.

If either differs from the repository's branch, the job pushes the commit `chore(agents): update AGENTS.md from AnkiQuest-Agents` to that branch: the rules were reviewed here. Only a refused push goes to a pull request from branch `agents-sync`, which merges by itself once its checks pass. When upstream changes its guidance, the fork's sync pull request (`sync/<owner>/<repo>`) brings the new text, written in the merge; once it is merged, the `agents` job writes the same text.

To generate one by hand:

```sh
{ cat shared.md; echo; cat repos/AnkiQuest-Android.md; } > AGENTS.md
```

AnkiQuest-Sync's `tools/fork-sync agents` does the same and adds the upstream guidance.

## Adding a repository

Add `repos/<repository>.md` here and the repository to `TARGETS` in AnkiQuest-Sync's `.github/workflows/agents.yml`.

## Secrets

`FORK_SYNC_TOKEN`: an organization secret shared with AnkiQuest-Sync, which distributes with it; sending the dispatch needs its Contents read and write on AnkiQuest/AnkiQuest-Sync.
