## This repository

AnkiQuest-Android-MCP is a fork of [ankimcp/ankidroid-mcp](https://github.com/ankimcp/ankidroid-mcp): an Android app (Kotlin, Compose) that serves MCP over the AnkiMCP tunnel relay and reads AnkiDroid or AnkiQuest through its content provider.

- **Upstream's instructions.** `CLAUDE.md` is upstream's, with `@AGENTS.md` added as its first line. Its rules still apply to code in this project: the layout, tunnel protocol compatibility, never logging tokens, Firebase imports, tool conventions and `docs/DECISIONS.md`. Where it contradicts the shared rules above, follow it for upstream's code and ask hill.
- **Branches.** `master` is our version; today it equals upstream, and our CI, Nix shell and, once published, `org.ankiquest:api` are to follow. `ankidroid-provider-check` and `ankiquest-support` are proposals for upstream: keep them in upstream's style, without AnkiQuest-only changes; merge upstream into them when it moves.
- **Upstream merges** come from the sync job's pull request; merge with a merge commit.
- **Releases** to Google Play are upstream's; don't publish from this fork.
- **Checks to run** before pushing: `./gradlew :app:testDebugUnitTest` and `./gradlew :app:lintDebug`.
