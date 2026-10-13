# Next solo test

The **Basic Marine arena** recovery test passed. Version 0.1.2 removes portraits
and adds compact **Race → Unit** text dropdowns. The same four action buttons
handle every unit.

Test the submenus:

1. Reopen the Basic map using **Open Arena.cmd**, then press **Ctrl+F9**.
2. The top dropdown should show **Terran**, and the next should show **Marine**.
   Spawn a Marine on each side to confirm the previous working behavior.
3. Choose **Marauder** in the unit dropdown. Both spawn button captions should
   change to Marauder. Changing the selection should leave unit counts unchanged.
   Click each spawn button once: each click should create one Marauder on that side.
4. Switch the race dropdown to **Protoss**. Its unit list should contain only
   **Zealot, Stalker, Sentry, Immortal**, with Zealot selected initially.
   Choose Stalker and spawn one on each side.
5. Switch to **Zerg**. Its list should contain only
   **Zergling, Roach, Hydralisk, Ultralisk**, starting with Zergling.
   Choose Hydralisk and spawn one on each side.
6. Switch back to Terran. Its list should contain only
   **Marine, Marauder, Reaper, Hellion**, starting with Marine. Repeat race switches
   several times and check that entries never accumulate or carry over.
7. Try every remaining unit once on each side, then test **Clear My Army** and
   **Reset Arena**. Reset should zero both counters and keep your selected unit.
8. Fight, lose all your units, then spawn again. The session should continue.

Galaxy syntax and all four recovery checks pass. SC2 runtime launches have produced
no script-error log. The first run reported dropdown text overflow; the controls
now use 52px height to provide enough padding. Dropdown rendering and clicks
still need this manual play check. The game has normal unit abilities and combat
rules; selection changes do not train, upgrade, or issue orders to existing units.

For the original four-button recovery test, see [SOLO_TEST.md](SOLO_TEST.md).
For the cause of the earlier compile failures, see [ROOT_CAUSE.md](ROOT_CAUSE.md).

Open **Open Arena.cmd**, then press **Ctrl+F9**. The launcher now opens
`src/InstantArena_Basic.SC2Map/ComponentList.SC2Components`.

Do not use the archived race-menu builder. The current text menus are built by
`tools/build_map.py` from `src/Arena.galaxy`.
