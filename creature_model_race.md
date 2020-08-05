Back to [world database](mangosdb_struct) list of tables.

## The \`creature\_model\_race\` table

This table contains data to override displayed models based on the race
of the player. Use creature\_entry or modelid\_racial to specify the new
models, but not both.

### Structure

| Field                                                 | Type                  | Null | Key | Default | Extra |
| ----------------------------------------------------- | --------------------- | ---- | --- | ------- | ----- |
| [modelid](Creature_model_race#modelid)                | mediumint(8) unsigned | NO   | PRI | 0       |       |
| [racemask](Creature_model_race#racemask)              | mediumint(8) unsigned | NO   | PRI | 0       |       |
| [creature\_entry](Creature_model_race#creature_entry) | mediumint(8) unsigned | NO   |     | 0       |       |
| [modelid\_racial](Creature_model_race#modelid_racial) | mediumint(8) unsigned | NO   |     | 0       |       |

### Description of the fields

#### modelid

The model id to override with a different model.

#### racemask

The racemask you want to trigger the model override for.

#### creature\_entry

A creature\_template entry id - this will override the model using the
model(s) from the specified creature\_template entry.

#### modelid\_racial

The id of a specific model to use when overriding.
