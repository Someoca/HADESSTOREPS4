# PS4 Compatibility and Validation Plan

This branch tracks work toward a reproducible DolphinPS4 build and validation on PS4 Fat, Slim, and Pro.

## Target matrix

| Console | Firmware | Status | Required evidence |
|---|---|---|---|
| PS4 Fat | 13.52 | Not independently verified in this fork | Install/launch, Vulkan, GameCube and Wii test set, logs |
| PS4 Fat | 14.00 | Not verified | Same test set |
| PS4 Slim | 13.52 | Not verified | Same test set |
| PS4 Slim | 14.00 | Not verified | Same test set |
| PS4 Pro | 13.52 | Not verified | Same test set |
| PS4 Pro | 14.00 | Not verified | Same test set |

Do not mark a combination as supported based only on reports from a different console, firmware, or game.

## Validation stages

1. **Source/build baseline**
   - Record the upstream commit and submodule revisions.
   - Follow the repository's BUILDING.md instructions without changing compiler or toolchain versions.
   - Save complete build logs and the generated package checksum.
2. **Install and launch**
   - Confirm package installation, first launch, clean exit, and relaunch.
   - Test with GoldHEN plugins disabled first; re-enable them individually if stable.
3. **Graphics and input**
   - Confirm Vulkan device initialization, shader compilation/cache, resolution changes, DualShock 4 input, and audio.
4. **Game tests**
   - Use only user-owned game backups.
   - Test at least one known GameCube title and one known Wii title, recording game ID, region, image format, settings, average FPS, glitches, and crashes.
5. **Persistence**
   - Verify memory cards, Wii saves, settings, and save states across app restarts and package updates.
6. **Regression**
   - Repeat the smoke test after every code or build-system change.

## Test report template

For every run, record:

- Console model: Fat / Slim / Pro (include CUH model if known)
- System software: exact firmware version
- GoldHEN version and enabled plugins
- DolphinPS4 commit and package version
- Game title, game ID, region, and backup format
- Graphics/performance settings
- Launch result, average FPS, audio/video issues, controller behavior
- Relevant /data/DolphinPS4/ logs and crash reports

## Build prerequisites

The upstream project documents a WSL2 Ubuntu/Linux cross-build using Clang 21, CMake, Ninja, Python 3 with Pillow, OpenOrbis PS4 toolchain, and the Mesa build dependencies. Follow the current BUILDING.md; do not assume that a package built on one firmware is validated on another.

## Release criteria

A firmware/model combination is supported only after the package installs and launches and the agreed GameCube/Wii smoke tests pass on that exact combination. Publish the test matrix and known limitations with every release.

## Legal and licensing

Preserve upstream copyright and license notices. DolphinPS4 is distributed under GPL-2.0-or-later; any distributed modified build must comply with the applicable license and source-offer requirements. Do not bundle commercial game images, BIOS files, console keys, or proprietary firmware.