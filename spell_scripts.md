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