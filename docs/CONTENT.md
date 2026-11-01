# MultiActionEmotes — emote inventory and player-facing text

This inventory records the original **ROARRunlimited** addon content, now presented under my repository name **MultiActionEmotes**. The change did not alter emote tokens or game text.

**Project author:** Babuni.  
**Canonical implementation:** `EMOTE_TOKENS_BATTLE` in `ROARRunlimited.lua`.

## Current emote pool (four tokens)

| Built-in game emote | Expressive purpose |
| --- | --- |
| `ROAR` | Battle cry and presence |
| `CHARGE` | Aggressive forward momentum |
| `CHEER` | Encouragement and celebration |
| `FLEX` | Pride and strength |

These are **game-native `DoEmote` tokens**, not original audio, bespoke animations or a text-generation model. The game client controls their realized emote/animation behavior.

An older December 2025 version additionally contained **`BORED`**. Commit `ce86437` (2026-01-09) removed it, leaving the present four-token selection. That establishes a content change, but not the creator's reason for it.

The code's fallback when `DoEmote` is missing is a generic authored text emote: “makes a battle cry!”

## Chat-command language

User-facing feedback is prefixed with `ROED:`. The addon uses `/roed` (not `/roarr`) with numbered command patterns:

- `slotX` assigns which physical action slot an instance watches.
- `chanceX` adjusts its percentage.
- `timerX` adjusts its interval.
- `watch`, `info`, `reset`, `on`, `off` support setup and control.

Source strings and the README are in English. No separate locale tables or embedded sound assets are committed.

## Content-edit standards

Preserve the distinction between a **new emote token** (game-owned vocabulary) and a **new original written line** (author-owned text), and do not claim a real animation or sound effect without checking the actual client. For any content revision, document the author's direction, source diff and observed behavior.

## Related development history

Multi Action Emotes (originally ROARRunlimited) made a major advance by supporting multiple independently configured watched-action-slot instances. Its **four built-in emote tokens**—ROAR, CHARGE, CHEER, FLEX—form a fixed Lua array; `slotX`, `chanceX` and `timerX` configure each instance, but there is **no command to add a new emote token**. Editable registries appear in the subsequent Roar Guild Addon and Wrath port. See [the full comparative record](EMOTE_FAMILY_HISTORY.md) for the wider evolution.
