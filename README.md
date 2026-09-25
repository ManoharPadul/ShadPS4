<!--
SPDX-FileCopyrightText: 2024 shadPS4 Emulator Project
SPDX-License-Identifier: GPL-2.0-or-later
-->

# Mindro shadPS4 – Uncharted Build

This is a custom **shadPS4 experimental build focused specifically on the Uncharted games included in Uncharted: The Nathan Drake Collection**.

### Supported / Target Games

- **Uncharted: Drake's Fortune Remastered**
- **Uncharted 2: Among Thieves Remastered**
- **Uncharted 3: Drake's Deception Remastered**
- **Uncharted: The Nathan Drake Collection**

This build is intended mainly for testing, improving performance, fixing graphical issues, reducing crashes, and experimenting with renderer/CPU/GPU optimizations for the Nathan Drake Collection.

---

## Community

### Discord

Join the Discord server for discussion about the Mindro fork, testing, bugs, builds and development:

https://discord.gg/wJYmkje8Q

### YouTube

For the latest **shadPS4 Mindro fork updates, Uncharted testing, performance comparisons, fixes, settings, tips and gameplay on PC**, check out:

https://www.youtube.com/@MindroXD

---

# Important

> [!IMPORTANT]
> This is an experimental custom build based on shadPS4.
>
> It is focused specifically on **Uncharted 1, Uncharted 2 and Uncharted 3 from The Nathan Drake Collection**.
>
> Do not expect every chapter or scene to work perfectly.

The emulator and these modifications are still experimental.

You may encounter:

- Crashes
- Freezes
- High RAM usage
- High VRAM usage
- Shader compilation stutters
- Graphical artifacts
- Missing effects
- Incorrect textures
- Broken lighting
- Frame pacing problems
- CPU bottlenecks
- GPU synchronization problems
- Readback stalls
- Performance drops in demanding chapters

Different hardware may produce very different results.

---

# Current Development Focus

The main goal of this branch is improving **Uncharted: The Nathan Drake Collection**.

Current areas of experimentation include:

- CPU → GPU performance
- GPU synchronization
- Vulkan renderer performance
- RAM and VRAM usage
- Texture handling
- Buffer management
- Readback optimization
- Frame pacing
- Shader performance
- Graphical fixes
- Renderer synchronization
- GPU resource lifetime management
- Memory-pressure protection
- Crash reduction
- Stutter reduction
- Uncharted-specific workarounds

---

# Uncharted 1

## Uncharted: Drake's Fortune Remastered

Testing focuses on:

- Performance improvements
- Frame pacing
- Renderer stability
- Texture correctness
- Memory usage
- Crash reduction
- GPU synchronization
- Graphical bugs

Some areas can still behave differently depending on GPU, driver and available VRAM.

---

# Uncharted 2

## Uncharted 2: Among Thieves Remastered

Testing focuses on:

- CPU/GPU performance
- GPU stalls
- Renderer synchronization
- Texture problems
- Memory pressure
- VRAM usage
- Frame pacing
- Crash reduction
- Graphical improvements

Large or demanding chapters can still cause significant CPU, RAM, GPU and VRAM pressure.

---

# Uncharted 3

## Uncharted 3: Drake's Deception Remastered

Uncharted 3 is one of the main development targets of this build.

Testing includes:

- CPU → GPU optimization
- GPU readbacks
- Renderer synchronization
- Frame pacing
- RAM usage
- VRAM usage
- Texture handling
- Shader behavior
- Graphical fixes
- Crash fixes
- Performance improvements

Some experimental optimizations may improve performance in one scene while causing regressions somewhere else.

For that reason, changes require testing across multiple chapters before they can be considered stable.

---

# VRAM / Memory Requirements

The Nathan Drake Collection can currently place significant pressure on system RAM and GPU VRAM when running through shadPS4.

For this experimental build, a GPU with **8 GB VRAM or more is strongly recommended**.

Systems with less VRAM may experience:

- Freezing
- Heavy stuttering
- Missing textures
- Driver resets
- Emulator crashes
- Out-of-memory errors

Higher-resolution rendering can increase VRAM requirements further.

---

# Experimental Features

This branch may contain experimental features or optimizations that are not available in the official shadPS4 build.

Experimental features can:

- Improve FPS
- Reduce stalls
- Improve frame pacing
- Reduce memory pressure
- Fix specific Uncharted scenes

But they can also introduce:

- New crashes
- Visual corruption
- Missing graphics
- Regression in other chapters
- Increased memory usage

Testing is therefore very important.

---

# Reporting Problems

If you encounter a problem, please provide as much information as possible.

Useful information includes:

- Game
- Chapter
- Exact location
- GPU
- CPU
- RAM
- VRAM
- Resolution
- shadPS4 build/version
- Settings
- Screenshot or video
- Log file
- Crash diagnostics

If the emulator crashes, please enable **Crash Diagnostics** before reproducing the problem whenever possible.

Reports without logs or enough information can be difficult to investigate.

Discord:

https://discord.gg/wJYmkje8Q

---

# Development Status

This project is experimental.

I am currently not continuously working on this branch.

Development may resume when the main shadPS4 project makes further progress with the major CPU, GPU, RAM, VRAM and renderer problems affecting the Uncharted games.

There is no fixed schedule for future updates.

The source code is public, so anyone is welcome to:

- Test it
- Modify it
- Experiment with it
- Improve it
- Remove or add features
- Use AI/LLM coding tools to experiment with the code
- Report useful fixes or regressions

If you find a real improvement or important problem, feel free to share it.

---

# General Information

**shadPS4** is an early PlayStation 4 emulator for:

- Windows
- Linux
- macOS

It is written primarily in C++ and uses Vulkan for graphics rendering.

This repository is a custom experimental fork/build and is **not the official shadPS4 repository**.

---

# Building

Users who only want to test the provided build do not need to compile the emulator themselves.

Developers who want to modify the project can build it using the standard shadPS4 development environment.

The source code remains available so developers and testers can experiment with the Uncharted-specific changes.

---

# Keyboard Shortcuts

| Button | Function |
|---|---|
| F10 | FPS Counter |
| Ctrl + F10 | Video Debug Information |
| F11 | Fullscreen |
| F12 | RenderDoc Capture / Game Screenshot |
| Alt + F12 | Screenshot including HUD/dialog overlays |

> [!NOTE]
> Some keyboards may require holding the **Fn** key when using F-keys.

Xbox and DualShock/DualSense-compatible controllers can also be used.

---

# Firmware Files

Some games require PlayStation 4 system modules to function correctly.

Required firmware files must be dumped from a **legally owned PlayStation 4 console** and placed inside the appropriate shadPS4 `sys_modules` directory.

Firmware files are **not included with this repository**.

---

# Legal

This repository does not contain:

- PlayStation 4 firmware
- Copyrighted Sony system files
- Game files
- Uncharted game data

You must provide legally obtained game and firmware files yourself.

---

# Credits

### shadPS4

This project is based on the work of the **shadPS4 Emulator Project** and its contributors.

### Mindro Fork

Additional experimental modifications, Uncharted testing, optimizations and fixes are maintained/tested as part of the Mindro custom branch.

### Community

Thanks to everyone testing the Uncharted games, submitting logs, reporting crashes and helping identify graphical or performance regressions.

---

# Links

**Mindro Discord**

https://discord.gg/wJYmkje8Q

**Mindro YouTube**

https://www.youtube.com/@MindroXD

---

# License

GPL-2.0-or-later

See the repository `LICENSE` file for complete licensing information.
