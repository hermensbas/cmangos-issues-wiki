With cmake Option "BUILD_EXTRACTORS" turned on, you will be able to built required data for your CMaNGOS Server to be fully functional.

Default mmap Extraction Values, which can be adjusted per [map](https://github.com/cmangos/issues/wiki/Map.dbc) and tile in config.json

Generator command line args

--offMeshInput      [file.*]        Path to file containing off mesh connections data.
                                    Format must be: (see offmesh_example.txt)
                                    "map_id tile_x,tile_y (start_x start_y start_z) (end_x end_y end_z) size  //optional comments"
                                    Single mesh connection per line.

--silent                            Make us script friendly. Do not wait for user input
                                    on error or completion.

--maxAngle          [#]             Max walkable inclination angle float between 45 and 90 degrees (default 60)

--skipLiquid                        liquid data for maps false: include liquid data (default)

--skipContinents    [true|false]    continents are maps 0 (Eastern Kingdoms), 1 (Kalimdor), 530 (Outlands), 571 (Northrend) false: build continents (default)

--skipJunkMaps      [true|false]    junk maps include some unused maps, transport maps, and some other true: skip junk maps (default)

--skipBattlegrounds [true|false]    does not include PVP arenas false: skip battlegrounds (default)

--debugOutput       [true|false]    create debugging files for use with RecastDemo and Wavefront obj files of the navmesh
                                    if you are only creating mmaps for use with MaNGOS,
                                    you don't want debugging files
                                    false: don't create debugging files (default)

--tile              [XX,YY]         Build the specified tile
                                    seperate number with a comma ','
                                    must specify a map number (see below)
                                    if this option is not used, all tiles are built

[MAPID](https://github.com/cmangos/issues/wiki/Map.dbc)                             Build only the map specified by MAPID
                                    this command will build the map regardless of --skip* option settings
                                    If you do not specify a map number, builds all maps that pass the filters specified by --skip* options
                                    Maps that only consists of a wmo and no terrain will not be built unless specified with ID. Ex. Ragefire Chasm
Examples:

movemapgen
builds maps using the default settings (see above for defaults)

movemapgen --skipContinents true
builds the default maps, except continents

movemapgen 0
builds all tiles of map 0

movemapgen 0 --tile 34,46
builds only tile 34,46 of map 0 (this is the southern face of blackrock mountain)

"MoveMapGen.exe --offMeshInput offmesh.txt "mapid" --tile XX,YY"

```
    json MapBuilder::getDefaultConfig()
    {
        return {
            {"borderSize", 5}, -- Values: 1 - 5 (TC walkableRadius + 3) - dont use value below 5 as tiles dont connect then!
            {"detailSampleDist", 2.0f}, -- Values: 0.1 - 2 (TC 17) - For height detail only. Sets the sampling distance to use when generating the detail mesh.
            {"detailSampleMaxError", BASE_UNIT_DIM * 2}, -- Values: 0.1 - 2 (Default: ~= 0.5)(TC bigBaseUnit ? 0.5333333f : 0.2666666f) - For height detail only.
            {"maxEdgeLen", VERTEX_PER_TILE + 1}, -- Values: 81-85 (Default: 81) (TC bigBaseUnit ? 40 : 80 + 1) - The maximum allowed length for contour edges along the border of the mesh.
            {"maxSimplificationError", 1.8f}, -- Values: 1 - 2.5 (The effect of this parameter only applies to the xz-plane. eliminates most jagged edges (tiny polygons)
            {"mergeRegionArea", 10}, -- Values: 5 - 75 (TC 50) - Any regions with a span count smaller than this value will, if possible, be merged with larger regions.
            {"minRegionArea", 30}, -- Values: 15 - 90 (TC 60) - The minimum number of cells allowed to form isolated island areas.
            {"walkableClimb", 4}, -- Values: 3.5 - 10 (0.2666666f * walkableClimb) (TC m_bigBaseUnit ? 3 : 6) - "Old Info: keep less than walkableHeight - 0.5" - Maximum ledge height that is considered to still be traversable.
            {"walkableHeight", 3}, -- Values: 3.5 - 10 (0.2666666f * walkableHeight) (TC m_bigBaseUnit ? 3 : 6) - Minimum floor to 'ceiling' height that will still allow the floor area to be considered walkable.
            {"walkableRadius", 2}, -- Values: 1 - 5 (0.2666666f * walkableRadius) (TC m_bigBaseUnit ? 1 : 2) - The distance to erode/shrink the walkable area of the heightfield away from obstructions.
            {"walkableSlopeAngle", 60.0f}, -- Values: 50 - 90 - The maximum slope that is considered walkable. Dont Increase too much due to "Fear", though "Blink" also needs it to work, old Default was 70
        };
    }
```

Predefines:

BASE_UNIT_DIM:

```
// value have to divide GRID_SIZE(533.33333f) ( aka: 0.5333, 0.2666, 0.3333, 0.1333, etc )
// All are in UNIT metrics!
const static float BASE_UNIT_DIM = 0.2666666f; // 0.24242424f in Nostalrius Core -- WARNING: A bad 'BASE_UNIT_DIM' value will cause pathfinding issue between tiles.
```

Links:

CMaNGOS Default Should always be same across all repos: https://github.com/cmangos/mangos-tbc/blob/master/contrib/mmap/src/MapBuilder.cpp#L1198

RecastNaviWikis: 
http://www.stevefsp.org/projects/rcndoc/prod/structrcConfig.html

https://docs.unrealengine.com/5.0/en-US/API/Runtime/Navmesh/Recast/rcConfig

https://wiki.jmonkeyengine.org/docs/3.4/contributions/ai/recast.html

Other Cores Defaults:

VMaNGOS: https://github.com/vmangos/core/blob/development/contrib/mmap/src/MapBuilder.cpp#L1575

TC: https://github.com/TrinityCore/TrinityCore/blob/3.3.5/src/tools/mmaps_generator/MapBuilder.cpp#L1089

LH: https://github.com/lh-server/core/blob/development/contrib/mmap/src/MapBuilder.cpp#L574

L4G: https://github.com/Looking4Group/L4G_Core/blob/master/tools/mmap/src/MapBuilder.cpp#L376

