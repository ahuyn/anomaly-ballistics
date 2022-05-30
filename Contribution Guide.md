# Integrating your own ammo types

This framework provides robust support for making ammo types do whatever you want in terms of damage, armor piercing, etc, as well as other effects.

## Ammo Importer

The format of a custom ammo config looks like the following:
```
[ammo_7.62x25_ps_bad] ; acid
handler     = arti_handlers.acid_damage
name		= ammo_new_7.62x25_cor
impair      = 1.3
cost        = 2700

k_hit		= 1
k_ap		= 0.049
special     = acid
dg_ammo     = ammo_7.62x25_ps
dg_chance   = 0.7
```

All properties except `handler` are optional.
Of these properties, the first four properties are leveraged by the base framework as follows:

- `handler` : This specifies the function used to compute damage. More on specifics later. If not specified, defaults to `ballistic_handlers.default` which does nothing.
- `name` : Custom string used to define the name of the ammo. Short name and description will be autofilled using `name_s` and `name_descr` respectively. If not specified, defaults to properties in `weapon_ammo.ltx`.

**NOTE** : Game will not respect the short name if it is specified this way in ammo preview. You will need to manually specify short name in weapon_ammo in order to have the ammo show up in weapon tooltip.
- `impair` : Custom impair value that will be applied when the weapon is shot. How this works is the base degradation for the ammo from engine level is stored, and the difference in degradation multiplied by `condition_shot_dec` (respecting upgrades) is applied. If not supplied or the MCM option is toggled, this calculation is ignored.
- `cost` : Custom base cost for buy/sell of this ammo type. If not supplied or the MCM option is toggled, falls back to `cost` parameter in `weapon_ammo.ltx`.

To leverage these custom properties use `ballistics_utils.ini_ammo` where the file handler has been provided for you.

## Damage Calculation

The format of a handler function looks as follows:
```
function default(npc, s_hit, ctx)
    return s_hit
end
```
Arguments are as follows:
| Arg   | Type | Description |
| ----- |------| ----------- |
| npc   | userdata | Userdata object of npc that takes the hit by this ammo type. |
| s_hit | hit | Hit object. Modify `s_hit.power` and return `s_hit` in order for custom calculations to take effect. Behaves differently based on mutant vs. NPC hit - more later |
| ctx   | table | Table containing `hit_data`, `bone_id`, `is_npc` properties. |
| ctx.hit_data | table | Contains data used to perform the bullet hit. Contains 3 keys: `wpn`: userdata of weapon used to perform the hit. `sec`:(Parent) Section of the weapon. `ammo`: section of ammo that performed the hit. |
| ctx.bone_id   | int | ID of the bone where the bullet landed. Can use the utility functions `npc_bone_mult` and `npc_bone_protection` to pull bone multiplier and   |
| ctx.is_npc    | boolean | True if the NPC hit by a bullet is a human, false if mutant. **NOTE** : Behavior of how the hit is returned to the engine differs based on type. For humans, the bone multiplier needs to be accounted for when processing the hit, allowing for things such as bone-specific custom damage multipliers. For mutants, owing the the very specific nature of each mutant's bone map, the hit will be sent to engine and bone multipler does not require accounting for. |

## Utility Functions

Following utility functions are also exposed in `ballistics_utils.script` to help with building custom damage functions. More docs available at script level.

| Function | Description |
| ---------| ----------- |
| play_particle| Plays a particle by name at NPC's bone position, or position if bone id is nil. |
| npc_bone_mult | Fetches standard bone damage multiplier for NPC bone. |
| npc_bone_protection| Fetches bone armor data of specified bone for the given NPC. Respects custom bone armor values. |
| npc_bone_data | Collects and combines data from `npc_bone_mult` and `npc_bone_protection`. |
| modify_bone | Sets a specific bone to have a custom bone armor. |
| mutant_prot_values | Returns protection data in the same format as npc_bone_data, adjusted for mutants. As mutants have global skin armor, this function exists primarily for compatibility. |
| modify_distance | Provides a distance and air-res based damage reduction based on GBO formula. |
| modify_velocity | Provides a flatness-based damage multiplier from the currently equipped weapon. Defaults to 20% of the flatness bonus. |