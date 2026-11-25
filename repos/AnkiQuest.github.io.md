## This repository

AnkiQuest.github.io is the AnkiQuest art gallery on GitHub Pages (coming).

- **Poses come from AnkiQuest-Art.** The build downloads the masters, archive, `manifest.json` and `poses.json` of the AnkiQuest-Art release pinned in `ankiquest-art.json` and makes the previews. Never commit a picture here. AnkiQuest-Sync updates the pin.
- **Companions come from server master.** The live and planned companions and the moods come from AnkiQuest-Server `master`'s `tests/fixtures/`, cloned into `server/` at build time (not a submodule); the `pages` workflow runs daily to pick up server changes.
- **Checks to run** before pushing: `nix develop -c npm test` and `nix develop -c node src/build.ts server .art _site`, after cloning the fixtures as the README says.
- **Pages** are TypeScript, as the server's web pages are.
