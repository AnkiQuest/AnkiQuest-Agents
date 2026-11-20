## This repository

AnkiQuest-Android-Backend is a fork of [ankidroid/Anki-Android-Backend](https://github.com/ankidroid/Anki-Android-Backend): the Rust backend and its Kotlin bindings that AnkiQuest-Android depends on.

- **Branches.** `main` mirrors upstream; the sync job fast-forwards it, nobody else writes it. `ankiquest` is upstream plus our commits: local build switches, `org.ankiquest.anki` coordinates, the `anki` submodule on AnkiQuest/anki `ankiquest`, and the build and publish workflow. Work from `ankiquest` and open pull requests against it.
- **Publishing.** `.github/workflows/ankiquest-publish.yml` builds four ABIs on macOS and checks the AAR. It publishes `org.ankiquest.anki:anki-backend-android`, `anki-backend-core` and `anki-android-backend-testing` to Maven Central on a `*-ankiquest.*` tag or a manual run with `publish`. `VERSION_NAME` is upstream's version plus `-ankiquest.<n>`. Secrets: `MAVEN_CENTRAL_USERNAME`, `MAVEN_CENTRAL_PASSWORD`, `SIGNING_PRIVATE_KEY`, `SIGNING_PASSWORD`.
- **New upstream versions.** AnkiQuest-Sync opens an issue when upstream's `VERSION_NAME` moves. Merge the Anki release into AnkiQuest/anki `ankiquest`, merge upstream's version into `ankiquest` here as a merge commit, move the submodule, tag and publish, then bump AnkiQuest-Android. kuma3's backend (Pedrubik2000/kuma3-anki-backend) is watched the same way.
- **Upstream's workflows** stay unchanged to keep merges clean, and also run on pull requests to `ankiquest`.
- **No weights.** The publish workflow fails if a model file is tracked.
- **Checks to run** before pushing: `./check-rust.sh` for Rust changes. Leave the Android build to the publish workflow.
