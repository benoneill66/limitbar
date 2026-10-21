# Security policy

LimitBar runs other programs (the AI CLIs you installed) and is installed with a script, so its security
matters more than its size suggests. Reports are welcome.

**Report privately:** use GitHub's "Report a vulnerability" button on this repository's Security tab
(private vulnerability reporting). Please do not open a public issue for a vulnerability.

In scope, for example:
- any way LimitBar could read, store or send a credential, or expose one to a CLI's environment;
- running an executable it should have refused (see `CLI.trusted` in `Sources/LimitBar/Spawn.swift`);
- escaping or weakening the CLI sandbox (`Resources/cli.sb`) that codex, agy and grok run in;
- a `claude` invocation that loads user hooks, MCP servers or settings despite the isolation flags;
- the installer accepting a modified archive, or `--from-source` building a different commit.

Supported: the latest release.
