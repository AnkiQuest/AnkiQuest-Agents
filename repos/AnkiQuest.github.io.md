## This repository

AnkiQuest.github.io is the AnkiQuest art gallery on GitHub Pages (coming).

- **Poses come from AnkiQuest-Art.** The build downloads the masters, archive, `manifest.json` and `poses.json` of the AnkiQuest-Art release pinned in `ankiquest-art.json` and makes the previews. Never commit a picture here. AnkiQuest-Sync updates the pin.
- **Checks to run** before pushing: `nix develop -c npm test` and `nix develop -c node src/build.ts server _site`.
- **Pages** are TypeScript, as the server's web pages are.
