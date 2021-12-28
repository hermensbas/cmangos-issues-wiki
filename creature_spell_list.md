Back to [world database](https://github.com/cmangos/issues/wiki/mangosdb_struct) list of tables.

## The `creature_spell_list` table

holds basic creature combat spell_lists previously held by `creature_ai_scripts` "(EventAI / ACID)".

### Structure

| Field| Type| Null| Key| Default| Comment|
| ---|---| ---|--- |--- |--- |
|[Id](https://github.com/cmangos/issues/wiki/creature_spell_list#Id)|int(11) unsigned|NO|Primary Key|0|List ID - Primary Key #1|
|[Position](https://github.com/cmangos/issues/wiki/creature_spell_list#Position)|int(11) unsigned|YES|Primary Key|0|Position on list - Primary Key #2|
|[SpellId](https://github.com/cmangos/issues/wiki/creature_spell_list#SpellId)|int(11) unsigned|YES|NULL|0|SpellId|
|[Flags](https://github.com/cmangos/issues/wiki/creature_spell_list#Flags)|int(11) unsigned|YES|NULL|0|Spell Flags - enum SpellListFlags|
|[TargetId](https://github.com/cmangos/issues/wiki/creature_spell_list#TargetId)|int(11) unsigned|YES|NULL|0|Targeting ID - enum SpellListTargetingHardcoded|
|[ScriptId](https://github.com/cmangos/issues/wiki/creature_spell_list#ScriptId)|int(11) unsigned|YES|NULL|0|Dbscript to be launched on success|
|[Availability](https://github.com/cmangos/issues/wiki/creature_spell_list#Availability)|int(11) unsigned|YES|NULL|0|Chance on spawn for spell to be included|
|[Probability](https://github.com/cmangos/issues/wiki/creature_spell_list#Probability)|int(11) unsigned|YES|NULL|0|Weight of spell when multiple are available|
|[InitialMin](https://github.com/cmangos/issues/wiki/creature_spell_list#InitialMin)|int(11) unsigned|YES|NULL|0|Initial delay minimum|
|[InitialMax](https://github.com/cmangos/issues/wiki/creature_spell_list#InitialMax)|int(11) unsigned|YES|NULL|0|Initial delay maximum|
|[RepeatMin](https://github.com/cmangos/issues/wiki/creature_spell_list#RepeatMin)|int(11) unsigned|YES|NULL|0|Repeated delay minimum|
|[RepeatMax](https://github.com/cmangos/issues/wiki/creature_spell_list#RepeatMax)|int(11) unsigned|YES|NULL|0|Repeated delay maximum|
|[Comments](https://github.com/cmangos/issues/wiki/creature_spell_list#Comments)|varchar(255) unsigned|YES|NULL|0|Description of spell use|

#### Id

Primary Key #1

#### Position

Primary Key #2, Priority

#### SpellId

[spellId](spell_template#Id) of the spell.

#### Flags

This is the text type of the text. "enum SpellListFlags"

```
    SPELL_LIST_FLAG_SUPPORT_ACTION  = 1,
    SPELL_LIST_FLAG_RANGED_ACTION   = 2, // previously known as main ranged spell in EAI
```

#### TargetId

This is the ingame language of the text. "enum SpellListTargetingHardcoded"

| ID | Name           | Description                                                                 |
| -- | -------------- | ----------------------------------------------------------------------------|
| 0  | SPELL_LIST_TARGET_NONE							| Spell decides Target - nullptr			|
| 1  | SPELL_LIST_TARGET_CURRENT						| m_unit->GetVictim();						|
| 2  | SPELL_LIST_TARGET_SELF							| m_unit									|
| 3  | SPELL_LIST_TARGET_DISPELLABLE_FRIENDLY        	| DoFindFriendlyEligibleDispel				|
| 4  | SPELL_LIST_TARGET_DISPELLABLE_FRIENDLY_NO_SELF	| DoFindFriendlyEligibleDispel (bool self)	|

#### ScriptId

Launch dbscripts_on_relay dbscript

#### Availability

#### Probability

when probability is 0 for all spells, they will use priority based on positions

#### InitialMin
#### InitialMax
#### RepeatMin
#### RepeatMax

Basic Timers, more Cooldown orientated due to focus on Availability & Probability and SPELL_LIST_FLAG_SUPPORT_ACTION / SPELL_LIST_FLAG_RANGED_ACTION Chance

## The `creature_spell_list_entry` table

holds basic chance of a ai to perform either a SPELL_LIST_FLAG_SUPPORT_ACTION or SPELL_LIST_FLAG_RANGED_ACTION.

chance is either base in ranged mode or chance - 50 in melee mode

meant to simulate chaincasting in ranged mode and mostly not chaincasting in melee mode

### Structure

| Field| Type| Null| Key| Default| Comment|
| ---|---| ---|--- |--- |--- |
|[Id](https://github.com/cmangos/issues/wiki/creature_spell_list#Id)|int(11) unsigned|NO|Primary Key|0|creature_template entry or * 100 + 1-99|
|[Name](https://github.com/cmangos/issues/wiki/creature_spell_list#Name)|varchar(200)|YES|NULL|0|MAP - Creature Name (Description of usage)|
|[ChanceSupportAction](https://github.com/cmangos/issues/wiki/creature_spell_list#ChanceSupportAction)|int(11) unsigned|YES|NULL|0|Chance of support action per tick (1200ms) - GENERIC_ACTION_SPELL_LIST|
|[ChanceRangedAttack](https://github.com/cmangos/issues/wiki/creature_spell_list#ChanceRangedAttack)|int(11) unsigned|YES|NULL|0|Chance of ranged attack per tick (1200ms) - GENERIC_ACTION_SPELL_LIST|

