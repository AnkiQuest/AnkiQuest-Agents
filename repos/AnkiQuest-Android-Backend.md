## This repository

AnkiQuest-Android-Backend is a fork of [ankidroid/Anki-Android-Backend](https://github.com/ankidroid/Anki-Android-Backend): the Rust backend and its Kotlin bindings that AnkiQuest-Android depends on.

- **Branches.** `master` is upstream's `main` plus our commits: local build switches, `org.ankiquest` coordinates, the `anki` submodule on AnkiQuest-Anki `master`, and the build and publish workflow. Work from `master` and open pull requests against it.
- **Publishing.** `.github/workflows/ankiquest-publish.yml` builds four ABIs on macOS and checks the AAR. It publishes `org.ankiquest:anki-backend-android`, `anki-backend-core` and `anki-android-backend-testing` to Maven Central on a `*-ankiquest.*` tag or a manual run with `publish`. `VERSION_NAME` is upstream's version plus `-ankiquest.<n>`. Secrets: `MAVEN_CENTRAL_USERNAME`, `MAVEN_CENTRAL_PASSWORD`, `SIGNING_PRIVATE_KEY`, `SIGNING_PASSWORD`.
- **Upstream merges** come from the sync job's pull request; merge with a merge commit. When upstream moves its `anki` submodule, the merge conflicts there: point the submodule at the AnkiQuest-Anki `master` commit that contains upstream's (merge the sync pull request in AnkiQuest-Anki first). Then tag and publish, and bump AnkiQuest-Android. kuma3's backend (Pedrubik2000/kuma3-anki-backend) is watched by AnkiQuest-Sync and ported by hand.
- **Upstream's workflows** stay unchanged to keep merges clean, and run on pull requests to `master`. One exception (hill, 2026-11-21): `determine-macos-runner` uses a concurrency group per run, since a shared group cancelled builds whenever two pull requests ran; keep it in upstream merges.
- **No weights.** The publish workflow fails if a model file is tracked.
- **Checks to run** before pushing: `./check-rust.sh` for Rust changes. Leave the Android build to the publish workflow.
