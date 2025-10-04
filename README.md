# Dharma Agents Manifest Sync

This repository exists solely to expose the canonical `AGENTS.md` manifest as a public, easily fetchable artifact. Downstream developer workflows—especially pre-commit hooks across other Dharma repositories—retrieve the raw contents of this file during formatting and validation steps to keep their local `AGENTS.md` copies perfectly in sync.

## Why this repository is public

The manifest documents high-level agent metadata and omits any personally identifiable information, proprietary algorithms, or sensitive operational details. Publishing it removes the need for authenticated fetches inside automation, which keeps the pre-commit hooks snappy and removes an unnecessary credential management burden for contributors.

## What the hooks do

* On each run, the hooks pull the raw file served from this repository (e.g., via `curl https://raw.githubusercontent.com/dharma-app/dharma-docs/main/AGENTS.md`).
* They compare or overwrite the local `AGENTS.md`, ensuring every codebase shares the exact same agent roster without manual edits.
* Because the source of truth is version-controlled here, any updates propagate automatically the next time a developer hits the pre-commit boundary.

## Contributing changes to `AGENTS.md`

1. Propose updates in this repository and open a pull request for review.
2. Once merged, downstream hooks will pick up the change on their next invocation.
3. No additional configuration is required in consuming repositories—the hooks already know where to look.

That’s the entire purpose of this repo: a minimal, transparent distribution point that keeps the agent manifest synchronized everywhere with zero friction.
