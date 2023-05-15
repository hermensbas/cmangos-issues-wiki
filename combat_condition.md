Back to [world database](https://github.com/cmangos/issues/wiki/mangosdb_struct) list of tables.

## The `combat_condition` table

Official table structure - used for combat condition checks on units for [creature_spell_list](creature_spell_list)

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