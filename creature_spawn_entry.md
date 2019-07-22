Back to [world database](https://github.com/cmangos/issues/wiki/mangosdb_struct) list of tables.

## The `creature_spawn_entry` table

holds multiple `creature_template`.`entry` a `creature`.`guid` can be spawned as.

It therefore removes the need of abusing the pooling system for a 100% spawn and lets the pooling system be used for chanced spawns.

### Structure

| Field| Type| Null| Key| Default| Extra|
| ---|---| ---|--- |--- |--- |
|[guid](https://github.com/cmangos/issues/wiki/creature_spawn_entry#guid)|int(10) unsigned|NO||0||
|[entry](https://github.com/cmangos/issues/wiki/creature_spawn_entry#entry)|mediumint(8)|NO||0||

#### guid

`creature`.`guid` that has multiple `creature_template`.`entry` possibilities.

Set `creature`.`id` to **0** for this guid as identifier.

#### entry

`creature_template`.`entry` that should be assigned to the `creature`.`guid`.

Currently these entries are all even chanced.