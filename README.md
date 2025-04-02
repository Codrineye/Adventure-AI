# Adventure automation script

This is a fork of the remake by d0sboots. You can find the version I built uppon [here](https://github.com/d0sboots/TPTAdventure).

[version 3.3.9](CHANGELOG.md)

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
- 42 Max Actions

## Strategy

The scripts primairy function is to reach the highest difficulty possible such that your armor negates the enemies attack or your attack is high enough that enemies die in one hit. The global variable `leon.adventure.maxDifficulty` determines the highest difficulty the script can reach.<br>
Once the script reaches the maximum difficulty, it will complete a full loop on said difficulty until it reaches a room it already cleared. At this point, the script will increment `leon.adventure.maxDifficulty` by 2 only if it determines that the next difficulty can be survived without taking damage.

Its secondairy function is to farm `keys`, `bombs`, `health` and `mana` for you whenever it enters a room.

The AI takes just under 30 seconds on average per room on difficulty 80, or a bit faster with the phase boots.

It will eventually stall around distance 93 if you don't have 37+ armor.<br>
Getting past this will require manual farming for the Lantern first, and then more swords/armor past distance 100. It _will_ handle mimics past d100, but in a minimal and not-entirely-safe way: It is not 100% rated for high-distance pushing yet.

## Usage

To Start the script press R. To stop the script press R again.<br>
If you want to restart the script but already reached or surpassed the maxDifficultyInit you can press I to set `leon.adventure maxDifficulty` to maxDifficultyInit and the keys `U` and `J` to increase or decrease `leon.adventure.maxDifficulty`.<br>
You can also press `k` to make the script stop trying to advance and instead enter the farming loop which it'll exit only after all your items are topped up.

### Bundle Import:

```
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
```
