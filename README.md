# Introduction
Base framework for playing with ballistic damage in Anomaly.

This framework maps ammo types to custom damage functions, allowing a user to pass cutsom calculations for damage on a per-bullet, per-npc or per-mutant basis. Additional utilities are provided to overwrite many properties of weapon_ammo, reducing the dependency on the file as much as possible.

## Requirements
- Requires 1.5.2 RC4 or later.

## Detail

This addon does nothing by itself. However, two addons are provided to give an idea of how to use this framework.

Properties that may be overridden by default include:
- `inv_name`
- `inv_name_short` (looks for `inv_name_s`)
- `description` (looks for `inv_name_descr`)
- `cost`
- `impair`

Properties passed on hit such as k_hit and k_ap can be overridden at your discretion. Do note that weapon_ammo provided k_ap also provides a level of cover and body penetration that this script does not mimic.

Other properties such as air_resistance, bullet_speed and k_disp must be changed manually, but are of relatively little importance.

Consult the Contribution Guide for an idea of how to add your own ammo types.

## Integration Notes:
- NPC hits do not account for implicit bone armor. Bone multiplier is applied manually and then damage is done via health removal.
- Monster hits do not take into account bone armor and relies on engine to apply damage. Only AP calcs are done.

## Credit
- HarukaSai - Provided code, balancing
- themrdemonized - Borrowed code from PBA
- Lucy - Providing functions that made this addon possible
- Grok - Borrowed formulas from GBO
- Maid - Icons