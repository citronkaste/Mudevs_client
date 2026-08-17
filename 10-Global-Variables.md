# Global Variables

This document describes all global variables available in the Client Lua API.

## Overview

Global variables are objects and values ​​that are always available anywhere in the script, without the need to call functions to obtain them.

## Hero

The local player object (player character).

**Type:**`GameCharacter`

**Description:** Represents the character of the player who is playing. It is equivalent to calling `GetCharacter(index)` to the local player index.

**Properties:** See[GameCharacter](04-Game-Objects.md#gamecharacter)for complete list.

**Example:**
```lua
function BridgeFunction_OnInterfaceRender()
    if Hero then
        --Access player properties
        local level = Hero.Level
        local name = Hero.ID
        local hp = Hero.CurHP
        local maxHp = Hero.MaxHP
        
        --Calculate HP percentage
        local hpPercent = (hp / maxHp) * 100
        
        --Render information
        local text = string.format("%s (Lv.%d) - HP: %.1f%%", name, level, hpPercent)
        UIRenderText_RenderText(10, 10, text, 300, 20, 1)
    end
end
```**Note:** Always valid if ` Hero` it is not ` nil` before use, especially during charging or disconnection.

## MouseX

Current X position of the mouse cursor on the screen.

**Type:**`int`

**Description:** Mouse X coordinate in pixels (0 = left of screen).

**Example:**
```lua
function BridgeFunction_OnInterfaceRender()
    --Show mouse position
    local text = string.format("Mouse X: %d", MouseX)
    UIRenderText_RenderText(MouseX + 10, MouseY + 10, text, 150, 20, 1)
end
```

## MouseY

Current Y position of the mouse cursor on the screen.

**Type:**`int`

**Description:** Mouse Y coordinate in pixels (0 = top of screen).

**Example:**
```lua
function BridgeFunction_OnInterfaceRender()
    --Show mouse position
    local text = string.format("Mouse Y: %d", MouseY)
    UIRenderText_RenderText(MouseX + 10, MouseY + 10, text, 150, 20, 1)
end
```

## MouseLButton

Left mouse button state.

**Type:**`int`

**Values:**
- `0`: Button not pressed
- `1`: Button pressed

**Description:** Indicates whether the left mouse button is currently pressed.

**Example:**
```lua
function BridgeFunction_OnInterfaceRender()
    if MouseLButton == 1 then
        --Left button is pressed
        UIRenderText_RenderText(10, 10, "Left Button Pressed", 250, 20, 1)
    end
end
```**Note:** To detect single clicks, use ` IsMouseClicked()` instead of checking this variable.

## MouseRButton

Right mouse button status.

**Type:**`int`

**Values:**
- `0`: Button not pressed
- `1`: Button pressed

**Description:** Indicates whether the right mouse button is currently pressed.

**Example:**
```lua
function BridgeFunction_OnInterfaceRender()
    if MouseRButton == 1 then
        --Right button is pressed
        UIRenderText_RenderText(10, 10, "Right Button Pressed", 250, 20, 1)
    end
end
```

## SelectedCharacter

The character currently selected by the player.

**Type:**`GameCharacter ` or`nil`

**Description:** Represents the character (player, monster, NPC) that is currently selected by the player. Could it be `nil` if no character is selected.

**Properties:** See[GameCharacter](04-Game-Objects.md#gamecharacter)for complete list.

**Example:**
```lua
function BridgeFunction_OnInterfaceRender()
    if SelectedCharacter then
        --Show selected character information
        local text = string.format("Selected: %s (Lv.%d)", 
            SelectedCharacter.ID, SelectedCharacter.Level)
        UIRenderText_RenderText(10, 10, text, 300, 20, 1)
        
        --Show target's HP
        if SelectedCharacter.CurHP > 0 then
            local hpPercent = (SelectedCharacter.CurHP / SelectedCharacter.MaxHP) * 100
            local hpText = string.format("HP: %.1f%%", hpPercent)
            UIRenderText_RenderText(10, 35, hpText, 200, 20, 1)
        end
    end
end
```

## SelectedItem

The item currently selected by the player.

**Type:**`GameItem ` or`nil`

**Description:** Represents the item that is currently selected by the player. Could it be `nil` if no item is selected.

**Properties:** See[GameItem](04-Game-Objects.md#gameitem)for complete list.

**Example:**
```lua
function BridgeFunction_OnInterfaceRender()
    if SelectedItem then
        --Show selected item information
        local text = string.format("Item: Type %d, Level +%d", 
            SelectedItem.Type, SelectedItem.Level)
        UIRenderText_RenderText(10, 10, text, 300, 20, 1)
        
        --Show durability
        local durText = string.format("Durability: %d", SelectedItem.Durability)
        UIRenderText_RenderText(10, 35, durText, 200, 20, 1)
    end
end
```## Complete Example: HUD with Global Variables```lua
function BridgeFunction_OnInterfaceRender()
    --Player information
    if Hero then
        --HP Bar
        local hpPercent = (Hero.CurHP / Hero.MaxHP) * 100
        UIRenderText_SetTextColor(255, 0, 0, 255)
        local hpText = string.format("HP: %.0f/%.0f (%.1f%%)", 
            Hero.CurHP, Hero.MaxHP, hpPercent)
        UIRenderText_RenderText(10, 10, hpText, 300, 20, 1)
        
        --Basic information
        UIRenderText_SetTextColor(255, 255, 255, 255)
        local infoText = string.format("%s - Level %d", Hero.ID, Hero.Level)
        UIRenderText_RenderText(10, 35, infoText, 300, 20, 1)
    end
    
    --Target information
    if SelectedCharacter then
        UIRenderText_SetTextColor(255, 255, 0, 255)
        local targetText = string.format("Alvo: %s (Lv.%d)", 
            SelectedCharacter.ID, SelectedCharacter.Level)
        UIRenderText_RenderText(10, 60, targetText, 300, 20, 1)
    end
    
    --Mouse position
    UIRenderText_SetTextColor(200, 200, 200, 255)
    local mouseText = string.format("Mouse: %d, %d", MouseX, MouseY)
    UIRenderText_RenderText(MouseX + 15, MouseY + 15, mouseText, 150, 20, 1)
    
    --State of the mouse buttons
    if MouseLButton == 1 then
        UIRenderText_SetTextColor(0, 255, 0, 255)
        UIRenderText_RenderText(10, 500, "Left Button", 150, 20, 1)
    end
    if MouseRButton == 1 then
        UIRenderText_SetTextColor(0, 255, 0, 255)
        UIRenderText_RenderText(170, 500, "Right Button", 150, 20, 1)
    end
end
```## Example: Tooltip Following Mouse```lua
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
    
    --Additional state-based information
    if Hero then
        local info = string.format("Level: %d", Hero.Level)
        UIRenderText_RenderText(tooltipX + 5, tooltipY + 30, info, 190, 20, 11)
    end
end
```

## Important Notes

1. **Validation**: Always validate that variables are not `nil ` before use (especially `Hero `, ` SelectedCharacter `, ` SelectedItem`)
2. **Update**: Variables are updated every frame in the `OnInterfaceRender`
3. **Performance**: Accessing global variables is very fast, but avoid heavy calculations in loops
4. **Thread Safety**: Variables are only accessible on the client's main thread

## Related Functions

- [GetCharacter](../Functions/GetCharacter.md) - Gets character by index
- [IsMouseClicked](../Functions/IsMouseClicked.md) - Detects mouse clicks
- [CheckMouseIn](../Functions/CheckMouseIn.md) - Check mouse position
- [Game Objects](04-Game-Objects.md) - Complete documentation of objects

