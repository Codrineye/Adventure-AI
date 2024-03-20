# Arcade Adventure full auto script

`v3.3`

This script will fully automatically play the adventure game for you.
It will start by farming 11 keys, so don't wonder if it apears to be stuck betwenn the starting room and the first room.
After it has the keys it will start to clear the rooms always aiming for the highest difficulty it can safely defeat, farming keys whenever necessary. It will also farm health, mana and bombs, once it has purchased the appropriate items. (Health requires the leech sword, Mana requires the mana sword and the spellbook, Bombs require the leech sword and distance 80+.)

## Requirements
- 8 Script slots
- 2 Impulses
- 1 Condition
- 17 Actions
- `turbo exec v2`, found here: https://github.com/d0sboots/TPT2_scripts/blob/main/common/turbo_exec/README.md

## Strategy
The script tries to reach the highest difficulty possible so you are guaranteed to either take no damage from enemies or you can one-hit them. Secondly there is a variable called leon.adventure.maxDifficulty, which is visible in the top right. It will not go past this difficulty until it completed a whole round on this difficulty. Once it reaches a room that has already been cleared and is at the targeted difficulty, it will increase the maxDifficulty by 2 and therefore start a new round on the slightly higher difficulty.

The AI takes just under 30 seconds on average per room on difficulty 80, or a bit faster with the phase boots.

Unless you buy significant quantities of cheat armor, it will eventually stall around distance 92.
Getting past this will require manual farming for the Lantern first, and then
more swords/armor past distance 100. It *will* handle mimics past d100, but in
a minimal and not-entirely-safe way: It is not 100% rated for high-distance pushing yet.

## Usage
To Start the script press R. To stop the script press R again.
If you want to restart the script but already reached or surpassed the maxDifficultyInit you can press I to set leon.adventure.maxDifficulty to maxDifficultyInit and the use U and J to increase or decrease leon.adventure.maxDifficulty.
You also can press K to kill all enemies while the script is not running.

### Bundle Import:
```
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
```
