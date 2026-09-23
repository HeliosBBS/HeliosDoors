# Constitution

The estate's shared constitution, in the `helios` plugin, is loaded first in every session and
holds the principles: authority from features down, security designed in, multi-node from the
start, the estate and its contracts, the spec rules. This file adds only what is specific to
HeliosDoors, and is loaded right after it, unchanged.

## Role

A separate daemon that runs doors and takes callers from any BBS that supports its hosting protocol, in the spirit of the classic door servers. Helios Advance itself never launches a door; it hands the caller to this service and gets them back.

It owns the door hosting protocol and consumes the door wire protocol's host side. An interface it owns changes here first, with a version,
before any consumer moves; an interface it consumes is cited by name and version from the
contracts register, never restated.

## How this file is used

Loaded after the shared constitution by every skill, every prompt and every loop iteration. A
change to it is a pull request the developer approves, and nothing else edits it.
