## This repository

AnkiQuest/anki is a fork of [ankitects/anki](https://github.com/ankitects/anki): Anki's core, built into the Android app through AnkiQuest-Android-Backend.

- **Branches.** `main` mirrors ankitects/anki; the sync job fast-forwards it, nobody else writes it. `ankiquest` is the Anki release AnkiDroid uses plus our carried commits: the RWKV engine and scheduler, FSRS-7 with JSchoreels' fsrs-rs fork, their protobuf messages and strings. Work from `ankiquest` and open pull requests against it.
- **Upstream's instructions.** `CLAUDE.md` is upstream's, with `@AGENTS.md` added as its first line; its rules still apply to code in this project (`just` recipes, `just check` before finishing). Upstream's own `AGENTS.md` is a link to it; ours replaces that link on `ankiquest`.
- **New Anki releases.** When AnkiDroid adopts a release, merge its tag into `ankiquest` as a merge commit, never rebase, then update the backend's submodule and publish (see AnkiQuest-Android-Backend). The queue builder and the scheduler conflict most often.
- **Watched sources.** JSchoreels/anki, JSchoreels/fsrs-rs, open-spaced-repetition/fsrs-rs and Pedrubik2000/kuma3-anki-core are ported by hand. AnkiQuest-Sync opens an issue here when they move; after porting or skipping, set `reviewed` in AnkiQuest-Sync's `watched.json`.
- **RWKV models** are user-supplied files with no public licence. Never commit weights. Tests that need a model file run only when one is placed locally; CI runs without them.
- **Checks to run** before pushing, for what you changed: `cargo fmt --check`, `cargo clippy -p anki --lib --tests -- -D warnings`, `cargo test -p anki --lib`; `just check` for changes outside rslib. Android targets are checked only by the backend's build.
