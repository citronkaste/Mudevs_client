# Input system

This document describes the complete input capture system (mouse and keyboard) available in the Lua Client API.

## Overview

The input system allows you to capture mouse and keyboard events, allowing you to create interactive interfaces and respond to user actions.

## Mouse

### IsMouseClicked

Checks whether the left mouse button was clicked in the current frame.

```lua
IsMouseClicked() -> bool
```**Return:**` true ` if the button was clicked in this frame,` false ` otherwise.

**Features:**
- Return `true` just once per click
- Useful for detecting unique (non-maintained) clicks

**Example:**
```lua
function BridgeFunction_OnInterfaceRender()
    if IsMouseClicked() then
        --Button was clicked in this frame
        print("Mouse clicked!")
    end
end
```

### IsMouseHeld

Checks whether the left mouse button is being held down.

```lua
IsMouseHeld() -> bool
```**Return:**` true ` if the button is pressed,` false ` otherwise.

**Features:**
- Return `true` while the button is pressed
- Useful for drag & drop, continuous selection, etc.

**Example:**
```lua
function BridgeFunction_OnInterfaceRender()
    if IsMouseHeld() then
        --Button is being held down
        --Do something continually
    end
end
```

### CheckMouseIn

Checks whether the mouse cursor is within a rectangular area.

```lua
CheckMouseIn(x, y, w, h) -> bool
```

**Parameters:**
- `x`(number): X coordinate of the top left corner
- `y`(number): Y coordinate of the upper left corner
- `w`(number): Width of the rectangle
- `h`(number): Height of the rectangle

**Return:**`true ` if the mouse is within the area,`false` otherwise.

**Example:**
```lua
function BridgeFunction_OnInterfaceRender()
    local buttonX, buttonY = 100, 100
    local buttonW, buttonH = 200, 50
    
    --Check if the mouse is over the button
    if CheckMouseIn(buttonX, buttonY, buttonW, buttonH) then
        --Mouse is over the button (hover)
        --Render highlighted button
    end
    
    --Check button click
    if IsMouseClicked() and CheckMouseIn(buttonX, buttonY, buttonW, buttonH) then
        --Button was clicked
        --Take action
    end
end
```

### Mouse Global Variables

| Variable | Type | Description |
| :------- | :--- | :-------- |
| `MouseX ` | ` int`| Current mouse X position (pixels) |
| `MouseY ` | ` int`| Current mouse Y position (pixels) |
| `MouseLButton ` | ` int`| Left button status (0 or 1) |
| `MouseRButton ` | ` int`| Right button status (0 or 1) |

**Example:**
```lua
function BridgeFunction_OnInterfaceRender()
    --Show mouse position
    local text = string.format("Mouse: %d, %d", MouseX, MouseY)
    UIRenderText_RenderText(MouseX + 10, MouseY + 10, text, 150, 20, 1)
    
    --Check right button
    if MouseRButton == 1 then
        --Right button pressed
    end
end
```

## Keyboard

### SEASON3B_IsPress

Checks whether a key has been pressed in the current frame.

```lua
SEASON3B_IsPress(key) -> bool
```

**Parameters:**
- `key `(number): VK code of the key (ex:` 0x4D`for M)

**Return:**`true ` if the key was pressed in this frame,`false` otherwise.

**Features:**
- Return `true` just once per press
- Useful for toggles, shortcuts, etc.

**Example:**
```lua
local uiVisible = false

function BridgeFunction_OnInterfaceRender()
    --Toggle UI with M key
    if SEASON3B_IsPress(0x4D) then --VK_M
        uiVisible = not uiVisible
    end
    
    if uiVisible then
        --Render UI
    end
end
```

### SEASON3B_IsRelease

Checks whether a key was released in the current frame.

```lua
SEASON3B_IsRelease(key) -> bool
```

**Parameters:**
- `key`(number): VK key code

**Return:**`true ` if the key was released in this frame,`false` otherwise.

**Example:**
```lua
function BridgeFunction_OnInterfaceRender()
    if SEASON3B_IsRelease(0x1B) then --VK_ESCAPE
        --ESC key was released
        --Close menu, etc.
    end
end
```

### SEASON3B_IsRepeat

Checks whether a key is being held down (repeat).

```lua
SEASON3B_IsRepeat(key) -> bool
```

**Parameters:**
- `key`(number): VK key code

**Return:**`true ` if the key is being held down,`false` otherwise.

**Features:**
- Return `true` continuously while the key is pressed
- Useful for continuous movement, scrolling, etc.

**Example:**
```lua
function BridgeFunction_OnInterfaceRender()
    --Continuous movement with arrows
    if SEASON3B_IsRepeat(0x25) then --VK_LEFT
        --Move left continuously
    elseif SEASON3B_IsRepeat(0x27) then --VK_RIGHT
        --Move right continuously
    end
end
```

### SEASON3B_IsNone

Checks whether a key is not being pressed.

```lua
SEASON3B_IsNone(key) -> bool
```

**Parameters:**
- `key`(number): VK key code

**Return:**`true ` if the key is not pressed,`false` otherwise.

**Example:**
```lua
function BridgeFunction_OnInterfaceRender()
    if SEASON3B_IsNone(0x20) then --VK_SPACE
        --Space is not pressed
        --Reset status, etc.
    end
end
```

## Key Codes (VK Codes)

Virtual Windows key codes. Look[02-Enumerations.md](02-Enumerations.md)for complete list.

**Common examples:**
- `0x4D`= M
- `0x1B`= ESC
- `0x20`= Space
- `0x0D`= Enter
- `0x25`= Left Arrow
- `0x26`= Up Arrow
- `0x27`= Right Arrow
- `0x28`= Arrow Down
- `0x70`= F1
- `0x71`=F2
- ... until `0x7B`= F12

## Input Blocking

### SetBlockInput

Locks or unlocks the game input.

```lua
SetBlockInput(block) -> void
```

**Parameters:**
- `block `(bool):` true `to block game input,` false`to unlock

**Usage:** Useful when you have a modal UI that must capture all input.

**Example:**
```lua
local modalOpen = false

function BridgeFunction_OnInterfaceRender()
    if modalOpen then
        --Block game input
        SetBlockInput(true)
        
        --Render modal
        --Process custom input
        
        --Close modal with ESC
        if SEASON3B_IsPress(0x1B) then
            modalOpen = false
            SetBlockInput(false)
        end
    end
end
```## Complete Example: Button System```lua
--Button structure
local buttons = {
    {x = 100, y = 100, w = 200, h = 50, text = "Button 1", clicked = false},
    {x = 100, y = 160, w = 200, h = 50, text = "Button 2", clicked = false}
}

function BridgeFunction_OnInterfaceRender()
    for i, button in ipairs(buttons) do
        --Check hover
        local hovered = CheckMouseIn(button.x, button.y, button.w, button.h)
        
        --Check click
        if IsMouseClicked() and hovered then
            button.clicked = true
            --Execute button action
            print("Button clicked:" .. button.text)
        end
        
        --Render button
        local color = hovered and RGBA(100, 150, 255, 255) or RGBA(50, 100, 200, 255)
        --Render rectangle (using RenderBitmap or similar)
        
        --Render text
        UIRenderText_SetTextColor(255, 255, 255, 255)
        UIRenderText_RenderText(button.x + 10, button.y + 15, button.text, button.w - 20, 20, 1)
    end
end
```## Example: Shortcut System```lua
function BridgeFunction_OnInterfaceRender()
    --Shortcut Ctrl+S
    if SEASON3B_IsPress(0x11) and SEASON3B_IsPress(0x53) then --Ctrl + S
        --Save something
        print("Saving...")
    end
    
    --Alt+T shortcut
    if SEASON3B_IsPress(0x12) and SEASON3B_IsPress(0x54) then --Alt + T
        --toggle something
        print("Toggle activated")
    end
end
```

## Good Practices

1. **Use IsMouseClicked for single actions**: Avoid using IsMouseHeld for actions that should only happen once
2. **Check area before processing click**: Use `CheckMouseIn` before processing clicks
3. **Block input when necessary**: Use `SetBlockInput` for modals and UIs that must capture all input
4. **Use VK codes as constants**: Set constants for common key codes
5. **Process input in OnInterfaceRender**: Input must be processed every frame

## Related Functions

- [IsMouseClicked](../Functions/IsMouseClicked.md) - Detailed documentation
- [CheckMouseIn](../Functions/CheckMouseIn.md) - Detailed documentation
- [SEASON3B_IsPress](../Functions/SEASON3B_IsPress.md) - Detailed documentation
- [SetBlockInput](../Functions/SetBlockInput.md) - Detailed documentation
- [Enumerations](02-Enumerations.md) - Complete VK codes
- [Global Variables](10-Global-Variables.md) - MouseX, MouseY, etc.

