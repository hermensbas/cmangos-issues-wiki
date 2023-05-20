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
    SESSILE                     = 0x00000100, - Synonymic to rooted, equivalent to dynamic Creature_ai_scripts - ACTION_T_SET_IMMOBILIZED_STATE
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
    NO_MELEE_FLEE               = 0x00100000, - Does not melee, if capable of moving, flees in combat immediately.
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

    NO_DAMAGE_HISTORY              = 0x00000001, - NYI
    DONT_PVP_ENABLE_OWNER          = 0x00000002, - NYI
    DO_NOT_FADE_IN                 = 0x00000004, - NYI
    MASK_UID                       = 0x00000008, - NYI
    SKIN_WITH_ENGINEERING          = 0x00000010, - NYI
    NO_AGGRO_ON_LEASH              = 0x00000020, - NYI
    NO_FRIENDLY_AREA_AURAS         = 0x00000040, - NYI
    EXTENDED_CORPSE_DURATION       = 0x00000080, - NYI
    CANNOT_SWIM                    = 0x00000100, - NYI
    TAMEABLE_EXOTIC                = 0x00000200, - NYI
    GIGANTIC_AOI                   = 0x00000400, - NYI
    INFINITE_AOI                   = 0x00000800, - NYI
    CANNOT_PENETRATE_WATER         = 0x00001000, - NYI
    NO_NAME_PLATE                  = 0x00002000, - NYI
    CHECKS_LIQUIDS                 = 0x00004000, - NYI
    NO_THREAT_FEEDBACK             = 0x00008000, - NYI
    USE_MODEL_COLLISION_SIZE       = 0x00010000, - NYI
    ATTACKER_IGNORES_FACING        = 0x00020000, - NYI
    ALLOW_INTERACTION_WHILE_IN_COMBAT = 0x00040000, - NYI
    SPELL_CLICK_FOR_PARTY_ONLY     = 0x00080000, - NYI
    FACTION_LEADER                 = 0x00100000, - NYI
    IMMUNE_TO_PLAYER_BUFFS         = 0x00200000, - NYI
    COLLIDE_WITH_MISSILES          = 0x00400000, - NYI
    CAN_BE_MULTITAPPED             = 0x00800000, - NYI
    DO_NOT_PLAY_MOUNTED_ANIMATIONS = 0x01000000, - NYI
    CANNOT_TURN                    = 0x02000000, - NYI
    ENEMY_CHECK_IGNORES_LOS        = 0x04000000, - NYI
    FOREVER_CORPSE_DURATION        = 0x08000000, - NYI
    PETS_ATTACK_WITH_3D_PATHING    = 0x10000000, - NYI
    LINK_ALL                       = 0x20000000, - NYI
    AI_CAN_AUTO_TAKEOFF_IN_COMBAT  = 0x40000000, - NYI
    AI_CAN_AUTO_LAND_IN_COMBAT     = 0x80000000  - NYI

### CreatureStaticFlags4

    NO_BIRTH_ANIM                            = 0x00000001, - NYI
    TREAT_AS_PLAYER_FOR_DIMINISHING_RETURNS  = 0x00000002, - NYI
    TREAT_AS_PLAYER_FOR_PVP_DEBUFF_DURATION  = 0x00000004, - NYI
    INTERACT_ONLY_WITH_CREATOR               = 0x00000008, - NYI
    DO_NOT_PLAY_UNIT_EVENT_SOUNDS            = 0x00000010, - NYI
    HAS_NO_SHADOW_BLOB                       = 0x00000020, - NYI
    DEALS_TRIPLE_DAMAGE_TO_PC_CONTROLLED_PETS = 0x00000040, - NYI
    NO_NPC_DAMAGE_BELOW_85PTC                = 0x00000080, - NYI
    OBEYS_TAUNT_DIMINISHING_RETURNS          = 0x00000100, - NYI
    NO_MELEE_APPROACH                        = 0x00000200, - NYI
    UPDATE_CREATURE_RECORD_WHEN_INSTANCE_CHANGES_DIFFICULTY = 0x00000400, - NYI
    CANNOT_DAZE                              = 0x00000800, - NYI
    FLAT_HONOR_AWARD                         = 0x00001000, - NYI
    IGNORE_LOS_WHEN_CASTING_ON_ME            = 0x00002000, - NYI
    GIVE_QUEST_KILL_CREDIT_WHILE_OFFLINE     = 0x00004000, - NYI
    TREAT_AS_RAID_UNIT_FOR_HELPFUL_SPELLS    = 0x00008000, - NYI
    DONT_REPOSITION_IF_MELEE_TARGET_IS_TOO_CLOSE = 0x00010000, - NYI
    PET_OR_GUARDIAN_AI_DONT_GO_BEHIND_TARGET = 0x00020000, - NYI
    MINUTE_5_LOOT_ROLL_TIMER                 = 0x00040000, - NYI
    FORCE_GOSSIP                             = 0x00080000, - NYI
    DONT_REPOSITION_WITH_FRIENDS_IN_COMBAT   = 0x00100000, - NYI
    DO_NOT_SHEATHE                           = 0x00200000, - NYI
    IGNORE_SPELL_MIN_RANGE_RESTRICTIONS      = 0x00400000, - NYI
    SUPPRESS_INSTANCE_WIDE_RELEASE_IN_COMBAT = 0x00800000, - NYI
    PREVENT_SWIM                             = 0x01000000, - NYI
    HIDE_IN_COMBAT_LOG                       = 0x02000000, - NYI
    ALLOW_NPC_COMBAT_WHILE_UNINTERACTIBLE    = 0x04000000, - NYI
    PREFER_NPCS_WHEN_SEARCHING_FOR_ENEMIES   = 0x08000000, - NYI
    ONLY_GENERATE_INITIAL_THREAT             = 0x10000000, - NYI
    DO_NOT_TARGET_ON_INTERACTION             = 0x20000000, - NYI
    DO_NOT_RENDER_OBJECT_NAME                = 0x40000000, - NYI
    QUEST_BOSS                               = 0x80000000  - NYI