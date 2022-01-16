Back to [world database](https://github.com/cmangos/issues/wiki/Mangosdb_struct) list of tables.

## The `pool_creature_template` table

DEPRECATED : Use https://github.com/cmangos/issues/wiki/spawn_group instead. Pooling is also dynguid incompatbile.

holds data on creatures that are pooled by their [`creature_template`.`entry`](Creature_template#entry).

All creatures have to be located on the same [`instance_template`.`map`](https://github.com/cmangos/issues/wiki/instance_template#map) / [`world_template``map`](https://github.com/cmangos/issues/wiki/world_template#map).

### Structure

| Field | Type | Null | Key | Default |
| --- | --- | --- | --- | --- |
|[id](pool_creature_template#id)|int(10) unsigned|NO|PRI|0|||
|[pool_entry](pool_creature_template#pool_entry)|mediumint(8) unsigned|NO|PRI|0|||
|[chance](pool_creature_template#chance)|float unsigned|NO||0|||
|[description](pool_creature_template#description)|varchar(255)|NO||0|||

### Description of the fields

#### id

[`creature_template`.`entry`](Creature_template#entry) of the creature

#### pool_entry

[`pool_template`.`entry`](pool_template#entry) of the pool

#### chance

Chance the creature(s) will be spawned in the pool. 
If 0, maxlimit of [`pool_template`.`entry`](pool_template#entry) is spawned

#### description

Description of the stored data