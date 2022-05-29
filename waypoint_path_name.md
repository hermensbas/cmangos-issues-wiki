Back to [world database](mangosdb_struct) list of tables.

## The `waypoint_path_name` tables

Hold name and description for waypoint_path paths.

### Structure

| Field                                                | Type                  | Null | Key | Default | Extra |
| ---------------------------------------------------- | --------------------- | ---- | --- | ------- | ----- |
| [PathId](waypoint_path_name#PathId)| int(11)|NO|PRIMARY KEY|NULL|PathId from waypoint_path |
| [Name](waypoint_path_name#Name)|VARCHAR(200)|NO||NULL|Name and use path|

#### PathId

PathId from waypoint_path.

#### Name

Name and use of path. Example: ThousandNeedles - Kanati Greycloud - Escort path


Mainly a bookkeeping table for naming and documenting uses. We are introducing magic numbers based on various rules and need to know what each is for. Refer to correct Id use at [`waypoint_path`](https://github.com/cmangos/issues/wiki/waypoint_path)

