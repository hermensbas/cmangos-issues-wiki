Worldstates are serverside variables for various purposes.

Clientside worldstates can be used for 3 main purposes:

* Entries from WorldStateUI.dbc - these are UIs like in WSG, AB, AV or Theramore for example
* Entries from WorldStateZoneSounds.dbc (TBC+) - these govern a music in a given zone at a given time - first use was on Isle of Quel'Danas
* Texts in gossip_menu - these enable displaying counters in texts for various purposes, examples are War Effort, Naxx Invasions or Love is in the Air counters

All of these are sent in two packets: SMSG_INIT_WORLD_STATES (entering world or map) and SMSG_UPDATE_WORLD_STATE

cMaNGOS also uses serverside worldstates (which we suspect are also used officially) in a safe region of IDs 10000+. The reason being wotlk using range 4000-ish and not wanting to overlap. These are never sent to client.

Such predefined serverside worldstates are for boss kills which are in the following format: instance_dungeon_encounters boss entry * 100 + (0 or 1)  
+ 0 variable is set to 1 when given boss dies. + 1 variable is set to 1 when given boss is alive. So variable 16500 would be 1 when boss Cookie dies and 16501 would be 1 when boss Cookie is alive.

Custom worldstates can be also defined in C++ in WorldStateDefines.h and used in a C++ script. Such example is "WORLD_STATE_CUSTOM_SPAWN_MALACRASS = 10000" which is set to 1 when Zul'Aman first 4 bosses are dead, which triggers automatic spawning of Malacrass. He is despawned by default to prevent griefing through door. (actual official fix)