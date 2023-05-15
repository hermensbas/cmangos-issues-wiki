Back to [world database](mangosdb_struct) list of tables.

## The `unit_condition` table

Official table structure - used for condition checks on units

### Structure

| Field                           | Type             | NULL | Key     | Default | Comments                    |
| ------------------------------- | ---------------- | ---- | ------- | ------- | --------------------------- |
| Id          | int(11) unsigned | NO   | PRIMARY | 0       | Primary Key |
| Flags       | int(11) unsigned | NO   |         | 0       |             |
| Variable_0  | int(11) unsigned | NO   |         | 0       |             |
| Variable_1  | int(11) unsigned | NO   |         | 0       |             |
| Variable_2  | int(11) unsigned | NO   |         | 0       |             |
| Variable_3  | int(11) unsigned | NO   |         | 0       |             |
| Variable_4  | int(11) unsigned | NO   |         | 0       |             |
| Variable_5  | int(11) unsigned | NO   |         | 0       |             |
| Variable_6  | int(11) unsigned | NO   |         | 0       |             |
| Variable_7  | int(11) unsigned | NO   |         | 0       |             |
| Op_0        | int(11) unsigned | NO   |         | 0       |             |
| Op_1        | int(11) unsigned | NO   |         | 0       |             |
| Op_2        | int(11) unsigned | NO   |         | 0       |             |
| Op_3        | int(11) unsigned | NO   |         | 0       |             |
| Op_4        | int(11) unsigned | NO   |         | 0       |             |
| Op_5        | int(11) unsigned | NO   |         | 0       |             |
| Op_6        | int(11) unsigned | NO   |         | 0       |             |
| Op_7        | int(11) unsigned | NO   |         | 0       |             |
| Value_0     | int(11) unsigned | NO   |         | 0       |             |
| Value_1     | int(11) unsigned | NO   |         | 0       |             |
| Value_2     | int(11) unsigned | NO   |         | 0       |             |
| Value_3     | int(11) unsigned | NO   |         | 0       |             |
| Value_4     | int(11) unsigned | NO   |         | 0       |             |
| Value_5     | int(11) unsigned | NO   |         | 0       |             |
| Value_6     | int(11) unsigned | NO   |         | 0       |             |
| Value_7     | int(11) unsigned | NO   |         | 0       |             |

### Uses

[combat_condition](combat_condition)  
[creature_spell_targeting](creature_spell_targeting)  

### Description of the fields

#### Id

Numeric identifier

#### Flags

By default, multiple conditions are executed with AND operation. Possible to set UNIT_CONDITION_FLAG_OR to make them OR.

#### Variable_0
#### Variable_1
#### Variable_2
#### Variable_3
#### Variable_4
#### Variable_5
#### Variable_6
#### Variable_7

