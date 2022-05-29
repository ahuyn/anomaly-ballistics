# Introduction

Overhauls ammo to convert bad ammo into cooler, fancier ammo. Reworks ballistic damage to curb the strength of smallbore AP ammo and makes ammo strength strongly relative to armor.

# Ballistic Damage Overhaul
- Reworked ballistic system based on tiers of armor.
- Ammo properties (hit, ap) are almost completely script driven.
- Script-based support for complex damage interactions between bullets and NPCs/mutants (e.g. buckshot dealing more damage to limbs, HP rounds only dealing expansion damage on penetration)

## Details
Armor classes are broken down roughly into the following:
| Class | Bone Armor | Armors      |
| ------|------------| ----------- |
| None  | 0          | Leather jackets, trenchcoats |
| I     | 0.05       | SSP suits |
| IIA   | 0.1        | Stalker Suits |
| II    | 0.15       | PS5 suits, heavier stalker suits |
| III   | 0.2        | Berill-5M |
| IV    | 0.25       | SKAT-9 |
| V     | 0.3        | Exosuits |
| VI+   | 0.35+      | Exoskeletons |

More granularity would have been nice but this based on the model capture, which breaks down armor broadly into these categories.

Each ammo type has a corresponding AP amount that also falls into one of these classes. Ammo performance is evaluated based on the difference in tier between the armor and the ammo, as follows:

| Difference | Effects
| -----------|------------|
| -3-7       | Deflection. Deal fractional impact damage |
| -2-0       | Partial penetration, damage reduction up to 90% |
|  1-3       | Full penetration, full damage |
|  4-7       | Overkill penetration, reduced damage |

The aim of this system is to provide a semi-realistic and balanced system for ballistic damage vs. armor while providing for fun gameplay.

# Ammo Overhaul

- Existing good ammo is reduced slightly in overall effectiveness.
- Ammo types are BROADLY subdivided into FMJ/HP/AP variants (like in GBO)
- Bad ammo is converted into stronger 'very good' ammo roughly aligned with their parent type.
- The 'very good' ammo generally trades off faster damage wear with more damage, AP, etc. within reason. 
- Some 'very good' ammo is extremely exotic. Explore!

General properties of new ammo:

| Ammo       | Effects
| -----------|------------|
| FMJ        | Plain jane ammo, good damage, dispersion and penetration. |
| HP         | Expansive ammo with a high multiplier IF it penetrates fully. |
| AP         | Armor piercing rounds that deal reduced damage to NPCs with light armor. | 
| Soft Point | Chance to stumble enemies on impact. Reduced HP performance. |
| Flat Point | Ignores armor on headshots. |
| Corrosive  | ???? |
| Incendiary | ???? |
| Varmageddon HP | ???? |
| Saboted AP | ???? |
| CHAOS      | ???? |
| Explosive  | ???? |
| Ionic      D| ???? |

Autoinjector scripts ensure that the distribution of very good ammo is appropriately rare.