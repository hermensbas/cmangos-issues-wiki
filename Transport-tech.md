There are two kinds of transports in Vanilla/TBC - GO type 11 Transport and GO type 15 Motion Transport. WOTLK has an additional transport-in-essence and thats Vehicles.

GO type 11 are generally elevators, however Deeprun Tram is also one example.

GO type 15 are cross map Ships, Zeppelins, Naxxramas in EPL or also ICC Gunship in WOTLK.

Vehicles are Units which have the added capability of being boarded, this can be a motorcycle, a horse, a ship, or anything really.

Transports have one thing in common, Local Coordinate Space and Global coordinate Space. Global coordinates are common for everything in the world. Local coordinates are coordinates on a transport, roughly from the center of the model of the Transport. Local coordinates are also known as an offset, and that is also how they can be translated. Local passenger position + Global transport position = Global passenger position. In Vanilla/TBC only Units have the capability of truly being boarded on a transport, in WOTLK this is extended to GOs and DynGos. (note, Classic is based on a Legion client and supports everything Wotlk supports).

The reason why this is important is pathfinding, sending data to the client, etc. A different packet is sent for motion while on a transport, hence proper simulation serverside is critical for any functionality. In Vanilla/TBC only motion generators need to be Transport-aware however in WOTLK this also pertains to Spell system. When standing still on a transport, global coordinates can change, because the transport can move, however for all checks a player is still regarded as standing still, hence in such cases local coordinates need to be used for any such calculation.

Vanilla/TBC only are capable of changing Transport XYZO, however in WOTLK it is also possible to rotate Transports using Quaternions (lookup term on wikipedia). A quaternion can be present inside GO type 11 path or the DB quaternion rotation can influence the direction a transport path should be oriented towards in 3D space (taking spawning location as initial XYZO origin for the path and rotating upon that).

It is important to mention two things when working with transports. LOS checks with VMAPs use Global coordinate space, whereas pathfinding MMAPs need to use Local Coordinate Space. Pathfinder class in core generally abstracts this with two different Calculate methods (one autotransforming coordinates, and one taking them as-is). It is not possible to pathfind onto/off-of a transport in any blizzlike fashion, and player pets teleport on/off with a small delay following their master.