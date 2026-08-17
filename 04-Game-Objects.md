# Game Objects

This document describes the main objects exposed by the Lua Client API.

## Overview

The game objects are C++ entities exposed to Lua through the sol2 library. They represent game elements such as characters, 3D models and items.

## GameCharacter

Represents a character in the game (player, monster, NPC). Accessible via `GetCharacter(index)` or through the global variable ` Hero`(local player).

### Properties

| Property | Type | Description |
| :---------- | :--- | :-------- |
| `ID ` | ` string`| Character Name/ID |
| `Class ` | ` int`| Character class code |
| `Skin ` | ` int`| Current model/skin ID |
| `CtlCode ` | ` int`| Control code (GM/Normal) |
| `Level ` | ` int`| Character Level |
| `GuildStatus ` | ` int`| Guild position settings |
| `PK ` | ` int`| PK Level/Status |
| `Dead ` | ` int`| 1 if dead, 0 otherwise |
| `Run ` | ` int`| 1 if you are running |
| `PositionX ` | ` int`| X coordinate (World) |
| `PositionY ` | ` int`| Y Coordinate (World) |
| `TargetX ` | ` int`| Target X (Movement) |
| `TargetY ` | ` int`| Target Y (Movement) |
| `MaxHP ` | ` float`| Maximum life |
| `CurHP ` | ` float`| Current life |
| `MoveSpeed ` | ` float`| Movement speed |
| `Rot ` | ` float`| Rotation |
| `SafeZone ` | ` int`| 1 if you are in Safe Zone |
| `Wing ` | ` int`| Wing Item ID (Visual) |
| `Helper ` | ` int`| ID do pet/helper (Visual) |
| `CurrentSkill ` | ` int`| Skill ID in use |
| `MonsterIndex ` | ` int`| Monster Table Index |
| `Kind ` | ` int`| Entity type (Player/Monster/NPC) |

### Examples

```lua
--Access local player
if Hero then
    local level = Hero.Level
    local name = Hero.ID
    local hp = Hero.CurHP / Hero.MaxHP * 100
end

--Access character by index
local character = GetCharacter(index)
if character then
    if character.Kind == 0 then --Player
        --Do something with player
    elseif character.Kind == 1 then --Monster
        --Do something with monster
    end
end
```

## GameBMD (GameObject/Model)

Represents a visual object/3D model in the engine. Accessible via `GetModel(index)`.

### Properties

| Property | Type | Description |
| :---------- | :--- | :-------- |
| `Visible ` | ` bool`| Visibility flag |
| `Alpha ` | ` float`| Alpha Transparency (0.0 - 1.0) |
| `Scale ` | ` float`| Model scale |
| `Position ` | ` Vector3`| Position (x, y, z) |
| `Velocity ` | ` float`| Speed ​​|
| `Gravity ` | ` float`| Gravity |
| `AnimationFrame ` | ` float`| Current animation frame |
| `PlaySpeed ` | ` float`| Animation speed |
| `LightEnable ` | ` bool`| Lighting enabled |
| `ContrastEnable ` | ` bool`| Contrast enabled |

### Examples

```lua
local model = GetModel(index)
if model then
    model.Visible = true
    model.Alpha = 0.8
    model.Scale = 1.5
end
```

## GameItem

Represents an item on the client.

### Properties

| Property | Type | Description |
| :---------- | :--- | :-------- |
| `Type ` | ` int`| ID do item (Section*512 + Index) |
| `Level ` | ` int`| Item Level |
| `Durability ` | ` int`| Current durability |
| `DamageMin ` | ` int`| Minimum damage |
| `DamageMax ` | ` int`| Maximum damage |
| `RequireLevel ` | ` int`| Required level |
| `SocketCount ` | ` int`| Number of sockets |
| `Option1 ` | ` int`| Excellent Option/Skill |

### Examples

```lua
--Access selected item
if SelectedItem then
    local itemLevel = SelectedItem.Level
    local itemType = SelectedItem.Type
end
```

## Packet

Used to build and read network packets. Identical to `CPacket` of the server.

### Methods

#### Constructor

```lua
Packet() -> Packet
```

Creates a new Packet object.

#### Writing

```lua
packet:WriteByte(val) -> void
packet:WriteWord(val) -> void
packet:WriteDword(val) -> void
packet:WriteString(val) -> void
```

Writes data to the packet.

**Parameters:**
- `val`: Value to be written (byte, word, dword or string)

#### Reading

```lua
packet:ReadByte() -> number
packet:ReadWord() -> number
packet:ReadDword() -> number
packet:ReadString() -> string
```

Reads data from the packet.

**Return**: Read value of the corresponding type.

### Examples

```lua
--Create and send package (in the OnPacketRecv hook)
function BridgeFunction_OnPacketRecv(index, head, packet)
    if head == 0x1234 then
        local subCode = packet:ReadByte()
        local message = packet:ReadString()
        
        --Create response
        local response = Packet()
        response:WriteByte(0x01) --Success
        response:WriteString("OK")
        
        --Send response (client specific function)
        --SendPacket(index, 0x5678, response)
    end
end
```

## Global Variables

Some objects are available as global variables:

| Variable | Type | Description |
| :------- | :--- | :-------- |
| `Hero ` | ` GameCharacter`| Local Player Object |
| `MouseX ` | ` int`| Current mouse X position |
| `MouseY ` | ` int`| Current mouse Y position |
| `MouseLButton ` | ` int`| Left Mouse Button State |
| `MouseRButton ` | ` int`| Right-click status |
| `SelectedCharacter ` | ` GameCharacter`| Currently selected character |
| `SelectedItem ` | ` GameItem`| Currently selected item |

### Examples

```lua
function BridgeFunction_OnInterfaceRender()
    --Use Hero directly
    if Hero then
        local text = string.format("Level: %d", Hero.Level)
        UIRenderText_RenderText(10, 10, text, 200, 20, 1)
    end
    
    --Use mouse position
    local mouseText = string.format("Mouse: %d, %d", MouseX, MouseY)
    UIRenderText_RenderText(MouseX + 10, MouseY + 10, mouseText, 150, 20, 1)
end
```

## Important Notes

1. **Validation**: Always validate that objects are not `nil` before use
2. **Read-only properties**: Some properties can be read-only on the client
3. **Performance**: Accessing properties is fast, but avoid unnecessary loops
4. **Thread Safety**: Objects are only accessible on the client's main thread

## Related Functions

- [GetCharacter](../Functions/GetCharacter.md) - Gets character object
- [GetModel](../Functions/GetModel.md) - Get model object
- [Global Variables](10-Global-Variables.md) - Complete documentation of global variables
- [Bridge Functions](05-Bridge-Functions.md) - Hooks that use these objects

