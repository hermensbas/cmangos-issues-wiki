This can be divided into 3 sections. Current, Future and Reference (B).

Currently we have 3 main multithreading contexts and 1 WIP.

1. Network thread context  
    - executes input operations sent from client to server and output operations to client from server. Directly handles query opcodes for speed.
2. World thread context  
    - executes main game world operations. Game event scheduling, maintaining sessions, most input packet processing and even some scripts. Too much.
3. Map thread context  
    - executes operations local to a map. Update of entities, plenty of spells, scripts, movement. Is synchronized every tick against world thread and is schedules by it.  
4. Wotlk LFG  

Future plans:

We want to offload as much of 2s work into 3 whenever possible and remove as many barriers due to which map thread must be synchronized against world thread. As such, anything that is to be added in the future that communicates from map to world and vice versa should be added through messaging queues.

The wotlk LFG is a template that should also house Battleground dispatching in the future. Worldstate management should be generic for Realm level, and should synchronize to each map periodically for some variables.

Reference(B):

Servers are comprised of several nodes. The main ones are Login (comparable to our realmd), Connection Manager (we do it in world thread), Realm (our world), Map (actual instance of a map, even world map), a Battlegroup server (where wotlk RDF and Battlegrounds since patch 1.5 are housed) and several instance servers (Assume that several instances(dungeons/bgs) can run on a single one since they are not as taxing as a world map).

They are interconnected through messaging queues, similar to how client communicates with server. These nodes run in separate processes (or these days maybe even services) for scalability. Players connect to Connection Manager which forwards traffic to the correct node.