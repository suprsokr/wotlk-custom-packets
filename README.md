# WotLK Custom Packets

ClientExtensions.dll for WoW 3.3.5a (build 12340) - enables custom packet communication between client addons and TrinityCore server scripts.

Based on [TSWoW client-extensions](https://github.com/tswow/tswow/tree/master/misc/client-extensions) (MIT License).

## Features

- **Custom Packets**: Send/receive custom opcodes between Lua addons and C++ server scripts
- **No Runtime Dependencies**: Built with static linking - no MSVCP140.dll or VCRUNTIME140.dll required
- **Wine Compatible**: Works with Wine on macOS/Linux

## Download

Download the latest `ClientExtensions.dll` from the [Releases](../../releases) page.

## Installation

1. Download `ClientExtensions.dll` from Releases
2. Place it in your WoW 3.3.5a folder (next to `WoW.exe`)
3. Patch your WoW.exe using [Thorium](https://github.com/your/thorium):
   ```bash
   thorium patch
   ```

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

## Usage

### Client-Side (Lua Addon)

```lua
-- Requires CustomPackets addon
-- Send packet to server
local packet = CreateCustomPacket(1001, 0)
packet:WriteUInt32(12345)
packet:WriteString("Hello Server")
packet:Send()

-- Receive packet from server
OnCustomPacket(1002, function(reader)
    local value = reader:ReadUInt32(0)
    local message = reader:ReadString("")
    print("Received:", value, message)
end)
```

### Server-Side (TrinityCore C++)

See [Thorium custom-packets documentation](https://github.com/your/thorium/blob/main/docs/custom-packets.md).

## License

MIT License - see [LICENSE](LICENSE)

Based on TSWoW client-extensions, Copyright (c) 2021 tswow contributors.
