Back to [world database](https://github.com/cmangos/issues/wiki/mangosdb_struct) list of tables.

## The `creature_spawn_data_template` table

Contains data to override spawned creatures `UnitFlags`,`Faction`,`ModelId`,`EquipmentId`,`CurHealth`,`CurMana`,`SpawnFlags`
Linked to [creature_spawn_data.Id](creature_spawn_data)

### Structure

| Name                                                    | Type                  | Null | Key | Default | Extra |
| ------------------------------------------------------- | --------------------- | ---- | --- | ------- | ----- |
| [Entry](creature_spawn_data_template#Entry)             | int(10) unsigned      | NO   | PRI | (NULL)  |       |
| [NpcFlags](creature_spawn_data_template#NpcFlags)       | int(10)               | NO   | PRI | -1      |       |
| [UnitFlags](creature_spawn_data_template#UnitFlags)     | bigint(20)            | NO   | PRI | -1      |       |
| [Faction](creature_spawn_data_template#Faction)         | int(10) unsigned      | NO   |     | 0       |       |
| [ModelId](creature_spawn_data_template#ModelId)         | mediumint(8) unsigned | NO   | PRI | 0       |       |
| [EquipmentId](creature_spawn_data_template#EquipmentId) | int(10) unsigned      | NO   | PRI | -1      |       |
| [CurHealth](creature_spawn_data_template#CurHealth)     | int(10) unsigned      | NO   | PRI | 0       |       |
| [CurMana](creature_spawn_data_template#CurMana)         | int(10) unsigned      | NO   | PRI | 0       |       |
| [SpawnFlags](creature_spawn_data_template#SpawnFlags)   | int(10) unsigned      | NO   | PRI | 0       |       |
| [RelayId](creature_spawn_data_template#RelayId)         | int(10) unsigned      | NO   |     | 0       | dbscripts_on_relay |
| [StringId](string_id#id)         | int(10) unsigned      | NO   |     | 0       | dbscripts_on_relay |
| [Name](creature_spawn_data_template#Name)         | varchar(200)      | NO   |     | 0       |  |

### Description of the fields

#### Entry

Unique ID for each `creature_spawn_data_template`. Linked to [creature_spawn_data.Id](creature_spawn_data#Id)
To avoid conflicts between Expansions, please use:

| Version:              | Range         |
| ----------------------|---------------|
| Generic All Expansions| 0- 999        |
| Vanilla       | 1000 - 9999   |
| TBC           | 10000 - 19999 |
| WotLK         | 20000+        |
| Generic All Expansions| 30000 - 30999 |
| Specific Creature Entry Case|[`creature_template`.`entry`](creature_template#entry) * 100 + (1 – 99)|

#### NpcFlags

New value that will be applied to creature. Ref: [creature_template.NpcFlags](creature_template#NpcFlags)
`Important` Default -1. Value `0` will remove all NpcFlags from creature
Use with CREATURE_EXTRA_FLAG_DYNGUID for entry. Old legacy code breaks it on respawn and a lot of other stuff relied on this "feature", with dynguid the problem does not exist.

#### UnitFlags

New value that will be applied to creature. Ref: [creature_template.UnitFlags](creature_template#UnitFlags)
`Important` Default -1. Value `0` will remove all UnitFlags from creature
 
#### Faction

New value that will be applied to creature. Ref: [FactionTemplate.dbc.content](FactionTemplate.dbc#content)
`0` - will leave creatures default value

#### ModelId

New value that will be applied to creature. Ref: [Creature_Model_Info.Entry](Creature_Model_Info#Entry)
`0` - will leave creatures default value

#### EquipmentId

New value that will be applied to creature. Ref: [creature_equip_template.entry](creature_equip_template#entry)
`-1` - will leave creatures default value, 0 sets no equipment.

#### CurHealth

New value that will be applied to creature. Ref: [Creature_Model_Info.Entry](Creature_Model_Info#Entry)
`0` - will leave creatures default value

#### CurMana

New value that will be applied to creature. Ref: [creature.curmana](creature#curmana)
`0` - will leave creatures default value

#### SpawnFlags

Special Flags applied to creature:

| Bit: |Hex  | Name                       |
| -----|-----|----------------------------|
| 1    |0x01 |SPAWN_FLAG_RUN_ON_SPAWN     |
| 2    |0x02 |SPAWN_FLAG_HOVER (flying)   |

#### RelayId

[dbscripts.id](dbscripts#id) - RelayId

