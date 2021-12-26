Tables:

spawn_group  
spawn_group_spawn  
spawn_group_entry  

Logically a replacement of linking and pooling. Groups spawns into a logical group, which can behave differently. Benefits are much easier handling in core and during creation of new entries. Also introduces conditional spawning through worldstate alteration.

spawn_group  
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

spawn_group_spawn  
Id - Spawn Group ID  
Guid - Guid in Creature or GameObject table, used as DbGuid in core, due to SpawnGroups automatically using Dynamic Guid system (when spawned, has unique guid)  

spawn_group_entry - non mandatory  
Id - Spawn Group ID  
Entry - Entry for picking on spawn from creature_template or gameobject_template  
MinCount - Minimum count of entries before random chances or other entries become eligible  
MaxCount - Maximum count of given entry in the world for whole spawn group  
Chance - Chance of entry to be picked over other chanced entries. First chanced entries are tried and then all chanced with 0. MinCount overrides this  

