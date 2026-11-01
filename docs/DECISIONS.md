# MultiActionEmotes — design decisions and evidence

**Human creative authority:** Babuni.  
**Status legend:** Implemented in source, historical Git evidence, or not yet decided.

## Implemented choices

| Topic | Evidence | Interpretation boundary |
| --- | --- | --- |
| Multiple watched slots | `WATCH_SLOTS`, `UseAction` loop | Core difference from single-slot ROAR/ROARR |
| Numbered instances | `slotX/chanceX/timerX`, commit `fcba0bf` | Independent configuration entries, not a verified conversation |
| Per-instance cooldown and probability | Each `cfg.cd`, `cfg.chance`, `cfg.last` | Missed chance still advances `last` |
| Native game emotes | `DoEmote` and fixed token pool | Four tokens in current v1.1 |
| Global suspension | `ENABLED`, `/roed on/off` | All instances disabled together |
| Stored settings | `ROEDDB.slots`, `ROEDDB.enabled` | Account-wide; timer timestamp also persists |
| Source compatibility work | `ad7d6a2` replaced `string.match` with `string.find` | Intended Lua 5.0 support, not proof of current runtime success |

## Documented historical turns

The 2025-12-14 first uploaded Lua indexed configurations by **action-slot number** and originally changed chance/cooldown values more broadly. Subsequent commits introduced per-configuration adjustments and, later that same day, **numbered instance records** pointing at separate physical slots.

On 2026-01-09 the source was labeled **v1.1 FIXED**, restored/normalized default fields when loading saved entries, and removed `BORED`. The TOC version was also updated. These are direct code changes; the commit labels cannot substitute for a game-client test result or a recovered explanation of author intent.

## Unresolved engineering questions

- **Packaging:** the TOC references lowercase `roarrunlimited.lua`, which does not exactly match `ROARRunlimited.lua` in Git.
- **Session clocks:** saved `cfg.last` depends on `GetTime()`, so session boundaries can affect cooldown eligibility.
- **Saved-state initialization:** logout does not call `ensureLoaded` and may replace settings if no interaction occurred.
- **Duplicate physical slots:** two instances can emit for one button press.
- **Unbounded instances:** every `UseAction` call iterates all registered instances.

These are **risks / observable semantics**, not proven client failures or implicitly approved changes.

## Pending creator decisions

1. Which capitalization/package fix should be used?
2. Should last-attempt timestamps be reset at login while keeping chance/cooldown preferences?
3. Is multiple output for the same physical slot desirable?
4. Should users be able to remove a single instance?
5. Should the source's removal of `BORED` be treated as a permanent artistic choice?

The documentation pass settled none of these on Babuni's behalf.

## November 2026 — repository identity

The new repository name, **MultiActionEmotes**, describes the multiple independently configured action-slot triggers without discarding the historical **ROARRunlimited** addon identity. This naming choice is mine; AI updated the documentation at my direction. No runtime identifiers were changed or tested.

## Related development history

Multi Action Emotes (originally ROARRunlimited) made a major advance by supporting multiple independently configured watched-action-slot instances. Its **four built-in emote tokens**—ROAR, CHARGE, CHEER, FLEX—form a fixed Lua array; `slotX`, `chanceX` and `timerX` configure each instance, but there is **no command to add a new emote token**. Editable registries appear in the subsequent Roar Guild Addon and Wrath port. See [the full comparative record](EMOTE_FAMILY_HISTORY.md) for the wider evolution.
