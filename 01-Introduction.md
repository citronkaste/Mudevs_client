# Introduction and Design Principles

## Overview

This documentation describes the Lua API available for scripting in the Mu Online client. The system allows you to create custom scripts that interact with the game engine (C++) through a secure and powerful interface, enabling custom UI rendering, input manipulation, and network packet processing.

## Design Principles

### 1. Based on sol2

API uses library `sol2` to link C++ with Lua, offering a secure and powerful interface. This allows:

- **Secure typing**: Automatic validation of parameter types
- **Memory management**: Automatic and secure
- **Performance**: Minimum overhead in communication between Lua and C++

### 2. Object Oriented

The system exposes key game objects as first-class entities:

- `Hero`- Represents the local player
- `GameCharacter`- Represents a character (player, monster, NPC)
- `GameBMD`- Represents a 3D model
- `GameItem`- Represents a game item
- `Packet`- Represents a network packet

### 3. Real-Time Rendering

The system allows customized rendering through the hook `BridgeFunction_OnInterfaceRender`, which is called every frame of the game. This allows:

- Create custom user interfaces
- Render custom text and images
- Manipulate rendering states (alpha, depth, etc.)

**Basic example:**
```lua
function BridgeFunction_OnInterfaceRender()
    --Render custom text
    UIRenderText_SetTextColor(255, 255, 0, 255) --Yellow
    UIRenderText_RenderText(100, 100, "My Custom UI", 200, 20, 1)
end
```

### 4. Event-Driven

The system is based on *hooks* or *callbacks* that are executed in response to specific game events:

- `OnLoadInterface`- When the UI is initializing
- `OnInterfaceRender`- Called every frame for rendering
- `OnPacketRecv`- When a specific packet is received

### 5. Input Handling

The system provides functions to capture user input:

- Mouse (clicks, position, hover)
- Keyboard (press, release, repeat)
- Input blocking for custom UI

## Documentation Structure

The documentation is organized as follows:

1. **Global Functions**: Utility functions accessible from any part of a script
2. **Enums**: Global constants that represent fixed game values
3. **Data Types (Userdata)**: Description of C++ objects exposed to Lua
4. **Game Hooks**: Special functions that the Client calls at key moments
5. **Global Variables**: Available global variables (Hero, MouseX, etc.)

## Naming Conventions

- **Global functions**:`PascalCase `(ex:` GetCharacter `, ` RenderBitmap`)
- **Objects**:`camelCase `(ex:` Hero.Level `, ` character.ID`)
- **Constants**:`UPPER_SNAKE_CASE `(ex:` VK_M `, ` VK_SPACE`)
- **Bridge Functions**:`BridgeFunction_On...`(ex:` BridgeFunction_OnInterfaceRender`)

## Differences between Client and Server

### Client-Side
- Focus on rendering and UI
- Handling user input
- Processing of received packets
- Limited access to game data (view only)

### Server-Side
- Focus on game logic
- Server data manipulation
- Complete event processing
- Full access to game data

## Next Steps

- Read about[Enumerations and Constants](02-Enumerations.md) - Explore as[Global Functions](03-Global-Functions.md) - Understand the[Game Objects](04-Game-Objects.md) - Learn about[Bridge Functions](05-Bridge-Functions.md)

