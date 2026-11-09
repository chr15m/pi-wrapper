# Sandboxed Pi Coding Agent

A wrapper script that runs the Pi coding agent inside a lightweight
Bubblewrap (`bwrap`) sandbox.

## Overview

The `pi` wrapper script ensures that Pi runs with least privilege:

- Restricts host filesystem access.
- Restricts process visibility.
- Retains outbound network connectivity for LLM API calls.
- Preserves user configuration and session history across runs.

## Sandbox Configuration

The wrapper script mounts the following resources:

- System mounts (read-only): `/usr`, `/bin`, `/lib`, `/lib64`,
  `/etc/resolv.conf`, and `/etc/ssl`.
- Node.js runtime: The Node 22 installation directory resolved via `nvm`.
- Working directory: The current working directory is mounted read-write
  as the target workspace.
- Configuration:
  - `~/.pi`: Mounted read-write for sessions and settings.
  - `~/.gitconfig` and `~/.gitignore_global`: Mounted read-only if present.
- Isolation:
  - Fresh in-memory `tmpfs` on `/tmp`.
  - Process isolation via `--unshare-all` (separate PID namespace).
  - Network namespace shared via `--share-net` for API requests.

## Prerequisites

- Bubblewrap (`bwrap`)
- `nvm` with Node.js 22 installed

## Usage

Run the script from any target project directory:

```bash
/path/to/pi [options]
```
