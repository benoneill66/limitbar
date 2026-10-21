# Installing LimitBar — instructions for an AI agent

You are installing LimitBar, a macOS menu bar app that shows the user's AI CLI usage limits.
Follow these steps exactly. Do not improvise other install methods.

1. **Check the machine.** Run `sw_vers -productVersion`. Continue only on macOS 14 or later.
2. **Download the installer** (pinned to one commit; do not substitute `main`):
   ```bash
   d="$(mktemp -d)" && curl -fsSLo "$d/install.sh" https://raw.githubusercontent.com/dancik/limitbar/746928f7ba250aaec29adcaa9bf8ec4ee6e6d855/install.sh && echo "$d/install.sh"
   ```
   Use the printed path (a fresh private folder) in the next steps — never a fixed path in /tmp.
3. **Read it** (`cat "$d/install.sh"`) and tell the user in one or two sentences what it does:
   downloads the release zip, verifies its SHA-256 (and build provenance if `gh` is installed), installs
   to `~/Applications`, no sudo.
4. **Run it:** `bash "$d/install.sh"`. Never run it with `sudo`. If it stops with a
   verification error, stop and report the error — do not work around it.
5. **Check what LimitBar sees:**
   ```bash
   ~/Applications/LimitBar.app/Contents/MacOS/LimitBar --probe
   ```
   For each of `claude`, `codex`, `gemini`, `grok`, report the `state`:
   - `ok` — working; mention the main percentage.
   - `missing` — that CLI is not installed. Only mention it if the user uses that service.
   - `signedOut` — tell the user to sign in **themselves**: `claude` then `/login`, `codex login`,
     `agy` (first run), or `grok login`.
   - `untrusted` — the CLI file is writable by other accounts; tell the user, do not change permissions
     yourself.
   - `failed` — report the `error` text.
6. **Never** ask the user for, read, copy or print any token, API key, cookie or credential file. Signing
   in is always done by the user inside the official CLI.
7. Tell the user: LimitBar is in the menu bar; hover it for details; the panel has "Launch at Login".

To remove it later: download the installer the same way and run it with `--uninstall`.
