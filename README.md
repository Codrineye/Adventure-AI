# Adventure automation script

This is a fork of the remake by d0sboots. You can find the version I built uppon [here](https://github.com/d0sboots/TPTAdventure).

[version 3.3.8](CHANGELOG.md)

This script will automatically play the adventure game for you.<br>
It will start by farming 11 keys, so don't worry if it apears to be stuck betwenn the starting room and the first room.<br>
After it has the keys it will start to clear the rooms, always aiming for the highest difficulty it can safely defeat, farming keys whenever necessary. It will also farm health, mana and bombs, once it has purchased the appropriate items.<br>
(Health requires the leech sword, Mana requires the mana sword and the spellbook, Bombs require the leech sword and distance 80+.)

The AI buys the market items in the following order

1. impaler (To deal extra damage)
2. hammer (So it can spare bombs)
3. boots of phasing (So it can exit rooms quicker)
4. leech Sword (To farm health)
5. mana reaver (So killing enemies can drop mana)
6. thorns armor (Just because it's something to buy)
7. holy bomb (Just because)
8. eod armor (Just because)
9. spell book (So that killing enemies can drop mana)

## Requirements

- 2 Script slots
- 5 Impulses
- 1 Condition
- 44 Max Actions

## Strategy

The scripts primairy function is to reach the highest difficulty possible such that your armor negates the enemies attack or your attack is high enough that enemies die in one hit. The global variable `leon.adventure.maxDifficulty` determines the highest difficulty the script can reach.<br>
Once the script reaches the maximum difficulty, it will complete a full loop on said difficulty until it reaches a room it already cleared. At this point, the script will increment `leon.adventure.maxDifficulty` by 2 only if it determines that the next difficulty can be survived without taking damage.

Its secondairy function is to farm `keys`, `bombs`, `health` and `mana` for you whenever it enters a room.

The AI takes just under 30 seconds on average per room on difficulty 80, or a bit faster with the phase boots.

Unless you buy significant quantities of cheat armor, it will eventually stall around distance 92.<br>
Getting past this will require manual farming for the Lantern first, and then more swords/armor past distance 100. It _will_ handle mimics past d100, but in a minimal and not-entirely-safe way: It is not 100% rated for high-distance pushing yet.

## Usage

To Start the script press R. To stop the script press R again.<br>
If you want to restart the script but already reached or surpassed the maxDifficultyInit you can press I to set `leon.adventure maxDifficulty` to maxDifficultyInit and the keys `U` and `J` to increase or decrease `leon.adventure.maxDifficulty`.<br>
You can also press `k` to make the script stop trying to advance and instead enter the farming loop which it'll exit only after all your items are topped up.

### Bundle Import:

```
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
```
