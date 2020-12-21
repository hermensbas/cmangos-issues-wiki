Back to [world database](https://github.com/cmangos/issues/wiki/mangosdb_struct) list of tables.

## The `script_texts` table

holds all the texts used by core scripted creatures (ScriptDev). This table handles the actual text, display type (say/yell/emote) and corresponding sounds or emote (if any).

### Structure

|Field|Type|Attributes|Null|Default|Comments|
|--- |--- |--- |--- |--- |--- |
|[entry](https://github.com/cmangos/issues/wiki/script_texts#entry)|int(11)|signed|NO|0|Text Entry|
|[content_default](https://github.com/cmangos/issues/wiki/script_texts#content_default)|text||YES|NULL|Default Locale Text|
|[content_loc1](https://github.com/cmangos/issues/wiki/script_texts#content_loc)|text||YES|NULL|Locale 1 Text|
|[content_loc2](https://github.com/cmangos/issues/wiki/script_texts#content_loc)|text||YES|NULL|Locale 2 Text|
|[content_loc3](https://github.com/cmangos/issues/wiki/script_texts#content_loc)|text||YES|NULL|Locale 3 Text|
|[content_loc4](https://github.com/cmangos/issues/wiki/script_texts#content_loc)|text||YES|NULL|Locale 4 Text|
|[content_loc5](https://github.com/cmangos/issues/wiki/script_texts#content_loc)|text||YES|NULL|Locale 5 Text|
|[content_loc6](https://github.com/cmangos/issues/wiki/script_texts#content_loc)|text||YES|NULL|Locale 6 Text|
|[content_loc7](https://github.com/cmangos/issues/wiki/script_texts#content_loc)|text||YES|NULL|Locale 7 Text|
|[content_loc8](https://github.com/cmangos/issues/wiki/script_texts#content_loc)|text||YES|NULL|Locale 8 Text|
|[sound](https://github.com/cmangos/issues/wiki/script_texts#sound)|int(11)|unsigned|NO|0|Sound Id|
|[type](https://github.com/cmangos/issues/wiki/script_texts#type)|int(11)|unsigned|NO|0|Text Type|
|[language](https://github.com/cmangos/issues/wiki/script_texts#language)|int(11)|unsigned|NO|0|Text Language|
|[emote](https://github.com/cmangos/issues/wiki/script_texts#emote)|int(11)|unsigned|NO|0|Emote Id|
|[comment](https://github.com/cmangos/issues/wiki/script_texts#comment)|text||YES|NULL|Comment|

### Description of the fields

#### entry

This is the entry of the text. It corresponds to a cpp script using DoScriptText(); to display the text. This number is always negative.

#### content_default

This is the actual text presented in the default language (English).

#### content_loc

This is the actual text presented in the Localization #(1-8) Clients

|Value|Localization|
|--- |--- |
|1|Korean|
|2|French|
|3|German|
|4|Chinese|
|5|Taiwanese|
|6|Spanish|
|7|Spanish Mexico|
|8|Russian|

#### sound

This is the sound Id that will play with along with the corresponding text. All sounds are from [SoundEntries.dbc](https://github.com/cmangos/issues/wiki/SoundEntries.dbc).

#### type

This is the method the text is displayed.

| Value | Type            | Original Value                              | Example                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| ----- | --------------- | ------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 0     | Say             | 12 (MonsterSay)                             | ![](https://api.media.atlassian.com/file/4bb2a4e1-1fdf-4491-8bfb-ffa4dd9c53d1/binary?token=eyJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJmNDFkYTNhMC00MmQ0LTRlNmMtOTFmYS1lNjBlM2UyYzY0ZmYiLCJhY2Nlc3MiOnsidXJuOmZpbGVzdG9yZTpmaWxlOjRiYjJhNGUxLTFmZGYtNDQ5MS04YmZiLWZmYTRkZDljNTNkMSI6WyJyZWFkIl19LCJleHAiOjE2MDg2NDE1MzksIm5iZiI6MTYwODU1ODU1OX0.c3j1IaBEyX8J9Jds2oHu2N9U9iiUIl6dJU6wamkoERk&client=f41da3a0-42d4-4e6c-91fa-e60e3e2c64ff&name=Say.png&max-age=2940)         |
| 1     | Yell            | 14 (MonsterYell)                            | ![](https://api.media.atlassian.com/file/62e7a89e-2f8f-494a-96ac-87f5ca116a08/binary?token=eyJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJmNDFkYTNhMC00MmQ0LTRlNmMtOTFmYS1lNjBlM2UyYzY0ZmYiLCJhY2Nlc3MiOnsidXJuOmZpbGVzdG9yZTpmaWxlOjYyZTdhODllLTJmOGYtNDk0YS05NmFjLTg3ZjVjYTExNmEwOCI6WyJyZWFkIl19LCJleHAiOjE2MDg2NDE1MzksIm5iZiI6MTYwODU1ODU1OX0.0arnB76K2yH988x2Vt-0TozgDNAZurEUc7tHnfsz824&client=f41da3a0-42d4-4e6c-91fa-e60e3e2c64ff&name=Yell.png&max-age=2940)        |
| 2     | Text Emote      | 16 (MonsterEmote)                           | ![](https://api.media.atlassian.com/file/3e5105dc-a309-4147-95b2-cb814a52c247/binary?token=eyJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJmNDFkYTNhMC00MmQ0LTRlNmMtOTFmYS1lNjBlM2UyYzY0ZmYiLCJhY2Nlc3MiOnsidXJuOmZpbGVzdG9yZTpmaWxlOjNlNTEwNWRjLWEzMDktNDE0Ny05NWIyLWNiODE0YTUyYzI0NyI6WyJyZWFkIl19LCJleHAiOjE2MDg2NDE1MzksIm5iZiI6MTYwODU1ODU1OX0.vYh2axnaLgbe9Jp_JFBravCvSgt39DJAM5uvzCCYgT0&client=f41da3a0-42d4-4e6c-91fa-e60e3e2c64ff&name=Emote.png&max-age=2940)       |
| 3     | Boss Emote      | 41 (RaidBossEmote)                          | ![](https://api.media.atlassian.com/file/73565156-c9d9-442c-97a4-6bfdf41f6eaa/binary?token=eyJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJmNDFkYTNhMC00MmQ0LTRlNmMtOTFmYS1lNjBlM2UyYzY0ZmYiLCJhY2Nlc3MiOnsidXJuOmZpbGVzdG9yZTpmaWxlOjczNTY1MTU2LWM5ZDktNDQyYy05N2E0LTZiZmRmNDFmNmVhYSI6WyJyZWFkIl19LCJleHAiOjE2MDg2NDE1MzksIm5iZiI6MTYwODU1ODU1OX0.k0iyrjALeooxc6b9q2UZxH-FHxuPqjHiytj9ovAqVJs&client=f41da3a0-42d4-4e6c-91fa-e60e3e2c64ff&name=BossEmote.png&max-age=2940)   |
| 4     | Whisper         | 15 (MonsterWhisper)                         | ![](https://api.media.atlassian.com/file/f083d843-9783-4ac7-abbd-6dc497b5fefb/binary?token=eyJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJmNDFkYTNhMC00MmQ0LTRlNmMtOTFmYS1lNjBlM2UyYzY0ZmYiLCJhY2Nlc3MiOnsidXJuOmZpbGVzdG9yZTpmaWxlOmYwODNkODQzLTk3ODMtNGFjNy1hYmJkLTZkYzQ5N2I1ZmVmYiI6WyJyZWFkIl19LCJleHAiOjE2MDg2NDE1MzksIm5iZiI6MTYwODU1ODU1OX0.PDxoc8LL1xGmZrJxSdXAMNkVNPtQNa8El9Y7zGgOG88&client=f41da3a0-42d4-4e6c-91fa-e60e3e2c64ff&name=Whisper.png&max-age=2940)     |
| 5     | Boss Whisper    | 42 (RaidBossWhisper)                        | ![](https://api.media.atlassian.com/file/9e81e115-8dc0-4f6b-bf03-478d4254c0e5/binary?token=eyJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJmNDFkYTNhMC00MmQ0LTRlNmMtOTFmYS1lNjBlM2UyYzY0ZmYiLCJhY2Nlc3MiOnsidXJuOmZpbGVzdG9yZTpmaWxlOjllODFlMTE1LThkYzAtNGY2Yi1iZjAzLTQ3OGQ0MjU0YzBlNSI6WyJyZWFkIl19LCJleHAiOjE2MDg2NDE1MzksIm5iZiI6MTYwODU1ODU1OX0.XkTx1o4J7x6iaNYvFmTjo8BzDwIYVGl70faJB4AiMJE&client=f41da3a0-42d4-4e6c-91fa-e60e3e2c64ff&name=BossWhisper.png&max-age=2940) |
| 6     | Zone Yell       | 14 (MonsterYell) with zone wide visibility  | ![](https://api.media.atlassian.com/file/62e7a89e-2f8f-494a-96ac-87f5ca116a08/binary?token=eyJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJmNDFkYTNhMC00MmQ0LTRlNmMtOTFmYS1lNjBlM2UyYzY0ZmYiLCJhY2Nlc3MiOnsidXJuOmZpbGVzdG9yZTpmaWxlOjYyZTdhODllLTJmOGYtNDk0YS05NmFjLTg3ZjVjYTExNmEwOCI6WyJyZWFkIl19LCJleHAiOjE2MDg2NDE1MzksIm5iZiI6MTYwODU1ODU1OX0.0arnB76K2yH988x2Vt-0TozgDNAZurEUc7tHnfsz824&client=f41da3a0-42d4-4e6c-91fa-e60e3e2c64ff&name=Yell.png&max-age=2940)        |
| 7     | Zone Text Emote | 16 (MonsterEmote) with zone wide visibility | ![](https://api.media.atlassian.com/file/3e5105dc-a309-4147-95b2-cb814a52c247/binary?token=eyJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJmNDFkYTNhMC00MmQ0LTRlNmMtOTFmYS1lNjBlM2UyYzY0ZmYiLCJhY2Nlc3MiOnsidXJuOmZpbGVzdG9yZTpmaWxlOjNlNTEwNWRjLWEzMDktNDE0Ny05NWIyLWNiODE0YTUyYzI0NyI6WyJyZWFkIl19LCJleHAiOjE2MDg2NDE1MzksIm5iZiI6MTYwODU1ODU1OX0.vYh2axnaLgbe9Jp_JFBravCvSgt39DJAM5uvzCCYgT0&client=f41da3a0-42d4-4e6c-91fa-e60e3e2c64ff&name=Emote.png&max-age=2940)   |

#### language

This is the ingame language of the text. Languages are from [Languages.dbc](https://github.com/cmangos/issues/wiki/Languages.dbc).

|ID|Name|Description|
|--- |--- |--- |
|0|UNIVERSAL|Text in this language is understood by ALL Races.|
|1|ORCISH|Text in this language is understood ONLY by Horde Races.|
|2|DARNASSIAN|Text in this language is understood ONLY by the Night Elf Race.|
|3|TAURAHE|Text in this language is understood ONLY by the Tauren Race.|
|6|DWARVISH|Text in this language is understood ONLY by the Dwarf Race.|
|7|COMMON|Text in this language is understood ONLY by Alliance Races.|
|8|DEMONIC|Text in this language is understood ONLY by the Demon Race (Not Implemented).|
|9|TITAN|This language was used by Sargeras to speak with other Titians (Not Implemented).|
|10|THALASSIAN|Text in this language is understood ONLY by the Blood Elf Race.|
|11|DRACONIC|Text in this language is understood ONLY by the Dragon Race.|
|12|KALIMAG|Text will display as Kalimag (not readable by players, language of all elementals)|
|13|GNOMISH|Text in this language is understood ONLY by the Gnome Race.|
|14|TROLL|Text in this language is understood ONLY by the Troll Race.|
|33|GUTTERSPEAK|Text in this language is understood ONLY by the Undead Race.|
|35|DRAENEI|Text in this language is understood ONLY by the Draenai Race.|
|36|ZOMBIE|(not currently used?)|
|37|GNOMISH BINARY|Binary language used by Alliance when drinking Binary Brew|
|38|GOBLIN BINARY|Binary language used by Horce when drinking Binary Brew|                                                                                                    

#### emote

This is the emote that the creature performs along with the corresponding text.

#### comment

This field allows you to label a text entry.
