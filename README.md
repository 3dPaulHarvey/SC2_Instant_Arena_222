# Instant Arena

A local StarCraft II solo prototype for instant unit spawning and continuous combat.
Version 0.2 adds three race submenus, unit icons, and live game speed controls.
Nothing has been published to Battle.net.

## Open and test

1. Exit the previous test game and close its map in the Editor. Avoid saving the
   old in-memory version over the updated source files.
2. Choose **File > Open** and open:
   `C:\Dropbox\_CODE\_CODEX\Starcraft_1v1\src\InstantArena.SC2Map\ComponentList.SC2Components`
   Select the component-folder file type if the dialog filters it out.
   You can also double-click **Open Arena.cmd** in this project's root.
3. Press **Ctrl+F9**, the Editor's **Test Document** command.
4. The panel should show **Terran**, **Protoss**, and **Zerg** tabs with a grid of
   small unit icon buttons. Hover an icon for its name.
5. Select **Mine** or **Enemy**, then click a unit icon to spawn one for that side.
   Enemy attackers attack-move toward your spawn area; non-attacking support units
   move toward it. Select your own units and command them normally.
6. Drag the **Game speed** slider to switch between Slower, Slow, Normal, Fast,
   and Faster during the same game. **Clear My Army** and **Reset Arena** still work.

Publishing is not required for this solo test. Test Document starts a local SC2 game;
it does not upload the map. Installed game dependencies and the game's normal account
access still apply.

Status: the Marine-only version compiled and its spawning buttons worked in the
user's solo test. Version 0.2 passed generated-source, XML, API argument, unit-ID,
and icon-reference checks. Its menu rendering, clicks, and live speed control still
need an SC2 play test. See the [next solo test checklist](docs/NEXT_SOLO_TEST.md).

## What is stored here

| Path | Purpose |
| --- | --- |
| `src/InstantArena.SC2Map/` | The editable map saved in SC2 component-folder form: terrain, settings, triggers, and text |
| `src/Arena.galaxy` | The spawning and UI code we edit |
| `src/units.json` | The three races, unit IDs, names, and built-in icon paths |
| `tools/build_map.py` | Generates roster code and copies it into the map's editable trigger data |
| `maps/` | Destination for a packed `.SC2Map` file when saved from the Editor |
| `docs/NEXT_SOLO_TEST.md` | Instructions and the next gameplay checks |
| `backups/v0.1-marine-only/` | The working Marine-only code and trigger files |

The source directory ends with `.SC2Map`, but it is a **folder**, not a single map
archive. Open its `ComponentList.SC2Components` file in the Editor.

To create the usual single-file map, use **File > Save As**, choose **StarCraft II
Map Files (.SC2Map)**, and save as `maps/InstantArena.SC2Map`. A packed file can also
be tested locally. Keep the component-folder version as the editable project.

These files can stay in this Dropbox project folder. They do not need to be installed
under Program Files or uploaded anywhere for Editor solo testing.

## Editing the code

Close this map in the Editor before editing its files externally, so an Editor save
does not overwrite those changes. Edit `src/Arena.galaxy` or `src/units.json`, then run:

```powershell
python tools/build_map.py
```

Reopen `ComponentList.SC2Components` and test again. The build script updates only
the trigger/code files; it preserves terrain and map settings. If the Editor changes
trigger code directly, transfer those changes back to `Arena.galaxy` before running
the build script again.

## Scope of this first version

- Flat 32 by 32 Agria arena, with no placed units or economy.
- Player 1 controls friendly units; hostile Player 15 owns test enemies.
- Three race tabs, each containing 13 classic units (39 total).
- Unit buttons are 60 by 60 logical UI pixels, with 50 by 50 unit icons and name tooltips.
- One unit per icon click, with no cost or production time.
- Up to 100 living spawned units on each side.
- A live slider for the five standard game speeds. Initial speed comes from the
  Editor's Test Document preferences; the slider changes it during play.
- Full visibility for the solo player.
- No melee starting armies, AI economy, or automatic victory/defeat initialization.
- Dead spawned units are removed to bound long-session accumulation.

This is a **solo prototype**. Online 1v1 will need a second human lobby slot,
per-player controls and spawn points, plus online testing. We will publish after the
local controls work. The initial template uses Liberty unit data; switching to current
Legacy of the Void multiplayer dependencies is part of preparing the online version.
The standard unit rules still apply, including air targets, cloaking/detection, and
researched abilities. Those can be made configurable in a later arena version.

Game speed is global. The future online version should let one designated player
control it, and verify both clients observe the same change. SC2 also exposes
`GameSetGlobalTimeScale` for finer unit time scaling if we want slow-motion presets
later. This version uses the standard game-speed API.

## References

Terrain is adapted from Blizzard's SC2 Editor tutorial
[`021_Units_Layer.SC2Map`](https://github.com/SC2Mapster/blizzard-tutorials/blob/master/docs/New_Tutorials/02_Terrain_Editor/maps/021_Units_Layer.SC2Map),
preserved by SC2Mapster. Its placed units were removed and its triggers replaced.

- [Blizzard's Trigger Module tutorial, including local Test Document](https://s2editor-guides.readthedocs.io/Classic_Tutorials/02_Trigger_Module/1/)
- [Component-folder export](https://s2editor-guides.readthedocs.io/New_Tutorials/07_Lessons/083_Export_Game_Assets/)
- [Dialog buttons](https://s2editor-guides.readthedocs.io/New_Tutorials/03_Trigger_Editor/043_Dialogs/)
- [Native SC2 API declarations preserved by SC2Mapster](https://github.com/SC2Mapster/SC2GameData/blob/master/mods/core.sc2mod/base.sc2data/TriggerLibs/natives.galaxy)
- [Set Game Speed](https://mapster.talv.space/galaxy/reference/game-set-speed-value)
- [Set Global Time Scale](https://mapster.talv.space/galaxy/reference/game-set-global-time-scale)
