# Changelog

All notable changes to the Claude Code Sessions Registry (`ccs`) are recorded here.

Format based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/). Dates use DD-MM-YYYY.

## [0.2.0] - 02-07-2026

### Added

- `cleanupPeriodDays` retention setting. Claude Code auto-deletes local session transcripts after a retention period (default 30 days), which leaves `ccs open` with nothing to resume. The bootstrap prompt now writes `cleanupPeriodDays` into `~/.claude/settings.json` automatically, and the README documents how to set it manually. Set any number of days you like.

## [0.1.0] - 20-05-2026

Initial release. A three-piece local session manager: a bash CLI at `~/.local/bin/ccs`, a global registry at `~/.claude/named-sessions.json`, and a per-project `<project>/.claude/claude-sessions-registry.md`.

### Added

- `ccs` CLI with `add`, `list`, `pids`, `sessions`, `open`, `rename`, `update`, `remove`, and `sync` commands.
- Single-file HTML bootstrap (`claude-sessions-registry-bootstrap.html`) with a paste-ready prompt, statusline setup, and a first-session walkthrough. Hand it to a fresh Claude Code session to install `ccs` end to end.
- Statusline setup that captures `$PPID` into `claude_pid` on the first line, so the PID shown in the statusline is unambiguous versus the session ID and child PIDs.
- Auto-created per-project registry markdown with a Registered Sessions table, rewritten on every `add`, `remove`, `rename`, and `sync`.
- README with install, usage, and requirements.

### Fixed

- HTML-entity rendering inside the bootstrap prompt.

### Changed

- Hardened bootstrap: HTML entity note, shell-aware `PATH` setup, robust PID resolution, 7-digit PID handling, an entity warning on step 6, a troubleshooting table, a manual-install cross-reference, and an uninstall section.
