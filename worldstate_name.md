Back to [world database](mangosdb_struct) list of tables.

## The `worldstate_name` tables

holds data on worldstate variables used for [`conditions`.`CONDITION_WORLDSTATE` (42)](https://github.com/cmangos/issues/wiki/conditions)

### Structure

| Field                                                | Type                  | Null | Key | Default | Extra |
| ---------------------------------------------------- | --------------------- | ---- | --- | ------- | ----- |
| [Id](worldstate_name#Id)| int(11)|NO|PRIMARY KEY|NULL|Worldstate variable Id|
| [Name](worldstate_name#Name)|VARCHAR(200)|NO||NULL|Name and use of variable|

#### Id

Worldstate variable Id

#### Name

Name and use of variable