# Adventure automation script

This is a fork of the remake by d0sboots. You can find the version I built uppon [here](https://github.com/d0sboots/TPTAdventure).

[version 3.4.1](CHANGELOG.md)

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

- 3 Script slots
- 5 Impulses
- 1 Condition
- 33 Max Actions

## Strategy

The scripts primairy function is to reach the highest difficulty possible such that your armor negates the enemies attack or your attack is high enough that enemies die in one hit. The global variable `leon.adventure.maxDifficulty` determines the highest difficulty the script can reach.<br>
Once the script reaches the maximum difficulty, it will complete a full loop on said difficulty until it reaches a room it already cleared. At this point, `leon.adventure.maxDifficulty` will be incremented by 2 only if it determines that the next difficulty can be survived without taking damage, if it can't, it decrements the maximum difficulty by 2.

Its secondairy function is to farm `keys`, `bombs`, `health` and `mana` for you whenever it enters a room.

The AI takes just under 30 seconds on average per room on difficulty 80, or a bit faster with the phase boots.

It will eventually stall around distance 93 if you don't have 37+ armor.<br>
Getting past this will require manual farming for the Lantern first, and then more swords/armor past distance 100. It _will_ handle mimics past d100, but in a minimal and not-entirely-safe way: It is not 100% rated for high-distances.

## Usage

To toggle the script on and off, press `r`.<br>
If you want to quickly set `leon.adventure.maxDifficulty` to `81`, you can press `i` to assign it to the value in maxDifficultyInit, this value is set to 81 by default. You can increment and decrement `leon.adventure.maxDifficulty` with the keys `u` and `j`.<br>
If you want to get mana armor and are in a room that you can survive in, you can press `k`. This will put the AI in a "zombie" mode where it no longer tries to reach the maximum difficulty it can, and instead it farms everything for you. It will fully shut down once your health, mana and bombs are at 99, you have more than 10 keys and your mana armor is equal to or higher than your armor amount. It will not try to buy items from the shop while in this state.

### Bundle Import:

```
7R3rb+NI/V/xBXRCd91gp027qfZ13a7gpJ5Yslv1EDlVjj1pTB1Pzo8+bvfECsE3EF+BT/AZCYEE6JCQkJp/DPmRxLF/Y894xo+01krZu6w9md9vfu/XvOs4mm3MXadz+PN3HVVzDWz5/90ZebKsyCbWVLOrY29soq6D3NFYw5bjqpbr/7u8FzylzNSbY2MyMTTPdG8/t4zkY7vBp0z6fPH2RWcn/EHlwsRj1ew6rm1YF8RfPHjiGN+gp/IzVb/6vqvaF8g9n2PnBbTGBeMa0VbkSbTMGGMT3MjEf9H2LMuwLl6Er2h4Nldtw8FW8Fq4ndiX4ZaCZ1GI964xm3umg6Atyr2PnoLf9y/RbfcSfuXjj4lb2QQJwssmSKQt8UL1NAMqm4ESXH+3c9WdhthHLrIt1b6N74cRYkryif0wBIichIHMP9978kOfCp+ZCFtdVb9CluvZqLvBUJvAhWvRkdv62eRWAKiotgKBqzxhY/cN1ocp5P37UonMGFkRHmbqDc/m0zKSJG0AGUk81ojyNGy5qmE5IBzjgFneh4IAQorAQydstLTj8cLVVdtwpzPkGlpVhPxpEVpY/P25SHKqAexHBcH2xdzkAlnINrTuBXZxSJlLSjGi5YRrxSzaIWjFUKBUuxU7W0Hz6OLeyALOJfHMR+lHlrYNCmUW0bTxP/d9nETcv2thN/UiQdQtXyysyJcSNUMBj9GN4Z7rxspa2F2SIbpBmuci59bSQDmsfbbkDOlqt7vXVQ4n2DTxteT//HK1fLPX0jfEI5Fr01/HRQXhESZuXHzAsBJVHoWncYW0Xjf8rbFqa6qOYtLBxnj2EmNbd9geJojPeoC7ZQGO4mERumHxAS8+rNgtLiSNSYqZg2cIK8GGPPQlin0ZyV5lPwXnGM/GBBCTdlxPyxUyGzKNZHvmW0hxdgJ/4FlSzlLpqLcE8zLa7uMUcqaq87mLZun9mQhp0zfX2NaXMmKQetlz0Js5Ms20eJuplvqZPcM2LUFMSiEGNbXl1cZIBBGIzNRrc1O9RTb5xQIIHmN8GWAPps2l1oTA6oNgUdJRyHx9PlU5sRDSnXMHz5A7Xbme1GfF92V5XFfMsftZtk9HTxP+54GpWr49WUTslGgy+3QkSLJlxGsIgMm7Rk8vypnhxuVxtGUNGSZJUwsiok+SRLT49w9Go7vfL361+NfiD8+pAwAxBEDOKCNdGbO5aiKbBRlrvOskvLuuqsEeSBoNd3+6++Pyz+Ifz7l/YUmTwOYnEYA29iw967grpILh3XfB2ujuN4u//pRECMVdcsJq1KgoA+Z3wcp7d3/70eIv39z9k0D7mRHcEr5s7cYq7EbmuAR4LiS58GOkmu60pOOpCF5qJDAYfJUC7+9iiNQrVJlVHKGTDkmX6JawzJO0VZwfX8o3zIsQ6zPQPgd4NBGryYgurYJFI9fxxlGED4zRf3kqSdKJJElDSZKOJUkKQYvWNiwd3fwk6axFr0oD5bEkDyRJeTyQBnL06r6GLU2NJI/eSwdZ0i5ZiKLX2IFeus19iRJ74HMKEctUXtCBc2nM50jP4HCazMbe6cnwGDjazDhg5ZoUoneUOhcNe5b7ynIN10AwtP1XpuHCwWV6XoChDzO13IBSRHxT/i+rpGjNjWrUbxZDbAFFk9WdjGJWPI/++ZQgYXMiZc/ATSSA1SnhjILbu3rPGG2RRxd3aO/+I9KfG40JWYB0bOF3i9+u/vw3M7iwtVxAlqM1c4FvRxJ2ERLzkmonJsZ2Q6h20yf/dSVhiE+y0eQxxKQaHshLv0SFuO8IqwWCsUjYM5Pl6XPamQzJlCRPmkyUtRQ0S6/scEjKHORKmeA5hZwRATzLa9Vw1+n+CAj/y4mtzhD5vRm+QqPJEkbfwxnBBo/hvLLQLKxFmMQIfPUKvUsUl3AyukJad2ITMr8MtTsgJqmFRIO2suWnkRa57Jhr0Fa2/DT4CfLuf43ay5afRwBDY9ijOXvhpY34J0dRJJwE7rn42upeG5aOr7uGg+cIzoZHMZRsx19AA0DJtdmXML4gb+fAsNxVqVkxJ23JqTX6eHzkAdPMVkklfsmcXUTwwJCREqtbjA0RNtQ9QoYAjQn5etAq0HMkGUYpvRqU/OF2+XnjCUwZk7YS5AGkZtpKkLYSZEsrQciRRUg7VNb6BTVAgXptP/85ci9V2yzUNgvxpovu/rxuFhLYNF5PC63H0K1ecUNDlKAstTMgQxAXijG8nCIHtiHFVFMQxDGF/R0QNtH8Jkhq7vgaP321XTQspnfbRUPceNOT720XTdtFs9TKAuOqDe+i4Zg+w/Dq2l7LL0BfKcoNrotPKarWCkpNlRISZq/ajogV87PgtTUJRq1J0JoErUnQmgQPxiSIcksnx8NTUtbpeBgyQH6vV/xpPl3OGUFjVCKLD+fZyYzMTRaMhDGnXYi7VBqAcnHQlInzVFyoMMqP60e5MGBKpfJU2qQwyk/gr5Nyi7uxM6cXNhKWzCKxuLkvqlWV0h8bz1T7ErnnuuqqGbj4paLISi+yaZQDubc7VWczZCt9eU8eY+w6r6eqY1gXSl/u99c5T2VfPpDXWUBlV368706xbTmBCansyoPBFJu3R3g2VvqK0kNYD/5F7iu9g1iyL8CW0zMS7g4lnjeghPAIYR16jrJEhEjxJYJASzI0oAJzt3iGXNZYugltMsOUL+dogCaS5HP5SfgwRzugfG6c/1xGLjedoRl7t18EUDYOTQJHpq/mFOQMSNiT5GDMgSwPJOWxPJDkwTIhQzEjoR+MVwjmKwQDFoIJC1KVWmMv97lI3R4yzxUdpOaK+s1NM2S5Zc5BXWKllDGouVMKocoQkiwUUnpe86wRUVcCbDcuvtrpaNjSjc2bIhhVnb9KVOgTrBFMZe/sdJZXAARjwKO/fxH9fem/ZPkNhYcdwwo6Dueqdqle+F8k6bmz0xl7+gVyO4ePlJ2O56Cj6H9d20Pf7qTuusgdceJqquX61l5GunnZAsoQNJvErcismF3qqItJwlXwwEt0UIhopwj6IThLHYr/ul+47bOqHZ6kDw54kI6L5i/99Rj5n9K12A+1a3hmtFkJ6ubhGBlmEgtFEfLYF/bnjo/sadK04bxEpRI1zXgu/a895EXefmwuE2D7eLHJS9xlaeGnQfD3w3op2pFQtM49rf9TP8zFJlrxwAxyzZvDxKSrYHNEDte81YSuZGOHF3q7ejFfIaLRcv1ctt7bUoChjTsIBIYxX2/oN7UdISAA6Xdvmxi7r7ETGmghjRaJ4GYCHhecII9PGDAW4BpkS8oiQnKENwZEOqqLfHPi9u3tHKU4n9gUFHE+y27Xdg2odxqogzhQcW90Uq04gIMSlCyVFgDML5GlDYlyuYVAjtVcTDSVtUNuwUa42I9g57L+pGi9lW+QC8rKACa6aFgomn1ST8ThL1eXNplgG0RVTHGSomU/QC8cSbUQuTZX47OQFEPp4gHQ2H6mmtEbQF87t/XTpBEI2YP1xURYoEKCREdbYZPKE2aKFKxbCT979BNg4HIPfqIqVChLIgAyR9Zvcz5ou5tUFyqSB0QVPJYUgDo9HLWqoARVQJqGU50uMCwuNhfOB0JFaoW6QKwSa3XBQ9YFRW88rkYXHLe6gAr9gmaBtW5BdW5BE3VYI1VBthgU5F01xiSuX+c2M+bfG7aqgM6s3zpd0LoFTVRiD1cXNMYkbnUBQTadHPL0onCNZwCzOEVSmTk1GgKyVOzpMehQoJYMalzXX8wJgKRQ3vwiAx00XMVHMWHKXVUqtpYhdRrhT/kMzZzrTAAOITbfCMmr/qqxODGGGx7YmlGcmANMo4sTE4RWBqFS9KOlnihUkR0Icq8ZRlYbe22O/SOytbH2ep36zzOk6XJ8+nC0Lo2eSQnhLyVZkiXlUUgoeR2kY+lUOpaG0gnFqRBOgsvCrEXPpT4pkKo8UnzEtkil+ryv0rvl9i0nzJbbt4DbQaed0AaivMkMOa9iBql7cqpznGN+kUcwcjgdrAgVh6KAqqO1iRYJBC7IppLs0ubG0IaQs2PrhqqsJRkSpeXhuWxyy4RTCCsLPqaHgn7uiIr4rW+1QE13qAihxJgdvbqLtDLqFB6FJRR+sMX9gAB1pmnTHK1VBXGybqxobL/18LbcGaFEauvhMSCVLkN+72O9bf6igfUbhEKJVFwgXBAYRcpJy8kfz8wEshV3gJNTk89IMLtSJno2ZyMyxiO82A0sNJbH+sda7VzdeM57omS3BTdtrp5bztePg9p1XbFrsJo/BkO0JUkpFRhzCGFpn053fAq5soxPA3NEbGOL0orH2HhPcMX1eE+PMEuIfjrreDmXHzyOvaOzszPSr4i8fSy299wxZg3v3cggUr6Wg0pnxd1zJIefhD6/IoheT0be5r6j0miX+m6amvp8FJgU9o9OT8+O2W4JaiUgPxWRhlq0IlC0CFx8aGVgVdRboRBkvFQsW3rvHx0fn52etlKQlw4E9fC2UjBXitWI6fshBcvuQK9kuJ5gKXhycjYcEv5tODw7OeELD9C7/XmBhFhlDf1VIR5QDFJ0SxvUyHBLG210gm2+KjARt1lZD5hrvTKzHjVSKm0sNl+ibGlWpcV91mcDpBYl5u7RzZmpmdJ2RI0msi7caQE6BTf85Ckf/SqIQDVcIyIaZQO3Ur+V+g8R96C8IFTn7A0xaaZ9NJeJ3sQM2DS88xqUOBT37QbPUdzfm1EfJPReU+628gr6UvhHMOTeZ+llD40JmUKhvQs2i3q5Y11iMcxW2sZlS2QtVf/NrZt3sK4vV43dXEx1wWpPlnNvWN00BNncUPh6QA0d4dk4bWRSstNy7X5q7WvVKHhps/DyhyKaCRYDtC581lWMtEuOLXTjfoGvomvVtsaC49H522BDUGK+BvvtnmOeViW7vuhZ34Is0h9juGJ10//KcePWvM6SIQivRFwL2Uh+++BPbF8JEYXzbCVWaDdGsmA86nF+DF8mO91ApJwdNZlbNjwFGMzcsYZrOqbNcdwv+s7EaSWXZYSTMAteLM2wXUFDfDe2m38ntAeENYulQDYbK3K0XSD8z6RGsy/9ei7hSQZxt8XeUBHJJCDES/I6qZ2zzXhGcf/sq2//Dw==
```
