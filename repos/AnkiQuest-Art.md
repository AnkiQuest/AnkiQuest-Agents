## This repository

AnkiQuest-Art holds every companion picture: the masters, the archive, `manifest.json` (which file each pose uses, with framing, licence and credit), `poses.json` (every pose and its fallback) and `tools/` (`art-check` and `art-export`).

- **Masters** are `<companion folder>/<pose>.png`. A picture several poses share is named after its main pose and listed for the others in `manifest.json`. Never two files with the same bytes, in the archive or not.
- **Archive.** A picture nothing uses moves to `archive/<companion>/` with an entry in `manifest.json`'s `archive.retired` and in that folder's README (where it came from, SHA-256). Never delete a picture.
- **Exports** are made only by `tools/art-export` and published by the release workflow as `art-<N>`. Never commit an exported copy.
- **Checks to run** before pushing: `cargo run --locked --manifest-path tools/art-check/Cargo.toml -- .` and `cargo test` in each tool.
- **Releases** reach the other repositories through AnkiQuest-Sync; a change here shows up there as a "Use AnkiQuest-Art" pull request.
