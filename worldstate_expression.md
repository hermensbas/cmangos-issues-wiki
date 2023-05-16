Back to [world database](https://github.com/cmangos/issues/wiki/mangosdb_struct) list of tables.

## The `worldstate_expression` table

Official table structure - used for evaluating worldstate conditions. On more info about worldstate variables go to [Worldstates](Worldstates)

Reader application https://github.com/killerwife/WorldstateExpressionReader - produces a console output with all conditions in readable format.

https://gist.github.com/killerwife/20a822b785944dcb10cffc4018b5f48d - 16.05.2023 generated file

### Structure

| Field                           | Type             | NULL | Key     | Default | Comments                    |
| ------------------------------- | ---------------- | ---- | ------- | ------- | --------------------------- |
| [Id](#Id)                  | int(11) unsigned | NO   | PRIMARY | 0       | Primary Key |
| [Expression](#Expression)  | varchar(255)     | NO   |         | 0       |             |

#### Id

Numeric identifier

Uses:

[combat_condition.WorldStateExpressionID](combat_condition#WorldStateExpressionID)

#### Expression

String expression in Hex format that contains information about evaluation:

1. IsEnabled  
2. EvalLeftValue  
3. ConditionOperation (enum class ConditionOperation)  
4. EvalRightValue  
5. ConditionLogic (enum class ConditionLogic - NONE, AND, OR, XOR)  

Evaluation of value consists of:  

1. Constant  
2. Worldstate Variable - this is the part most people think is a worldstate (example 2174 General Rajaxx dead)
3. Function  

Functions are (taken from Dragonflight, some might not apply):

    WSE_FUNCTION_NONE = 0,
    WSE_FUNCTION_RANDOM,
    WSE_FUNCTION_MONTH,
    WSE_FUNCTION_DAY,
    WSE_FUNCTION_TIME_OF_DAY,
    WSE_FUNCTION_REGION,
    WSE_FUNCTION_CLOCK_HOUR,
    WSE_FUNCTION_OLD_DIFFICULTY_ID,
    WSE_FUNCTION_HOLIDAY_START,
    WSE_FUNCTION_HOLIDAY_LEFT,
    WSE_FUNCTION_HOLIDAY_ACTIVE,
    WSE_FUNCTION_TIMER_CURRENT_TIME,
    WSE_FUNCTION_WEEK_NUMBER,
    WSE_FUNCTION_UNK13,
    WSE_FUNCTION_UNK14,
    WSE_FUNCTION_DIFFICULTY_ID,
    WSE_FUNCTION_WAR_MODE_ACTIVE,
    WSE_FUNCTION_UNK17,
    WSE_FUNCTION_UNK18,
    WSE_FUNCTION_UNK19,
    WSE_FUNCTION_UNK20,
    WSE_FUNCTION_UNK21,
    WSE_FUNCTION_WORLD_STATE_EXPRESSION, - effectively a recursion
    WSE_FUNCTION_KEYSTONE_AFFIX,
    WSE_FUNCTION_UNK24,
    WSE_FUNCTION_UNK25,
    WSE_FUNCTION_UNK26,
    WSE_FUNCTION_UNK27,
    WSE_FUNCTION_KEYSTONE_LEVEL,
    WSE_FUNCTION_UNK29,
    WSE_FUNCTION_UNK30,
    WSE_FUNCTION_UNK31,
    WSE_FUNCTION_UNK32,
    WSE_FUNCTION_MERSENNE_RANDOM,
    WSE_FUNCTION_UNK34,
    WSE_FUNCTION_UNK35,
    WSE_FUNCTION_UNK36,
    WSE_FUNCTION_UI_WIDGET_DATA,
    WSE_FUNCTION_TIME_EVENT_PASSED,