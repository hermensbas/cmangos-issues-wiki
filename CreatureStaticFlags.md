Back to [creature_template](https://github.com/cmangos/issues/wiki/creature_template).

Documentation for columns StaticFlags1, StaticFlags2, StaticFlags3, StaticFlags4 in all creature_template tables.

Enums from Entities/CreatureDefines.h

### CreatureStaticFlags

    MOUNTABLE                   = 0x00000001, - NYI
    NO_XP                       = 0x00000002,
    NO_LOOT                     = 0x00000004,
    UNKILLABLE                  = 0x00000008,
    TAMEABLE                    = 0x00000010, - NYI
    IMMUNE_TO_PC                = 0x00000020, - NYI
    IMMUNE_TO_NPC               = 0x00000040, - NYI
    CAN_WIELD_LOOT              = 0x00000080, - NYI
    SESSILE                     = 0x00000100, - NYI
    UNINTERACTIBLE              = 0x00000200, - NYI
    NO_AUTOMATIC_REGEN          = 0x00000400, - NYI
    DESPAWN_INSTANTLY           = 0x00000800, - NYI
    CORPSE_RAID                 = 0x00001000, - NYI
    CREATOR_LOOT                = 0x00002000, - NYI
    NO_DEFENSE                  = 0x00004000, - NYI
    NO_SPELL_DEFENSE            = 0x00008000, - NYI
    BOSS_MOB                    = 0x00010000, - NYI
    COMBAT_PING                 = 0x00020000, - NYI
    AQUATIC                     = 0x00040000, - NYI
    AMPHIBIOUS                  = 0x00080000, - NYI
    NO_MELEE                    = 0x00100000, - NYI
    VISIBLE_TO_GHOSTS           = 0x00200000, - NYI
    PVP_ENABLING                = 0x00400000, - NYI
    DO_NOT_PLAY_WOUND_ANIM      = 0x00800000, - NYI
    NO_FACTION_TOOLTIP          = 0x01000000, - NYI
    IGNORE_COMBAT               = 0x02000000, - NYI
    ONLY_ATTACK_PVP_ENABLING    = 0x04000000, - NYI
    CALLS_GUARDS                = 0x08000000, - NYI
    CAN_SWIM                    = 0x10000000, - NYI
    FLOATING                    = 0x20000000, - NYI
    MORE_AUDIBLE                = 0x40000000, - NYI
    LARGE_AOI                   = 0x80000000  - NYI

### CreatureStaticFlags2

    NO_PET_SCALING                      = 0x00000001, - NYI
    FORCE_PARTY_MEMBERS_INTO_COMBAT     = 0x00000002, - NYI
    LOCK_TAPPERS_TO_RAID_ON_DEATH       = 0x00000004, - NYI
    SPELL_ATTACKABLE                    = 0x00000008, - NYI
    NO_CRUSHING_BLOWS                   = 0x00000010,
    NO_OWNER_THREAT                     = 0x00000020, - NYI
    NO_WOUNDED_SLOWDOWN                 = 0x00000040,
    USE_CREATOR_BONUSES                 = 0x00000080, - NYI
    IGNORE_FEIGN_DEATH                  = 0x00000100,
    IGNORE_SANCTUARY                    = 0x00000200, - NYI
    ACTION_TRIGGERS_WHILE_CHARMED       = 0x00000400, - NYI
    INTERACT_WHILE_DEAD                 = 0x00000800, - NYI
    NO_INTERRUPT_SCHOOL_COOLDOWN        = 0x00001000, - NYI
    RETURN_SOUL_SHARD_TO_MASTER_OF_PET  = 0x00002000, - NYI
    SKIN_WITH_HERBALISM                 = 0x00004000, - NYI
    SKIN_WITH_MINING                    = 0x00008000, - NYI
    ALERT_CONTENT_TEAM_ON_DEATH         = 0x00010000, - NYI
    ALERT_CONTENT_TEAM_AT_90_PCT_HP     = 0x00020000, - NYI
    ALLOW_MOUNTED_COMBAT                = 0x00040000, - NYI
    PVP_ENABLING_OOC                    = 0x00080000, - NYI
    NO_DEATH_MESSAGE                    = 0x00100000, - NYI
    IGNORE_PATHING_FAILURE              = 0x00200000, - NYI
    FULL_SPELL_LIST                     = 0x00400000, - NYI
    DOES_NOT_REDUCE_REPUTATION_FOR_RAIDS = 0x00800000, - NYI
    IGNORE_MISDIRECTION                 = 0x01000000, - NYI
    HIDE_BODY                           = 0x02000000, - NYI
    SPAWN_DEFENSIVE                     = 0x04000000, - NYI
    SERVER_ONLY                         = 0x08000000, - NYI
    CAN_SAFE_FALL                       = 0x10000000, - NYI
    CAN_ASSIST                          = 0x20000000, - NYI
    NO_SKILL_GAINS                      = 0x40000000,
    NO_PET_BAR                          = 0x80000000  - NYI

### CreatureStaticFlags3

### CreatureStaticFlags4

