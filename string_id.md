Back to [world database](mangosdb_struct) list of tables.

## The `string_id` table

This table contains id and string connection between string_id variables. StringId is assigned to a world object, and then enables querying. Effectively supercedes guid, entry, or other kind of targeting, and enables custom targeting from spells or even per dbscript.

### Structure

| Field                           | Type             | NULL | Key     | Default | Comments                    |
| ------------------------------- | ---------------- | ---- | ------- | ------- | --------------------------- |
| Id     | int(11) unsigned | NO   | PRIMARY | 0       | Primary Key |
| Name   | varchar(255) | YES  |         |         |                             |

### Description of the fields

#### Id

Numeric identifier of string_id variable  

Found in:

[creature_template](creature_template#stringid1)  
[creature_template](creature_template#stringid2)  
[creature_spawn_data_template](creature_spawn_data_template#stringid)  
[gameobject_template](gameobject_template#stringid)  
[gameobject_addon](gameobject_addon#stringid)  
[spawn_group](spawn_group#stringid)  
[dbscripts - SCRIPT_COMMAND_SET_STRING_ID](https://github.com/cmangos/issues/wiki/dbscripts)  

#### Name

String identifier of string_id variable - should be descriptive on where it is used, without spaces and limited to 255 characters.

### Uses

Targeting for [dbscripts](dbscripts)  
Targeting for spells - [spell_script_target](spell_script_target)  
Targeting for C++ scripts:  
Spells:  
```cpp
auto creaturesWithStringId = spell->GetCaster()->GetMap()->GetCreatures("STRING_ID");
```  
AI:  
```cpp
auto creaturesWithStringId = m_creature->GetMap()->GetCreatures("STRING_ID");
```