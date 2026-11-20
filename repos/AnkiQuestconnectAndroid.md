## This repository

AnkiQuestconnectAndroid is a fork of [KamWithK/AnkiconnectAndroid](https://github.com/KamWithK/AnkiconnectAndroid): the AnkiConnect API on Android (Java), backed by AnkiDroid or AnkiQuest through their content provider.

- **Branches.** `master` is our version: upstream plus our CI, Nix shell and Dependabot, `ankiquest-support` merged, and, once published, `org.ankiquest.anki:api`. `ankidroid-provider-check` and `ankiquest-support` are proposals for upstream: keep them in upstream's style, without AnkiQuest-only changes; merge upstream into them when it moves.
- **Upstream merges** come from the sync job's pull request; merge with a merge commit.
- **Languages.** Java, as upstream.
- **Releases** are upstream's; don't publish from this fork. The nightly debug APK on `master` is for testing.
- **Checks to run** before pushing: `./gradlew testDebugUnitTest lintDebug`, and `nix flake check` for Nix changes.
