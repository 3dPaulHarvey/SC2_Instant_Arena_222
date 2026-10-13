# Instant Arena

A StarCraft II custom arena for instant unit spawning and continuous combat.

The active build is the **Basic Marine arena**, restored from the version that
worked in the user's solo test. The user also confirmed the recovery test works.
Race menus, unit icons, and speed controls are archived while the baseline is
stabilized. Nothing has been published to Battle.net.

## Open and test

1. Exit the previous test game and close the old map in the Editor.
2. Double-click **Open Arena.cmd** in this project.
3. The launcher opens `src/InstantArena_Basic.SC2Map/ComponentList.SC2Components`.
4. Press **Ctrl+F9** to run the local test.
5. Use **Spawn My Marine**, **Spawn Enemy Marine**, **Clear My Army**, and **Reset Arena**.

Enemy Marines attack-move toward your spawn area. You command your own units
normally. Losing all units does not end the session. Each side can have up to 100
living spawned units.

If you see race menus, close the old experimental map and reopen the Basic map
with the launcher. See [SOLO_TEST.md](docs/SOLO_TEST.md) for the recovery checklist
and [ROOT_CAUSE.md](docs/ROOT_CAUSE.md) for the compiler failure and repair.

## Project files

| Path | Purpose |
| --- | --- |
| `src/Arena.galaxy` | The tested Marine-only source |
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

Add a plain Zealot button and a plain Zergling button first. Test that small change
before bringing back navigation, icons, or speed controls, one feature at a time.

Online 1v1 still needs a second human slot, per-player controls, and a two-client
test before publishing.

## References

Terrain is adapted from Blizzard's SC2 Editor tutorial
[021_Units_Layer.SC2Map](https://github.com/SC2Mapster/blizzard-tutorials/blob/master/docs/New_Tutorials/02_Terrain_Editor/maps/021_Units_Layer.SC2Map),
preserved by SC2Mapster. Its placed units were removed and its triggers replaced.

- [Blizzard's Trigger Module tutorial and local Test Document](https://s2editor-guides.readthedocs.io/Classic_Tutorials/02_Trigger_Module/1/)
- [Component-folder export](https://s2editor-guides.readthedocs.io/New_Tutorials/07_Lessons/083_Export_Game_Assets/)
- [Bundled parser provenance and MIT license](tools/galaxy_parser/README.md)
