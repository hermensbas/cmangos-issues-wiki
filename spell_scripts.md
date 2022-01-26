Table spell_scripts:  
Id - Spell Id from spell_template  
ScriptName - Assigned script name in core  

Assignment .sql file located in each repo under sql/scriptdev2/spell.sql  

Used to add custom behaviour to any spell. List of all available hooks can be found in core in SpellScript.h. This file contains a thorough explanation of when they occur. There are two types, SpellScript or AuraScript. Both auras have a plethora of examples available. Almost all variables which are meant to be alterable in spellscripts have an appropriate public function in Spell, Aura and SpellAuraHolder. Currently there is no DB equivalent to this system, mainly due to reverse engineering.

Examples:

Registering a script works using functions RegisterSpellScript, RegisterAuraScript or RegisterScript(this one is when its both aura and spellscript). By searching for these functions its also possible to find hundreds of examples.  
Code example of registering:  
```cpp
RegisterSpellScript<EntangleFankriss>("spell_entangle_fankriss");
```

The above registers the script to ScriptName "spell_entangle_fankriss".  
And this is its script:  
```cpp
struct EntangleFankriss : public SpellScript
{
    void OnEffectExecute(Spell* spell, SpellEffectIndex effIdx) const override
    {
        if (effIdx == EFFECT_INDEX_0)
        {
            uint32 spellId = 0;
            switch (spell->m_spellInfo->Id)
            {
                default:
                case SPELL_ENTANGLE_1: spellId = SPELL_SPAWN_VEKNISS_HATCHLING_1; break;
                case SPELL_ENTANGLE_2: spellId = SPELL_SPAWN_VEKNISS_HATCHLING_2; break;
                case SPELL_ENTANGLE_3: spellId = SPELL_SPAWN_VEKNISS_HATCHLING_3; break;
            }
            spell->GetCaster()->CastSpell(nullptr, spellId, TRIGGERED_OLD_TRIGGERED);
        }
    }
};
```
This script picks a spell, based on which spell is casting it, to be cast and caster casts it when Effect 0 is executed. It is used by three spells with similar behaviour hence the switch case.  

```cpp
struct GammeritaTurtleCamera : public SpellScript
{
    SpellCastResult OnCheckCast(Spell* spell, bool /*strict*/) const override
    {
        Unit* target = spell->m_targets.getUnitTarget();
        // Gammerita Turtle Camera can be cast only on this target
        if (!target || target->GetEntry() != 7977)
            return SPELL_FAILED_BAD_TARGETS;

        return SPELL_CAST_OK;
    }
};
```
This script restricts it to only work on Gammerita. There are many single target quest or other custom spells which need to work only on a specific target.  

```cpp
struct CallOfTheBeast : public AuraScript
{
    void OnApply(Aura* aura, bool apply) const override
    {
        if (apply)
            aura->GetTarget()->CastSpell(nullptr, SPELL_CALL_OF_THE_BEAST, TRIGGERED_OLD_TRIGGERED);
    }
};
```
This script triggers a cast of another spell on receiving an aura. A very common occurence.  