Back to [world database](https://github.com/cmangos/issues/wiki/Mangosdb_struct) list of tables.

## The `creature_template_spells` table

holds creature spell data, which was previously held in [creature_template](https://github.com/cmangos/issues/wiki/creature_template) table. DEPRECATED: use [creature_spell_list](https://github.com/cmangos/issues/wiki/creature_spell_list) instead

### General Use

TotemAI uses creature_template_spells for spell reference.

Creatures with creature_template_spells entry, which are subject to Aura Id 2 (SPELL_AURA_MOD_POSSESS) will hold these spells as actions in the Pet Action Bar.

creature_template_spells data can also give information on missing CreatureAI. However, this has to be evaltuated carefully, as creatures might hold spell data, which is either incorrect or has spells inserted which they only have available when possessed / used as pet.

### Structure

| Field | Type | Null | Key | Default |
| --- | --- | --- | --- | --- |
|[entry](creature_template_spells#entry)||NO|PRI|0|
|[spell1](creature_template_spells#spell1)||NO||0|
|[spell2](creature_template_spells#spell2)||NO||0|
|[spell3](creature_template_spells#spell3)||NO||0|
|[spell4](creature_template_spells#spell4)||NO||0|
|[spell5](creature_template_spells#spell4)||NO||0|
|[spell6](creature_template_spells#spell4)||NO||0|
|[spell7](creature_template_spells#spell4)||NO||0|
|[spell8](creature_template_spells#spell4)||NO||0|

### Description of the fields

#### entry

[`creature_template`.`entry`](Creature_template#entry) of the creature possessing these spells.

#### spell1

[`spell_template`.`id`](spell_template#id) of the spell