Back to [world database](mangosdb_struct) list of tables.

## The `gameobject_addon` tables

holds individual gameobject data, which does not use default fallback values. This data along with the [`gameobject_template`.`entry`](https://github.com/cmangos/issues/wiki/gameobject_template) data is read and used to instantiate the objects in the world.

### Structure

| Field                                                | Type                  | Null | Key | Default | Extra |
| ---------------------------------------------------- | --------------------- | ---- | --- | ------- | ----- |
| [guid](gameobject_addon#guid)| int(10)|NO|PRIMARY KEY|NULL|gameobject guid|
| [animprogress](gameobject_addon#animprogress)|tinyint(3)|NO||100 (classic/tbc) / 255 (wotlk)|Setting nondefault animprogress|
| [state](gameobject_addon#state)|tinyint(4)|NO||-1 (default fallback value)|Setting nondefault state|
| [path_rotation0](gameobject_addon#path_rotation)|float|NO||0|wotlk+|
| [path_rotation1](gameobject_addon#path_rotation)|float|NO||0|wotlk+|
| [path_rotation2](gameobject_addon#path_rotation)|float|NO||0|wotlk+|
| [path_rotation3](gameobject_addon#path_rotation)|float|NO||0|wotlk+|
| [StringId](gameobject_addon#StringId)| int(10)|NO||0|StringId|

#### guid

The global unique identifier for the [`gameobject`.`guid`](https://github.com/cmangos/issues/wiki/gameobject). This field must be unique among all gameobjects.

#### animprogress

Default: 100 (classic/tbc) / 255 (wotlk)

#### state

Only for chests. 1 = closed, 0 = open

GAMEOBJECT_TYPE_DOOR, GAMEOBJECT_TYPE_BUTTON & GAMEOBJECT_TYPE_AURA_GENERATOR use data0 (startOpen) from their gameobject_template as default state.

gameobject_template StartsOpen is inverted, 1 in gameobject_template is actually 0 in state.

#### path_rotation

rotation value, wotlk+

