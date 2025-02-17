Tables:

[spawn_group](https://github.com/cmangos/issues/wiki/spawn_group#spawn_group)  
[spawn_group_spawn](https://github.com/cmangos/issues/wiki/spawn_group#spawn_group_spawn)  
[spawn_group_entry](https://github.com/cmangos/issues/wiki/spawn_group#spawn_group_entry)  
[spawn_group_formation](https://github.com/cmangos/issues/wiki/spawn_group#spawn_group_formation)  
[spawn_group_linked_group](https://github.com/cmangos/issues/wiki/spawn_group#spawn_group_linked_group)

[waypoint_path](https://github.com/cmangos/issues/wiki/spawn_group#waypoint_path)
[waypoint_path_name](https://github.com/cmangos/issues/wiki/spawn_group#waypoint_path_name)

Logically a replacement of linking and pooling. Groups spawns into a logical group, which can behave differently. Benefits are much easier handling in core and during creation of new entries. Also introduces conditional spawning through worldstate alteration.

---
## spawn_group

Id - Spawn Group ID

```
1-18999 for Classic (Eastern Kingdoms 0 & Kalimdor 1)
19000-19999 for tbc-db added classic content, 19999-19000 for wotlk-db added classic content
20000-29999 TBC (Outland 530)
30000-39999 WOTLK (Northrend 571)
      for WoTlk Pls Use:
      30000 - zul'drak
      30500 - borean
      31000 - dragonblight
      31500 - howling
      32000 - grizzly
      32500 - Sholazar
      33000 - Storm Peaks
      33500 - crystalong
      33700 - Dalaran
      34000 - IC
      34950 - Hrothgar's Landing
      35000 - DK starting Zone
3000000+ Instance Files
```

Name - Mandatory name restricted to 200 characters. Name structure example: EPL - Musty Tome - Annals of Darrowshire  
Type - Type of group - 0 creature, 1 gameobject (enum SpawnGroupType)

```
    SPAWN_GROUP_CREATURE = 0,
    SPAWN_GROUP_GAMEOBJECT = 1,
```

MaxCount - Maximum count of spawns that can be spawned at a time for whole group. If set to 0, automatically calculated from either spawns or entries, whichever lower.  

WorldState - Evaluates condition from conditions table. Intended to be used in connection with type CONDITION_ACTIVE_GAME_EVENT 12, CONDITION_ACTIVE_HOLIDAY 26 and CONDITION_WORLDSTATE 42 conditions only for performance and safety reasons. Consult [worldstate](https://github.com/cmangos/issues/wiki/Worldstates) for more information.  

WorldStateExpression - [worldstate_expression.Id](https://github.com/cmangos/issues/wiki/worldstate_expression)  
Exclusive with WorldState - Uses official data for expressions like in combat_condition

Flags - enum CreatureGroupFlags

```
    CREATURE_GROUP_AGGRO_TOGETHER    = 0x01,
    CREATURE_GROUP_RESPAWN_TOGETHER  = 0x02,
    CREATURE_GROUP_EVADE_TOGETHER    = 0x04,
```

Flags - enum SpawnGroupFlags // flags that are common between both creature and gos (GO groups currently have no unique flags)

```
    SPAWN_GROUP_DESPAWN_ON_COND_FAIL = 0x08,
```

StringId - [string_id](string_id#id) - will be set to all spawns of spawn_group

---
## spawn_group_spawn

Id - Spawn Group ID  
Guid - Guid in Creature or GameObject table, used as DbGuid in core, due to SpawnGroups automatically using Dynamic Guid system (when spawned, has unique guid)
SlotId - Formation Slot, -1 for gameobjects or creatures that are not in formation but part of a spawn group.

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

#### Id - Spawn Group ID

#### FormationType

enum SpawnGroupFormationType

|Value|Name|Example|
|---|---|---|
|0|SPAWN_GROUP_FORMATION_TYPE_RANDOM(subject to change)| ![](https://i.imgur.com/6ta9ZNX.png) |
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

#### PathId

##### waypoint_path 

Table waypoint_path holds the waypoint data for PathId used in spawn_group_formation.

##### waypoint_path_name

Table waypoint_path_name PathId holds names used for PathId

#### MovementType

MovementType of the Formation, Overwrites creature.MovementType. 0 (Idle) 2 (waypoint movement) 3 (path movement) or 4 (linear movement) are applicable

#### Comment

Same as [`spawn_group`.`Name`](https://github.com/cmangos/issues/wiki/spawn_group#Name)

---

## spawn_group_linked_group

#### Id - Spawn Group ID

#### LinkedId - Linked Spawn Group ID

One directional linkage to another spawn group for aggro. In some dungeons, you are forced to clear packs in iterative order or boss pull triggers aggro on several other groups. When Spawn Group with Id aggroes, LinkedId Spawn Group also aggroes.