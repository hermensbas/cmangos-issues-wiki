Back to [world database](mangosdb_struct) list of tables.

## The `string_id` table

This table contains id and string connection between string_id variables

### Structure

| Field                           | Type             | NULL | Key     | Default | Comments                    |
| ------------------------------- | ---------------- | ---- | ------- | ------- | --------------------------- |
| [Id]     | int(11) unsigned | NO   | PRIMARY | 0       | Primary Key |
| [Name]   | varchar(255) | YES  |         |         |                             |

### Description of the fields

#### Id

Numeric identifier of string_id variable

#### Name

String identifier of string_id variable

### Uses

Targeting for [dbscripts](dbscripts)