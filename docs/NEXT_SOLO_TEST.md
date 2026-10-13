# Next solo test

The **Basic Marine arena** recovery test passed. This increment adds just the
Marine's built-in portrait icon to **Spawn My Marine**.

Test the portrait:

1. Reopen the Basic map using **Open Arena.cmd**, then press **Ctrl+F9**.
2. Check that a small Marine face appears inside the left side of **Spawn My Marine**.
   The text should remain readable and the other three buttons should look the same.
3. Click directly on the portrait five times. Five controllable Marines should
   appear and the friendly counter should increase by five.
4. Click the text and the right edge of the same button. Each click should still
   create exactly one Marine.
5. Try **Spawn Enemy Marine**, **Clear My Army**, and **Reset Arena** again.

Galaxy syntax and all four recovery checks pass. The SC2 runtime test produced no
script-error log. Portrait rendering and clicks still need this manual play check.

For the current four-button test, follow [SOLO_TEST.md](SOLO_TEST.md).
For the cause of the earlier compile failures, see [ROOT_CAUSE.md](ROOT_CAUSE.md).

Open **Open Arena.cmd**, then press **Ctrl+F9**. The launcher now opens
`src/InstantArena_Basic.SC2Map/ComponentList.SC2Components`.

Do not use the archived race-menu builder. Menus, icons, and speed controls will
return through separate syntax, Editor compile, and gameplay checks.
