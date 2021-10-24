Back to [world database](https://github.com/cmangos/issues/wiki/mangosdb_struct) list of tables.

## The `broadcast_text` table

holds all texts previously held by `dbscript_string`, `creature_ai_texts` and more.

There are even unused texts in this table, which indicate missing scripts / missing variety of texts a npc can use.

### Structure

| Field| Type| Null| Key| Default| Comment|
| ---|---| ---|--- |--- |--- |
|[Id](https://github.com/cmangos/issues/wiki/broadcast_text#Id)|int(11) unsigned|NO|Primary Key|0|Primary Key|
|[Text](https://github.com/cmangos/issues/wiki/broadcast_text#Text)|NULL|YES|NULL|0|Male text|
|[Text1](https://github.com/cmangos/issues/wiki/broadcast_text#Text1)|NULL|YES|NULL|0|Female text|
|[ChatTypeID](https://github.com/cmangos/issues/wiki/broadcast_text#ChatTypeID)|int(11) unsigned|YES|NULL|0|Text Type - enum ChatMsg|
|[LanguageID](https://github.com/cmangos/issues/wiki/broadcast_text#LanguageID)|int(11) unsigned|YES|NULL|0|Text Language - enum Language|
|[ConditionID](https://github.com/cmangos/issues/wiki/broadcast_text#ConditionID)|int(11) unsigned|YES|NULL|0|Unused|
|[EmotesID](https://github.com/cmangos/issues/wiki/broadcast_text#EmotesID)|int(11) unsigned|YES|NULL|0|Unused|
|[Flags](https://github.com/cmangos/issues/wiki/broadcast_text#Flags)|int(11) unsigned|YES|NULL|0|Unused|
|[SoundEntriesID1](https://github.com/cmangos/issues/wiki/broadcast_text#SoundEntriesID1)|int(11) unsigned|YES|NULL|0|Sound on broadcast (male?)|
|[SoundEntriesID2](https://github.com/cmangos/issues/wiki/broadcast_text#SoundEntriesID2)|int(11) unsigned|YES|NULL|0|Sound on broadcast (female?) - Unused|
|[EmoteID1](https://github.com/cmangos/issues/wiki/broadcast_text#EmoteID1)|int(11) unsigned|YES|NULL|0|Emote on gossip|
|[EmoteID2](https://github.com/cmangos/issues/wiki/broadcast_text#EmoteID2)|int(11) unsigned|YES|NULL|0|Emote on gossip|
|[EmoteID3](https://github.com/cmangos/issues/wiki/broadcast_text#EmoteID3)|int(11) unsigned|YES|NULL|0|Emote on gossip|
|[EmoteDelay1](https://github.com/cmangos/issues/wiki/broadcast_text#EmoteDelay1)|int(11) unsigned|YES|NULL|0|Emote delay on gossip|
|[EmoteDelay2](https://github.com/cmangos/issues/wiki/broadcast_text#EmoteDelay2)|int(11) unsigned|YES|NULL|0|Emote delay on gossip|
|[EmoteDelay3](https://github.com/cmangos/issues/wiki/broadcast_text#EmoteDelay3)|int(11) unsigned|YES|NULL|0|Emote delay on gossip|
|[VerifiedBuild](https://github.com/cmangos/issues/wiki/broadcast_text#VerifiedBuild)|int(11) unsigned|YES|NULL|0|Build of bruteforce|

#### Id

Primary Key

#### ChatTypeID

This is the text type of the text. "enum ChatMsg"

| Value | Type            | Original Value                              | Example                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| ----- | --------------- | ------------------------------------------- |--- |
| 0     | Say             | 12 (MonsterSay)                             |![0](https://user-images.githubusercontent.com/19734826/138616964-f9fb1236-9c01-48be-9e83-73a0afe10a9b.PNG)|
| 1     | Yell            | 14 (MonsterYell)                            |![1](https://user-images.githubusercontent.com/19734826/138617141-910ced5f-51b3-4f85-86f9-2e555519b429.PNG)|
| 2     | Text Emote      | 16 (MonsterEmote)                           |![2](https://user-images.githubusercontent.com/19734826/138617095-62faa8d0-d672-4037-816c-69dd40798fbd.PNG)|
| 3     | Boss Emote      | 41 (RaidBossEmote)                          |![3](https://user-images.githubusercontent.com/19734826/138617067-a64ea29b-cf2b-48ce-aed9-188e9670ecc7.PNG)|
| 4     | Whisper         | 15 (MonsterWhisper)                         |![4](https://user-images.githubusercontent.com/19734826/138616538-cafa389e-7137-4db8-90cf-09729f9e5070.PNG)|
| 5     | Boss Whisper    | 42 (RaidBossWhisper)                        |![5](https://user-images.githubusercontent.com/19734826/138616695-bbdb1a16-d8ed-47a3-9bc0-a0eb4d3e0292.PNG)|
| 6     | Zone Yell       | 14 (MonsterYell) with zone wide visibility  |![6](https://user-images.githubusercontent.com/19734826/138617046-880f53b1-3b7e-4e6b-8980-aab7110f51ed.PNG)|
| 7     | Zone Text Emote | 16 (MonsterEmote) with zone wide visibility |![7](https://user-images.githubusercontent.com/19734826/138616999-37cf898a-bd3d-467d-8e65-b180f78545b8.PNG)|

#### LanguageID

This is the ingame language of the text. "enum Language"

| ID | Name           | Description                                                                        |
| -- | -------------- | ---------------------------------------------------------------------------------- |
| 0  | UNIVERSAL      | Text in this language is understood by ALL Races.                                  |
| 1  | ORCISH         | Text in this language is understood ONLY by Horde Races.                           |
| 2  | DARNASSIAN     | Text in this language is understood ONLY by the Night Elf Race.                    |
| 3  | TAURAHE        | Text in this language is understood ONLY by the Tauren Race.                       |
| 6  | DWARVISH       | Text in this language is understood ONLY by the Dwarf Race.                        |
| 7  | COMMON         | Text in this language is understood ONLY by Alliance Races.                        |
| 8  | DEMONIC        | Text in this language is understood ONLY by the Demon Race (Not Implemented).      |
| 9  | TITAN          | This language was used by Sargeras to speak with other Titians (Not Implemented).  |
| 10 | THALASSIAN     | Text in this language is understood ONLY by the Blood Elf Race.                    |
| 11 | DRACONIC       | Text in this language is understood ONLY by the Dragon Race.                       |
| 12 | KALIMAG        | Text will display as Kalimag (not readable by players, language of all elementals) |
| 13 | GNOMISH        | Text in this language is understood ONLY by the Gnome Race.                        |
| 14 | TROLL          | Text in this language is understood ONLY by the Troll Race.                        |
| 33 | GUTTERSPEAK    | Text in this language is understood ONLY by the Undead Race.                       |
| 35 | DRAENEI        | Text in this language is understood ONLY by the Draenai Race.                      |
| 36 | ZOMBIE         | (not currently used?)                                                              |
| 37 | GNOMISH BINARY | Binary language used by Alliance when drinking Binary Brew                         |
| 38 | GOBLIN BINARY  | Binary language used by Horce when drinking Binary Brew                            |