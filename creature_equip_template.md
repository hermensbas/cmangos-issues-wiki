Back to [world database](mangosdb_struct) list of tables.

## The \`creature\_equip\_template\` table

creature_equip_template_raw has to be converted to this new file format!

This table contains all equipment mobs can wear.

### Structure

| Field                                              | Type                  | Null | Key | Default | Extra |
| -------------------------------------------------- | --------------------- | ---- | --- | ------- | ----- |
| [entry](Creature_equip_template#entry)             | int(11) unsigned      | NO   | PRI | 0       |       |
| [equipentry1](Creature_equip_template#equipentry1) | mediumint(8) unsigned | NO   |     | 0       |       |
| [equipentry2](Creature_equip_template#equipentry2) | mediumint(8) unsigned | NO   |     | 0       |       |
| [equipentry3](Creature_equip_template#equipentry3) | mediumint(8) unsigned | NO   |     | 0       |       |

### Description of the fields

#### entry

Unique Id of the equipment, no link with any official data. This id is
free.

#### equipentry1

This is the item of the equipment used in right hand (Mainhand) from
[\`item\_template\`.\`entry\`](https://github.com/cmangos/issues/wiki/item_template#entry).

Shields cant be set as equipentry1.

#### equipentry2

This is the item of the equipment used in left hand (Offhand) from
[\`item\_template\`.\`entry\`](https://github.com/cmangos/issues/wiki/item_template#entry).

#### equipentry3

This is the item of the equipment used in distance slot (Ranged). It
comes from
[\`item\_template\`.\`entry\`](https://github.com/cmangos/issues/wiki/item_template#entry).
