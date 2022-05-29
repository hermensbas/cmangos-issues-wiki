Back to [world database](https://github.com/cmangos/issues/wiki/mangosdb_struct) list of tables

## The `waypoint_path` table
***
This table holds information on waypoints for a given PathId. In essence, a waypoint just defines a path that the creature will follow by going from point to point. More specifically, once the creature arrives at a point, it can do different things like cast a spell, do an emote, etc. Usually this table is filled through the .wp command (and its various subcommands) in the world.

Please note that for a creature to use waypoints, its MovementType must be 2.

To add waypoints in-game:
- .npc setmovetype way creature guid or select npc
- .wp add guid or select npc

### Structure:

*Field* | *Type* | *Null* | *Key* | *Default* | *Extra*
------------ | ------------- | -----------  | -----------  | -----------  | -----------
[PathId](https://github.com/cmangos/issues/wiki/creature_movement#id)|int(10) unsigned|NO|PRI|0||
[Point](https://github.com/cmangos/issues/wiki/creature_movement#point)|mediumint(8)|NO|PRI|0||
[PositionX](https://github.com/cmangos/issues/wiki/creature_movement#position_x)|float|NO||0||
[PositionY](https://github.com/cmangos/issues/wiki/creature_movement#position_y)|float|NO||0||
[PositionZ](https://github.com/cmangos/issues/wiki/creature_movement#position_z)|float|NO||0||
[Orientation](https://github.com/cmangos/issues/wiki/creature_movement#orentation)|float|NO||0||
[WaitTime](https://github.com/cmangos/issues/wiki/creature_movement#waittime)|int(10)|NO||0||
[ScriptId](https://github.com/cmangos/issues/wiki/creature_movement#script_id)|mediumint(8)|NO||0||
[Comment](https://github.com/cmangos/issues/wiki/creature_movement#comment)|text|YES||||


### Description of the fields

#### PathId
PathId of a given waypoint sequence. Disconnected from any other Id system. Usable in spawn_group_formation, dbscripts, EAI and C++.

#### Point

Defines the waypoint number. A creature will go from waypoint to waypoint in the order controlled by this field.

As a convention, the first point of a path **must be greater than zero**. This is expected by core.
#### PositionX

The X position of the waypoint.

#### PositionY

The Y position of the waypoint.

#### PositionZ

The Z position of the waypoint.

#### Orientation

The orientation the creature will face once it reaches the waypoint. 
(North = 0.0; South = pi (3.14159))  

Setting this field to 100 means the creature will not change its orientation upon reaching the waypoint.

#### WaitTime

The time that the creature will wait before heading to the next waypoint, in milliseconds.

#### ScriptId

Reference to [DBScripts_on_creature_movement](https://github.com/cmangos/issues/wiki/DBScripts_on_creature_movement)

#### Comment

Short description of any event happening at a point - especially when dbscript is used

