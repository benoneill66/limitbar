# Backlog

Planned work, not yet released. Shipped changes are in [CHANGELOG.md](CHANGELOG.md).

## Next release (together with Kiro)

- **Kiro support.** Read Kiro's remaining credits through its own CLI (`kiro-cli chat --no-interactive
  "/usage"`, or its ACP mode), inside the same sandbox as the other CLIs — no tokens, cookies or private
  APIs. Requested in [#1](https://github.com/dancik/limitbar/issues/1). Copilot and Cursor wait until
  their CLIs report remaining quota.
- **Installer: overlapping installs.** Two installs running at the same time (for example an agent
  retrying while the first is still placing the app) can delete the previous LimitBar copy. Fix: place and
  restore with an exclusive rename that never nests into an existing folder, put the previous copy back on
  any failure after it was moved aside, and keep the temp folder until the new app is verified.
- **Installer: unrelated link at `~/Applications/LimitBar.app`.** When upgrading, a link there is replaced
  even if it points somewhere other than LimitBar (the link's target is never touched). Fix: replace the
  link only when it points to this LimitBar; otherwise leave it and stop.
