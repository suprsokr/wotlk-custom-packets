# WotLK Custom Packets

ClientExtensions.dll for WoW 3.3.5a (build 12340) - enables custom packet communication between client addons and TrinityCore server scripts.

All credits to [TSWoW client-extensions](https://github.com/tswow/tswow/tree/master/misc/client-extensions) (MIT License).

## Why?

We pair down client-extensions to just the custom packets feature and modify the build process slightly to make the resulting .dll more compatible across operating systems.

## Features

- **Custom Packets**: Send/receive custom opcodes between Lua addons and C++ server scripts
- **No Runtime Dependencies**: Built with static linking - no MSVCP140.dll or VCRUNTIME140.dll required
- **Wine Compatible**: Works with Wine on macOS/Linux

## Download

Download the latest `ClientExtensions.dll` from the Releases page.

## Installation

Place ClientExtensions.dll from Releases next to your 3.3.5 Wow.exe

## Usage

Expected to be used in a [Mithril](https://github.com/suprsokr/mithril) or [TSWoW](https://github.com/tswow/tswow) project.

## Building from Source

### Requirements
- Windows 10/11
- Visual Studio 2022 with C++ workload
- CMake 3.22+

### Build Commands

```bash
# Configure (32-bit Release build)
cmake -B build -G "Visual Studio 17 2022" -A Win32 -DCMAKE_BUILD_TYPE=Release

# Build
cmake --build build --config Release

# Output: build/ClientExtensions/Release/ClientExtensions.dll
```

### Build Options

| Option | Default | Description |
|--------|---------|-------------|
| `CMAKE_BUILD_TYPE` | Release | Build type (Release/Debug) |
| `LOG_LEVEL` | DEBUG | Logging level (DEBUG/INFO/WARN/ERROR/NONE) |
| `LUA_LOGGING` | ON | Enable Lua logging functions |
| `CLIENT_PATH` | "" | Auto-copy DLL to this path after build |

## License

MIT License - see [LICENSE](LICENSE)

Based on TSWoW client-extensions, Copyright (c) 2021 tswow contributors.
