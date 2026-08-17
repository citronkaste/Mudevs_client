# BridgeFunction_OnPacketRecv

Called when a specific packet is received from the server.

## Signature

```lua
function BridgeFunction_OnPacketRecv(index, head, packet)
    --Process package
    return 0 --or 1 to consume
end
```

## Parameters

- `index`(number): Related character index
- `head`(number): Package header (header/opcode)
- `packet`(Packet): Packet object with data

## Return

- `0`: Continues normal package processing
- `1`: Consumes the packet (blocks standard processing)

## Usage

Ideal for:
- Process custom server packages
- Intercept and modify existing packages
- Implement package-based client-side functionalities

## Examples

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
```### Notification System```lua
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
```### Multiple Packages```lua
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
```## Error Handling```lua
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

## Important Notes

1. **Consumption**: Return `1` blocks standard packet processing
2. **Read**: Read the data in the correct order (as written on the server)
3. **Validation**: Always validate data size before reading
4. **Performance**: Process packages quickly to avoid customer lock-in
5. **Use constants**: Define constants for custom package headers

## Related Functions

- [Packet](../04-Game-Objects.md#packet) - Packet object documentation
- [BridgeFunction_OnInterfaceRender](BridgeFunction_OnInterfaceRender.md) - Rendering loop
- [BridgeFunction_OnLoadInterface](BridgeFunction_OnLoadInterface.md) - Initialization
- [Packet System](../09-Packet-System.md) - Complete package system documentation
- [Bridge Functions](../05-Bridge-Functions.md) - Complete documentation of hooks

