## This repository

AnkiQuest-Agents is the source of every AnkiQuest repository's `AGENTS.md`.

- **Layout.** `shared.md`: everything above "This repository". `repos/<repository>.md`: each repository's "This repository" section, named after the repository. `README.md`: how generation works.
- **Changing rules.** Edit `shared.md` or a section here, never `AGENTS.md` in another repository. A shared change reaches every repository; check that it holds for the forks too. After merging, AnkiQuest-Sync opens one pull request per repository whose `AGENTS.md` differs; those merge under that repository's own rules.
- **A new repository** gets a section here and an entry in the `TARGETS` map of AnkiQuest-Sync's `agents` workflow.
- **Format.** Each section starts with `## This repository` and has no other second-level heading; `shared.md` has none. The check workflow enforces this.
