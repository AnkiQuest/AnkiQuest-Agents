## This repository

AnkiQuest-Agents is the source of every AnkiQuest repository's `AGENTS.md`.

- **Layout.** `shared.md`: everything above "This repository". `repos/<repository>.md`: each repository's "This repository" section, named after the repository. `upstream.md`: the introduction of a fork's "Upstream guidance" section, which AnkiQuest-Sync fills with upstream's own `CLAUDE.md` and `AGENTS.md`. `README.md`: how generation works.
- **Changing rules.** Edit `shared.md`, `upstream.md` or a section here, never `AGENTS.md` in another repository. A shared change reaches every repository; check that it holds for the forks too, next to their upstream guidance. After merging, AnkiQuest-Sync pushes the new `AGENTS.md` to every repository where it differs.
- **A new repository** gets a section here and an entry in the `TARGETS` map of AnkiQuest-Sync's `agents` workflow.
- **Checks to run** before pushing: `nix flake check`.
- **Format.** Each section starts with `## This repository` and has no other second-level heading; `shared.md` has none; `upstream.md` has no heading and names `{upstream}`. The check workflow enforces this.
