Back to [world database](mangosdb_struct) list of tables.

## The \`creature\_movement(\_template)\` table

holds all the information on creature’s waypoints by
[\`creature\`.\`guid\`](https://github.com/cmangos/issues/wiki/Creature#guid)
or
[\`creature\_template\`.\`entry\`](https://github.com/cmangos/issues/wiki/Creature_template#entry).
In essence, a waypoint just defines a path that the creature will follow
by going from point to point. More specifically, once the creature
arrives at a point, it can do different things like cast a spell, do an
emote, etc. Usually this table is filled through the .wp command (and
its various subcommands) in the world.

Please note that for a creature to use waypoints, its
[MovementType](creature#MovementType) must be 2 for its
[\`creature\`.\`guid\`](https://github.com/cmangos/issues/wiki/Creature#guid).

### Structure

| Field                                                 | Type                  | Null | Key | Default | Extra                   |
| ----------------------------------------------------- | --------------------- | ---- | --- | ------- | ----------------------- |
| [Guid/Entry](creature_movement_template#Guid/Entry)   | int(10) unsigned      | NO   | PRI | 0       |                         |
| [PathId](creature_movement_template#PathId)           | int(11) unsigned      | NO   | PRI | 0       | CURRENTLY TEMPLATE ONLY |
| [Point](creature_movement_template#Point)             | int(10) unsigned      | NO   | PRI | 0       |                         |
| [PositionX](creature_movement_template#PositionX)  | float                 | NO   |     | 0       |                         |
| [PositionY](creature_movement_template#PositionY)  | float                 | NO   |     | 0       |                         |
| [PositionZ](creature_movement_template#PositionZ)  | float                 | NO   |     | 0       |                         |
| [Orientation](creature_movement_template#Orientation) | float                 | YES  |     | 0       |                         |
| [WaitTime](creature_movement_template#WaitTime)       | int(5) unsigned       | NO   |     | 0       |                         |
| [ScriptId](creature_movement_template#ScriptId)    | mediumint(8) unsigned | NO   |     | 0       |                         |

### Description of the fields

#### Guid/Entry

The [creature.guid](creature#guid) or
[creature\_template.entry](Creature_template#Entry) of the creature.

#### PathId

0 means that this is the default path for any creature of the specified
template. Any creature summoned, which is not assigned to another path,
will start moving on pathId 0.  
Setting this field to any other value allows you to use it for setting
different paths to different creatures of the same template in DBScripts
and in EventAI.

#### Point

Defines the waypoint number. A creature will go from waypoint to
waypoint in the order controlled by this field.

As a convention, the first point of a path **must be greater than
zero**. This is expected by core.

#### PositionX

The X position of the waypoint.

#### PositionY

The Y position of the waypoint.

#### PositionZ

The Z position of the waypoint.

#### Orientation

The orientation the creature will face once it reaches the waypoint.  
(North = 0.0; South = pi (3.14159))

Setting this field to 100 means the creature will not change its
orientation upon reaching the waypoint.

#### WaitTime

The time that the creature will wait before heading to the next
waypoint, in milliseconds.

#### ScriptId

Reference to
[DBScripts\_on\_creature\_movement](DBScripts_on_creature_movement).

