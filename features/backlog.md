# Backlog

Features mentioned and not yet brainstormed, in dependency order. A line here is a name, a
purpose and what it depends on, plus anything the developer has already said about it, kept in
their words so nothing is lost before its brainstorm. Nothing on this list is designed or
built until it has been through `feature-brainstorm` and has a brief of its own.

## Hosting

- **Door hosting service**: `hadv-doors`, a standalone, BBS-agnostic service that hosts door
  games, installed alongside `hadv-service` on the same hardware or on dedicated hardware.
  Each instance is separate; there is no federation. It owns the door hosting protocol, over
  which a board keeps the caller's connection and relays the game. Depends on: nothing.
- **Board registration**: a board registers with an instance so the instance knows which
  boards may use it. A pairing code is the secret of a password-authenticated key exchange:
  single-use, expiring in minutes, a failing source locked out; afterwards each side proves
  itself with pinned keys on every connection. This follows the pattern HeliosAdvance's server
  join settled, specified in this protocol rather than shared as code. A board registers as a
  whole, and every server of a multi-server board proves it belongs to that board. Each board
  picks a board tag at registration, unique within the instance. Depends on: door hosting
  service.
- **Game sessions and status**: the board passes the chosen game and only the player details
  its drop file needs, never a password, with private profiles respected; the instance writes
  the drop file. The instance answers with status codes, not text (full, all nodes busy, door
  disabled, maintenance, out of time, door crashed, returned normally), which the board turns
  into messages. A session names its front end: a relayed terminal stream, or a web session on
  a sandboxed page with a short-lived token for that game and player, never the board's own
  session or origin. Door output is untrusted, and each door is treated as hostile to its
  host. The instance writes DOOR32.SYS (the default), DORINFO1.DEF, DOOR.SYS or CHAIN.TXT, as
  each door needs; EXITINFO.BBS is not supported, since it holds the user number in a signed
  16-bit field. The protocol also carries a door's high scores, for the board's theme to show,
  and a signal when a slot frees, for the board's wait queue. Depends on: board registration.
- **Player identity**: a player is identified by board and account number, never by handle;
  shared games show the handle with the board tag, such as `John@HELIOS`. A legacy door that
  keys players on the drop-file name gets a stable name per player that fits the door's limit,
  with a suffix on collision. A private user appears on other boards' scoreboards only by
  opting in or through a game alias. When a board reports an account permanently deleted, its
  players show as a placeholder. Depends on: board registration.
- **Games for other BBSes**: an instance offers its games to any BBS that supports the hosting
  protocol, not only Helios Advance. Depends on: player identity.
- **Legacy DOS doors**: DOS doors run under emulation, typically DOSEMU on Linux, DOSBox, or
  86Box on Windows. Evaluate one of the few x86 emulators written in Go as a replacement: a
  spike against a set of doors the developer chooses (such as LORD, TradeWars 2002, BRE and
  Usurper), with its pass mark set before it starts, and the FOSSIL interrupt implemented
  directly on the connection. DOSEMU2 and DOSBox-X stay behind the same interface as the
  fallback. Depends on: game sessions and status.
- **Door Kit doors**: doors built with the Door Kit run over its wire protocol; the kit's
  host-side renderer draws them as ANSI for terminal sessions and as HTML for web sessions.
  Depends on: game sessions and status; the door wire protocol (HeliosDoorKit).
- **Door setup**: each door is classed as native (a TCP program or a local process) or DOS,
  with its hosting method recorded. A door has a command-line template (node, handle, socket,
  time left) and a working directory; the template is expanded into an argument list and run
  directly, never through a shell, and a handle is sanitised before it reaches a drop file or
  a command line. A lock-file policy covers games whose data files are shared across nodes.
  Each door has a maximum number of concurrent players, and a single-instance game gets node
  and slot assignment. Exit codes and abnormal endings are logged and reported to the
  operator, and a door can be disabled after N failures. Depends on: game sessions and status.
- **Interactive fiction door**, for later: a Z-Machine door that ships with the service, built
  with the Door Kit, playing only freely licensed stories (from the IF Archive and the yearly
  competitions); the Infocom titles are not bundled, and a sysop can add their own story
  files. Depends on: Door Kit doors.
- **Configuration**: standalone configuration utilities; `hadv-config` and `hadv-config-gui`
  can also configure an instance, through an admin interface this repository owns as its own
  contract, with its own credentials. Every default is the secure setting. Depends on: board
  registration.
