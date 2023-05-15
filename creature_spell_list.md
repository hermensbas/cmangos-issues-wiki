Back to [world database](https://github.com/cmangos/issues/wiki/mangosdb_struct) list of tables.

## The `creature_spell_list` table

holds basic creature combat spell_lists previously held by `creature_ai_scripts` "(EventAI / ACID)".

Meant to emulate official server tool image logic. Ties into not just AI but also Charms and Possess for giving spells and cooldowns.
Set ID is changeable in EAI and C++ for now. Default is in creature_template SpellList column.
Logically a consolidation of EAI timer 0 event, 9 event for combat spells, creature_template_spells and creature_cooldowns tables. Meant to replace non-conditional
timers in CombatAI and is hot-reloadable. - https://github.com/cmangos/mangos-tbc/blob/master/doc/SpellLists.txt

### Structure

| Field| Type| Null| Key| Default| Comment|
| ---|---| ---|--- |--- |--- |
|[Id](https://github.com/cmangos/issues/wiki/creature_spell_list#Id)|int(11) unsigned|NO|Primary Key|0|List ID - Primary Key #1|
|[Position](https://github.com/cmangos/issues/wiki/creature_spell_list#Position)|int(11) unsigned|YES|Primary Key|0|Position on list - Primary Key #2|
|[SpellId](https://github.com/cmangos/issues/wiki/creature_spell_list#SpellId)|int(11) unsigned|YES|NULL|0|SpellId|
|[Flags](https://github.com/cmangos/issues/wiki/creature_spell_list#Flags)|int(11) unsigned|YES|NULL|0|Spell Flags - enum SpellListFlags|
|[CombatCondition](https://github.com/cmangos/issues/wiki/creature_spell_list#CombatCondition)|int(11) unsigned|YES|NULL|0||
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

`creature_template`.`entry` * 100 + 1-99 for the "first list/phase of an NPC.

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

#### CombatCondition

[combat_condition.Id](combat_condition#Id) - evaluated on target

#### TargetId

This is the ingame language of the text. "enum SpellListTargetingHardcoded"

| ID | Name           | Description                                                                 |
| -- | -------------- | ----------------------------------------------------------------------------|
| 0  | SPELL_LIST_TARGET_NONE | Spell decides Target - nullptr |
| 1  | SPELL_LIST_TARGET_CURRENT | m_unit->GetVictim(); |
| 2  | SPELL_LIST_TARGET_SELF | m_unit |
| 3  | SPELL_LIST_TARGET_DISPELLABLE_FRIENDLY | DoFindFriendlyEligibleDispel |
| 4  | SPELL_LIST_TARGET_DISPELLABLE_FRIENDLY_NO_SELF | DoFindFriendlyEligibleDispel (bool self) |
| 5  | SPELL_LIST_TARGET_FRIENDLY_MISSING_BUFF | DoFindFriendlyMissingBuff |
| 6  | SPELL_LIST_TARGET_FRIENDLY_MISSING_BUFF_NO_SELF| DoFindFriendlyMissingBuff (bool self) |
| 7  | SPELL_LIST_TARGET_CURRENT_NOT_ALONE| m_unit->getThreatManager().getThreatList().size() > 1; |

#### ScriptId

Launch dbscripts_on_relay dbscript at successful cast start.

If possible use same value as for Id. `creature_template`.`entry` * 100 + 1-99

#### Availability

Chance for spell to be included in spell list at assignment. Assignment happens by default on spawn.

#### Probability

when probability is 0 for all spells, they will use priority based on positions

If several spells are eligible in the same spell list tick, this is the weight with which its likely this spell will go off. Higher probability, higher chance for spell to go off.

#### InitialMin
#### InitialMax
#### RepeatMin
#### RepeatMax

Timers in Milliseconds (1sec = 1000) used for casting spell. Will emplace a cooldown on the user unlike EAI which only starts a timer. Repeat timers are used, during charm to give spells cooldowns as well.

Basic Timers, more Cooldown orientated due to focus on Availability & Probability and SPELL_LIST_FLAG_SUPPORT_ACTION / SPELL_LIST_FLAG_RANGED_ACTION Chance

## The `creature_spell_list_entry` table

holds basic chance of a ai to perform either a SPELL_LIST_FLAG_SUPPORT_ACTION or SPELL_LIST_FLAG_RANGED_ACTION.

chance is either base in ranged mode or chance - 50 in melee mode

meant to simulate chaincasting in ranged mode and mostly not chaincasting in melee mode

### Structure

| Field| Type| Null| Key| Default| Comment|
| ---|---| ---|--- |--- |--- |
|[Id](https://github.com/cmangos/issues/wiki/creature_spell_list#`creature_spell_list_entry`.`Id`)|int(11) unsigned|NO|Primary Key|0|creature_template entry or * 100 + 1-99|
|[Name](https://github.com/cmangos/issues/wiki/creature_spell_list#`creature_spell_list_entry`.`Name`)|varchar(200)|YES|NULL|0|MAP - Creature Name (Description of usage)|
|[ChanceSupportAction](https://github.com/cmangos/issues/wiki/creature_spell_list#`creature_spell_list_entry`.`ChanceSupportAction`)|int(11) unsigned|YES|NULL|0|Chance of support action per tick (1200ms) - GENERIC_ACTION_SPELL_LIST|
|[ChanceRangedAttack](https://github.com/cmangos/issues/wiki/creature_spell_list#`creature_spell_list_entry`.`ChanceRangedAttack`)|int(11) unsigned|YES|NULL|0|Chance of ranged attack per tick (1200ms) - GENERIC_ACTION_SPELL_LIST|

#### `creature_spell_list_entry`.`Id`

Spell List ID - entry * 100 + 01...

#### `creature_spell_list_entry`.`Name`

Mandatory - Spell name with zone prefix. Example: Westfall - Defias Pillager. This naming enables querying npcs by zone, very useful in dungeons.

#### `creature_spell_list_entry`.`ChanceSupportAction`
#### `creature_spell_list_entry`.`ChanceRangedAttack`

ChanceSupportAction and ChanceRangedAttack - Chance at each spell list tick in combat (1200ms) for the action with SPELL_LIST_FLAG_SUPPORT_ACTION (1) or
SPELL_LIST_FLAG_RANGED_ACTION (2) set respectively. If multiple are set, always one spell is selected. During melee mode, ranged attack chance is -50.
The 1200ms loop has been checked on official servers and will intentionally make the AI less responsive and less impactful on performance. EAI has a 500ms tick rate on timers,
however that is not an issue due to it needing a finer control. A normal spell list entry should never have more than 10 spells, since that was an official limitation

## The `creature_spell_targeting` table

holds mostly hardcoded targeting types for [`creature_spell_list`.`TargetId`](https://github.com/cmangos/issues/wiki/creature_spell_list#TargetId)

### Structure

| Field| Type| Null| Key| Default| Comment|
| ---| ---| ---| ---| ---| ---|
|[Id](https://github.com/cmangos/issues/wiki/creature_spell_list#`creature_spell_targeting`.`Id`)|int(11)|NO|Primary Key|0|Targeting ID|
|[Type](https://github.com/cmangos/issues/wiki/creature_spell_list#`creature_spell_targeting`.`Type`)|int(11)|NO|NO|0|Type of targeting ID (Hardcoded (0) / Attack (1) / Support (2))|
|[Param1](https://github.com/cmangos/issues/wiki/creature_spell_list#`creature_spell_targeting`.`Param1`)|int(11)|NO|NO|0|First parameter|
|[Param2](https://github.com/cmangos/issues/wiki/creature_spell_list#`creature_spell_targeting`.`Param2`)|int(11)|NO|NO|0|Second parameter|
|[Param3](https://github.com/cmangos/issues/wiki/creature_spell_list#`creature_spell_targeting`.`Param3`)|int(11)|NO|NO|0|Third parameter|
|[UnitCondition](https://github.com/cmangos/issues/wiki/creature_spell_list#`creature_spell_targeting`.`UnitCondition`)|int(11)|NO|NO|0||
|[Comments](https://github.com/cmangos/issues/wiki/creature_spell_list#`creature_spell_targeting`.`Comments`)|varchar(255)|NO|NO|Empty String|Description of target|

#### `creature_spell_targeting`.`Id`

Spell Targeting ID - Ids below 100 are reserved for future use with hardcoded targets.

#### `creature_spell_targeting`.`Type`

Hardcoded/Attack/Support - Hardcoded dont need additional parameters

#### `creature_spell_targeting`.`Param1`

Type 1 - Attack: Param1  - enum AttackingTarget

```
enum AttackingTarget
{
    ATTACKING_TARGET_RANDOM = 0,                            // Just selects a random target
    ATTACKING_TARGET_TOPAGGRO,                              // Selects targes from top aggro to bottom
    ATTACKING_TARGET_BOTTOMAGGRO,                           // Selects targets from bottom aggro to top
    ATTACKING_TARGET_NEAREST_BY,                            // Selects the nearest by target
    ATTACKING_TARGET_FARTHEST_AWAY,                         // Selects the farthest away target
    ATTACKING_TARGET_ALL_SUITABLE,
};
```

Type 2 - Support: Param1 - Minimum missing health or health% if Param2 = 1


#### `creature_spell_targeting`.`Param2`

Type 1 - Attack: Param2  - Number of positions from the top of the threat list to be skipped.

Type 2 - Support: Param2 - 0 or 1, 0 if minimum missing is flat health and 1 if minimum missing is percentage.


#### `creature_spell_targeting`.`Param3`

Type 1 - Attack: Param3  - enum SelectFlags

```
enum SelectFlags
{
    SELECT_FLAG_IN_LOS              = 0x0001,               // Default Selection Requirement for Spell-targets
    SELECT_FLAG_PLAYER              = 0x0002,
    SELECT_FLAG_POWER_MANA          = 0x0004,               // For Energy based spells, like manaburn
    SELECT_FLAG_POWER_RAGE          = 0x0008,
    SELECT_FLAG_POWER_ENERGY        = 0x0010,
    SELECT_FLAG_IN_MELEE_RANGE      = 0x0040,
    SELECT_FLAG_NOT_IN_MELEE_RANGE  = 0x0080,
    SELECT_FLAG_HAS_AURA            = 0x0100,
    SELECT_FLAG_NOT_AURA            = 0x0200,
    SELECT_FLAG_RANGE_RANGE         = 0x0400,               // For direct targeted abilities like charge or frostbolt but need custom data
    SELECT_FLAG_RANGE_AOE_RANGE     = 0x0800,               // For AOE targeted abilities like frost nova but need custom data
    SELECT_FLAG_POWER_NOT_MANA      = 0x1000,               // Used in some dungeon encounters
    SELECT_FLAG_USE_EFFECT_RADIUS   = 0x2000,               // For AOE targeted abilities which have correct data in effect index 0
    SELECT_FLAG_SKIP_TANK           = 0x4000,               // Not GetVictim - tank is not always top threat
    SELECT_FLAG_CASTING             = 0x8000,               // Selects only targets that are casting
    SELECT_FLAG_SKIP_CUSTOM         =0x10000,               // skips custom target
    SELECT_FLAG_NOT_IMMUNE          =0x20000,
};
```

Type 2 - Support: Param2 - Param3 - 0 or 1, 0 if self should not be eligible.

#### `creature_spell_targeting`.`UnitCondition`

[unit_condition.Id](unit_condition#Id) - evaluated on target

#### `creature_spell_targeting`.`Comments`

Description of target in format: Type - Use.