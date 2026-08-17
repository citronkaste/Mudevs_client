# Packet System

This document describes the complete network packet handling system available in the Lua Client API.

## Overview

The packet system allows you to read packets received from the server and create custom packets to send. This allows bidirectional communication between client and server through customized packages.

## Packet Object

The object `Packet ` is used to read and write network packet data. It is identical to ` CPacket` of the server.

### Creation

```lua
local packet = Packet()
```

Creates a new empty Packet object.

## Packet Reading

No hook `BridgeFunction_OnPacketRecv `, you receive an object ` Packet`that can be read.

### ReadByte

Reads one byte (8 bits) from the packet.

```lua
local value = packet:ReadByte() -> number
```

**Return:** Value from 0 to 255.

### ReadWord

Reads a word (16 bits) from the packet.

```lua
local value = packet:ReadWord() -> number
```

**Return:** Value from 0 to 65535.

### ReadDword

Reads a dword (32-bit) from the package.

```lua
local value = packet:ReadDword() -> number
```

**Return:** Value from 0 to 4294967295.

### ReadString

Reads a string from the package.

```lua
local value = packet:ReadString() -> string
```

**Return:** String read from the package.

**Note:** The string is usually preceded by a byte or word indicating its size.

## Package Writing

To create custom packages (usually to send to the server).

### WriteByte

Writes one byte to the packet.

```lua
packet:WriteByte(value) -> void
```

**Parameters:**
- `value`(number): Value from 0 to 255

### WriteWord

Write a word on the package.

```lua
packet:WriteWord(value) -> void
```

**Parameters:**
- `value`(number): Value from 0 to 65535

### WriteDword

Write a dword to the package.

```lua
packet:WriteDword(value) -> void
```

**Parameters:**
- `value`(number): Value from 0 to 4294967295

### WriteString

Writes a string to the package.

```lua
packet:WriteString(value) -> void
```

**Parameters:**
- `value`(string): String to be written

**Note:** It is generally necessary to write the size of the string before (byte or word).

## BridgeFunction_OnPacketRecv

Hook called when a specific packet is received from the server.

### Signature

```lua
function BridgeFunction_OnPacketRecv(index, head, packet)
    --Process package
    return 0 --or 1 to consume
end
```

### Parameters

- `index`(number): Related character index
- `head`(number): Package header (header/opcode)
- `packet`(Packet): Packet object with data

### Return

- `0`: Continues normal package processing
- `1`: Consumes the packet (blocks standard processing)

### Basic Example

```lua
--Custom header constant
local CUSTOM_HEADER = 0x1234

function BridgeFunction_OnPacketRecv(index, head, packet)
    --Check if it is our customized package
    if head == CUSTOM_HEADER then
        --Read packet data
        local subCode = packet:ReadByte()
        local message = packet:ReadString()
        
        --Process message
        if subCode == 0x01 then
            --Show notification
            UIRenderText_RenderText(100, 100, message, 300, 20, 1)
        end
        
        --Consume package (block default processing)
        return 1
    end
    
    --Continue normal processing for other packages
    return 0
end
```## Example: Notification System```lua
--Custom headers
local NOTIFICATION_HEADER = 0x1234
local NOTIFICATION_TYPE_INFO = 0x01
local NOTIFICATION_TYPE_WARNING = 0x02
local NOTIFICATION_TYPE_ERROR = 0x03

function BridgeFunction_OnPacketRecv(index, head, packet)
    if head == NOTIFICATION_HEADER then
        local type = packet:ReadByte()
        local title = packet:ReadString()
        local message = packet:ReadString()
        
        --Determine color based on type
        local r, g, b = 255, 255, 255 --White standard
        if type == NOTIFICATION_TYPE_INFO then
            r, g, b = 100, 150, 255 --Azul
        elseif type == NOTIFICATION_TYPE_WARNING then
            r, g, b = 255, 200, 0 --Yellow
        elseif type == NOTIFICATION_TYPE_ERROR then
            r, g, b = 255, 0, 0 --Red
        end
        
        --Show notification
        UIRenderText_SetTextColor(r, g, b, 255)
        UIRenderText_RenderText(100, 100, title, 400, 25, 10)
        UIRenderText_SetTextColor(255, 255, 255, 255)
        UIRenderText_RenderText(100, 130, message, 400, 20, 10)
        
        return 1
    end
    
    return 0
end
```## Example: Custom Data System```lua
--Header for custom character data
local CUSTOM_CHAR_DATA_HEADER = 0x5678

function BridgeFunction_OnPacketRecv(index, head, packet)
    if head == CUSTOM_CHAR_DATA_HEADER then
        --Read custom data
        local customLevel = packet:ReadDword()
        local customExp = packet:ReadDword()
        local customPoints = packet:ReadWord()
        local customName = packet:ReadString()
        
        --Store data (in global variable or structure)
        customPlayerData = {
            level = customLevel,
            exp = customExp,
            points = customPoints,
            name = customName
        }
        
        --Update UI with custom data
        -- ...
        
        return 1
    end
    
    return 0
end
```## Example: Multiple Packages```lua
--Multiple headers
local HEADER_CHAT = 0x1001
local HEADER_ITEM = 0x1002
local HEADER_SKILL = 0x1003

function BridgeFunction_OnPacketRecv(index, head, packet)
    if head == HEADER_CHAT then
        local channel = packet:ReadByte()
        local sender = packet:ReadString()
        local message = packet:ReadString()
        
        --Process custom chat
        ProcessCustomChat(channel, sender, message)
        return 1
        
    elseif head == HEADER_ITEM then
        local itemId = packet:ReadWord()
        local itemLevel = packet:ReadByte()
        local itemOptions = packet:ReadDword()
        
        --Process custom item
        ProcessCustomItem(itemId, itemLevel, itemOptions)
        return 1
        
    elseif head == HEADER_SKILL then
        local skillId = packet:ReadWord()
        local skillLevel = packet:ReadByte()
        
        --Process custom skill
        ProcessCustomSkill(skillId, skillLevel)
        return 1
    end
    
    return 0
end
```

## Package Shipping

**Note:** Sending packages often requires a specific client function that may not be available in the standard Lua API. Consult the documentation for your specific client.

**Conceptual example:**
```lua
function SendCustomPacket(header, packet)
    --Customer specific role (may vary)
    --SendPacketToServer(header, packet)
end

--Create and send package
local packet = Packet()
packet:WriteByte(0x01) --SubCode
packet:WriteString("Custom message")
SendCustomPacket(0x1234, packet)
```

## Good Practices

1. **Use constants for headers**: Define constants for custom package headers
2. **Validate data before reading**: Always check if there is enough data in the packet
3. **Read in correct order**: Read the data in the same order as it was written to the server
4. **Consume packages when necessary**: Return `1` to block standard processing
5. **Treat errors**: Use `pcall` to protect against reading errors
6. **Document formats**: Document the format of each custom package

## Error Handling

```lua
function BridgeFunction_OnPacketRecv(index, head, packet)
    if head == CUSTOM_HEADER then
        local success, error = pcall(function()
            --Read packet data
            local subCode = packet:ReadByte()
            local message = packet:ReadString()
            
            --Process
            ProcessMessage(subCode, message)
        end)
        
        if not success then
            --Error processing package
            --Error log (if available)
            return 1 --Consume even if there is an error
        end
        
        return 1
    end
    
    return 0
end
```

## Related Functions

- [BridgeFunction_OnPacketRecv](../Functions/BridgeFunction_OnPacketRecv.md) - Detailed documentation
- [Packet](04-Game-Objects.md#packet) - Packet object documentation
- [Bridge Functions](05-Bridge-Functions.md) - Complete hook system

