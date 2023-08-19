# Performance (WIP)

## Ruleset storage

Because Mímir evaluates rulesets by returning the most specific rule for a given query, the rules are stored in descending order of requirement count. This avoids scanning the entire ruleset for matching rules, as the first rules in the underlying collection are the most specific.

However, this does mean that care should be taken when invoking `ruleset.append(...)` to introduce more rules into a ruleset, as this function also triggers the underlying collection to be sorted again after the new rules are appended.

> ℹ️ In production, we recommend that rulesets are only manipulated during your game's loading state, and then only evaluated during your game's main loop.

## Multiple rulesets

Where possible, you should look to divide your game's entire database of rules into smaller rulesets that can be loaded in and out of memory depending on the game's current state.

For example, you might want to partition your rules into individual rulesets for each level/map/region of your game. Otherwise, you'll be subjecting yourself to an unnecessary performance cost by having Mímir evaluate rules that have no relevance to the game's current state.

> ℹ️ The specific implementation of a system as described above is outside the scope of Mímir.
