# MultiActionEmotes — concept and creative direction

**By:** Babuni

## When one roar is not enough

After my earlier single-slot emote experiments, the idea grew into making several action buttons independently expressive. My **MultiActionEmotes** repository retains that older **ROARRunlimited** implementation and its original “action bar into a war drum” image.

Earlier ROAR/ROARR addons let the player pick one action-bar button to occasionally trigger a built-in emote. **ROARRunlimited expands that idea from one watched action into a configurable collection of independent expressive triggers.** A different button can have a different personality rhythm: frequent enthusiasm on one action, rarer celebration on another.

The source implements this through numbered configurations (“instances”), each pairing a WoW action slot with a probability and a cooldown. The numbering is a convenient reference in slash commands, not a cap of one or two predefined buttons. The player retains control of every actual action.

The original repository description says ROARRunlimited “plays battle-themed emotes from multiple watched action slots.” Its README finishes with the creator's metaphor of turning the **action bar into a war drum**. This supports the artistic goal without requiring us to invent an original design dialogue.

## Experience principles embodied in code

- **Player action drives expression:** `UseAction` presses provide timing rather than an autonomous interval event.
- **Independent patterns:** a chosen instance may have its own emote probability and cooldown.
- **One coherent voice:** the built-in token pool makes gestures recognizable in the game without custom graphics or music.
- **Simple configuration:** `/roed slotX`, `chanceX`, and `timerX` pair numbers with settings; no persistent window.
- **Reversible quiet:** `/roed off` suspends the effect without clearing the configuration.
- **Lightweight flavor:** no targeting choices, damage, cast automation or PvP advantage.

## A meaningful evolution across the committed code

The first December 2025 source indexed entries directly by watched action-slot ID. A subsequent revision indexed entries by **instance number**, allowing slot assignments to be changed while chance/cooldown values remain associated with a named configuration. In January 2026 a further source revision normalized old saved entries and reduced the pool to four native emotes, removing BORED. These changes are supported by actual diffs; they are **not proof of a recorded author vote, a specific design disagreement, or a tested release process**.

## What still needs author input

The code allows more than one instance to watch the same physical action slot, potentially producing multiple emotes on one press. Whether this is creative flexibility or an edge case to prevent is for me to decide. The current documentation does not implicitly approve restricting it.

This repo should be preserved as a distinct step in the broader ROAR addon family, but direct migration or inheritance beyond demonstrated similarities requires evidence.

## Related development history

Multi Action Emotes (originally ROARRunlimited) made a major advance by supporting multiple independently configured watched-action-slot instances. Its **four built-in emote tokens**—ROAR, CHARGE, CHEER, FLEX—form a fixed Lua array; `slotX`, `chanceX` and `timerX` configure each instance, but there is **no command to add a new emote token**. Editable registries appear in the subsequent Roar Guild Addon and Wrath port. See [the full comparative record](docs/EMOTE_FAMILY_HISTORY.md) for the wider evolution.
