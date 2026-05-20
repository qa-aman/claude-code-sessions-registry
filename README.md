# Claude Code Sessions Registry (`ccs`)

A tiny session manager for [Claude Code](https://claude.com/claude-code). Name, list, and resume your sessions across many terminals without ever using the `/resume` picker.

If you run 5+ Claude Code sessions in parallel across projects, the built-in resume picker becomes unusable — every session looks like a hex ID and you forget which is which. `ccs` fixes that with three small pieces, all local:

1. A single bash script at `~/.local/bin/ccs` — the CLI.
2. A global registry JSON at `~/.claude/named-sessions.json` — the source of truth.
3. A per-project `<project>/.claude/claude-sessions-registry.md` — auto-created the first time you register a session in that project, so you can browse "what sessions exist for this project" right in your repo.

No daemons, no databases, no cloud sync. Pure bash + python3.

## Install

The fastest way: hand the single HTML file in this repo to a fresh Claude Code session and tell it to follow the instructions.

1. Open [`claude-sessions-registry-bootstrap.html`](./claude-sessions-registry-bootstrap.html) in your browser. ([Raw view](https://raw.githubusercontent.com/qa-aman/claude-code-sessions-registry/main/claude-sessions-registry-bootstrap.html) also works.)
2. Copy the **bootstrap prompt** from Section 2.
3. Paste it into any Claude Code session.
4. Claude installs `ccs`, sets up your `PATH`, initialises the registry, and runs a smoke test.

Manual install instructions are in Section 3 of the same HTML, if you prefer.

## Usage

Look at the statusline of the Claude Code window you want to register. It shows the project name and a PID, for example `my-project  pid:54057`. Then:

```bash
ccs add my-session 54057
ccs add my-session 54057 "Working on the auth refactor"
```

From inside Claude Code, prefix with `!`:

```bash
! ccs add my-session 54057
```

Other commands:

```bash
ccs list                    # all named sessions with live/idle status
ccs pids                    # currently running Claude PIDs
ccs sessions                # last 30 sessions from history
ccs open my-session         # resume by name (run outside Claude Code)
ccs rename old new
ccs update my-session "Updated description"
ccs remove my-session
ccs sync                    # rewrite every project's registry table from the JSON
```

## How the per-project registry works

The first time you run `ccs add` in a project, `ccs` auto-creates `<project>/.claude/claude-sessions-registry.md` from an embedded template. Every subsequent `ccs add`, `ccs remove`, `ccs rename`, and `ccs sync` rewrites the Registered Sessions table inside it. You never copy a template by hand.

You can commit that file to your project's repo if you want your team to see what sessions you maintain — there's nothing sensitive in it (no tokens, no transcripts).

## Requirements

- macOS or Linux
- `bash`, `python3` (>= 3.9), `mkdir`, `chmod`
- Claude Code installed and authenticated

## License

MIT. Share freely.
