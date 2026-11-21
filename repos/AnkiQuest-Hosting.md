## This repository

AnkiQuest-Hosting is the NixOS configuration of `aws`, the EC2 instance that serves ankiquest.org. It is private.

- **Layout.** `configuration.nix`: the host, nginx, ACME and the AnkiQuest service settings. `launch.sh`: creates the EC2 instance in AWS CloudShell.
- **Not a flake.** It is mounted at `nixos/hosts/aws` in float3/nixos as a git submodule, and `configuration.nix` imports roles and modules from there through the `paths` argument, so it only builds inside float3/nixos: `nix build .#nixosConfigurations.aws.config.system.build.toplevel`.
- **Changing the server.** Merge the change here, then commit the new submodule revision in float3/nixos and deploy from there (see its README). Deploy only when hill asks.
- **Secrets** are plain files under `/etc/nixos/secrets/` on the host, never in this repository.
- **Checks to run** before pushing: `nix run github:AnkiQuest/AnkiQuest-Dev#formatter.x86_64-linux -- --check .` and `shellcheck launch.sh` (the CI workflow runs both), and the `aws` build above from a float3/nixos checkout with this branch in the submodule.
