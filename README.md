# LalaPad Gen2 Cross-Pad Gesture Example

📄 **[日本語版](README_ja.md)**

An example firmware configuration for LalaPad Gen2 with the [cross-pad gesture feature of zmk-driver-iqs9151](https://github.com/matoi/zmk-driver-iqs9151/tree/feature/cross-pad-gesture) enabled.

## What is Cross-Pad Gesture?

A feature that executes special gestures by **simultaneously touching** the trackpads on both halves of a split keyboard.

### Pinch In/Out (Zoom)

Place **one finger** on each trackpad and slide either finger **horizontally**.

- Spread fingers outward → **Zoom in**
- Bring fingers inward → **Zoom out**

By default, this works as Ctrl + scroll wheel. The modifier can be changed in the configuration (e.g., Mouse Button 4).

### Press & Hold (Drag)

Place **two fingers** on one trackpad and **one finger** on the other.

- The two-finger side acts as the "button held down" for dragging
- Move the cursor with the one-finger side to perform **drag operations**
- Even if you lift and re-place the one-finger side, the drag continues as long as the two-finger side is maintained
- Lifting the two-finger side ends the drag

## Changes from the Original

This example configuration applies only the following changes to the original [zmk-config-LalaPadGen2](https://github.com/ShiniNet/zmk-config-LalaPadGen2):

- `config/west.yml` — Changed the driver repository and branch to the fork
- `config/boards/shields/lalapadgen2/lalapadgen2_left.conf` — Added `CONFIG_INPUT_IQS9151_CROSS_PAD=y`
- `config/boards/shields/lalapadgen2/lalapadgen2_right.conf` — Added `CONFIG_INPUT_IQS9151_CROSS_PAD=y`
- `config/boards/shields/lalapadgen2/lalapadgen2_left.overlay` — Added `cross-pad-peer-input` property
- `config/boards/shields/lalapadgen2/lalapadgen2_right.overlay` — Added `cross-pad-peer-input` property

## Notice

This feature is **an independent PoC (Proof of Concept) extension** not included in the upstream [ShiniNet/zmk-driver-iqs9151](https://github.com/ShiniNet/zmk-driver-iqs9151). It comes with no guarantee of functionality and may be changed or removed without notice. Compatibility with the upstream driver is not guaranteed.

## Driver Repository

https://github.com/matoi/zmk-driver-iqs9151/tree/feature/cross-pad-gesture
