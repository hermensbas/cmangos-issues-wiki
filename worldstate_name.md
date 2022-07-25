Back to [world database](mangosdb_struct) list of tables.

## The `worldstate_name` tables

holds data on worldstate variables used for [`conditions`.`CONDITION_WORLDSTATE` (42)](https://github.com/cmangos/issues/wiki/conditions) or [`dbscripts`.`SCRIPT_COMMAND_SET_WORLDSTATE` (53)](https://github.com/cmangos/issues/wiki/DBScripts)

### Structure

| Field                                                | Type                  | Null | Key | Default | Extra |
| ---------------------------------------------------- | --------------------- | ---- | --- | ------- | ----- |
| [Id](worldstate_name#Id)| int(11)|NO|PRIMARY KEY|NULL|Worldstate variable Id|
| [Name](worldstate_name#Name)|VARCHAR(200)|NO||NULL|Name and use of variable|

#### Id

Worldstate variable Id. Can be either official or custom defined in cMaNGOS. Officially discovered ones are in src/Game/World/WorldStateDefines.h

Official WorldStateID range from 1-10k (WoTLK ends at about 5k), Custom defined cMaNGOS WorldStateIDs start at 10k+.

[`instance_dungeon_encounters`.`Id`](instance_dungeon_encounters#Id) is used for instanced Encounter WorldStateIDs * 100 + 2-99. 0 and 1 are always reserved by Core for "Alive" & "Killed".

#### Name

Name and use of variable. Example: (78202, 'ZA - first 4 bosses dead - spawn Malacrass')

Mainly a bookkeeping table for naming and documenting uses. As we are introducing custom ones, we dont want to have undecipherable magic numbers.

