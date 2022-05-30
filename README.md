Base framework for playing with ballistic damage in Anomaly.

This framework maps ammo types to custom damage functions, allowing a user to pass cutsom calculations for damage on a per-bullet basis. Additional utilities are provided to overwrite many properties of weapon_ammo, reducing the dependency on the file as much as possible.

This addon does nothing by itself. However, two addons are provided to give an idea of how to use this framework.

Properties that may be overridden by default include:
inv_name
inv_name_short (looks for inv_name_s)
description (looks for inv_name_descr)
cost
impair

Properties passed on hit such as k_hit and k_ap can be overridden at your discretion.

Other properties such as air_resistance, bullet_speed and k_disp must be changed manually, but are of relatively little importance.

Some notes on integration:
- NPC hits do not account for implicit bone armor. Bone multiplier is applied manually and then damage is done via health removal.
- Monster hits do not take into account bone armor and relies on engine to apply damage. Only AP calcs are done.

Requires 1.5.2 RC4 or later.