## This repository

AnkiQuest-Anki is a fork of [ankitects/anki](https://github.com/ankitects/anki): Anki's core, built into the Android app through AnkiQuest-Android-Backend.

- **Branches.** `master` is ankitects/anki `main` plus our carried commits: the RWKV engine and scheduler, FSRS-7 with JSchoreels' fsrs-rs fork, their protobuf messages and strings. Work from `master` and open pull requests against it. Our protobuf fields take numbers after upstream's; when upstream takes a number we use, renumber ours in the upstream merge.
- **Upstream's instructions.** Upstream's `CLAUDE.md` is kept in the "Upstream guidance" section at the end of this file; its rules still apply to code in this project (`just` recipes, `just check` before finishing). Upstream's own `AGENTS.md` is a link to it; ours replaces that link on `master`.
- **Upstream merges** come from the sync job's pull request; merge with a merge commit, never rebase. The queue builder, the scheduler, search and `Cargo.toml` conflict most often. After merging, move the backend's submodule when the backend needs it (see AnkiQuest-Android-Backend).
- **Watched sources.** JSchoreels/anki, JSchoreels/fsrs-rs, open-spaced-repetition/fsrs-rs and Pedrubik2000/kuma3-anki-core are ported by hand. AnkiQuest-Sync opens an issue here when they move; after porting or skipping, set `reviewed` in AnkiQuest-Sync's `watched.json`.
- **RWKV models** are user-supplied files with no public licence. Never commit weights. Tests that need a model file run only when one is placed locally; CI runs without them.
- **Checks to run** before pushing, for what you changed: `cargo fmt --check`, `cargo clippy -p anki --lib --tests -- -D warnings`, `cargo test -p anki --lib`; `just check` for changes outside rslib. Android targets are checked only by the backend's build.
