Back to [world database](https://github.com/cmangos/issues/wiki/mangosdb_struct) list of tables.

## The `creature_immunities` table

is an extension to `creature_template`.`MechanicImmuneMask` and `creature_template`.`SchoolImmuneMask` and various `creature_template`.`ExtraFlags` which define a npcs Immunities to certain actions used on them.

These new Immunities can be pooled up into different Sets inbetween we can switch to dynamically change a mobs behavior against certain actions used on them.

(E.g a mob rides a horse, while he is riding that horse he uses `creature_immunities`.`SetId` = 0 which doesnt allow him to be sheeped. After he dismounts he switches to `creature_immunities`.`SetId` = 1 which removes this Immunity.)

### Structure

|Field|Type|Null|Key|Default|Comment|
|---|---|---|---|---|---|
|[Entry](https://github.com/cmangos/issues/wiki/creature_immunities#Entry)|int(10) unsigned|NO|Primary|0|creature_template entry|
|[SetId](https://github.com/cmangos/issues/wiki/creature_immunities#SetId)|int(10) unsigned|NO|Primary|0|immunity set ID|
|[Type](https://github.com/cmangos/issues/wiki/creature_immunities#Type)|tinyint(3)|NO|Primary|0|enum SpellImmunity|
|[Value](https://github.com/cmangos/issues/wiki/creature_immunities#Value)|int(10) unsigned|NO|Primary|0|value depending on type|

#### Entry

`creature_template`.`entry` of the npc.

#### SetId

SetId of the Immunityset to Summarize all different Immunities, Default: 0

#### Type

|Value|Name|Description|
|---|---|---|
|0|IMMUNITY_EFFECT|[enum SpellEffects](https://github.com/cmangos/issues/wiki/creature_immunities#SpellEffects)|
|1|IMMUNITY_STATE|[enum AuraType](https://github.com/cmangos/issues/wiki/creature_immunities#AuraType)|
|2|IMMUNITY_SCHOOL|[enum SpellSchoolMask](https://github.com/cmangos/issues/wiki/creature_immunities#SpellSchoolMask)|
|3|IMMUNITY_DAMAGE|[enum SpellSchoolMask](https://github.com/cmangos/issues/wiki/creature_immunities#SpellSchoolMask)|
|4|IMMUNITY_DISPEL|[enum DispelType](https://github.com/cmangos/issues/wiki/creature_immunities#DispelType)|
|5|IMMUNITY_MECHANIC|[enum SpellEffects](https://github.com/cmangos/issues/wiki/creature_immunities#Mechanics)|

#### Value

#### SpellEffects

#### AuraType

#### SpellSchoolMask

|Value|Name|Description|
|---|---|---|
|0|SPELL_SCHOOL_MASK_NONE|unused|
|1|SPELL_SCHOOL_MASK_NORMAL|Physical (Armor)|
|2|SPELL_SCHOOL_MASK_HOLY|Holy|
|4|SPELL_SCHOOL_MASK_FIRE|Fire|
|8|SPELL_SCHOOL_MASK_NATURE|Nature|
|16|SPELL_SCHOOL_MASK_FROST|Frost|
|32|SPELL_SCHOOL_MASK_SHADOW|Shadow|
|64|SPELL_SCHOOL_MASK_ARCANE|Arcane|

#### DispelType

|Value|Name|Description|
|---|---|---|
|0|DISPEL_NONE||
|1|DISPEL_MAGIC|Magic|
|2|DISPEL_CURSE|Curse|
|3|DISPEL_DISEASE|Disease|
|4|DISPEL_POISON|Poison|
|5|DISPEL_STEALTH|Stealth|
|6|DISPEL_INVISIBILITY|Invisibility|
|7|DISPEL_ALL|All|
|8|DISPEL_SPE_NPC_ONLY||
|9|DISPEL_ENRAGE|Enrage|
|10|DISPEL_ZG_TICKET||

##### Mechanics

|Value|Name|Description|
|---|---|---|
|0|MECHANIC_NONE||
|1|MECHANIC_CHARM||
|2|MECHANIC_DISORIENTED||
|3|MECHANIC_DISARM||
|4|MECHANIC_DISTRACT||
|5|MECHANIC_FEAR||
|6|MECHANIC_GRIP|MECHANIC_FUMBLE in tbc and classic|
|7|MECHANIC_ROOT||
|8|MECHANIC_PACIFY||
|9|MECHANIC_SILENCE||
|10|MECHANIC_SLEEP||
|11|MECHANIC_SNARE||
|12|MECHANIC_STUN||
|13|MECHANIC_FREEZE||
|14|MECHANIC_KNOCKOUT||
|15|MECHANIC_BLEED||
|16|MECHANIC_BANDAGE||
|17|MECHANIC_POLYMORPH||
|18|MECHANIC_BANISH||
|19|MECHANIC_SHIELD||
|20|MECHANIC_SHACKLE||
|21|MECHANIC_MOUNT||
|22|MECHANIC_INFECTED|MECHANIC_PERSUADE in tbc and classic|
|23|MECHANIC_TURN||
|24|MECHANIC_HORROR||
|25|MECHANIC_INVULNERABILITY||
|26|MECHANIC_INTERRUPT||
|27|MECHANIC_DAZE||
|28|MECHANIC_DISCOVERY||
|29|MECHANIC_IMMUNE_SHIELD||
|30|MECHANIC_SAPPED||
|31|MECHANIC_ENRAGED|wotlk only|

###### Examples

-- CREATURE_EXTRA_FLAG_NOT_TAUNTABLE
```
(entry, 0, 0, 114), -- SPELL_EFFECT_ATTACK_ME
(entry, 0, 1, 11), -- SPELL_AURA_MOD_TAUNT
```

-- CREATURE_EXTRA_FLAG_HASTE_SPELL_IMMUNITY
```
(entry, 0, 1, 216), -- SPELL_AURA_HASTE_SPELLS
```

-- CREATURE_EXTRA_FLAG_POISON_IMMUNITY
```
(entry, 0, 4, 4), -- DISPEL_POISON
```

-- Life Draining Effects (Mechanical Units)
```
(entry, 0, 0, 9), -- SPELL_EFFECT_HEALTH_LEECH
(entry, 0, 1, 53), -- SPELL_AURA_PERIODIC_LEECH
```