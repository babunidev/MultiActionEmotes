# MultiActionEmotes — development instructions

**By:** Babuni.

## Identity and writing rules

The current GitHub repository is **MultiActionEmotes**, formerly `ROARRunlimited`; the actual addon retains `ROARRunlimited.lua`, `ROARRunlimited.toc`, `/roed`, and `ROEDDB`. The case mismatch between the TOC's `roarrunlimited.lua` reference and the on-disk `ROARRunlimited.lua` is unresolved and must not be silently fixed as part of renaming documentation.

Write public-facing history in my first-person perspective, never starting a sentence with “I” or “My.” Use **Babuni** for the person and **babuni.dev** for the portfolio. Use **creative**, not “creator,” for the human role label. Attribute AI work separately and only when evidenced; distinguish proposals, implemented edits, tests and retrospective reconstruction. Neutral technical voice is acceptable for reference material.

## Preserve this project's role

ROARRunlimited is the **multi-instance** branch of the action-triggered emote idea: each numbered instance configures a physical action slot, chance and cooldown. Keep that architecture distinct from the single-slot `roar` and `roarr` repositories and from later RoarForever unless specific Git or creator evidence establishes a connection.

Read `README.md`, `CONCEPT.md`, `docs/ARCHITECTURE.md`, `docs/DEVLOG.md`, `docs/DECISIONS.md` and current Lua/TOC before designing any change.

## Collaboration history and truthfulness

1. Credit Babuni for the idea and human creative direction; assign AI only work specifically evidenced as AI assistance.
2. Preserve source-backed iterations (2025 per-slot configuration → v1.1 instance numbering → 2026 four-token pool) without inventing dialogue, approval or rationale.
3. Separate user decisions from AI proposals and mark outstanding options clearly.
4. Every material change should update README, ROADMAP, CHANGELOG and relevant `docs/` records with exact changed paths and commit.
5. Never claim a successful WoW test when only inspecting source or Git diffs.
6. Preserve MIT license, copyright notice and author identification. The source's older display alias may be historically relevant; don't rewrite executable files in an incidental docs pass.
7. Do not publish credentials or private player conversations in portfolio narratives.

## Technical review checklist

- **Fix/verify case mismatch only with explicit implementation authorization:** `roarrunlimited.lua` in TOC versus `ROARRunlimited.lua` in tree.
- Use WoW 1.12/Lua 5.0-safe APIs. Historical source revisions replaced `string.match` with `string.find`.
- Preserve delegation to original `UseAction`; test global-hook interoperability and per-press iteration performance.
- A failed chance roll still consumes a per-instance interval.
- `cfg.last` is stored in persisted `ROEDDB.slots`; beware session-relative `GetTime()` after restarts.
- Loading of saved settings is lazy; `PLAYER_LOGOUT` saves whether or not `ensureLoaded` was invoked.
- Two instances can watch the same physical slot and each may emit one emote.
- Test actual client behavior and record failures as failures, not inferred successes.

## Lineage and technical limits

Consult [the emote-family history](docs/EMOTE_FAMILY_HISTORY.md) before describing the ROARRunlimited progression. Multiple slot configurations are implemented here; a user-editable emote registry is not. Do not claim an unbounded emote list or reuse features from later Roar Guild versions as current behavior.
