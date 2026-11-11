# Mojave Co-op Crash Lab

An unofficial modified test build based on [New Vegas Co-op by Zyrcxies](https://github.com/Zyrcxies/NewVegasCoop).

A co-op multiplayer mod for Fallout: New Vegas (Steam) for a host and 2-4 friends doing a playthrough together.

This branch tests a fix for a guest crash when using **Take All** on a corpse and collects evidence for a separate
host crash during a manual save after a disconnect. See the [changelog](CHANGELOG.md) for the original symptoms,
the changes in this build and the in-game checks still needed.

The original release and play instructions are available on the [upstream project page](https://github.com/Zyrcxies/NewVegasCoop).
The upstream project also has a [Discord server](https://discord.gg/dU3g6CZK8F).


## Requirements
- Fallout: New Vegas on Steam, with [xNVSE](https://github.com/xNVSE/NVSE/releases)
- To build: Visual Studio Community 2026 with "Desktop development with C++", and Git

## Building
1. Clone with the build dependencies included using `git clone --recurse-submodules <repo-url>`.
   In an existing checkout, run `git submodule update --init --recursive`.
2. Optional, to copy the plugin into your game after each build: copy this into a new file `CMakeUserPresets.json` (it's personal, not committed) and set your game folder:
   ```json
   { "version": 6,
     "configurePresets": [{ "name": "local", "inherits": "x86",
       "cacheVariables": { "GAME_DIR": "C:/Path/To/Fallout New Vegas" } }],
     "buildPresets": [{ "name": "local-debug", "configurePreset": "local", "configuration": "Debug" }] }
   ```
3. For a 32-bit release build, run `cmake --preset x86` and `cmake --build --preset release`.
   The resulting DLL is at `build/Release/NVCoop.dll`. For the optional local preset above, run
   `cmake --preset local` and `cmake --build --preset local-debug`.
4. Start the game with `nvse_loader.exe`. The plugin writes `NVCoop.log` in the game folder.

## Credits
Built on [xNVSE](https://github.com/xNVSE/NVSE). Facts about the game's memory and functions were learned from the
source of [JIP LN NVSE](https://github.com/jazzisparis/JIP-LN-NVSE), JohnnyGuitar NVSE, kNVSE, ShowOff NVSE and
Real Time Menus, and from reverse engineering with Ghidra; thanks to their authors. A big thank you also to the
[FNV decompilation](https://fnvdecomp.com) project ([source](https://github.com/momusdigital/fnv_decomp)) and its
community of contributors, who rebuilt the game function by function: it let us check how the game really works.
AI (Claude) was used as a coding assistant. No game code is included.

## License
See [LICENSE](LICENSE). In short: use it and change it however you like; don't reupload the original; you may share
a meaningfully changed version (or a project using its code) if you credit this project, say it's modified and not
the official mod, include the license, and publish its full source code under this same license.

**Reusing or rewriting this code?** You're welcome to use the ideas and features. If you copy, port or rewrite the
code itself, by hand or with an AI tool, the [license](LICENSE) asks you to credit it as "based on New Vegas Co-op by
Zyrcxies", keep the license notices and use the same license.
