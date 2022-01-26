Tables:

[spawn_group](https://github.com/cmangos/issues/wiki/spawn_group#spawn_group)  
[spawn_group_spawn](https://github.com/cmangos/issues/wiki/spawn_group#spawn_group_spawn)  
[spawn_group_entry](https://github.com/cmangos/issues/wiki/spawn_group#spawn_group_entry)  
[spawn_group_formation](https://github.com/cmangos/issues/wiki/spawn_group#spawn_group_formation)  
[spawn_group_linked_group](https://github.com/cmangos/issues/wiki/spawn_group#spawn_group_linked_group)   
[waypoint_path](https://github.com/cmangos/issues/wiki/spawn_group#waypoint_path) - paths for spawn_group_formation.PathId  

Logically a replacement of linking and pooling. Groups spawns into a logical group, which can behave differently. Benefits are much easier handling in core and during creation of new entries. Also introduces conditional spawning through worldstate alteration.

---
## spawn_group

Id - Spawn Group ID

```
1-9999 for anything in vanilla (Eastern Kingdoms 0 & Kalimdor 1)
10000-19999 TBC (Outland 530)
20000-29999 WOTLK (Northrend 571)
30000+ Instance Files
```

Name - Mandatory name restricted to 200 characters. Name structure example: EPL - Musty Tome - Annals of Darrowshire  
Type - Type of group - 0 creature, 1 gameobject (enum SpawnGroupType)

```
    SPAWN_GROUP_CREATURE = 0,
    SPAWN_GROUP_GAMEOBJECT = 1,
```

MaxCount - Maximum count of spawns that can be spawned at a time for whole group. If set to 0, automatically calculated from either spawns or entries, whichever lower.  

WorldState - If a given worldstate is set to 1, the group will automatically spawn. When set to 0, it will no longer respawn. Usable for many dungeon packs or scripts. Defining own worldstates is vague to existence of official worldstates. Must be done in core C++ currently through WorldStateVariableManager. Ask your friendly neighbourhood c++ coder. Consult [worldstate](https://github.com/cmangos/issues/wiki/Worldstates) for more information.  

Flags - enum CreatureGroupFlags (GO groups currently have no flags)  

```
    CREATURE_GROUP_AGGRO_TOGETHER   = 0x01,
    CREATURE_GROUP_RESPAWN_TOGETHER = 0x02,
    CREATURE_GROUP_EVADE_TOGETHER   = 0x04,
```

---
## spawn_group_spawn

Id - Spawn Group ID  
Guid - Guid in Creature or GameObject table, used as DbGuid in core, due to SpawnGroups automatically using Dynamic Guid system (when spawned, has unique guid)  

---
## spawn_group_entry

not mandatory, only for randomization of spawns

#### Id - Spawn Group ID  
#### Entry - Entry for picking on spawn from creature_template or gameobject_template  
#### MinCount - Minimum count of entries before random chances or other entries become eligible  
#### MaxCount - Maximum count of given entry in the world for whole spawn group  
#### Chance - Chance of entry to be picked over other chanced entries. First chanced entries are tried and then all chanced with 0. MinCount overrides this  

---
## spawn_group_formation

#### SpawnGroupID

#### FormationType

enum SpawnGroupFormationType

|Value|Name|Example|
|---|---|---|
|0|SPAWN_GROUP_FORMATION_TYPE_RANDOM              | ![](https://i.imgur.com/6ta9ZNX.png) |
|1|SPAWN_GROUP_FORMATION_TYPE_SINGLE_FILE         | ![](https://i.imgur.com/9p8LiFU.png) |
|2|SPAWN_GROUP_FORMATION_TYPE_SIDE_BY_SIDE        | ![](https://i.imgur.com/dmO3eT6.png) |
|3|SPAWN_GROUP_FORMATION_TYPE_LIKE_GEESE          | ![](https://i.imgur.com/LjPVReZ.png) |
|4|SPAWN_GROUP_FORMATION_TYPE_FANNED_OUT_BEHIND   | ![](https://i.imgur.com/i5OAJGc.png) |
|5|SPAWN_GROUP_FORMATION_TYPE_FANNED_OUT_IN_FRONT | ![](https://i.imgur.com/ihGrdDu.png) |
|6|SPAWN_GROUP_FORMATION_TYPE_CIRCLE_THE_LEADER   | ![](https://i.imgur.com/lUqwMHw.png) |

#### FormationSpread

Distance between formation members, Value between -15 and 15 - raw distance ingame
Only positive make sense for all formation except random(0)
For random position spread mean the distance from leader and the pack of members.
By using negative spread in that case we can push the pack above leader.

Humanoid Npcs 2 minimum, then target circles tangate each other. 5 good default value for SPAWN_GROUP_FORMATION_TYPE_SINGLE_FILE to not make it look too stacked

#### FormationOptions

enum SpawGroupFormationOptions

|BitMask|Name|
|---|---|
|0x00|SPAWN_GROUP_FORMATION_OPTION_NONE           |
|0x01|SPAWN_GROUP_FORMATION_OPTION_FOLLOWERS_WILL_NOT_PATHFIND_TO_LOCATION |
|0x02|SPAWN_GROUP_FORMATION_OPTION_KEEP_COMPACT   |

#### MovementID

Table waypoint_path PathId

#### MovementType

MovementType of the Formation, Overwrites creature.MovementType. 0 (Idle) 2 (waypoint movement) 3 (path movement) or 4 (linear movement) are applicable

#### Comment

Same as [`spawn_group`.`Name`](https://github.com/cmangos/issues/wiki/spawn_group#Name)