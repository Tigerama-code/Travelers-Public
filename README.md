# Travelers

A peer-to-peer game of settlement and trade. One player hosts from their own
device, shares a five-letter room code, and everyone else joins by typing a
name. **No accounts, no usernames, no server, no running costs.**

### ▶ [Play in the browser](https://tigerama-code.github.io/Travelers-Public/)

Nothing to install and nothing to trust — this is the easiest way to get a game
going with friends. Send them the link and the room code.

### Or download it for Windows

| Download | What it is |
| --- | --- |
| **[Travelers-Setup.exe](https://github.com/Tigerama-code/Travelers-Public/releases/latest/download/Travelers-Setup.exe)** | Installer. Per-user, so **no administrator rights needed**. |
| **[Travelers-portable.exe](https://github.com/Tigerama-code/Travelers-Public/releases/latest/download/Travelers-portable.exe)** | A single file that runs without installing. |

Either file is the whole game — the engine and the interface are bundled inside,
so there is nothing else to install. Three things are worth knowing:

- **Windows SmartScreen will warn you** on first run. The binary is unsigned,
  because a code-signing certificate costs about $200 a year for a game nobody
  is being charged for. The browser version avoids the question entirely.
- **Multiplayer needs internet** — for matchmaking, not for a server. Two
  browsers are introduced to each other over a public relay and then talk
  directly. Pass-and-play on one machine works with no connection at all.
- **Both sides need the same version.** The wire protocol is not versioned, so
  a 0.1.0 host and a 0.2.0 guest are not guaranteed to agree.

---

## How it runs without a server

Matchmaking runs through [Trystero](https://github.com/dmotz/trystero) over
public Nostr relays, which carry only the WebRTC handshake — a few kilobytes to
introduce two browsers. After that, all game traffic flows **directly between
players**, end-to-end encrypted with the room code as the key.

```
  Host browser  ──── WebRTC (game data, E2E encrypted) ────  Peer browser
        └──────── Nostr relay (handshake only) ────────────────────┘
```

Whoever clicked *Host a game* runs the rules engine and is the authority on
game state. Peers send intents ("I want to build a road here") and receive a
**redacted** view back: your own hand in full, and only card *counts* for
everyone else. Opening dev tools reveals nothing hidden, and a peer cannot
fabricate resources because it never writes state — it only asks.

There is no backend to deploy and nothing to pay for. The site is static files,
which GitHub Pages serves free.

---

## About this repository

This repository is **published output, not source.** `site/` is the built web
bundle and the releases hold the built Windows binaries; both are rebuilt and
pushed here automatically whenever the source changes.

The source itself lives in a separate private repository. Anything committed
here by hand will be overwritten by the next publish, so there is nothing useful
to send a pull request against.

---

## Legal note

CATAN and its expansions are trademarks of Catan GmbH. This is an unofficial,
non-commercial implementation built for personal play. It ships no artwork or
text from the published games — only original code and an original interface.
