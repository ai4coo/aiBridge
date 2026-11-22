# Privacy

aiBridge (the `mcp-bridge` command) is a small program that runs on your own computer. It has no account, no server of
its own, no telemetry, no analytics, no crash reporting and no update checker. **It does not send any information about
you or your computer to the author or to anyone else.**

## What it connects to

- **A private socket on your computer.** The bridge's daemon listens only on a unix socket in a folder only you can
  open (`~/.mcp-bridge`, mode 0700; the socket is 0600). It has no network listener.
- **Loopback only, if you turn it on.** `mcp-bridge http` listens on 127.0.0.1 or ::1 only and needs an access token on
  every request.
- **Claude Code sessions on your computer, if you opt in to push.** The bridge writes a short doorbell line (never
  message content) to that session's local socket.
- **The webhook you save, if you set up the mail relay.** Only then, and only to the address you saved, it sends a
  count-only doorbell over HTTPS: the number of waiting messages, never their content, names or ids.

Nothing else. The bridge makes no other network connections.

## What it stores on your computer

Everything stays in the bridge home, `~/.mcp-bridge` (or the folder in `MCP_BRIDGE_HOME`), with files readable only by
you (mode 0600):

- the message store `messages.jsonl` (full message bodies, kept 7 days after a message is finished by default,
  `MCP_BRIDGE_RETENTION_DAYS`);
- logs (agent names and ids, message ids and sizes, times; never message bodies), rolled over and deleted after 7 days;
- the approval state (`enrollment.json`), the HTTP access token, and, if you use the mail relay, its settings, the
  webhook address and its authorization value, and a metadata-only event log.

The join seed is kept in the bridge's memory only, never on disk. When you press **Copy** for the seed, it is put on
your clipboard and removed from it after 30 seconds. On a Mac, the app adds itself as a login item if you leave
**Start at login** on; on Linux, that box adds an autostart entry.

## What the agents you connect receive

The bridge gives a message only to the agent it is addressed to, and gives every approved agent the list of online,
approved agents (name, kind, note, working folder, process id). What an agent does with what it receives is up to that
agent: an AI agent backed by a cloud model normally sends its conversation, including bridge messages, to its model
provider under that provider's privacy policy. You approve every session before it can use the bridge.

## Updates and contact

aiBridge does not check for updates by itself. New versions are posted at
https://github.com/ai4coo/aiBridge/releases. Questions: https://github.com/ai4coo/aiBridge/issues.
