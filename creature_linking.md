Back to [world database](mangosdb_struct) list of tables.  
To link creatures by entry, please refer to
[creature\_linking\_template](creature_linking_template)

## The \`creature\_linking\` table

### Structure

| Name                                         | Type                  | Null | Key | Default | Extra | Comment                                       |
| -------------------------------------------- | --------------------- | ---- | --- | ------- | ----- | --------------------------------------------- |
| [guid](creature_linking#guid)                | int(10) unsigned      | NO   | PRI | 0       |       | creature.guid of the slave mob that is linked |
| [master\_guid](creature_linking#master_guid) | int(10) unsigned      | NO   |     | 0       |       | master to trigger events                      |
| [flag](creature_linking#flag)                | mediumint(8) unsigned | NO   |     | 0       |       | flag - describing what should happen when     |

### Description of the fields

#### guid

[creature.guid](creature#guid) of the slave mob that is linked

#### master\_guid

[creature.guid](creature#guid) of the master to trigger events

#### flag

flag - describing what should happen when

| Flag  | Name                                     | Comment                                                                           |
| ----- | ---------------------------------------- | --------------------------------------------------------------------------------- |
| 1     | FLAG\_AGGRO\_ON\_AGGRO                   | the "slave\&quot; aggroes when the "master\&quot; aggroes                         |
| 2     | FLAG\_TO\_AGGRO\_ON\_AGGRO               | the master aggroes when the slave aggroes                                         |
| 4     | FLAG\_RESPAWN\_ON\_EVADE                 | the slave respawns when the master evades                                         |
| 8     | FLAG\_TO\_RESPAWN\_ON\_EVADE             | the master respawns when the slave evades                                         |
| 16    | FLAG\_DESPAWN\_ON\_DEATH                 | the slave despawns when the master dies                                           |
| 32    | FLAG\_SELFKILL\_ON\_DEATH                | the slave goes suicide when the master dies                                       |
| 64    | FLAG\_RESPAWN\_ON\_DEATH                 | the slave respawn when the master dies                                            |
| 128   | FLAG\_RESPAWN\_ON\_RESPAWN               | the slave respawns on master respawn                                              |
| 256   | FLAG\_DESPAWN\_ON\_RESPAWN               | the slave despawns on master respawn (TODO: check for slave \!= master)           |
| 512   | FLAG\_FOLLOW                             | the slave follows the master, very basic, see TODO notes in commit, or post below |
| 1024  | FLAG\_CANT\_SPAWN\_IF\_BOSS\_DEAD        | the slave cannot respawn while boss is dead                                       |
| 2048  | FLAG\_CANT\_SPAWN\_IF\_BOSS\_ALIVE       | the slave cannot respawn while boss is alive                                      |
| 4096  | FLAG\_DESPAWN\_ON\_EVADE                 | the slave despawn after the master evade                                          |
| 8192  | FLAG\_DESPAWN\_ON\_DESPAWN               | the slave despawn after the master despawns                                       |
| 16384 | FLAG\_EVADE\_ON\_EVADE                   | the slave evades on master evade                                                  |
