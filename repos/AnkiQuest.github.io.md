## This repository

AnkiQuest.github.io is the AnkiQuest art gallery on GitHub Pages (coming).

- **Poses come from their masters.** `server` is a submodule pinning AnkiQuest-Server; the build reads the masters in `server/static/<companion>/` and makes the previews. Never commit a picture here. Dependabot bumps the submodule; review the new poses in its pull request.
- **Checks to run** before pushing: `nix develop -c npm test` and `nix develop -c node src/build.ts server _site`.
- **Pages** are TypeScript, as the server's web pages are.
