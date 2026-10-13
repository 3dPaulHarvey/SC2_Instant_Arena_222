# Next solo test

Version **0.1.3** adds a live game-speed slider below the arena controls.
The race/unit dropdowns and four army buttons are still available.

Test live speed:

1. Reopen the Basic map using **Open Arena.cmd**, then press **Ctrl+F9**.
2. Check that the speed label says **Game speed: Normal** and the slider starts
   in the middle. The slider should remain below the reset button and help text.
3. Spawn a few units for yourself and an enemy unit. Watch the enemy moving toward
   your army, or order your own units to move across the arena.
4. While those units are moving, drag the slider all the way left. It should snap
   to **Slower**, update the label, and immediately slow movement and combat.
5. Drag it all the way right. It should snap to **Faster**, update the label, and
   immediately speed up the same existing units. Reloading the map is unnecessary.
6. Try the three interior positions: **Slow**, **Normal**, and **Fast**. Drag back
   and forth repeatedly. The label and slider should settle on the same preset.
7. At Slower and Faster, switch races, select a different unit, and use both spawn
   buttons. Each click should still create one unit. Changing speed should not
   spawn, clear, or replace any units.
8. Test **Clear My Army** and **Reset Arena**. Reset should zero both counters while
   keeping the selected unit and speed. Move the slider back to Normal afterward.
9. If SC2's own speed controls are available in the game menu, change speed there
   once. The arena slider and label should catch up within about half a second.

The slider snaps to SC2's five native game-speed presets.
This affects the whole match. The current solo controller is Player 1; online 1v1
still needs a second-human setup and a two-client test.

Galaxy syntax and all four recovery checks pass. An isolated SC2 runtime test also
passed all five presets: each requested speed matched the engine's actual value
and slider position, Faster advanced game time faster than Slower, and the test
restored Normal afterward. No script or text-error log was produced during this run.
Slider rendering, physical dragging, and combat feel still need the manual play
check above. The automatic test harness is only in a separate test copy of the map.

For the original four-button recovery test, see [SOLO_TEST.md](SOLO_TEST.md).
For the cause of the earlier compile failures, see [ROOT_CAUSE.md](ROOT_CAUSE.md).

Open **Open Arena.cmd**, then press **Ctrl+F9**. The launcher now opens
`src/InstantArena_Basic.SC2Map/ComponentList.SC2Components`.

Do not use the archived race-menu builder. The current text menus are built by
`tools/build_map.py` from `src/Arena.galaxy`.
