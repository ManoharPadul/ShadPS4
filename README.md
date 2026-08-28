<!--
SPDX-FileCopyrightText: 2024 shadPS4 Emulator Project
SPDX-License-Identifier: GPL-2.0-or-later
-->

<h1 align="center">
  <br>
  <b>shadPS4 — Uncharted Edition</b>
  <br>
</h1>

<p align="center">
  <b>A custom shadPS4 development build focused on the Uncharted series, visual accuracy, performance, and high-resolution gameplay.</b>
</p>

---

# Overview

**shadPS4 — Uncharted Edition** is a custom development build of shadPS4 focused primarily on improving the emulation experience for the **Uncharted series**, with particular attention given to **Uncharted: The Nathan Drake Collection**.

The project is built around three priorities:

* **Visual accuracy**
* **Performance**
* **Stability**

The objective is not simply to make the games boot or render correctly in isolated scenes. The goal is to create a consistently playable experience with improved graphics, reduced rendering issues, smoother frame pacing, and stronger performance across the entire Uncharted series.

---

# Supported Development Targets

The primary games used for development and testing are:

* **Uncharted: Drake's Fortune**
* **Uncharted 2: Among Thieves**
* **Uncharted 3: Drake's Deception**
* **Uncharted: The Nathan Drake Collection**
* **Uncharted 4: A Thief's End**
* **Uncharted: The Lost Legacy**

The current main focus is **The Nathan Drake Collection**, especially Uncharted 3, due to its combination of rendering issues, performance challenges, and shader-related problems.

---

# Project Goals

The long-term objective of this build is to make the Uncharted series as close to fully playable as technically possible.

Development targets include:

* Improved graphical accuracy
* Reduced shader-related artifacts
* Correct character rendering
* Better texture and framebuffer behavior
* Improved lighting
* Better anti-aliasing
* Higher output resolutions
* Reduced GPU synchronization overhead
* Improved CPU and GPU utilization
* Better frame pacing
* Fewer crashes
* Reduced renderer stalls
* Up to **60 FPS where technically achievable**
* High-quality **1440p and 4K output**

Performance and visual correctness are treated equally.

A visual fix that introduces a major performance regression is not considered complete.

Likewise, an optimization that increases performance but causes graphical corruption is not considered acceptable.

---

# Uncharted: The Nathan Drake Collection

**The Nathan Drake Collection** is currently the primary development target.

The collection includes:

* Uncharted: Drake's Fortune
* Uncharted 2: Among Thieves
* Uncharted 3: Drake's Deception

Because all three games share several rendering and engine characteristics, changes are tested across the collection whenever possible.

The objective is to avoid game-specific hacks unless absolutely necessary.

Ideally, fixes should improve the underlying emulation behavior rather than correcting only a single scene or title.

---

# Graphics Development

A significant portion of development is focused on renderer accuracy.

Current areas of investigation and improvement include:

* Vertex interpolation
* Fragment interpolation
* Character geometry
* Hair rendering
* Texture sampling
* Shader translation
* Framebuffer behavior
* Depth handling
* Lighting
* Brightness
* Post-processing
* Image reconstruction
* Anti-aliasing
* High-resolution rendering
* Vulkan-specific behavior

The goal is to eliminate visible rendering errors while keeping the implementation efficient.

---

# Nathan Stretching and Geometry Corruption

One of the most important rendering issues being investigated is the well-known **Nathan stretching / geometry corruption problem**.

Testing has shown that incorrect interpolation behavior can produce severe character deformation and geometry artifacts.

A successful experimental path used **native fragment interpolation** instead of manually reconstructing interpolation through barycentric shader logic.

This significantly improved the rendering behavior in affected scenes.

However, the implementation must also maintain acceptable performance.

The final solution must satisfy both requirements:

**Correct geometry**

and

**Minimal performance impact**

The project therefore continues to investigate a more efficient and reliable interpolation solution.

---

# Character Rendering

Character rendering is one of the main priorities of this build.

Current work includes investigation of:

* Nathan stretching
* Vertex deformation
* Hair artifacts
* Broken geometry
* Incorrect interpolation
* Shader precision issues
* Missing surface detail
* Texture corruption
* Incorrect lighting
* Depth-related artifacts

Character models are especially useful for detecting subtle renderer problems because even small interpolation or shader errors can produce highly visible corruption.

---

# Uncharted 3 Development

**Uncharted 3: Drake's Deception** is currently one of the most demanding test cases.

Development areas include:

* Brightness correction
* Character rendering
* Hair rendering
* Geometry stability
* Shader accuracy
* Vulkan performance
* Texture correctness
* Frame pacing
* Resolution scaling
* Anti-aliasing
* GPU utilization
* Renderer synchronization

The long-term goal is to make Uncharted 3 consistently playable with correct graphics and strong performance across demanding scenes.

---

# Performance Optimization

Performance work focuses primarily on reducing unnecessary synchronization, transfers, allocations, and CPU-GPU communication.

Current optimization areas include:

* Reduced GPU synchronization
* Reduced staging-buffer allocations
* Improved resource reuse
* Resident resource caching
* Generation-checked GPU resources
* Reduced guest-memory round trips
* Faster vertex-buffer handling
* Faster index-buffer handling
* Improved indirect draw handling
* Improved indirect dispatch handling
* Improved sampled-image handling
* Improved storage-image handling
* Asynchronous graphics execution
* Asynchronous compute execution
* Reduced transfer overhead
* Reduced temporary resource creation
* Better GPU queue utilization

These optimizations are particularly important in large Uncharted scenes containing complex geometry, shaders, effects, and streaming workloads.

---

# Resident Resource System

The renderer is being extended with safer and more efficient resident-resource handling.

Generation-checked resources can be reused when their contents are still valid.

This allows the renderer to avoid unnecessary copies and guest-memory round trips.

The system is being extended to support:

* Storage buffers
* Vertex buffers
* Index buffers
* Indirect draw arguments
* Indirect dispatch arguments
* Sampled images
* Storage images
* Compute-generated data

When a valid resident resource exists, the renderer can consume that resource directly instead of recreating or retransferring the same data.

This can significantly reduce overhead in GPU-heavy workloads.

---

# Asynchronous Graphics

The graphics path is being improved to reduce situations where the CPU unnecessarily waits for GPU completion.

The goal is to allow safe workloads to continue asynchronously whenever resource lifetime and synchronization rules permit it.

This work includes:

* Command-buffer reuse
* Fence management
* Descriptor reuse
* Resource lifetime tracking
* Resident-buffer validation
* Generation checks
* Reduced synchronous waits

Unsafe resource usage continues to fall back to synchronous execution.

Correctness always takes priority over asynchronous execution.

---

# Asynchronous Compute

The compute path is also being optimized.

The compute system can reuse graphics-style command infrastructure while maintaining independent synchronization where required.

Development areas include:

* Compute command rings
* Descriptor-pool reuse
* Command-buffer reuse
* Fence-controlled lifetime management
* Resident compute resources
* Reduced per-dispatch waits
* Safe graphics/compute interaction
* Resource transition validation

The purpose is to reduce unnecessary synchronization between graphics and compute workloads.

---

# Reduced Guest-Memory Round Trips

One important optimization is allowing GPU-produced data to remain available to other GPU workloads when it is safe to do so.

Instead of:

**GPU → Guest RAM → GPU**

the renderer can sometimes use:

**GPU → GPU**

This is particularly useful for:

* Compute-generated vertex data
* Compute-generated index data
* Indirect arguments
* Sampled images
* Storage images
* Temporary GPU resources

Avoiding unnecessary guest-memory round trips can reduce latency and improve overall renderer efficiency.

---

# FSR 3

This build also includes experimental work related to **FSR 3**.

The intended behavior is automatic resolution-based configuration.

When FSR is enabled, the emulator should determine the most appropriate mode automatically.

## 1080p

Use:

**FSR Native AA**

This prioritizes image reconstruction and anti-aliasing while maintaining full-resolution rendering.

## 1440p

Automatically select an appropriate high-quality mode based on the output resolution and renderer requirements.

## 4K

Use:

**FSR Quality**

This provides a balance between image quality and rendering performance.

The objective is to avoid requiring users to manually select an FSR preset every time the output resolution changes.

---

# Image Quality

Image quality is an important part of the project.

Planned and experimental improvements include:

* Improved anti-aliasing
* Better temporal stability
* Reduced shimmering
* Reduced aliasing
* Higher-quality texture presentation
* Improved shader precision
* Better image reconstruction
* High-resolution output
* Reduced post-processing artifacts

The objective is to achieve a cleaner image without introducing excessive GPU overhead.

---

# Depth of Field

Depth-of-field behavior is also being investigated.

Certain post-processing effects can significantly reduce clarity at high resolutions.

Optional changes may allow depth of field to be reduced or disabled in selected situations.

This can provide a sharper image, particularly when playing at 1440p or 4K.

---

# Renderer Philosophy

The renderer follows a simple rule:

> **Correctness first, optimization second — but both are required for a final solution.**

A workaround that fixes a graphical issue while severely reducing frame rate is not considered finished.

An optimization that increases frame rate while introducing visual corruption is equally unacceptable.

Every major change should ideally improve one area without damaging another.

---

# Performance Target

The long-term performance objective is:

**High-resolution gameplay at up to 60 FPS where technically possible.**

Target output resolutions include:

* 1080p
* 1440p
* 4K

Actual performance depends on:

* CPU performance
* GPU performance
* Vulkan driver behavior
* Game scene complexity
* Shader workloads
* Resolution
* Emulator overhead
* Current compatibility
* Renderer implementation

60 FPS is a development target and is not guaranteed in every scene.

---

# Experimental Status

> [!IMPORTANT]
> This is an experimental development build.

The project is under active development.

Users may encounter:

* Crashes
* Broken shaders
* Geometry corruption
* Character artifacts
* Hair artifacts
* Missing graphics
* Incorrect lighting
* Incorrect brightness
* Texture problems
* Performance regressions
* Frame pacing issues
* Game-specific compatibility problems

Experimental features may change or be removed when a better implementation becomes available.

---

# Development Priorities

Current development priorities include:

1. Improve Nathan Drake Collection compatibility
2. Fix Nathan stretching
3. Fix character geometry corruption
4. Fix hair rendering
5. Improve shader accuracy
6. Improve Uncharted 3 rendering
7. Improve brightness and lighting
8. Reduce GPU synchronization
9. Improve resident-resource handling
10. Improve asynchronous graphics
11. Improve asynchronous compute
12. Reduce guest-memory transfers
13. Improve texture handling
14. Improve anti-aliasing
15. Improve FSR 3 integration
16. Improve 1440p rendering
17. Improve 4K rendering
18. Improve frame pacing
19. Reduce crashes
20. Improve overall Uncharted performance

---

# Controls

| Key        | Function                    |
| ---------- | --------------------------- |
| F10        | FPS Counter                 |
| Ctrl + F10 | Video Debug Information     |
| F11        | Fullscreen                  |
| F12        | Render Capture / Screenshot |
| Alt + F12  | Screenshot with overlays    |

Compatible Xbox, DualShock, and DualSense controllers can be used with the emulator.

Keyboard and mouse bindings can also be configured through the controller settings.

---

# Firmware Modules

Some PlayStation 4 system modules are required for correct game behavior.

Supported modules should be placed inside:

`sys_modules`

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
> Required firmware modules must be dumped from a legally owned PlayStation 4 console.

---

# Release Status

**shadPS4 — Uncharted Edition** remains a work in progress.

Development is currently focused on achieving a stable combination of:

* Accurate rendering
* Strong performance
* High-resolution output
* Stable frame pacing
* Reduced crashes
* Reliable Uncharted compatibility

The project will continue to evolve as renderer improvements, shader fixes, and performance optimizations are implemented.

---

# Project Vision

The final objective is simple:

> **Play the Uncharted series with accurate graphics, high image quality, smooth performance, and minimal emulation-related issues.**

The project is specifically designed around improving the experience rather than simply increasing compatibility statistics.

Every renderer change, shader fix, optimization, and experimental feature is evaluated based on how much it improves the actual gameplay experience.

---

# Disclaimer

This is an unofficial custom development build based on the open-source shadPS4 emulator project.

PlayStation, PlayStation 4, Uncharted, The Nathan Drake Collection, and all related trademarks and copyrighted properties belong to their respective owners.

No copyrighted games, firmware, keys, or proprietary PlayStation files are distributed with this project.

Users are responsible for providing legally obtained files from hardware and games they own.

---

# License

This project remains licensed under:

**GNU General Public License v2.0 or later — GPL-2.0-or-later**

Modifications based on shadPS4 remain subject to the applicable GPL licensing requirements.
