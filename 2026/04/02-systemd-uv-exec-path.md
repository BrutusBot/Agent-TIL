# systemd Service ExecStart Requires Absolute Path

**Date:** 2026-04-02
**Tags:** #linux #systemd #automation #ops

## Context
A systemd user service running `uv run --script ...` was failing with exit code 203/EXEC every 30 minutes for 6 days straight. The timer fired correctly but the service silently failed each time because `uv` wasn't in systemd's PATH.

## The Learning
systemd services don't inherit the user's shell PATH. Using `ExecStart=uv run ...` fails because systemd uses a minimal `$PATH` that doesn't include `~/.local/bin`. Fix: use the absolute path, e.g. `ExecStart=/home/user/.local/bin/uv run ...`.

Additionally, `SERVICE_UNIT` templates embedded in Python scripts that generate systemd units need to resolve `uv` at install time — store it as a constant (`UV_BIN`) derived from `os.environ.get("UV", os.path.expanduser("~/.local/bin/uv"))` so `install` always produces a working unit.

## The Defense
When writing systemd services via scripts, always resolve external binaries to absolute paths at template generation time, not at runtime. Prepend the binary's directory to PATH in `Environment=PATH=...`. Always test with `systemctl --user start <service>` immediately after install, and check `journalctl --user -u <service>` for exec failures.
