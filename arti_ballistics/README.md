# Introduction

Reworks ballistic damage to curb the strength of smallbore AP ammo and makes ammo strength strongly relative to armor. Overhauls ammo to convert bad ammo into cooler, fancier ammo.

# Ballistic Damage Overhaul
- Reworked ballistic system based on tiers of armor.
- Ammo properties (hit, ap) are almost completely script driven.
- Script-based support for complex damage interactions between bullets and NPCs/mutants (e.g. buckshot dealing more damage to limbs, HP rounds only dealing expansion damage on penetration)

## Disclaimer
 This is a huge system and I have not exhaustively tested every potential edge case. Please raise any issues you find.

## Details

Do note that mutant damage formula is more or less unchanged. There are a few edge cases but the majority of the work focuses on NPC interaction.

Armor classes are broken down roughly into the following:

NOTE: AP value is used in the ammo stat display. Due to the stats windows not supporting strings, the AP value had to be coerced to a number.

| Class | AP | Bone Armor | Armors      |
| ------|----| -----------| ----------- |
| None  |  0 | 0.0011     | Leather jackets, trenchcoats |
| I     |  1 | 0.05       | SSP suits | 
| IIA   |  2 | 0.1        | Stalker Suits | 
| II    |  3 | 0.15       | PS5 suits, heavier stalker suits |
| III   |  4 | 0.2        | Berill-5M |
| IV    |  5 | 0.25       | SKAT-9 |
| V     |  6 | 0.3        | Exosuits |
| VI+   |  7 | 0.35+      | Exoskeletons |

More granularity would have been nice but this based on the model capture, which breaks down armor broadly into these categories.

Each ammo type has a corresponding AP amount that also falls into one of these classes. Ammo performance is evaluated based on the difference in tier between the armor and the ammo, as follows:

| Difference | Effects    |
| -----------|------------|
| -3 to -7   | Deflection. Deal impact damage |
| -1 to 0    | Partial penetration, damage reduction up to 60% |
| 1 to 3     | Full penetration, full damage |
| 4 to 7     | Overkill penetration, reduced damage |

Impact damage is further subdivided based on bullet force (arbitrary values currently) vs. NPC tankiness, dealing up to 40% damage.

The aim of this system is to provide a semi-realistic and balanced system for ballistic damage vs. armor while providing for fun gameplay.


# Ammo Overhaul

- Existing good ammo is reduced slightly in overall effectiveness.
- Ammo types are BROADLY subdivided into FMJ/HP/AP variants (like in GBO)
- Bad ammo is converted into stronger 'very good' ammo roughly aligned with their parent type.
- The 'very good' ammo generally trades off faster damage wear with more damage, AP, etc. within reason. 
- Some 'very good' ammo is extremely exotic and has cool effects. Explore!
- Drop percentage of the new ammo types is controlled via auto-replacement at traders and NPC ammo drops.
- You can acquire most of this ammo through crafting. There is a mechanism to 'crush' some artifacts into fragments to use them in bullets.
- 7.62x54 PP rounds can be linked and unlinked to be used in the PKM or in sniper rifles.

General properties of new ammo:

| Ammo       | Effects
| -----------|------------|
| FMJ        | Plain jane ammo, good damage, dispersion and penetration. |
| HP         | Expansive ammo with a damage multiplier IF it penetrates fully. |
| AP         | Armor piercing rounds that deal reduced damage to NPCs with light armor. | 
| Buckshot   | Low AP. Ignores some armor on limb shots. | 
| Soft Point | Chance to stumble enemies on impact. Reduced HP performance. |
| Flat Point | Ignores armor on headshots. |
| Corrosive  | ???? |
| Incendiary | ???? |
| Varmageddon| ???? |
| Saboted AP | ???? |
| CHAOS      | ???? |
| Explosive  | ???? |
| Lightning  | ???? |

## Recipes

To balance the power of the new rounds, the recipes have been gated behind new items.

These recipes have a small chance to drop from stashes, or can be purchased. Be on the lookout!