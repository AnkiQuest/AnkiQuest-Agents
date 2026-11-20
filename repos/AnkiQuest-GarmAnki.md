## This repository

AnkiQuest-GarmAnki is a fork of [sypianski/garmanki](https://github.com/sypianski/garmanki): a Garmin Connect IQ watch app (Monkey C) and its Android companion (Kotlin), which reads cards from AnkiDroid or AnkiQuest.

- **Upstream's instructions.** `CLAUDE.md` is upstream's, with `@AGENTS.md` added as its first line. Its rules still apply to code in this project: `SCHEMA.md` is the data contract, `DECYZJE.md` holds the product decisions, the Backlog.md workflow and its CLI, the build commands and the gotchas. Where it contradicts the shared rules above, follow it for upstream's code and ask hill.
- **Branches.** `master` is our version: upstream plus our CI and Nix shell (on `ankiquest-ci`, not merged yet) and, once published, `org.ankiquest:api`. `ankidroid-provider-check` and `ankiquest-support` are proposals for upstream: keep them in upstream's style, without AnkiQuest-only changes; merge upstream into them when it moves.
- **Upstream merges** come from the sync job's pull request; merge with a merge commit.
- **Languages.** Monkey C and Kotlin, as upstream.
- **Releases** to the Connect IQ Store are upstream's; don't submit from this fork.
- **Checks to run** before pushing: `cd android && ./gradlew lint testDebugUnitTest`, and `nix flake check` for Nix changes.
