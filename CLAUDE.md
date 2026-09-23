# CLAUDE.md

Read `CONSTITUTION.md` first; the estate's shared constitution arrives through the `helios`
plugin before it. This file is the working rules for HeliosDoors. Anything local to one machine lives
in the gitignored `CLAUDE.local.md`, never here: this file is public.

## Project

BBS-agnostic door hosting service. A separate daemon that runs doors and takes callers from any BBS that supports its hosting protocol, in the spirit of the classic door servers. Helios Advance itself never launches a door; it hands the caller to this service and gets them back. One developer, six repositories under the `HeliosBBS` organisation
developed together; developer time is the scarcest resource, so the tooling does the
breaking-down, the model does the building, and the developer reviews in feature terms.

## Layout

| Path | Holds |
|---|---|
| `CONSTITUTION.md` | what is specific to this project; the shared principles come from the plugin |
| `features/` | feature briefs, one file per feature, developer-owned |
| `docs/spec/` | the derived corpus: `architecture.md` and one file per subsystem |
| `Makefile` | `make check` runs everything CI runs, once the first feature has chosen the stack |

The skills (`feature-brainstorm`, `feature-design`, `feature-plan`, `feature-build`,
`compound`) and the hooks come from the plugin; the issue form, labels and reusable workflows
from the estate's `.github` repository; the operational runbook and learnings live in this
repository's wiki, unreviewed and disposable by design.

## The stack

Not chosen yet. The first feature's design records it in `docs/stack.md`, outside the spec
corpus, which never names a language, file or query language,
and adds the `Makefile` whose `check` target becomes the required check on `development`.
Until then there is nothing to build and CI runs nothing.

## Work tracking, routing, branches

As in the engine's `CLAUDE.md`, which is the reference: GitHub Issues through the issue form
and `work`; Sonnet 5 at high effort by default with route-up decided by code and review never
downgraded; `main` is the default branch and holds releases only, `development` takes pull
requests on green checks, work branches are `issue-<n>-<slug>` in their own worktree; the
unattended loop commits as the organisation's App, never as the developer.

## Mandatory rules

- Never commit a credential, key or token. Push protection is on.
- Hooks enforce the mechanical rules: `features/`, `CONSTITUTION.md` and the licence files
  are developer-owned; edits are formatted; a turn does not end on a red `make check`.
- An interface crossing a repository boundary is a protocol or a wire format, versioned in the
  contracts register, or it does not cross.
- Questions: one at a time. Pushback: with reasoning, never an echo.
- State assumptions before coding; minimum code that solves the problem; touch only what the
  request needs; four attempts per bug, then raise it; fail loud.

## Code style

Allman braces in every language except Go. Names readable without knowing abbreviations. A
comment is the exception and explains a why the code cannot show. Every permission check gets
a negative-path test. Never log a secret. Supported targets: `linux/amd64`, `linux/arm64`,
`windows/amd64`.

## Licence

**GNU Affero General Public License, version 3 only** (not "or later"), with no additional permissions at present. The engine's Scripting API Exception does not apply here: doors reach this service over the Door Kit's wire protocol and never link into it. Should an exception ever be needed, it will be added deliberately and documented in this file. See `LICENSE`. Dependencies are weighed against writing the code natively and every
new one is audited for licence compatibility.
