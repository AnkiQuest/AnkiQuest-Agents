## This repository

AnkiQuest.github.io is the AnkiQuest art gallery on GitHub Pages: the matrix of companions and poses, a page per companion with what it is missing, and the archive.

- **Built from the art matrix.** `server` is a submodule pinning AnkiQuest-Server; the build runs its `xtask art-coverage --json` and copies the masters and archive files that output names, making previews at build time. Never commit a picture here. Dependabot bumps the submodule; review the new poses in its pull request.
- **Checks to run** before pushing: `nix develop -c npm test` and `nix develop -c node src/build.ts server _site` (needs `cargo` for the xtask).
- **Pages** are TypeScript, as the server's web pages are.
