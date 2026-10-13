# Version 0.2 solo test

Exit the old test game and close its map without saving the old in-memory copy over
the updated files. Reopen using **Open Arena.cmd**, then press **Ctrl+F9**.

## First pass: menus, ownership, and live speed

1. Choose **Terran > Mine**. Hover the Marine icon; its tooltip should say Marine
   and explain that it spawns for your army. Click the center of the portrait ten
   times. Ten controllable Marines should appear, and the Mine counter should show 10.
2. Choose **Protoss > Enemy** and click Zealot five times. Five hostile Zealots
   should appear and approach your Marines. Your Marines should remain yours.
3. During that fight, drag the speed slider toward **Slower**, then **Faster**.
   The speed label, movement, and attacks should change in the current match.
   Drag back through **Normal**. No restart should be needed.
4. Switch between all three race tabs. Units already on the map should remain.
   Only the icon submenu changes. The selected Mine/Enemy side should persist.
5. Click **Clear My Army**. Your surviving units disappear; enemies remain.
   Click **Reset Arena**. Both armies and counters should clear.
6. Choose **Zerg > Mine**, spawn Zerglings, and repeat with **Zerg > Enemy** Roaches.
   Confirm the images, tooltips, ownership, and counters.

## Second pass: roster and regressions

- Hover every icon and check that its name matches its image. There are 13 units
  in each race submenu, with two unused grid slots hidden.
- Click icons both at the center and at the frame edge. The image layer should
  allow the underlying button to receive clicks.
- Spawn one of each unit for your side. Air units, large ground units, casters,
  workers, and support units should all appear immediately.
- Try an enemy support unit such as an Overlord. It can move toward your side;
  it should retain its normal non-attacking behavior.
- Normal SC2 targeting rules apply: a ground-only attacker cannot hit an air unit,
  and cloaked units need detection. Use compatible matchups for speed tests.
- Let your entire army die. The session should continue and allow more spawning.
- Spawn 100 units on one side. Further spawning should stop with a limit message;
  deaths or clearing should free slots again.

The Marine-only version was successfully tested by the user. This update has passed
file/data/API checks, but these gameplay checks remain pending. Internet multiplayer
is a later test, after the second human player slot is configured.

If the Editor reports an error, capture the exact message and line number. If an
icon is blank, a click does nothing, or speed does not change, record the race,
unit name, selected side, and speed label so the failure can be reproduced.

Press **F6** to inspect the trigger list. It should contain **Instant Arena Code**
and **Initialize Instant Arena**. The custom code should say version 0.2 near its top.
