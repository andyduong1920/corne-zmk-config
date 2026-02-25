# Corne ZMK Keymap Guide

This file documents what `config/corne.keymap` does, so you do not need to read the raw DTS keymap directly.

## Quick Summary

- Keyboard: Corne (split)
- Total layers: 4
- Layer names: `base` (0), `mouse` (1), `number` (2), `symbol` (3)
- Macros: 3
- Custom hold-tap behaviors: 2
- Combos: 40

## Sections In The Keymap File

`config/corne.keymap` is organized into:

1. `macros` section: reusable multi-key actions
2. `combos` section: two-key (or virtual key position) chords that trigger actions
3. `behaviors` section: custom hold/tap behavior definitions
4. `keymap` section: per-layer key bindings

## Layers

### Layer 0: `base`

- Main typing layer (letters and standard modifiers).
- Home row uses `andy_press_hold_or_tap` for mod-tap behavior:
  - Tap: character (`A`, `S`, `D`, `F`, `J`, `K`, `L`, `;`)
  - Hold: modifier (Shift, Ctrl, Alt, GUI)
- Bottom row includes:
  - `&mo 2` (momentary access to layer 2 while held)
  - `&kp LEFT_GUI`
  - `&kp SPACE`
  - `&kp RET`
  - Hold/tap backspace behavior (`LG(BACKSPACE)` on hold, `BACKSPACE` on tap)

### Layer 1: `mouse`

- App/window control shortcuts and mouse clicks.
- Includes many OS shortcuts (quit, close, refresh, copy/paste variants, navigation).
- Bottom row uses `andy_mouse_tap_or_hold_layer 2 RCLK`:
  - Tap: right click
  - Hold: momentarily activate layer 2
- Also contains left click (`&mkp LCLK`).

### Layer 2: `number`

- Number pad style entry (`KP_N1..KP_N9`, `KP_NUMBER_0`) plus symbols.
- Arrow/navigation helpers.
- Contains `&tog 3` to toggle layer 3 (`symbol`) on/off.

### Layer 3: `symbol`

- Focused symbol layer (`&`, `+`, `-`, `*`, `/`, `$`, `%`, `^`, `_`, `=`, `!`, `@`, `#`, `` ` ``, `\`).
- Also contains `&tog 3` to toggle itself off/on.

## Layer Switching

- `to-layer-mouse` combo: switch from layer 0 to layer 1 (`&to 1`)
- `to_base_layout` combo: switch from layers 1/2/3 back to layer 0 (`&to 0`)
- `to-layer-number` combo: switch from layers 0/1/3 to layer 2 (`&to 2`)
- `&mo 2` in base layer: momentary layer 2 while held
- `&tog 3` in layers 2 and 3: toggles layer 3

## Macros

### `file_change_vscode`

- Sends `Ctrl+Shift+S`, then `Ctrl+Shift+Z`
- Used by combo `vscode_changes`

### `git_status`

- Sends terminal chord then `g s t Enter` (quick git status sequence)
- Defined but not directly used in current layer bindings/combos

### `git_push`

- Sends terminal chord then `g g p u s h Enter` (quick git push sequence)
- Defined but not directly used in current layer bindings/combos

## Custom Behaviors

### `andy_press_hold_or_tap`

- Type: hold-tap (`tap-preferred`)
- Tapping term: 350ms
- Pattern: `<&andy_press_hold_or_tap HOLD_ACTION TAP_ACTION>`
- Used widely for mod-taps and shortcut-or-key behavior

### `andy_mouse_tap_or_hold_layer`

- Type: hold-tap (`tap-preferred`)
- Tapping term: 170ms
- Pattern here: `<&andy_mouse_tap_or_hold_layer 2 RCLK>`
  - Hold: `&mo 2`
  - Tap: right click via `&mkp RCLK`

## Combos By Function

### Utility / System

- `bootloader`: enter bootloader (layer 1)
- `bluetooth_reset`: clear Bluetooth bonds (layer 1)
- `esc`: send Escape (layers 0,1)
- `lock`: lock screen (`GUI+L`, layers 0,1)

### Window / App Control

- `show_all_app`: `Ctrl+Up` (layers 1,0)
- `show_all_window`: `Ctrl+Down` (layers 1,0)
- `search-all-vs-code`: `GUI+Shift+F` (layers 1,0)
- `quit_app`: `GUI+Q` (layers 0,1)
- `close_window`, `close_window_2`: close window variations (layers 0,1)
- `refresh`, `refresh_2`: `GUI+R` (layers 0,1)
- `select_all`: `GUI+A` (layers 0,1)
- `save`: `GUI+S` (layers 0,1)
- `undo`: `GUI+Z` (layers 0,1)
- `search`: `GUI+F` (layers 0,1)
- `copy`: copy variant with hold/tap behavior (layers 0,1)
- `paste`: `GUI+V` (layers 0,1)
- `delete`: backspace/delete behavior combo (layers 0,1)
- `enter`: Enter key combo (layers 0,1)

### Navigation

- `home`: home/up behavior (layers 0,1)
- `end`: end/down behavior (layers 0,1)
- `back_and_forward`: browser/app back-forward behavior (layers 0,1)

### App Launch / Workflow

- `recently_vs_code`: `Alt+6` (layers 0,1)
- `clipboard_history`: `Alt+5` (layers 0,1)
- `slack`: `Alt+4` (layers 0,1)
- `vscode`: `Alt+1` (layers 0,1)
- `browser`: `Alt+2` (layers 0,1)
- `vscode_changes`: triggers `file_change_vscode` macro (layers 0,1)

### Symbol Helpers (Layers 2,3)

- `left_PARENTHESIS`, `right_PARENTHESIS`
- `left_BRACKET`, `right_BRACKET`
- `left_BRACE`, `right_BRACE`

### Layout / Layer Control

- `to-layer-mouse`
- `to_base_layout`
- `to-layer-number`
- `tab`
- `capsLock`

## Notes For External Users

- Some combos are duplicated with `_2` names to support multiple physical positions.
- Key positions such as `36`, `37`, and `38` are combo position indices from the board layout, not visible key labels.
- Timings (`timeout-ms`) vary by combo; quick combos are set as low as 20ms and many others use 50ms or 500ms.
