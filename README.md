# Instant Arena

A StarCraft II custom arena for instant unit spawning and continuous combat.

The active build is **v0.1.4: standard multiplayer roster**, based on the working solo
arena. Choose a race, choose a unit, then spawn it for your army or the enemy.
Drag the speed slider while playing to slow down or speed up the entire match.
Nothing has been published to Battle.net.

## Open and test

1. Exit the previous test game and close the old map in the Editor.
2. Double-click **Open Arena.cmd** in this project.
3. The launcher opens `src/InstantArena_Basic.SC2Map/ComponentList.SC2Components`.
4. Press **Ctrl+F9** to run the local test.
5. Choose **Terran**, **Protoss**, or **Zerg** in the top dropdown. The second
   dropdown lists that race's units.
6. Use **Spawn My [Unit]**, **Spawn Enemy [Unit]**, **Clear My Army**, and **Reset Arena**.
7. Drag the **Game speed** slider at the bottom of the panel. It snaps to
   **Slower, Slow, Normal, Fast, Faster**, from left to right.

Enemy combat units attack-move toward your spawn area; support units move there.
You command your own units
normally. Losing all units does not end the session. Each side can have up to 100
living spawned units.

| Race | Unit submenu |
| --- | --- |
| Terran (17) | Marine, Marauder, Reaper, Ghost, Hellion, Hellbat, Widow Mine, Cyclone, Siege Tank, Thor, Viking, Medivac, Liberator, Banshee, Raven, Battlecruiser, SCV |
| Protoss (18) | Zealot, Stalker, Sentry, Adept, High Templar, Dark Templar, Archon, Immortal, Colossus, Disruptor, Observer, Warp Prism, Phoenix, Void Ray, Oracle, Tempest, Carrier, Probe |
| Zerg (17) | Zergling, Baneling, Roach, Ravager, Hydralisk, Lurker, Infestor, Swarm Host, Ultralisk, Queen, Overlord, Overseer, Mutalisk, Corruptor, Brood Lord, Viper, Drone |

The 52 entries use **Void Multi (Mod)**, SC2's Legacy of the Void multiplayer
dependency. Units spawn in their normal mobile form. Use their own command cards
for siege, burrow, transport, and spell abilities. Research requirements, energy,
and attack-target restrictions follow the standard game data. Enemy units receive
a basic attack-move or move order; their spells and mode changes need separate AI.
The roster contains standard combat, support, and worker units. Buildings, campaign
heroes, summoned-unit menu entries, and the unique Mothership are omitted.

Changing race selects its first unit. Menu selections do not spawn anything.
Reset Arena clears both armies and leaves the menu selection in place.
The match starts at **Normal** speed. The slider changes SC2's live game speed;
its label displays the engine's actual preset. Reset Arena keeps your chosen speed.
Player 1 controls speed for the whole match. Online speed control still needs a
two-client test when multiplayer support is added.
See [NEXT_SOLO_TEST.md](docs/NEXT_SOLO_TEST.md) for the current play checklist
and [SOLO_TEST.md](docs/SOLO_TEST.md) for the original recovery test.
See [ROOT_CAUSE.md](docs/ROOT_CAUSE.md) for the compiler failure and repair.

## Project files

| Path | Purpose |
| --- | --- |
| `src/Arena.galaxy` | Arena source, race/unit submenus, and live speed control |
| `src/InstantArena_Basic.SC2Map/` | The active editable map, including terrain and triggers |
| `tools/build_map.py` | Checks syntax before updating the map's script and triggers |
| `tools/validate_galaxy.py` | Runs the bundled Galaxy syntax parser |
| `tests/test_recovery.py` | Regression checks for the failure and restored scripts |
| `backups/v0.1-marine-only/` | The original working source and trigger files |
| `experiments/race-menu-v0.2/` | The inactive menu attempt, retained for diagnosis |
| `maps/` | Destination for a packed map file saved from the Editor |

`InstantArena_Basic.SC2Map` is a component folder. Open its
`ComponentList.SC2Components` file in the Editor. To make a single packed map,
choose **File > Save As > StarCraft II Map Files (.SC2Map)** and save into `maps/`.

These files can stay in the project directory. Publishing is required later for
normal internet hosting with a friend, but not for local solo testing.

## Build and validate

Close the active map before editing its files externally. Edit `src/Arena.galaxy`,
then run:

~~~powershell
python tools/build_map.py
python -m unittest discover -s tests -v
~~~

Reopen the Basic map and test in SC2. The builder updates only code, trigger data,
and trigger names; it preserves terrain and map settings.
`MapScript.galaxy` and `Triggers` are generated files. Make logic changes in
`src/Arena.galaxy` and rebuild so the Editor and source stay consistent.

The syntax checker uses installed Node.js, or VS Code's bundled Node runtime when
Node is not on PATH. It needs no npm installation or network access. Opening and
testing the saved map does not require this build tooling.

The parser checks Galaxy grammar. It does not resolve game dependencies or replace
the Editor's native type checking and gameplay tests. Invalid syntax causes a build
failure before the playable map is overwritten.

## Next development steps

The user confirmed the live speed control worked. Test the expanded dropdowns,
ground and air combat, support units, and clear/reset behavior at both speed extremes.

Online 1v1 still needs a second human slot, per-player controls, and a two-client
test before publishing.

## References

Terrain is adapted from Blizzard's SC2 Editor tutorial
[021_Units_Layer.SC2Map](https://github.com/SC2Mapster/blizzard-tutorials/blob/master/docs/New_Tutorials/02_Terrain_Editor/maps/021_Units_Layer.SC2Map),
preserved by SC2Mapster. Its placed units were removed and its triggers replaced.

- [Blizzard's Trigger Module tutorial and local Test Document](https://s2editor-guides.readthedocs.io/Classic_Tutorials/02_Trigger_Module/1/)
- [Component-folder export](https://s2editor-guides.readthedocs.io/New_Tutorials/07_Lessons/083_Export_Game_Assets/)
- [Bundled parser provenance and MIT license](tools/galaxy_parser/README.md)
- [Blizzard's shipped native speed API and cinematic speed changes](https://github.com/SC2Mapster/SC2GameData/blob/master/mods/core.sc2mod/base.sc2data/TriggerLibs/NativeLib.galaxy)
- [Blizzard's standard Void multiplayer unit definitions](https://github.com/SC2Mapster/SC2GameData/blob/master/mods/voidmulti.sc2mod/base.sc2data/GameData/UnitData.xml)
