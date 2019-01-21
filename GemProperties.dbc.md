Back to [dbc files](https://github.com/cmangos/issues/wiki/dbc_files) list.

## `GemProperties.dbc`

This dbc contains all gem SpellItemEnchantment.

### Structure

|Field Number|Name|Type|Comment|
|--- |--- |--- |--- |
|1|ID|Integer||
|2|[iRefID_SpellItemEnchantment](https://github.com/cmangos/issues/wiki/GemProperties.dbc#iRefID_SpellItemEnchantment)|Integer||
|3|[maxcount_inv](https://github.com/cmangos/issues/wiki/GemProperties.dbc#maxcount_inv)|Boolean*|(Perhaps a 2nd iRefID_SpellItemEnchantment)|
|4|[maxcount_item](https://github.com/cmangos/issues/wiki/GemProperties.dbc#maxcount_item)|Boolean*|(Perhaps a 3rd iRefID_SpellItemEnchantment)|
|5|[type](https://github.com/cmangos/issues/wiki/GemProperties.dbc#type)|BitMask|Gem Color (a combination of Meta, Red, Yellow and Blue)|
|6|[min_item_level](https://github.com/cmangos/issues/wiki/GemProperties.dbc#min_item_level)|Integer|wotlk+|

### Content

#### [iRefID_SpellItemEnchantment]

#### [maxcount_inv]

#### [maxcount_item]

#### [type]

|BitMask|Colour|
|--- |--- |
|1|Meta|
|2|Red|
|4|Yellow|
|8|Blue|

#### [min_item_level]