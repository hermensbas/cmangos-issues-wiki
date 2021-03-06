Back to [world database](https://github.com/cmangos/issues/wiki/mangosdb_struct) list of tables.

## The `creature_spawn_data` table

Holds Link Between individual creature spawn `GUID` and `creature_spawn_data_template`<br>
See [creature_spawn_data_template.Entry](creature_spawn_data_template) for more details

### Structure

| Name                                         | Type                  | Null | Key | Default | Extra | Comment                                       |
| -------------------------------------------- | --------------------- | ---- | --- | ------- | ----- | --------------------------------------------- |
| [guid](creature_spawn_data#guid)             | int(10) unsigned      | NO   | PRI | 0       |       | individual creature.guid                      |
| [Id](creature_spawn_data#Id)                 | int(10) unsigned      | NO   |     | 0       |       | link to creature_spawn_data_template          |

### Description of the fields

#### guid

The `Guid` of the creature. See [creature.guid](creature#Guid)

#### Id

`Entry` from `creature_spawn_data_template` that our individual `Guid` is linked. See [creature_spawn_data_template.Entry](creature_spawn_data_template#Entry)
