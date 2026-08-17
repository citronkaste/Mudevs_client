# UI System

This document describes the complete user interface and text rendering system available in the Lua Client API.

## Overview

The UI System allows you to render text, configure fonts, colors and create custom user interfaces directly on the client.

## Text Rendering

### UIRenderText_SetFont

Sets the current font for text rendering.

```lua
UIRenderText_SetFont(fontHandle) -> void
```

**Parameters:**
- `fontHandle`(number): Source handle to be used

**Usage:** Configure the font before rendering text. The handle is usually obtained from the game's font system.

**Example:**
```lua
function BridgeFunction_OnInterfaceRender()
    --Set font (example: handle 0 = default font)
    UIRenderText_SetFont(0)
    
    --Render text with the defined font
    UIRenderText_RenderText(100, 100, "Text with standard font", 200, 20, 1)
end
```

### UIRenderText_SetTextColor

Sets the color of the text.

```lua
UIRenderText_SetTextColor(r, g, b, a) -> void
```

**Parameters:**
- `r `, ` g `, ` b `, ` a`(number): Cor components (0 - 255)

**Features:**
- The set color will be used for all rendered text until changed
- Alpha component controls transparency (255 = opaque, 0 = transparent)

**Example:**
```lua
function BridgeFunction_OnInterfaceRender()
    --Red text
    UIRenderText_SetTextColor(255, 0, 0, 255)
    UIRenderText_RenderText(100, 100, "Red Text", 200, 20, 1)
    
    --Semi-transparent green text
    UIRenderText_SetTextColor(0, 255, 0, 128)
    UIRenderText_RenderText(100, 130, "Green Text", 200, 20, 1)
    
    --White text
    UIRenderText_SetTextColor(255, 255, 255, 255)
    UIRenderText_RenderText(100, 160, "White Text", 200, 20, 1)
end
```

### UIRenderText_SetBgColor

Sets the background color of the text.

```lua
UIRenderText_SetBgColor(r, g, b, a) -> void
```

**Parameters:**
- `r `, ` g `, ` b `, ` a`(number): Cor components (0 - 255)

**Usage:** Creates a colored background behind text, useful for highlighting important information.

**Example:**
```lua
function BridgeFunction_OnInterfaceRender()
    --Semi-transparent black background
    UIRenderText_SetBgColor(0, 0, 0, 128)
    
    --White text
    UIRenderText_SetTextColor(255, 255, 255, 255)
    UIRenderText_RenderText(100, 100, "Text with background", 200, 30, 1)
end
```

### UIRenderText_RenderText

Renders text on the screen.

```lua
UIRenderText_RenderText(x, y, text, w, h, sort) -> void
```

**Parameters:**
- `x `, ` y`(number): Position on the screen (pixels)
- `text`(string): Text to be rendered
- `w `, ` h`(number): Width and height of the text area (pixels)
- `sort`(number): Rendering order (highest = rendered last/top)

**Features:**
- Text will be rendered using the previously defined font, color and background
- The parameter `sort` controls the rendering order (z-order)
- Text that is too long will be cut off if it exceeds the specified width

**Example:**
```lua
function BridgeFunction_OnInterfaceRender()
    if Hero then
        --Player information
        local info = string.format("Level: %d | HP: %.0f/%.0f", 
            Hero.Level, Hero.CurHP, Hero.MaxHP)
        
        UIRenderText_SetTextColor(255, 255, 255, 255)
        UIRenderText_RenderText(10, 10, info, 300, 20, 1)
    end
end
```

### RenderTipText

Renders tooltip style text.

```lua
RenderTipText(x, y, text) -> void
```

**Parameters:**
- `x `, ` y`(number): Position on the screen (pixels)
- `text`(string): Texto do tooltip

**Usage:** Renders text in tooltip format (usually with background and border).

**Example:**
```lua
function BridgeFunction_OnInterfaceRender()
    --Check hover over item
    if CheckMouseIn(100, 100, 50, 50) then
        --Show tooltip
        RenderTipText(MouseX + 10, MouseY + 10, "Item: Sword +15")
    end
end
```

## Interface Check

### IsWriteInterfaceOpen

Checks whether the writing interface (chat/input) is open.

```lua
IsWriteInterfaceOpen() -> bool
```**Return:**` true ` if the writing interface is open,` false ` otherwise.

**Usage:** Useful for disabling certain features when the player is typing.

**Example:**
```lua
function BridgeFunction_OnInterfaceRender()
    --Do not process custom input if chat is open
    if IsWriteInterfaceOpen() then
        return
    end
    
    --Process custom input
    if SEASON3B_IsPress(0x4D) then --M
        --Do something
    end
end
```## Complete Example: Custom HUD```lua
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
    
    --HP bar (red)
    UIRenderText_SetTextColor(255, 0, 0, 255)
    local hpText = string.format("HP: %.1f%%", hpPercent)
    UIRenderText_RenderText(10, 35, hpText, 300, 20, 1)
    
    --MP bar (blue)
    UIRenderText_SetTextColor(0, 100, 255, 255)
    local mpText = string.format("MP: %.1f%%", mpPercent)
    UIRenderText_RenderText(10, 60, mpText, 300, 20, 1)
    
    --Status PK
    if Hero.PK > 3 then
        UIRenderText_SetTextColor(255, 0, 0, 255)
        UIRenderText_RenderText(10, 85, "PK Status:" .. Hero.PK, 300, 20, 1)
    end
end
```## Example: Options Menu```lua
local menuVisible = false
local menuX, menuY = 100, 100
local menuW, menuH = 200, 300

function BridgeFunction_OnInterfaceRender()
    --Toggle menu with key M
    if SEASON3B_IsPress(0x4D) then --VK_M
        menuVisible = not menuVisible
    end
    
    if menuVisible then
        --Block game input
        SetBlockInput(true)
        
        --Menu background
        UIRenderText_SetBgColor(50, 50, 50, 200)
        UIRenderText_RenderText(menuX, menuY, "", menuW, menuH, 1)
        
        --Title
        UIRenderText_SetTextColor(255, 255, 0, 255)
        UIRenderText_RenderText(menuX + 10, menuY + 10, "Options Menu", menuW - 20, 25, 2)
        
        --Options
        UIRenderText_SetTextColor(255, 255, 255, 255)
        UIRenderText_RenderText(menuX + 10, menuY + 40, "Option 1", menuW - 20, 20, 2)
        UIRenderText_RenderText(menuX + 10, menuY + 65, "Option 2", menuW - 20, 20, 2)
        UIRenderText_RenderText(menuX + 10, menuY + 90, "Option 3", menuW - 20, 20, 2)
        
        --Close with ESC
        if SEASON3B_IsPress(0x1B) then --VK_ESCAPE
            menuVisible = false
            SetBlockInput(false)
        end
    end
end
```## Example: Item Tooltip```lua
function BridgeFunction_OnInterfaceRender()
    --Check if mouse is over item area
    local itemX, itemY = 100, 100
    local itemW, itemH = 50, 50
    
    if CheckMouseIn(itemX, itemY, itemW, itemH) then
        --Show tooltip
        local tooltipX = MouseX + 15
        local tooltipY = MouseY + 15
        
        --Tooltip background
        UIRenderText_SetBgColor(30, 30, 30, 220)
        UIRenderText_RenderText(tooltipX, tooltipY, "", 200, 100, 10)
        
        --Texto do tooltip
        UIRenderText_SetTextColor(255, 215, 0, 255) --Golden
        UIRenderText_RenderText(tooltipX + 5, tooltipY + 5, "Espada +15", 190, 20, 11)
        
        UIRenderText_SetTextColor(200, 200, 200, 255)
        UIRenderText_RenderText(tooltipX + 5, tooltipY + 30, "Dano: 150-200", 190, 20, 11)
        UIRenderText_RenderText(tooltipX + 5, tooltipY + 55, "Durability: 200/200", 190, 20, 11)
    end
end
```

## Good Practices

1. **Set color before rendering**: Always set the text color before calling `RenderText`
2. **Use sort for z-order**: Larger values ​​of `sort` render over
3. **Format strings efficiently**: Use `string.format` for dynamic texts
4. **Validate objects before use**: Always check that `Hero ` it is not `nil`
5. **Avoid rendering off-screen**: Make sure elements are visible before rendering
Error 500 (Server Error)!!1500.That’s an error.There was an error. Please try again later.That’s all we know.`RenderTipText` is ideal for contextual information

## Related Functions

- [UIRenderText_SetFont](../Functions/UIRenderText_SetFont.md) - Detailed documentation
- [UIRenderText_SetTextColor](../Functions/UIRenderText_SetTextColor.md) - Detailed documentation
- [UIRenderText_RenderText](../Functions/UIRenderText_RenderText.md) - Detailed documentation
- [RenderTipText](../Functions/RenderTipText.md) - Detailed documentation
- [IsWriteInterfaceOpen](../Functions/IsWriteInterfaceOpen.md) - Detailed documentation
- [Rendering System](06-Rendering-System.md) - Rendering images and graphics

