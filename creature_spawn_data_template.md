Back to [world database](https://github.com/cmangos/issues/wiki/mangosdb_struct) list of tables.

## The `creature_spawn_data_template` table

Contains data to override spawned creatures `UnitFlags`,`Faction`,`ModelId`,`EquipmentId`,`CurHealth`,`CurMana`,`SpawnFlags`<br>
Linked to [creature_spawn_data.Id](creature_spawn_data)

### Structure

| Name                                                    | Type                  | Null | Key | Default | Extra |
| ------------------------------------------------------- | --------------------- | ---- | --- | ------- | ----- |
| [Entry](creature_spawn_data_template#Entry)             | int(10) unsigned      | NO   | PRI | (NULL)  |       |
| [UnitFlags](creature_spawn_data_template#UnitFlags)     | bigint(20)            | NO   |     | -1      |       |
| [Faction](creature_spawn_data_template#Faction)         | int(10) unsigned      | NO   |     | 0       |       |
| [ModelId](creature_spawn_data_template#ModelId)         | mediumint(8) unsigned | NO   |     | 0       |       |
| [EquipmentId](creature_spawn_data_template#EquipmentId) | int(10) unsigned      | NO   |     | 0       |       |
| [CurHealth](creature_spawn_data_template#CurHealth)     | int(10) unsigned      | NO   |     | 0       |       |
| [CurMana](creature_spawn_data_template#CurMana)         | int(10) unsigned      | NO   |     | 0       |       |
| [SpawnFlags](creature_spawn_data_template#SpawnFlags)   | int(10) unsigned      | NO   |     | 0       |       |

### Description of the fields

#### Entry

Unique ID for each `creature_spawn_data_template`. Linked to [creature_spawn_data.Id](creature_spawn_data#Id)<br>
To avoid conflicts between Expansions, please use:

| Version:             | Range         |
| ---------------------|---------------|
| Generic:             | 0- 999        |
| Vanilla:             | 1000 - 9999   |
| TBC:                 | 10000 - 19999 |
| WotLK:               | 20000 +       |

#### UnitFlags

New value that will be applied to creature. Ref: [creature_template.UnitFlags](creature_template#UnitFlags)<br>
`Important` Only here default = -1. Value `0` will remove all unitFlags from creature
 
#### Faction

New value that will be applied to creature. Ref: [FactionTemplate.dbc.content](FactionTemplate.dbc#content)<br>
`0` - will leave creatures default value

#### ModelId

New value that will be applied to creature. Ref: [Creature_Model_Info.Entry](Creature_Model_Info#Entry)<br>
`0` - will leave creatures default value

#### EquipmentId

New value that will be applied to creature. Ref: [creature_equip_template.entry](creature_equip_template#entry)<br>
`0` - will leave creatures default value

#### CurHealth

New value that will be applied to creature. Ref: [Creature_Model_Info.Entry](Creature_Model_Info#Entry)<br>
`0` - will leave creatures default value

#### CurMana

New value that will be applied to creature. Ref: [creature.curmana](creature#curmana)<br>
`0` - will leave creatures default value

#### SpawnFlags

Special Flags applied to creature:

| Bit: |Hex  | Name                       |
| -----|-----|----------------------------|
| 1    |0x01 |SPAWN_FLAG_RUN_ON_SPAWN     |
| 2    |0x02 |SPAWN_FLAG_HOVER (flying)   |
