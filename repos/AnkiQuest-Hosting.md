## This repository

AnkiQuest-Hosting is the NixOS configuration of the host that serves ankiquest.org. It is private; this section is public (see "Git and pull requests").

- **Layout.** `configuration.nix`: the host, its web server and certificates, and the AnkiQuest service settings. `launch.sh`: creates the machine.
- **Not a flake.** It is mounted as a git submodule under `nixos/hosts/` in float3/nixos, and `configuration.nix` imports roles and modules from there through the `paths` argument, so it only builds inside float3/nixos. float3/nixos's README names the host and gives the build command.
- **Changing the server.** Merge the change here through a pull request, then commit the new submodule revision in float3/nixos and deploy from there (see its README). Deploy only when hill asks.
- **Secrets** are plain files on the host, never in this repository.
- **Checks to run** before pushing: `nix run github:AnkiQuest/AnkiQuest-Dev#formatter.x86_64-linux -- --check .` and `shellcheck launch.sh` (the CI workflow runs both), and the host's build from a float3/nixos checkout with this branch in the submodule.
