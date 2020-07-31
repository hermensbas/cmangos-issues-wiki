Back to [world database](mangosdb_struct) list of tables.

## The \`areatrigger\_tavern\` table

Enable a trigger when player enters a city or tavern. This causes the
player to enter a resting state.

### Structure

| Field                           | Type             | NULL | Key     | Default | Comments                    |
| ------------------------------- | ---------------- | ---- | ------- | ------- | --------------------------- |
| [id](areatrigger_tavern#id)     | int(11) unsigned | NO   | PRIMARY | 0       | Identifier, auto\_increment |
| [name](areatrigger_tavern#name) | text             | YES  |         |         |                             |

### Description of the fields

#### id

This is the trigger identifier, see
[[AreaTrigger.dbc]]

#### name

Name of the city or tavern. This is purely for descriptive purposes.
