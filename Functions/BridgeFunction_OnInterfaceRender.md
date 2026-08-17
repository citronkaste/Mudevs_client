# BridgeFunction_OnInterfaceRender

**CRITICAL**: Called every frame of the game to render the UI.

## Signature

```lua
function BridgeFunction_OnInterfaceRender()
    --Your rendering logic here
end
```

## Parameters

None.

## Return

`nil`- This function does not return a value.

## Usage

Ideal for:
- Render custom UI
- Draw text and images
- Process user input
- Update visual elements
- Create custom HUDs

## Examples

### Basic Example

```lua
function BridgeFunction_OnInterfaceRender()
    --Render custom text
    UIRenderText_SetTextColor(255, 255, 0, 255) --Yellow
    UIRenderText_RenderText(100, 100, "My Custom UI", 200, 20, 1)
end
```### Player Information HUD```lua
function BridgeFunction_OnInterfaceRender()
    if Hero == nil then return end
    
    --Calculate percentages
    local hpPercent = (Hero.CurHP / Hero.MaxHP) * 100
    local mpPercent = (Hero.CurMP / Hero.MaxMP) * 100
    
    --Semi-transparent background
    UIRenderText_SetBgColor(0, 0, 0, 150)
    
    --Player information
    UIRenderText_SetTextColor(255, 255, 255, 255)
    local playerInfo = string.format("%s (Level %d)", Hero.ID, Hero.Level)
    UIRenderText_RenderText(10, 10, playerInfo, 300, 20, 1)
    
    --HP bar
    UIRenderText_SetTextColor(255, 0, 0, 255)
    local hpText = string.format("HP: %.1f%%", hpPercent)
    UIRenderText_RenderText(10, 35, hpText, 300, 20, 1)
    
    --MP bar
    UIRenderText_SetTextColor(0, 100, 255, 255)
    local mpText = string.format("MP: %.1f%%", mpPercent)
    UIRenderText_RenderText(10, 60, mpText, 300, 20, 1)
end
```### Input System```lua
local uiVisible = false

function BridgeFunction_OnInterfaceRender()
    --Toggle UI with M key
    if SEASON3B_IsPress(0x4D) then --VK_M
        uiVisible = not uiVisible
    end
    
    if uiVisible then
        --Render UI
        UIRenderText_RenderText(10, 10, "Active UI", 100, 20, 1)
    end
end
```### Mouse Button System```lua
function BridgeFunction_OnInterfaceRender()
    --Check mouse click in specific area
    if IsMouseClicked() and CheckMouseIn(100, 100, 200, 50) then
        --Button clicked
        UIRenderText_RenderText(100, 200, "Button Clicked!", 150, 20, 1)
    end
    
    --Draw visual button
    RenderImage(buttonTextureId, 100, 100, 200, 50)
end
```### Tooltip Following Mouse```lua
function BridgeFunction_OnInterfaceRender()
    --Tooltip that follows the mouse
    local tooltipText = "Tooltip Information"
    
    --Tooltip position (next to the mouse)
    local tooltipX = MouseX + 15
    local tooltipY = MouseY + 15
    
    --Tooltip background
    UIRenderText_SetBgColor(30, 30, 30, 200)
    UIRenderText_RenderText(tooltipX, tooltipY, "", 200, 50, 10)
    
    --Texto do tooltip
    UIRenderText_SetTextColor(255, 255, 255, 255)
    UIRenderText_RenderText(tooltipX + 5, tooltipY + 5, tooltipText, 190, 20, 11)
end
```

## Good Practices

### 1. Object Validation

```lua
function BridgeFunction_OnInterfaceRender()
    if Hero == nil then return end
    
    --Use Hero safely
    local level = Hero.Level
end
```### 2. Performance Optimization```lua
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
```### 3. Code Organization```lua
--Global variables
local uiVisible = true
local buttonTextureId = 100

--Rendering function
function BridgeFunction_OnInterfaceRender()
    if uiVisible then
        RenderImage(buttonTextureId, 100, 100, 200, 50)
    end
end
```### 4. Error Handling```lua
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
```

## Important Notes

1. **Performance**: This function is called every frame. Keep the logic light!
2. **Rendering**: Configure rendering states before drawing
3. **Validation**: Always validate objects before using (Hero, GetCharacter, etc.)
Error 500 (Server Error)!!1500.That’s an error.There was an error. Please try again later.That’s all we know.`sort`)
5. **Do not block**: Avoid operations that could block the frame

## Related Functions

- [BridgeFunction_OnLoadInterface](BridgeFunction_OnLoadInterface.md) - Resource initialization
- [BridgeFunction_OnPacketRecv](BridgeFunction_OnPacketRecv.md) - Package processing
- [UIRenderText_RenderText](UIRenderText_RenderText.md) - Text rendering
- [RenderBitmap](RenderBitmap.md) - Image rendering
- [Bridge Functions](../05-Bridge-Functions.md) - Complete documentation of hooks

