# Arcade Adventure full auto script

`v3.3.1`

This script will fully automatically play the adventure game for you.
It will start by farming 11 keys, so don't wonder if it apears to be stuck betwenn the starting room and the first room.
After it has the keys it will start to clear the rooms always aiming for the highest difficulty it can safely defeat, farming keys whenever necessary. It will also farm health, mana and bombs, once it has purchased the appropriate items. (Health requires the leech sword, Mana requires the mana sword and the spellbook, Bombs require the leech sword and distance 80+.)

## Requirements
- 8 Script slots
- 2 Impulses
- 1 Condition
- 17 Actions

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
