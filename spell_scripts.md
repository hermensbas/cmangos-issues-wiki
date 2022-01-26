Table spell_scripts:  
Id - Spell Id from spell_template  
ScriptName - Assigned script name in core  

Assignment .sql file located in each repo under sql/scriptdev2/spell.sql  

Used to add custom behaviour to any spell. List of all available hooks can be found in core in SpellScript.h. There are two types, SpellScript or AuraScript.

Examples:

Registering a script works using functions RegisterSpellScript, RegisterAuraScript or RegisterScript(this one is when its both aura and spellscript).  
`
RegisterSpellScript<EntangleFankriss>("spell_entangle_fankriss");
`

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
