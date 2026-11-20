## This repository

AnkiQuest-Dev is the development environment for every AnkiQuest repository: NixOS on WSL (`nixosConfigurations.ankiquest-wsl`) one dev shell per kind of repository (`devShells.<system>.{default,server,desktop,gallery,android,android-emulator,android-app,anki}`), and the reusable workflows and label set every repository shares.

- **Layout.** `flake.nix`: the outputs. `shells/toolchains.nix`: every pinned version (Rust, Android SDK and NDK, JBR), each next to the repository file it follows. `shells/default.nix`: the dev shells. `nixos/hosts/ankiquest-wsl`: the WSL host; `nixos/roles` and `nixos/modules`: what it is made of, laid out as in float3/nixos.
- **Pins follow the repositories.** When a repository changes a version it pins (`rust-toolchain.toml`, `gradle/libs.versions.toml`, `gradle/gradle-daemon-jvm.properties`, a CI workflow), change the matching value in `shells/toolchains.nix`. Update one flake input at a time with `nix flake update <input>`.
- **Shared by every repository.** Each repository's `flake.nix` takes its shell, formatter and `lib.formatChecks` from here. Workflows used by more than one repository are reusable workflows in `.github/workflows/` (`android-ci`, `android-nightly`, the labelling ones); `labels.json` is the shared label set and `tests/labels.test.ts` tests it. `ankiquest-labels.yml` is the caller the other repositories copy. A change here reaches every repository: check the callers.
- **Nix only.** Configuration is Nix, formatted with alejandra. Shell stays a few lines of glue; anything larger becomes Rust.
- **Nothing private.** Signing keys, `keystore.properties`, `google-services.json`, tokens and proprietary SDKs (the Garmin Connect IQ SDK) are installed by hand, as the README says, and never committed.
- **Checks to run** before pushing: `nix flake check`, `alejandra --check .`, `nix develop .#<shell>` for each shell you changed, `actionlint`, and `node --test tests/*.test.ts` for the label workflows.
