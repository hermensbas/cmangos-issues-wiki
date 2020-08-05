Back to [world database](mangosdb_struct) list of tables.

## The \`creature\_(template\_)addon\` tables

define different things that are applied on creatures when they are
loaded, either by
[\`creature\`.\`guid\`](https://github.com/cmangos/issues/wiki/Creature#guid)
or
[\`creature\_template\`.\`entry\`](https://github.com/cmangos/issues/wiki/Creature_template#entry).  
So two creatures using the same creature\_template\_addon can look
different, if one is additionally defined in creature\_addon.

Through the use of the fields in this table, many things can be changed
about the outward visual appearance of the creature. Potential usage
examples are: to have the creature be mounted, to have it emote
something, to have it display an aura effect, etc.

NOTE:

  - A creature\_addon record will override a creature\_template\_addon
    record should they overlap on the same creature.
  - The data for this table is largely incomplete and is mostly just a
    regurgitation of what the client receives from the server. This
    article is a WIP as to what all the possible values are.

### Structure

| Field                                                | Type                  | Null | Key | Default | Extra |
| ---------------------------------------------------- | --------------------- | ---- | --- | ------- | ----- |
| [entry/guid](creature_template_addon#entry/guid)     | mediumint(8) unsigned | NO   | PRI | 0       |       |
| [mount](creature_template_addon#mount)               | mediumint(8) unsigned | NO   |     | 0       |       |
| [bytes1](creature_template_addon#bytes1)             | int(10) unsigned      | NO   |     | 0       |       |
| [b2\_0\_sheath](creature_template_addon#b2_0_sheath) | tinyint(3) unsigned   | NO   |     | 0       |       |
| [b2\_1\_flags](creature_template_addon#b2_1_flags)   | tinyint(3) unsigned   | NO   |     | 0       |       |
| [emote](creature_template_addon#emote)               | mediumint(8) unsigned | NO   |     | 0       |       |
| [moveflags](creature_template_addon#moveflags)       | int(10) unsigned      | NO   |     | 0       |       |
| [auras](creature_template_addon#auras)               | text                  | YES  |     |         |       |

### Description of the fields

#### entry/guid

For creature\_template\_addon, this field signifies the creature
template ID. It will affect all spawned creatures using that template
ID. For creature\_addon, this field signifies a unique creature guid. It
will affect just that creature whose GUID matches the one specified
here.

#### mount

The model ID of the mount to be used to make the creature appear
mounted. The value here overrides the value for the creature’s unit
field UNIT\_FIELD\_MOUNTDISPLAYID. List of known values and what their
visual effects on the creature

#### bytes1

(UNIT\_FIELD\_BYTES\_1,0)

| Bit | Name                                   | Comment                                                             |
| --- | -------------------------------------- | ------------------------------------------------------------------- |
| 0   | UNIT\_STAND\_STATE\_STAND              | normal behavior                                                     |
| 1   | UNIT\_STAND\_STATE\_SIT                | sitting on ground                                                   |
| 2   | UNIT\_STAND\_STATE\_SIT\_CHAIR         | sitting on normal chair                                             |
| 3   | UNIT\_STAND\_STATE\_SLEEP              | sleeping                                                            |
| 4   | UNIT\_STAND\_STATE\_SIT\_LOW\_CHAIR    | sitting on low chair                                                |
| 5   | UNIT\_STAND\_STATE\_SIT\_MEDIUM\_CHAIR | sitting on medium chair                                             |
| 6   | UNIT\_STAND\_STATE\_SIT\_HIGH\_CHAIR   | sitting on high chair                                               |
| 7   | UNIT\_STAND\_STATE\_DEAD               | play dead                                                           |
| 8   | UNIT\_STAND\_STATE\_KNEEL              | kneel                                                               |
| 9   | UNIT\_STAND\_STATE\_CUSTOM             | Depends on model animation. Submerge, freeze, hide, hibernate, rest |

#### bytes1\_flags

(UNIT\_FIELD\_BYTES\_1,3) used instead of bytes1 in some cases.

| Flag     | Name                             | Comment                                                                                                                                       |
| -------- | -------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------- |
| 0x01     | UNIT\_BYTE1\_FLAG\_ALWAYS\_STAND | always stand state                                                                                                                            |
| 0x02     | UNIT\_BYTE1\_FLAG\_FLY\_ANIM     | Creature that can fly and are not on the ground appear to have this flag. If they are on the ground, flag is not present.                     |
| 0x04     | UNIT\_BYTE1\_FLAG\_UNTRACKABLE   | untrackable                                                                                                                                   |
| 65536    | ?                                | Linked to Defensive Stance? (not actively added flag?)                                                                                        |
| 131072   | ?                                | no name & health bar visible with plate mode on (name only when targeted) Linked to Stealth? Linked to DeathState? (not actively added flag?) |
| 1048576  | ?                                | Linked to Defensive Stance? (not actively added flag?)                                                                                        |
| 33554432 | ?                                | Linked to Stealth? (not actively added flag?)                                                                                                 |
| 0xFF     | UNIT\_BYTE1\_FLAG\_ALL           | all                                                                                                                                           |

#### b2\_0\_sheath

(UNIT\_FIELD\_BYTES\_2,0)

| Bit | Name                   | Comment                     |
| --- | ---------------------- | --------------------------- |
| 0   | SHEATH\_STATE\_UNARMED | all weapons sheathed        |
| 1   | SHEATH\_STATE\_MELEE   | melee weapon(s) unsheathed  |
| 2   | SHEATH\_STATE\_RANGED  | ranged weapon(s) unsheathed |

#### b2\_1\_flags

(UNIT\_FIELD\_BYTES\_2,1)

| Bit | Name                                           | Comment |
| --- | ---------------------------------------------- | ------- |
| 16  | UNIT\_BYTE2\_CREATURE\_DEBUFF\_LIMIT           | ?       |
| 40  | UNIT\_BYTE2\_PLAYER\_CONTROLLED\_DEBUFF\_LIMIT | ?       |

#### emote

Emote ID that the creature should continually perform.

COMPLETE LIST OF EMOTES CAN BE FOUND IN: Emotes.dbc  
(They Are Different Between Client Versions
[classic](https://github.com/cmangos/mangos-classic/blob/master/src/game/Globals/SharedDefines.h#L1091),
[tbc](https://github.com/cmangos/mangos-tbc/blob/master/src/game/Globals/SharedDefines.h#L1227),
[wotlk](https://github.com/cmangos/mangos-wotlk/blob/master/src/game/Globals/SharedDefines.h#L1418\))

| Bit | Name                                    | Bit | Name                                   |
| --- | --------------------------------------- | --- | -------------------------------------- |
| 0   | EMOTE\_ONESHOT\_NONE                    | 400 | EMOTE\_STATE\_DANCESPECIAL             |
| 1   | EMOTE\_ONESHOT\_TALK                    | 401 | EMOTE\_ONESHOT\_DANCESPECIAL           |
| 2   | EMOTE\_ONESHOT\_BOW                     | 402 | EMOTE\_ONESHOT\_CUSTOMSPELL01          |
| 3   | EMOTE\_ONESHOT\_WAVE                    | 403 | EMOTE\_ONESHOT\_CUSTOMSPELL02          |
| 4   | EMOTE\_ONESHOT\_CHEER                   | 404 | EMOTE\_ONESHOT\_CUSTOMSPELL03          |
| 5   | EMOTE\_ONESHOT\_EXCLAMATION             | 405 | EMOTE\_ONESHOT\_CUSTOMSPELL04          |
| 6   | EMOTE\_ONESHOT\_QUESTION                | 406 | EMOTE\_ONESHOT\_CUSTOMSPELL05          |
| 7   | EMOTE\_ONESHOT\_EAT                     | 407 | EMOTE\_ONESHOT\_CUSTOMSPELL06          |
| 10  | EMOTE\_STATE\_DANCE                     | 408 | EMOTE\_ONESHOT\_CUSTOMSPELL07          |
| 11  | EMOTE\_ONESHOT\_LAUGH                   | 409 | EMOTE\_ONESHOT\_CUSTOMSPELL08          |
| 12  | EMOTE\_STATE\_SLEEP                     | 410 | EMOTE\_ONESHOT\_CUSTOMSPELL09          |
| 13  | EMOTE\_STATE\_SIT                       | 411 | EMOTE\_ONESHOT\_CUSTOMSPELL10          |
| 14  | EMOTE\_ONESHOT\_RUDE                    | 412 | EMOTE\_STATE\_EXCLAIM                  |
| 15  | EMOTE\_ONESHOT\_ROAR                    | 415 | EMOTE\_STATE\_SIT\_CHAIR\_MED          |
| 16  | EMOTE\_ONESHOT\_KNEEL                   | 422 | EMOTE\_STATE\_SPELLEFFECT\_HOLD        |
| 17  | EMOTE\_ONESHOT\_KISS                    | 423 | EMOTE\_STATE\_EAT\_NO\_SHEATHE         |
| 18  | EMOTE\_ONESHOT\_CRY                     | 424 | EMOTE\_STATE\_MOUNT                    |
| 19  | EMOTE\_ONESHOT\_CHICKEN                 | 425 | EMOTE\_STATE\_READY2HL                 |
| 20  | EMOTE\_ONESHOT\_BEG                     | 426 | EMOTE\_STATE\_SIT\_CHAIR\_HIGH         |
| 21  | EMOTE\_ONESHOT\_APPLAUD                 | 427 | EMOTE\_STATE\_FALL                     |
| 22  | EMOTE\_ONESHOT\_SHOUT                   | 428 | EMOTE\_STATE\_LOOT                     |
| 23  | EMOTE\_ONESHOT\_FLEX                    | 429 | EMOTE\_STATE\_SUBMERGED\_NEW           |
| 24  | EMOTE\_ONESHOT\_SHY                     | 430 | EMOTE\_ONESHOT\_COWER                  |
| 25  | EMOTE\_ONESHOT\_POINT                   | 431 | EMOTE\_STATE\_COWER                    |
| 26  | EMOTE\_STATE\_STAND                     | 432 | EMOTE\_ONESHOT\_USESTANDING            |
| 27  | EMOTE\_STATE\_READYUNARMED              | 433 | EMOTE\_STATE\_STEALTH\_STAND           |
| 28  | EMOTE\_STATE\_WORK                      | 434 | EMOTE\_ONESHOT\_OMNICAST\_GHOUL        |
| 29  | EMOTE\_STATE\_POINT                     | 435 | EMOTE\_ONESHOT\_ATTACKBOW              |
| 30  | EMOTE\_STATE\_NONE                      | 436 | EMOTE\_ONESHOT\_ATTACKRIFLE            |
| 33  | EMOTE\_ONESHOT\_WOUND                   | 437 | EMOTE\_STATE\_SWIM\_IDLE               |
| 34  | EMOTE\_ONESHOT\_WOUNDCRITICAL           | 438 | EMOTE\_STATE\_ATTACK\_UNARMED          |
| 35  | EMOTE\_ONESHOT\_ATTACKUNARMED           | 439 | EMOTE\_ONESHOT\_SPELLCAST\_W\_SOUND    |
| 36  | EMOTE\_ONESHOT\_ATTACK1H                | 440 | EMOTE\_ONESHOT\_DODGE                  |
| 37  | EMOTE\_ONESHOT\_ATTACK2HTIGHT           | 441 | EMOTE\_ONESHOT\_PARRY1H                |
| 38  | EMOTE\_ONESHOT\_ATTACK2HLOOSE           | 442 | EMOTE\_ONESHOT\_PARRY2H                |
| 39  | EMOTE\_ONESHOT\_PARRYUNARMED            | 443 | EMOTE\_ONESHOT\_PARRY2HL               |
| 43  | EMOTE\_ONESHOT\_PARRYSHIELD             | 444 | EMOTE\_STATE\_FLYFALL                  |
| 44  | EMOTE\_ONESHOT\_READYUNARMED            | 445 | EMOTE\_ONESHOT\_FLYDEATH               |
| 45  | EMOTE\_ONESHOT\_READY1H                 | 446 | EMOTE\_STATE\_FLY\_FALL                |
| 48  | EMOTE\_ONESHOT\_READYBOW                | 447 | EMOTE\_ONESHOT\_FLY\_SIT\_GROUND\_DOWN |
| 50  | EMOTE\_ONESHOT\_SPELLPRECAST            | 448 | EMOTE\_ONESHOT\_FLY\_SIT\_GROUND\_UP   |
| 51  | EMOTE\_ONESHOT\_SPELLCAST               | 449 | EMOTE\_ONESHOT\_EMERGE                 |
| 53  | EMOTE\_ONESHOT\_BATTLEROAR              | 450 | EMOTE\_ONESHOT\_DRAGONSPIT             |
| 54  | EMOTE\_ONESHOT\_SPECIALATTACK1H         | 451 | EMOTE\_STATE\_SPECIALUNARMED           |
| 60  | EMOTE\_ONESHOT\_KICK                    | 452 | EMOTE\_ONESHOT\_FLYGRAB                |
| 61  | EMOTE\_ONESHOT\_ATTACKTHROWN            | 453 | EMOTE\_STATE\_FLYGRABCLOSED            |
| 64  | EMOTE\_STATE\_STUN                      | 454 | EMOTE\_ONESHOT\_FLYGRABTHROWN          |
| 65  | EMOTE\_STATE\_DEAD                      | 455 | EMOTE\_STATE\_FLY\_SIT\_GROUND         |
| 66  | EMOTE\_ONESHOT\_SALUTE                  | 456 | EMOTE\_STATE\_WALKBACKWARDS            |
| 68  | EMOTE\_STATE\_KNEEL                     | 457 | EMOTE\_ONESHOT\_FLYTALK                |
| 69  | EMOTE\_STATE\_USESTANDING               | 458 | EMOTE\_ONESHOT\_FLYATTACK1H            |
| 70  | EMOTE\_ONESHOT\_WAVE\_NOSHEATHE         | 459 | EMOTE\_STATE\_CUSTOMSPELL08            |
| 71  | EMOTE\_ONESHOT\_CHEER\_NOSHEATHE        | 460 | EMOTE\_ONESHOT\_FLY\_DRAGONSPIT        |
| 92  | EMOTE\_ONESHOT\_EAT\_NOSHEATHE          | 461 | EMOTE\_STATE\_SIT\_CHAIR\_LOW          |
| 93  | EMOTE\_STATE\_STUN\_NOSHEATHE           | 462 | EMOTE\_ONE\_SHOT\_STUN                 |
| 94  | EMOTE\_ONESHOT\_DANCE                   | 463 | EMOTE\_ONESHOT\_SPELLCAST\_OMNI        |
| 113 | EMOTE\_ONESHOT\_SALUTE\_NOSHEATH        | 465 | EMOTE\_STATE\_READYTHROWN              |
| 133 | EMOTE\_STATE\_USESTANDING\_NOSHEATHE    | 466 | EMOTE\_ONESHOT\_WORK\_CHOPWOOD         |
| 153 | EMOTE\_ONESHOT\_LAUGH\_NOSHEATHE        | 467 | EMOTE\_ONESHOT\_WORK\_MINING           |
| 173 | EMOTE\_STATE\_WORK\_NOSHEATHE           | 468 | EMOTE\_STATE\_SPELL\_CHANNEL\_OMNI     |
| 193 | EMOTE\_STATE\_SPELLPRECAST              | 469 | EMOTE\_STATE\_SPELL\_CHANNEL\_DIRECTED |
| 213 | EMOTE\_ONESHOT\_READYRIFLE              | 470 | EMOTE\_STAND\_STATE\_NONE              |
| 214 | EMOTE\_STATE\_READYRIFLE                | 471 | EMOTE\_STATE\_READYJOUST               |
| 233 | EMOTE\_STATE\_WORK\_NOSHEATHE\_MINING   | 473 | EMOTE\_STATE\_STRANGULATE              |
| 234 | EMOTE\_STATE\_WORK\_NOSHEATHE\_CHOPWOOD | 474 | EMOTE\_STATE\_READYSPELLOMNI           |
| 253 | EMOTE\_zzOLDONESHOT\_LIFTOFF            | 475 | EMOTE\_STATE\_HOLD\_JOUST              |
| 254 | EMOTE\_ONESHOT\_LIFTOFF                 | 476 | EMOTE\_ONESHOT\_CRY\_JAINA             |
| 273 | EMOTE\_ONESHOT\_YES                     |     |                                        |
| 274 | EMOTE\_ONESHOT\_NO                      |     |                                        |
| 275 | EMOTE\_ONESHOT\_TRAIN                   |     |                                        |
| 293 | EMOTE\_ONESHOT\_LAND                    |     |                                        |
| 313 | EMOTE\_STATE\_AT\_EASE                  |     |                                        |
| 333 | EMOTE\_STATE\_READY1H                   |     |                                        |
| 353 | EMOTE\_STATE\_SPELLKNEELSTART           |     |                                        |
| 373 | EMOTE\_STATE\_SUBMERGED                 |     |                                        |
| 374 | EMOTE\_ONESHOT\_SUBMERGE                |     |                                        |
| 375 | EMOTE\_STATE\_READY2H                   |     |                                        |
| 376 | EMOTE\_STATE\_READYBOW                  |     |                                        |
| 377 | EMOTE\_ONESHOT\_MOUNTSPECIAL            |     |                                        |
| 378 | EMOTE\_STATE\_TALK                      |     |                                        |
| 379 | EMOTE\_STATE\_FISHING                   |     |                                        |
| 380 | EMOTE\_ONESHOT\_FISHING                 |     |                                        |
| 381 | EMOTE\_ONESHOT\_LOOT                    |     |                                        |
| 382 | EMOTE\_STATE\_WHIRLWIND                 |     |                                        |
| 383 | EMOTE\_STATE\_DROWNED                   |     |                                        |
| 384 | EMOTE\_STATE\_HOLD\_BOW                 |     |                                        |
| 385 | EMOTE\_STATE\_HOLD\_RIFLE               |     |                                        |
| 386 | EMOTE\_STATE\_HOLD\_THROWN              |     |                                        |
| 387 | EMOTE\_ONESHOT\_DROWN                   |     |                                        |
| 388 | EMOTE\_ONESHOT\_STOMP                   |     |                                        |
| 389 | EMOTE\_ONESHOT\_ATTACKOFF               |     |                                        |
| 390 | EMOTE\_ONESHOT\_ATTACKOFFPIERCE         |     |                                        |
| 391 | EMOTE\_STATE\_ROAR                      |     |                                        |
| 392 | EMOTE\_STATE\_LAUGH                     |     |                                        |
| 393 | EMOTE\_ONESHOT\_CREATURE\_SPECIAL       |     |                                        |
| 394 | EMOTE\_ONESHOT\_JUMPLANDRUN             |     |                                        |
| 395 | EMOTE\_ONESHOT\_JUMPEND                 |     |                                        |
| 396 | EMOTE\_ONESHOT\_TALK\_NOSHEATHE         |     |                                        |
| 397 | EMOTE\_ONESHOT\_POINT\_NOSHEATHE        |     |                                        |
| 398 | EMOTE\_STATE\_CANNIBALIZE               |     |                                        |
| 399 | EMOTE\_ONESHOT\_JUMPSTART               |     |                                        |

#### moveflags

Flags controlling how the creature will behave animation-wise while
moving. <span style="color: red">This table is 100% wrong as of 3.1. It
is still here for a period of time for reference and to convert values
in DB.

See the proper table under this one</span>

| Bit        | Name                        | Comment                                                                                |
| ---------- | --------------------------- | -------------------------------------------------------------------------------------- |
| 0          | MOVEMENTFLAG\_NONE          |                                                                                        |
| 1          | MOVEMENTFLAG\_FORWARD       | instantly teleport creature, then creature move forward animation but no real movement |
| 2          | MOVEMENTFLAG\_BACKWARD      | instantly teleport creature, then creature move back animation but no real movement    |
| 4          | MOVEMENTFLAG\_STRAFE\_LEFT  | instantly teleport creature, then creature move left animation but no real movement    |
| 8          | MOVEMENTFLAG\_STRAFE\_RIGHT | instantly teleport creature, then creature move right animation but no real movement   |
| 16         | MOVEMENTFLAG\_LEFT          | creature spin left animation                                                           |
| 32         | MOVEMENTFLAG\_RIGHT         | then creature spin right animation                                                     |
| 64         | MOVEMENTFLAG\_PITCH\_UP     | no effect on creature                                                                  |
| 128        | MOVEMENTFLAG\_PITCH\_DOWN   | no effect on creature                                                                  |
| 256        | MOVEMENTFLAG\_RUN\_MODE     | If flag set then player runs                                                           |
| 512        | MOVEMENTFLAG\_ONTRANSPORT   | causes creatures to fly while moving (not include standing)                            |
| 1024       | MOVEMENTFLAG\_HOVERING      | hovering animation at stand (not include moving)                                       |
| 2048       | MOVEMENTFLAG\_FLY\_UNK1     |                                                                                        |
| 4096       | MOVEMENTFLAG\_JUMPING       | Jump animation                                                                         |
| 8192       | MOVEMENTFLAG\_UNK1          |                                                                                        |
| 16384      | MOVEMENTFLAG\_FALLING       | Falling                                                                                |
| 32768      | MOVEMENTFLAG\_UNK2          |                                                                                        |
| 65536      | MOVEMENTFLAG\_UNK3          |                                                                                        |
| 131072     | MOVEMENTFLAG\_UNK4          |                                                                                        |
| 262144     | MOVEMENTFLAG\_UNK5          |                                                                                        |
| 524288     | MOVEMENTFLAG\_UNK6          |                                                                                        |
| 1048576    | MOVEMENTFLAG\_UNK7          | Causes creature to instantly appear at new position                                    |
| 2097152    | MOVEMENTFLAG\_SWIMMING      | appears with fly flag also (causes creatures to fall to ground at stand state)         |
| 4194304    | MOVEMENTFLAG\_FLY\_UP       | no effect on creature                                                                  |
| 8388608    | MOVEMENTFLAG\_CAN\_FLY      | no effect on creature                                                                  |
| 16777216   | MOVEMENTFLAG\_FLYING        | no effect on creature                                                                  |
| 33554432   | MOVEMENTFLAG\_UNK8          | Creature flying (not hover at stop moving)                                             |
| 67108864   | MOVEMENTFLAG\_SPLINE        | probably wrong name (no effect on creature)                                            |
| 134217728  | MOVEMENTFLAG\_SPLINE2       | no effect on creature                                                                  |
| 268435456  | MOVEMENTFLAG\_WATERWALKING  | also prevent creature from falling under water                                         |
| 536870912  | MOVEMENTFLAG\_SAFE\_FALL    | active rogue safe fall spell (passive) (no effect on creature)                         |
| 1073741824 | MOVEMENTFLAG\_UNK9          | Causes creature to hover at stand state (not include moving)                           |
| 2147483648 | MOVEMENTFLAG\_UNK10         | Causes creature to roll to strange angle                                               |

<span style="color: red">Proper table as of 3.1</span>

| Bit        | Name                         | Comment                                                                                         |
| ---------- | ---------------------------- | ----------------------------------------------------------------------------------------------- |
| 0          | MONSTER\_MOVE\_NONE          | [InhabitType](creature_template#InhabitType) and [MovementType](creature_template#MovementType) |
| 1          | MONSTER\_MOVE\_FORWARD       | Instantly teleport creature, then creature move forward animation but no real movement          |
| 2          | MONSTER\_MOVE\_BACKWARD      | Instantly teleport creature, then creature move back animation but no real movement             |
| 4          | MONSTER\_MOVE\_STRAFE\_LEFT  | Instantly teleport creature, then creature move left animation but no real movement             |
| 8          | MONSTER\_MOVE\_STRAFE\_RIGHT | Instantly teleport creature, then creature move right animation but no real movement            |
| 16         | MONSTER\_MOVE\_LEFT          | Creature spin left animation                                                                    |
| 32         | MONSTER\_MOVE\_RIGHT         | Then creature spin right animation                                                              |
| 64         | MONSTER\_MOVE\_PITCH\_UP     | Seams to have no effect                                                                         |
| 128        | MONSTER\_MOVE\_PITCH\_DOWN   | Seams to have no effect                                                                         |
| 256        | MONSTER\_MOVE\_TELEPORT      | Makes creature teleport instead of walking                                                      |
| 512        | MONSTER\_MOVE\_TELEPORT2     | Makes creature a better Fly Animation (2.4.3)                                                   |
| 1024       | MONSTER\_MOVE\_LEVITATING    |                                                                                                 |
| 2048       | MONSTER\_MOVE\_UNK1          |                                                                                                 |
| 4096       | MONSTER\_MOVE\_WALK          | Makes creature walk                                                                             |
| 8192       | MONSTER\_MOVE\_SPLINE        |                                                                                                 |
| 16384      | No name in core              | Makes creature run                                                                              |
| 32768      | No name in core              | Makes creature run                                                                              |
| 65536      | No name in core              | Makes creature run                                                                              |
| 131072     | No name in core              | Makes creature run                                                                              |
| 262144     | MONSTER\_MOVE\_SPLINE2       |                                                                                                 |
| 524288     | MONSTER\_MOVE\_UNK2          | Used for flying mobs                                                                            |
| 1048576    | MONSTER\_MOVE\_UNK3          | Used for flying mobs                                                                            |
| 2097152    | MONSTER\_MOVE\_UNK4          |                                                                                                 |
| 4194304    | MONSTER\_MOVE\_UNK5          | Run in place, then teleport to final point                                                      |
| 8388608    | MONSTER\_MOVE\_UNK6          | Teleport                                                                                        |
| 16777216   | MONSTER\_MOVE\_UNK7          | Run                                                                                             |
| 33554432   | MONSTER\_MOVE\_FLY           | Swimming / Flying                                                                               |
| 67108864   | MONSTER\_MOVE\_UNK9          | Run                                                                                             |
| 134217728  | MONSTER\_MOVE\_UNK10         | Run                                                                                             |
| 268435456  | MONSTER\_MOVE\_UNK11         | Run                                                                                             |
| 536870912  | MONSTER\_MOVE\_UNK12         | Run                                                                                             |
| 1073741824 | MONSTER\_MOVE\_UNK13         | Levitating                                                                                      |

Note: MONSTER\_MOVE\_SPLINE\_FLY = MONSTER\_MOVE\_WALK +
MONSTER\_MOVE\_SPLINE and makes creature fly by points. Note2: Copy from
Mangos

#### auras

This field controls any auras to be applied on the creature (both in
effect and visually). To apply multiple auras, you can add more aura
entries, separating each entry by a space.

List of useful aura entries:

  - ‘16380’ - Makes the creature invisible.
  - ‘18950’ - Makes the creature detect other invisible units (players
    or creatures).
  - ‘37613’ - Casting teleport forever.
