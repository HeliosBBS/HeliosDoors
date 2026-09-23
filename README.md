# HeliosDoors

BBS-agnostic door hosting service.

A separate daemon that runs doors and takes callers from any BBS that supports its hosting protocol, in the spirit of the classic door servers. Helios Advance itself never launches a door; it hands the caller to this service and gets them back.

## Status: pre-release, built in the open

No version has been released and no tag exists. `main` holds releases only; work lands on
`development` through pull requests, and the issues and the estate's project board show what
is being worked on now.

The project is designed feature-first: the developer writes a brief for each feature in
`features/`, and the specifications in `docs/spec/` are derived from those briefs, with every
section naming the features it serves. `CONSTITUTION.md` holds what is specific to this
project; the principles shared across the estate live in the
[HeliosSkills](https://github.com/HeliosBBS/HeliosSkills) plugin.

## The estate

Part of [Helios](https://github.com/HeliosBBS): the [engine](https://github.com/HeliosBBS/HeliosAdvance),
the [Door Kit](https://github.com/HeliosBBS/HeliosDoorKit), the
[door hosting service](https://github.com/HeliosBBS/HeliosDoors), the
[Portal](https://github.com/HeliosBBS/HeliosPortal) and the
[SIP gateway](https://github.com/HeliosBBS/HeliosSIP). Each project's interface to the engine
is a protocol, a wire format, or nothing at all. This one owns the door hosting protocol and consumes the door wire protocol's host side.

## Licence

**GNU Affero General Public License, version 3 only** (not "or later"), with no additional permissions at present. The engine's Scripting API Exception does not apply here: doors reach this service over the Door Kit's wire protocol and never link into it. Should an exception ever be needed, it will be added deliberately and documented in this file.

