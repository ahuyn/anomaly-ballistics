Base framework for playing with ballistic damage in Anomaly.

This framework maps ammo types to custom damage functions, allowing a user to pass cutsom calculations for damage on a per-bullet basis. Additional utilities are provided to overwrite many properties of weapon_ammo, reducing the dependency on the file as much as possible.

Properties that may be overridden include:
inv_name
inv_name_short
description
cost
impair
k_hit
k_ap

Other properties such as air_resistance, bullet_speed and k_disp must be changed manually, but are of relatively little importance.

Requires 1.5.2 RC4 or later.