Tables:

[spawn_group](https://github.com/cmangos/issues/wiki/spawn_group#spawn_group)  
[spawn_group_spawn](https://github.com/cmangos/issues/wiki/spawn_group#spawn_group_spawn)  
[spawn_group_entry](https://github.com/cmangos/issues/wiki/spawn_group#spawn_group_entry)  
[spawn_group_formation](https://github.com/cmangos/issues/wiki/spawn_group#spawn_group_formation)  
[spawn_group_linked_group](https://github.com/cmangos/issues/wiki/spawn_group#spawn_group_linked_group)  
[spawn_group_spawn](https://github.com/cmangos/issues/wiki/spawn_group#spawn_group_spawn)  
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
WorldState - If a given worldstate is set to 1, the group will automatically spawn. When set to 0, it will no longer respawn. Usable for many dungeon packs or scripts. Defining own worldstates is vague to existence of official worldstates. Must be done in core C++ currently through WorldStateVariableManager. Ask your friendly neighbourhood c++ coder.  
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

|Value|Name|
|---|---|
|0|SPAWN_GROUP_FORMATION_TYPE_RANDOM              |
|1|SPAWN_GROUP_FORMATION_TYPE_SINGLE_FILE         |
|2|SPAWN_GROUP_FORMATION_TYPE_SIDE_BY_SIDE        |
|3|SPAWN_GROUP_FORMATION_TYPE_LIKE_GEESE          |
|4|SPAWN_GROUP_FORMATION_TYPE_FANNED_OUT_BEHIND   |
|5|SPAWN_GROUP_FORMATION_TYPE_FANNED_OUT_IN_FRONT |
|6|SPAWN_GROUP_FORMATION_TYPE_CIRCLE_THE_LEADER   |

#### FormationSpread

Distance between formation members, Value between 0.5 and 15

#### FormationOptions

enum SpawGroupFormationOptions

|BitMask|Name|
|---|---|
|0x00|SPAWN_GROUP_FORMATION_OPTION_NONE           |
|0x01|SPAWN_GROUP_FORMATION_OPTION_KEEP_CONPACT   |

#### MovementID

Id from waypoint_path path

#### MovementType

MovementType of the Formation, Overwrites creature.MovementType

#### Comment

Same as [`spawn_group`.`Name`](https://github.com/cmangos/issues/wiki/spawn_group#Name)