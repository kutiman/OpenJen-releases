# OpenJen — downloads

Published builds of **OpenJen**, a Windows desktop app that manages scoped worker agents on Claude Code and the Gemini CLI: what each worker is responsible for, what it must not touch, and a manager that plans work you approve step by step.

**[Download the latest release →](https://github.com/kutiman/openjen-releases/releases/latest)**

This repository holds the builds and nothing else. The source lives in a private repository, and every file published here was built there by GitHub Actions on a Windows runner — never on anyone's laptop — so each release can be traced back to the commit named in its notes.

## What is in a release

Two Windows x64 files, both unsigned:

| File | What it is |
| --- | --- |
| `OpenJen.Setup.<version>.exe` | The installer: Start-menu and desktop shortcuts, and a choosable install folder. This is the one an installed OpenJen downloads when it updates itself. |
| `OpenJen-<version>-portable.exe` | One file, no installation. Run it from wherever you keep it. |

Because they are unsigned, Windows SmartScreen warns the first time you run one: **More info → Run anyway**.

## Updating

An installed OpenJen looks at this page by itself — a few seconds after it starts, and at most once every six hours. When there is a newer build, the sidebar offers it; clicking downloads the installer and runs it, and your work is untouched because all of it is files on disk. No account, no token and no `gh` CLI are needed to check or to download: the releases here are public.

## What OpenJen is

- **A worker cannot edit outside its lane.** Not "is asked not to" — the write is denied, by a `PreToolUse` hook on Claude Code and by a scope-checking MCP server on the Gemini CLI, in headless runs as well as interactive ones.
- **A manager never runs as a worker.** Tell one what you want and it writes a plan: a chain of tasks, one per worker, each with deliverables and acceptance criteria. OpenJen creates the tasks from that plan, not the manager. You approve the plan, and then every finished step.
- **Nothing on the network.** No port, no database, no account, no telemetry. The window reaches its engine over a named pipe whose name is generated at launch, and every byte of state is JSON inside your own project folder.

## Licence

MIT — see [LICENSE](LICENSE). The builds published here carry the same licence as the source.
