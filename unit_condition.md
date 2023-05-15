Back to [world database](mangosdb_struct) list of tables.

## The `unit_condition` table

Official table structure - used for condition checks on units

### Structure

| Field                           | Type             | NULL | Key     | Default | Comments                    |
| ------------------------------- | ---------------- | ---- | ------- | ------- | --------------------------- |
| [Id](#Id)                  | int(11) unsigned | NO   | PRIMARY | 0       | Primary Key |
| [Flags](#)                 | int(11) unsigned | NO   |         | 0       |             |
| [Variable_0](#Variable_0)  | int(11) unsigned | NO   |         | 0       |             |
| [Variable_1](#Variable_1)  | int(11) unsigned | NO   |         | 0       |             |
| [Variable_2](#Variable_2)  | int(11) unsigned | NO   |         | 0       |             |
| [Variable_3](#Variable_3)  | int(11) unsigned | NO   |         | 0       |             |
| [Variable_4](#Variable_4)  | int(11) unsigned | NO   |         | 0       |             |
| [Variable_5](#Variable_5)  | int(11) unsigned | NO   |         | 0       |             |
| [Variable_6](#Variable_6)  | int(11) unsigned | NO   |         | 0       |             |
| [Variable_7](#Variable_7)  | int(11) unsigned | NO   |         | 0       |             |
| [Op_0](#Op_0)              | int(11) unsigned | NO   |         | 0       |             |
| [Op_1](#Op_1)              | int(11) unsigned | NO   |         | 0       |             |
| [Op_2](#Op_2)              | int(11) unsigned | NO   |         | 0       |             |
| [Op_3](#Op_3)              | int(11) unsigned | NO   |         | 0       |             |
| [Op_4](#Op_4)              | int(11) unsigned | NO   |         | 0       |             |
| [Op_5](#Op_5)              | int(11) unsigned | NO   |         | 0       |             |
| [Op_6](#Op_6)              | int(11) unsigned | NO   |         | 0       |             |
| [Op_7](#Op_7)              | int(11) unsigned | NO   |         | 0       |             |
| [Value_0](#Value_0)        | int(11) unsigned | NO   |         | 0       |             |
| [Value_1](#Value_1)        | int(11) unsigned | NO   |         | 0       |             |
| [Value_2](#Value_2)        | int(11) unsigned | NO   |         | 0       |             |
| [Value_3](#Value_3)        | int(11) unsigned | NO   |         | 0       |             |
| [Value_4](#Value_4)        | int(11) unsigned | NO   |         | 0       |             |
| [Value_5](#Value_5)        | int(11) unsigned | NO   |         | 0       |             |
| [Value_6](#Value_6)        | int(11) unsigned | NO   |         | 0       |             |
| [Value_7](#Value_7)        | int(11) unsigned | NO   |         | 0       |             |

### Uses

[combat_condition](combat_condition)  
[creature_spell_targeting](creature_spell_list#the-creature_spell_targeting-table)  

### Description of the fields

#### Id

Numeric identifier

#### Flags

By default, multiple conditions are executed with AND operation. UNIT_CONDITION_FLAG_OR = 0x1 causes them to execute as OR.

#### Variable_0
#### Variable_1
#### Variable_2
#### Variable_3
#### Variable_4
#### Variable_5
#### Variable_6
#### Variable_7

Each condition has 3 parameters when evaluating: Condition source (Unit), Condition target (Unit), and Value (signed integer)  
All variables are enum class UnitCondition:  

    NONE                                     = 0,
    RACE                                     = 1, Result: Race
    CLASS                                    = 2, Result: Class
    LEVEL                                    = 3, Result: Level
    IS_SELF                                  = 4, Result: 1 if self
    IS_MY_PET                                = 5, Result: 1 if target is my pet
    IS_MASTER                                = 6, Result: 1 if target is my master
    IS_TARGET                                = 7, Result: 1 if source is target of target
    CAN_ASSIST                               = 8, Result: 1 if source can assist target
    CAN_ATTACK                               = 9, Result: 1 if source can attack target
    HAS_PET                                  = 10, Result: 1 if source has pet
    HAS_WEAPON                               = 11, Result: 1 if source has weapon
    HEALTH_PERCENT                           = 12,
    MANA_PERCENT                             = 13,
    RAGE_PERCENT                             = 14,
    ENERGY_PERCENT                           = 15,
    COMBO_POINTS                             = 16,
    HAS_HELPFUL_AURA_SPELL                   = 17,
    HAS_HELPFUL_AURA_DISPEL_TYPE             = 18,
    HAS_HELPFUL_AURA_MECHANIC                = 19,
    HAS_HARMFUL_AURA_SPELL                   = 20,
    HAS_HARMFUL_AURA_DISPEL_TYPE             = 21,
    HAS_HARMFUL_AURA_MECHANIC                = 22,
    HAS_HARMFUL_AURA_SCHOOL                  = 23,
    DAMAGE_PHYSICAL                          = 24,
    DAMAGE_HOLY                              = 25,
    DAMAGE_FIRE                              = 26,
    DAMAGE_NATURE                            = 27,
    DAMAGE_FROST                             = 28,
    DAMAGE_SHADOW                            = 29,
    DAMAGE_ARCANE                            = 30,
    IN_COMBAT                                = 31, Result: 1 if
    IS_MOVING                                = 32, Result: 1 if
    IS_CASTING                               = 33, Result: 1 if
    IS_CASTING_SPELL                         = 34, Result: 1 if
    IS_CHANNELING                            = 35, Result: 1 if
    IS_CHANNELING_SPELL                      = 36, Result: 1 if
    NUMBER_OF_MELEE_ATTACKERS                = 37,
    IS_ATTACKING_ME                          = 38, Result: 1 if
    RANGE                                    = 39,
    IN_MELEE_RANGE                           = 40,
    PURSUIT_TIME                             = 41,
    HAS_HARMFUL_AURA_CANCELLED_BY_DAMAGE     = 42,
    HAS_HARMFUL_AURA_WITH_PERIODIC_DAMAGE    = 43,
    NUMBER_OF_ENEMIES                        = 44,
    NUMBER_OF_FRIENDS                        = 45,
    THREAT_PHYSICAL                          = 46,
    THREAT_HOLY                              = 47,
    THREAT_FIRE                              = 48,
    THREAT_NATURE                            = 49,
    THREAT_FROST                             = 50,
    THREAT_SHADOW                            = 51,
    THREAT_ARCANE                            = 52,
    IS_INTERRUPTIBLE                         = 53, Result: 1 if
    NUMBER_OF_ATTACKERS                      = 54,
    NUMBER_OF_RANGED_ATTACKERS               = 55,
    CREATURE_TYPE                            = 56,
    IS_MELEE_ATTACKING                       = 57, Result: 1 if
    IS_RANGED_ATTACKING                      = 58, Result: 1 if
    HEALTH                                   = 59,
    SPELL_KNOWN                              = 60,
    HAS_HARMFUL_AURA_EFFECT                  = 61,
    IS_IMMUNE_TO_AREA_OF_EFFECT              = 62, Result: 1 if
    IS_PLAYER                                = 63, Result: 1 if
    DAMAGE_MAGIC                             = 64,
    DAMAGE_TOTAL                             = 65,
    THREAT_MAGIC                             = 66,
    THREAT_TOTAL                             = 67,
    HAS_CRITTER                              = 68, Result: 1 if
    HAS_TOTEM_IN_SLOT_1                      = 69, Result: 1 if
    HAS_TOTEM_IN_SLOT_2                      = 70, Result: 1 if
    HAS_TOTEM_IN_SLOT_3                      = 71, Result: 1 if
    HAS_TOTEM_IN_SLOT_4                      = 72, Result: 1 if
    HAS_TOTEM_IN_SLOT_5                      = 73, Result: 1 if
    CREATURE_ID                              = 74,
    STRING_ID                                = 75, Result: 1 if
    HAS_AURA                                 = 76, Result: 1 if
    IS_ENEMY                                 = 77, Result: 1 if
    IS_SPEC_MELEE                            = 78,
    IS_SPEC_TANK                             = 79,
    IS_SPEC_RANGED                           = 80,
    IS_SPEC_HEALER                           = 81,
    IS_PLAYER_CONTROLLED_NPC                 = 82, Result: 1 if
    IS_DYING                                 = 83, Result: 1 if
    PATH_FAIL_COUNT                          = 84, Result: 1 if target is not reachable - HACK (for now)
    UNUSED                                   = 85,
    LABEL                                    = 86,

#### Op_0
#### Op_1
#### Op_2
#### Op_3
#### Op_4
#### Op_5
#### Op_6
#### Op_7

All op are operations from enum class ConditionOperation:

    NONE                        = 0,
    EQUAL_TO                    = 1,
    NOT_EQUAL_TO                = 2,
    LESS_THAN                   = 3,
    LESS_THAN_OR_EQUAL_TO       = 4,
    GREATER_THAN                = 5,
    GREATER_THAN_OR_EQUAL_TO    = 6,

Used to compare result of condition against corresponding Value

#### Value_0
#### Value_1
#### Value_2
#### Value_3
#### Value_4
#### Value_5
#### Value_6
#### Value_7

Value for usage in specific unit condition types.
