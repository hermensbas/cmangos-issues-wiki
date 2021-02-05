Spell in cMaNGOS is the essential object which is used for most purposes.

Each Spell has up to three effects, which have generic behaviour, determined by values in spell.dbc and then custom behaviour, that is scripted either using C++ or dbscripts_on_spell (this is restricted to DUMMY, SCRIPT_EFFECT spell effects).

Spell script can be anything ranging from triggering additional spells under certain conditions, to restricting targets of given spell.

Spell.dbc - is the source of spell definitions. Tells us what effects/values/targets etc a given spell has.
Description of Spell.dbc https://github.com/cmangos/issues/wiki/Spell.dbc

Triggered spells - There are 3 main kinds of triggered spells:
1. Event/AI triggered
2. Triggered by another spell (arcane missiles)
3. Triggered by aura (Talents/Blizzard)
Triggered spell setting influences many aspects of given spell. It skips cast time, cooldown checking, can target unselectable targets and more. Also these three kinds heavily influence PROCs, meaning in case of wrong usage, spells tend to not proc properly among other things (namely skipping safety checks).

Spell knowledge can be separated to several topics.
* Spell opcodes - these are the entry points and exit points for client interactions. SMSG_SPELL_START, SMSG_SPELL_GO, SMSG_CAST_RESULT are a few of the common ones. Item usage and controlling a pet are one of the less intuitive spell related opcodes.
* Spell checks - designed to either emulate client behaviour, so that client checks cannot be bypassed or emulate server behaviour, which is not present in client. This can be for example PvP trinket behaviour, which enables using the item in any situation, but server needs to prevent it in cases where PvP trinket cannot remove a certain effect. It is also responsible for "partial application", where lets say if a creature is disarm immune or has no weapon, the damage part from riposte (rogue attack) should still go through. Checks for stacking and attributes also belong to this category.
* Spell targeting - targeting is a heavy topic on its own. Mainly situated in SpellTargets.h and SpellTargets.cpp, and Spell::SetTargetMap, it works through the logic each target imposes. The naming goes as follows. Targets with LOCATION in them produce XYZ coordinates in some way, mainly SRC and DEST. Targets with UNIT or GAMEOBJECT or ITEM target these specific objects. A detailed description is in core array SpellTargetInfoTable.
* Spell effects - main core of spells, SpellEffects.cpp. These need to be viewed as premade core messages, rather than spells. Dummy or script effects are whatever the scripter imagines them to be. These range from a damage effect, to something as complex as cross map summoning.
* Spell auras - whereas effects are one-off executions, auras are persistent effects for their duration (which can be infinite). Here we have 2 divisions, normal auras, persistent ground auras (consecration) or area auras (paladin devotion aura). Second distinction is non-periodic and periodic auras. Auras very frequently are substituted for using a timer, because a periodic aura with a certain tick rate is meant to execute a given message.
* Spell scripting - enables scripting and customizing spells to the desired effect. Less common in vanilla but heavily utilized in wotlk. List of hooks for scripting can be found in SpellScript.h and examples can be found by searching SpellScript or AuraScript class in core. Critical for removing per spell logic from spell/aura systems so that scripts have all their code contained. 99% coverage of possibilities, but for example Last Stand Maximum HP setting on increase is still currently hardcoded.

Many internal actions are all implemented through spells. This is for example /stuck, binding a hearthstone, teleporting, recruit a friend summon, and various other ingame actions.

NOTE: Work in progress - Author - Killerwife