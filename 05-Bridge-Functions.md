# Bridge Functions (Hooks)

This document describes the callback functions (hooks) available in the Lua Client API.

## Overview

Bridge Functions are special functions that the client automatically calls at specific times. You must implement these functions in your Lua script to respond to these events.

## BridgeFunction_OnLoadInterface

Called when the interface is being initialized.

### Signature

```lua
function BridgeFunction_OnLoadInterface()
    --Your logic here
end
```

### Parameters

None.

### Return

`nil`- This function does not return a value.

### Usage

Ideal for:
- Load textures and resources
- Initialize global variables
- Configure initial states

### Example

```lua
local myTextureId = 100

function BridgeFunction_OnLoadInterface()
    --Load custom texture
    LoadBitmap("Interface\\CustomUI\\button.bmp", myTextureId, 0, 0, 0, 1)
end
```

## BridgeFunction_OnInterfaceRender

**CRITICAL**: Called every frame of the game to render the UI.

### Signature

```lua
function BridgeFunction_OnInterfaceRender()
    --Your rendering logic here
end
```

### Parameters

None.

### Return

`nil`- This function does not return a value.

### Usage

Ideal for:
- Render custom UI
- Draw text and images
- Process user input
- Update visual elements

### Basic Example

```lua
function BridgeFunction_OnInterfaceRender()
    --Render custom text
    UIRenderText_SetTextColor(255, 255, 0, 255) --Yellow
    UIRenderText_RenderText(100, 100, "My Custom UI", 200, 20, 1)
end
```### Example with Input```lua
function BridgeFunction_OnInterfaceRender()
    --Check M key
    if SEASON3B_IsPress(0x4D) then --VK_M
        --Toggle UI
        showUI = not showUI
    end
    
    if showUI then
        --Render UI
        UIRenderText_RenderText(10, 10, "Active UI", 100, 20, 1)
    end
end
```### Example with Mouse```lua
function BridgeFunction_OnInterfaceRender()
    --Check mouse click in specific area
    if IsMouseClicked() and CheckMouseIn(100, 100, 200, 50) then
        --Button clicked
        UIRenderText_RenderText(100, 200, "Button Clicked!", 150, 20, 1)
    end
    
    --Draw visual button
    RenderImage(buttonTextureId, 100, 100, 200, 50)
end
```### Example with Hero```lua
function BridgeFunction_OnInterfaceRender()
    if Hero == nil then return end
    
    --Show player information
    local hpPercent = (Hero.CurHP / Hero.MaxHP) * 100
    local text = string.format("HP: %.1f%% | Level: %d", hpPercent, Hero.Level)
    
    UIRenderText_SetTextColor(0, 255, 0, 255) --Verde
    UIRenderText_RenderText(10, 10, text, 300, 20, 1)
end
```

### Important Notes

1. **Performance**: This function is called every frame. Keep the logic light!
2. **Rendering**: Configure rendering states before drawing
3. **Validation**: Always validate objects before using (Hero, GetCharacter, etc.)
Error 500 (Server Error)!!1500.That’s an error.There was an error. Please try again later.That’s all we know.`sort`)

## BridgeFunction_OnPacketRecv

Called when a specific packet is received from the server.

### Signature

```lua
function BridgeFunction_OnPacketRecv(index, head, packet)
    --Your logic here
end
```

### Parameters

- `index`(number): Related character index
- `head`(number): Package header (header)
- `packet`(Packet): Packet object with data

### Return

`number `- Return` 1 `to consume the package (block standard processing) or` 0`to continue normal processing.

### Usage

Ideal for:
- Process custom server packages
- Intercept and modify existing packages
- Implement package-based client-side functionalities

### Example

```lua
function BridgeFunction_OnPacketRecv(index, head, packet)
    --Intercept custom packet (header 0x1234)
    if head == 0x1234 then
        local subCode = packet:ReadByte()
        local message = packet:ReadString()
        
        --Process custom message
        if subCode == 0x01 then
            --Show notification
            UIRenderText_RenderText(100, 100, message, 300, 20, 1)
        end
        
        --Consume package (block default processing)
        return 1
    end
    
    --Continue normal processing
    return 0
end
```### Example with Multiple Packages```lua
--Header constants
local CUSTOM_HEADER_1 = 0x1234
local CUSTOM_HEADER_2 = 0x5678

function BridgeFunction_OnPacketRecv(index, head, packet)
    if head == CUSTOM_HEADER_1 then
        --Process first package type
        local data = packet:ReadDword()
        --Do something with date
        return 1
    elseif head == CUSTOM_HEADER_2 then
        --Process second package type
        local text = packet:ReadString()
        --Do something with text
        return 1
    end
    
    return 0
end
```

### Important Notes

1. **Consumption**: Return `1` blocks standard packet processing
2. **Read**: Read the data in the correct order (as written on the server)
3. **Validation**: Always validate data size before reading
4. **Performance**: Process packages quickly to avoid customer lock-in

## Good Practices

### 1. Object Validation

```lua
function BridgeFunction_OnInterfaceRender()
    if Hero == nil then return end
    
    --Use Hero safely
    local level = Hero.Level
end
```### 2. Error Handling```lua
function BridgeFunction_OnInterfaceRender()
    local success, error = pcall(function()
        --Your logic here
        if Hero then
            --Do something
        end
    end)
    
    if not success then
        --Error log (if available)
        --LogAdd(2, "Error: " .. tostring(error))
    end
end
```### 3. Performance Optimization```lua
local lastUpdate = 0
local updateInterval = 1000 --1 second

function BridgeFunction_OnInterfaceRender()
    local currentTime = GetTickCount() --If available
    
    --Update only every second
    if currentTime - lastUpdate > updateInterval then
        lastUpdate = currentTime
        --Heavy logic here
    end
    
    --Lightweight rendering every frame
    UIRenderText_RenderText(10, 10, "UI", 100, 20, 1)
end
```### 4. Code Organization```lua
--Global variables
local uiVisible = true
local buttonTextureId = 100

--Startup function
function BridgeFunction_OnLoadInterface()
    LoadBitmap("Interface\\button.bmp", buttonTextureId, 0, 0, 0, 1)
end

--Rendering function
function BridgeFunction_OnInterfaceRender()
    if uiVisible then
        RenderImage(buttonTextureId, 100, 100, 200, 50)
    end
end

--Packet processing function
function BridgeFunction_OnPacketRecv(index, head, packet)
    --Process packages
    return 0
end
```

## Related Functions

- [OnLoadInterface](../Functions/BridgeFunction_OnLoadInterface.md) - Detailed documentation
- [OnInterfaceRender](../Functions/BridgeFunction_OnInterfaceRender.md) - Detailed documentation
- [OnPacketRecv](../Functions/BridgeFunction_OnPacketRecv.md) - Detailed documentation
- [Packet](04-Game-Objects.md#packet) - Packet object documentation
- [Packet System](09-Packet-System.md) - Complete package system

