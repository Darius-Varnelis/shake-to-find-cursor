# Shake to Find Cursor

![Shake to Find Cursor demo](./shake-to-find.gif)

A [Windhawk](https://windhawk.net/) mod that brings macOS's "Shake to locate"
to Windows: shake the mouse and the cursor grows so you can spot it instantly.
Keep shaking and it keeps growing, slower and slower. Stop, and it shrinks
back down.

## Install

1. Install [Windhawk](https://windhawk.net/) if you don't have it.
2. Open Windhawk, find **Shake to Find Cursor** in the Explore tab, and click
   **Install**.

   (Not showing up yet? It may still be pending review — see
   [Development](#development) below for installing it manually in the
   meantime.)

## How it works

- Runs as a *tool mod*, in its own background `windhawk.exe` process. It
  never injects into or touches Explorer.
- Listens to raw mouse input, so there's no polling and no CPU use while the
  mouse is idle — and no input lag, unlike a low-level mouse hook.
- A shake is detected when the cursor travels a long distance while staying
  inside a small area, within a short time window.
- Enlarging swaps in bigger versions of your *actual* system cursors, loaded
  from your current cursor scheme's own files. There's no overlay and no
  trailing effect — it's a genuinely bigger pointer that keeps your cursor's
  style and colour.
- The grow and shrink animations are time-based and run at your monitor's
  refresh rate.

## Settings

| Setting | Default | What it does |
|---|---|---|
| Enlarged size (%) | 400 | Size of the first enlargement, relative to normal (400 = 4×). |
| Keep growing while shaking (%) | 50 | How much bigger it gets in the first extra second of continued shaking. Growth slows logarithmically after that — the next doubling takes 2 s, then 4 s, 8 s, and so on. Set to 0 to stop growing after the first enlargement. |
| Size limit (px) | 0 | Hard ceiling on cursor size. 0 = your screen height. |
| Shake distance (px) | 800 | Distance the cursor must travel within the time window to count as a shake. Lower = easier to trigger. |
| Back-and-forth ratio (%) | 350 | Distance travelled ÷ the diagonal of the area the cursor stayed in. A straight swipe is ~100; four strokes back and forth is ~400. Lower = easier to trigger, but fast ordinary movements may start to register as shakes. |
| Time window (ms) | 1000 | How much recent movement is considered when checking for a shake. |
| Stay enlarged for (ms) | 500 | How long the cursor stays big after you stop shaking. |
| Grow animation (ms) | 150 | Duration of the grow animation. 0 = instant. |
| Shrink animation (ms) | 250 | Duration of the shrink animation. 0 = instant. |
| Disable in fullscreen apps and games | On | Skip enlarging while a fullscreen app, game, or presentation has focus. |

## Notes

- Apps that draw their own custom cursor keep their normal-sized one - this
  mod only affects Windows' system cursors.
- Cursor files max out at 256 px, so sizes past that are upscaled and look
  a bit softer.
- If the mod's process is killed while the cursor is enlarged, the normal
  cursors are restored automatically the next time the mod starts. Re-applying
  your pointer scheme in **Mouse Properties** fixes it immediately.

## Development

The mod is a single file: [`shake-to-find-cursor.wh.cpp`](./shake-to-find-cursor.wh.cpp).

To install it manually (e.g. before it's in the Explore tab):

1. In Windhawk, click **Create a New Mod**.
2. Paste in the contents of `shake-to-find-cursor.wh.cpp`.
3. Click **Compile Mod**, then exit editing mode.

Contributions and issues are welcome - feel free to open a pull request or
an issue.

## License

[MIT](./LICENSE)
