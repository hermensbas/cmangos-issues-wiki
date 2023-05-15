Back to [world database](https://github.com/cmangos/issues/wiki/mangosdb_struct) list of tables.

## The `combat_condition` table

Official table structure - used for combat condition checks on units for [creature_spell_list](creature_spell_list)

Contains complex checks for executing combat events.

### Structure

| Field                           | Type             | NULL | Key     | Default | Comments                    |
| ------------------------------- | ---------------- | ---- | ------- | ------- | --------------------------- |
| [Id](#Id)                                         | int(11) unsigned | NO   | PRIMARY | 0       | Primary Key |
| [WorldStateExpressionID](#WorldStateExpressionID) | int(11) unsigned | NO   |         | 0       |             |
| [SelfConditionID](#SelfConditionID)               | int(11) unsigned | NO   |         | 0       |             |
| [TargetConditionID](#TargetConditionID)           | int(11) unsigned | NO   |         | 0       |             |
| [FriendConditionLogic](#FriendConditionLogic)     | int(11) unsigned | NO   |         | 0       |             |
| [EnemyConditionLogic](#EnemyConditionLogic)       | int(11) unsigned | NO   |         | 0       |             |
| [FriendConditionID_0](#FriendConditionID_0)       | int(11) unsigned | NO   |         | 0       |             |
| [FriendConditionID_1](#FriendConditionID_1)       | int(11) unsigned | NO   |         | 0       |             |
| [FriendConditionOp_0](#FriendConditionOp_0)       | int(11) unsigned | NO   |         | 0       |             |
| [FriendConditionOp_1](#FriendConditionOp_1)       | int(11) unsigned | NO   |         | 0       |             |
| [FriendConditionCount_0](#FriendConditionCount_0) | int(11) unsigned | NO   |         | 0       |             |
| [FriendConditionCount_1](#FriendConditionCount_1) | int(11) unsigned | NO   |         | 0       |             |
| [EnemyConditionID_0](#EnemyConditionID_0)         | int(11) unsigned | NO   |         | 0       |             |
| [EnemyConditionID_1](#EnemyConditionID_1)         | int(11) unsigned | NO   |         | 0       |             |
| [EnemyConditionOp_0](#EnemyConditionOp_0)         | int(11) unsigned | NO   |         | 0       |             |
| [EnemyConditionOp_1](#EnemyConditionOp_1)         | int(11) unsigned | NO   |         | 0       |             |
| [EnemyConditionCount_0](#EnemyConditionCount_0)   | int(11) unsigned | NO   |         | 0       |             |
| [EnemyConditionCount_1](#EnemyConditionCount_1)   | int(11) unsigned | NO   |         | 0       |             |

#### Id

Numeric identifier

#### WorldStateExpressionID

[worldstate_expression.Id](worldstate_expression#Id)

#### SelfConditionID

[unit_condition.Id](unit_condition#Id) - Condition executed against source

#### TargetConditionID

[unit_condition.Id](unit_condition#Id) - Condition executed against target of source

#### FriendConditionLogic
#### EnemyConditionLogic

enum class ConditionLogic (NONE - 0, AND - 1, OR - 2, XOR - 3)

Used against condition 0 and 1 of friend/enemy. If NONE, only cond 0 is evaluated.

#### FriendConditionID_0
#### FriendConditionID_1
#### EnemyConditionID_0
#### EnemyConditionID_1

[unit_condition.Id](unit_condition#Id) - Condition executed against friend (picked in range of spell) or enemy (taken from threat list)

#### FriendConditionOp_0
#### FriendConditionOp_1
#### EnemyConditionOp_0
#### EnemyConditionOp_1

enum class ConditionOperation

    NONE                        = 0,
    EQUAL_TO                    = 1,
    NOT_EQUAL_TO                = 2,
    LESS_THAN                   = 3,
    LESS_THAN_OR_EQUAL_TO       = 4,
    GREATER_THAN                = 5,
    GREATER_THAN_OR_EQUAL_TO    = 6,

See count explanation below

#### FriendConditionCount_0
#### FriendConditionCount_1
#### EnemyConditionCount_0
#### EnemyConditionCount_1

Compares number of eligible targets, either friendly or enemy that fulfilled condition respectively with corresponding operation against Count