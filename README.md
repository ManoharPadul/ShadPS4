<!--
SPDX-FileCopyrightText: 2024 shadPS4 Emulator Project
SPDX-License-Identifier: GPL-2.0-or-later
-->

<h1 align="center">
  <br>
  <b>shadPS4 – Uncharted Edition</b>
  <br>
</h1>

<p align="center">
Custom shadPS4 build focused on improving the <b>Uncharted series</b> and <b>Uncharted: The Nathan Drake Collection</b>.
</p>

# General Information

This is a custom build of **shadPS4**, an experimental PlayStation 4 emulator for Windows, Linux, and macOS.

This build is specifically being developed and tested for the **Uncharted series**.

The main focus is:

* Uncharted: Drake's Fortune
* Uncharted 2: Among Thieves
* Uncharted 3: Drake's Deception
* Uncharted: The Nathan Drake Collection
* Uncharted 4: A Thief's End
* Uncharted: The Lost Legacy

The primary development target is to improve compatibility, graphics, stability, image quality, and performance for these games.

# Project Goal

The main goal of this custom shadPS4 build is to make the **Uncharted series as close to fully playable as possible**, with a target of high-resolution gameplay and up to **60 FPS where hardware and emulation performance allow it**.

The project includes experimental renderer changes and game-specific fixes intended to improve the Uncharted experience.

# Current Development Focus

Development currently focuses on several major areas.

## Performance

Work is being done to reduce unnecessary GPU and CPU overhead, including:

* Renderer optimizations
* Vulkan performance improvements
* Reduced unnecessary GPU transfers
* Improved resource caching
* Improved buffer reuse
* Reduced synchronization stalls
* Improved asynchronous graphics work
* Improved asynchronous compute work
* Faster handling of resident GPU resources
* Reduced staging-buffer allocations
* Improved vertex and index buffer handling
* Improved indirect draw and dispatch handling

The long-term target is smoother gameplay, higher minimum FPS, and better GPU utilization in demanding Uncharted scenes.

# Graphics Improvements

Several graphics improvements are being researched or implemented specifically for Uncharted.

These include:

* Improved image quality
* Improved anti-aliasing
* Higher-resolution rendering
* Depth-of-field removal or adjustment
* Texture fixes
* Shader fixes
* Lighting fixes
* Brightness improvements
* Character rendering fixes
* Hair rendering fixes
* Geometry corruption fixes
* Improved interpolation handling
* Improved framebuffer behavior
* Vulkan renderer fixes

# Nathan Stretching Fix

One of the major graphical problems being investigated is the **Nathan stretching / geometry corruption issue**.

Testing showed that using native fragment interpolation instead of manually reconstructing interpolation through NVIDIA-specific barycentric handling can improve or fix some character geometry problems.

This area is still under active development because fixes must maintain both:

* Correct character rendering
* Good performance

A graphical fix that causes a major FPS regression is not considered a complete solution.

# Character and Hair Rendering

Additional work is being performed on character rendering issues that can appear in the Uncharted games.

Current areas of investigation include:

* Nathan character stretching
* Hair artifacts
* Incorrect vertex interpolation
* Missing fine detail
* Broken geometry
* Incorrect textures
* Shader-related character artifacts

The objective is to fix these problems without relying on expensive workarounds that significantly reduce performance.

# Uncharted 3

Uncharted 3 is one of the primary test games for this build.

Known areas being worked on include:

* Performance
* Brightness
* Visual bugs
* Character rendering
* Hair rendering
* Geometry issues
* Shader behavior
* Image quality
* Anti-aliasing
* High-resolution rendering

The goal is to eventually make Uncharted 3 consistently playable with correct graphics and strong performance.

# The Nathan Drake Collection

**Uncharted: The Nathan Drake Collection** is one of the primary targets of this project.

The collection contains:

* Uncharted: Drake's Fortune
* Uncharted 2: Among Thieves
* Uncharted 3: Drake's Deception

Development is focused on improving compatibility across the entire collection rather than optimizing only a single game.

Changes are tested carefully because a fix for one Uncharted title should ideally not introduce regressions into another.

# FSR 3

Experimental **FSR 3 support** is also being developed for this custom build.

The intended behavior is automatic.

When FSR is enabled:

### 1080p Output

Use:

**FSR Native AA**

This keeps the internal rendering resolution high while using FSR primarily for anti-aliasing and image reconstruction.

### 1440p Output

Automatically select an appropriate quality mode depending on rendering requirements.

### 4K Output

Use:

**FSR Quality**

The emulator should automatically determine the appropriate FSR mode based on the selected output resolution rather than requiring the user to manually change the quality preset every time.

Further work is planned for anti-aliasing quality and image stability.

# Renderer Optimization

The renderer contains experimental optimizations designed to reduce unnecessary work.

Areas being developed include:

* Resident resource caching
* Generation-checked GPU resources
* Reusable GPU allocations
* Reduced guest-memory round trips
* Improved compute-generated resource handling
* Async graphics execution
* Async compute execution
* Better synchronization
* Reduced temporary allocations
* Reduced transfer operations
* Faster texture handling
* Faster sampled-image handling

Special attention is being given to workloads commonly encountered in the Uncharted games.

# Compute and GPU Resource Improvements

Compute-generated resources can be reused directly by the renderer when it is safe to do so.

The generation-checked resource system is being extended to cover:

* Storage buffers
* Vertex buffers
* Index buffers
* Indirect draw arguments
* Indirect dispatch arguments
* Sampled images
* Storage images
* Compute-generated guest data

This can prevent unnecessary transfers back through guest memory before the renderer consumes the results.

# Experimental Status

> [!IMPORTANT]
> This is an experimental development build.

The emulator and these modifications are still under active development.

You may encounter:

* Crashes
* Graphical corruption
* Missing graphics
* Shader bugs
* Incorrect lighting
* Character artifacts
* Performance regressions
* Save-related issues
* Game-specific compatibility problems

A feature being present does not necessarily mean that it is finished or stable.

# Development Philosophy

The priority of this build is not simply to make a game boot.

The target is:

**Correct graphics + good performance + stability.**

A graphical workaround that fixes one visual issue but causes a large performance loss is not considered an ideal final solution.

Similarly, an optimization should not be retained if it introduces graphical corruption or instability.

# Performance Target

The long-term performance goal is:

**Up to 4K / 60 FPS for the Uncharted series where technically possible.**

Actual performance depends heavily on:

* CPU
* GPU
* Game
* Scene complexity
* Resolution
* Shader compilation
* Emulator overhead
* Current renderer implementation

60 FPS is a development target rather than a guarantee.

# Recommended Hardware

This experimental build benefits from modern high-end hardware.

A powerful GPU is particularly useful when testing:

* 4K output
* FSR
* High internal resolutions
* Expensive shader workloads
* Vulkan renderer modifications

Performance will continue to improve as emulator-level bottlenecks are identified and optimized.

# Keyboard Shortcuts

| Key        | Function                      |
| ---------- | ----------------------------- |
| F10        | FPS Counter                   |
| Ctrl + F10 | Video Debug Information       |
| F11        | Fullscreen                    |
| F12        | Render Capture / Screenshot   |
| Alt + F12  | Screenshot including overlays |

# Controllers

Xbox and DualShock/DualSense-compatible controllers can be used with the emulator.

Keyboard and mouse bindings can also be configured from the controller settings.

# Firmware Files

shadPS4 can use certain PlayStation 4 system modules.

Supported modules must be obtained from a **legally owned PlayStation 4 console** and placed inside the emulator's:

`sys_modules`

folder.

Examples include:

| Module                      | Module                         |
| --------------------------- | ------------------------------ |
| libSceAudiodec.sprx         | libSceAudiodecCpu.sprx         |
| libSceAudiodecCpuDdp.sprx   | libSceAudiodecCpuDtsHdLbr.sprx |
| libSceAudiodecCpuHevag.sprx | libSceAudiodecCpuM4aac.sprx    |
| libSceCesCs.sprx            | libSceFont.sprx                |
| libSceFontFt.sprx           | libSceFreeTypeOl.sprx          |
| libSceFreeTypeOptOl.sprx    | libSceFreeTypeOt.sprx          |
| libSceJpegDec.sprx          | libSceJpegEnc.sprx             |
| libSceJson.sprx             | libSceJson2.sprx               |
| libSceLibcInternal.sprx     | libSceNgs2.sprx                |
| libScePngEnc.sprx           | libSceRtc.sprx                 |
| libSceRudp.sprx             | libSceSystemGesture.sprx       |
| libSceUlt.sprx              | libSceWkFontConfig.sprx        |
| libSceXml.sprx              |                                |

> [!CAUTION]
> Firmware modules and game files must be dumped from hardware and games you legally own.

# Current Priorities

The current development priority is approximately:

1. Fix major Uncharted rendering problems
2. Fix Nathan stretching and geometry corruption
3. Fix hair and character artifacts
4. Improve shader accuracy
5. Improve renderer performance
6. Reduce GPU synchronization stalls
7. Improve asynchronous GPU execution
8. Improve texture and image handling
9. Improve Uncharted 3 brightness and visual issues
10. Improve anti-aliasing
11. Improve FSR 3 integration
12. Improve 1440p and 4K rendering
13. Improve frame pacing
14. Reduce crashes
15. Reach stable 60 FPS where possible

# Release Status

This build is currently a **work in progress**.

It is being actively tested and improved with the Uncharted series as the primary workload.

A public release should only be considered once the build reaches an acceptable level of:

* Stability
* Visual accuracy
* Performance
* Compatibility

# Disclaimer

This project is an unofficial custom development build based on shadPS4.

PlayStation, PS4, Uncharted, The Nathan Drake Collection, and related trademarks belong to their respective owners.

No copyrighted game files or PlayStation firmware files are distributed with this project.

Users must provide files dumped from hardware and games they legally own.

# License

This project remains licensed under:

**GPL-2.0-or-later**

Any modifications based on GPL-licensed shadPS4 source code must continue to comply with the applicable GPL license requirements.
