# IsMouseHeld

Checks whether the left mouse button is being held down.

## Signature

```lua
IsMouseHeld() -> bool
```## Parameters

None.

## Return `bool `-` true ` if the left mouse button is being held down,` false` otherwise.

## Features

- Return `true` continuously while the button is pressed
- Useful for drag & drop, continuous selection, dragging elements
- Must be called within `BridgeFunction_OnInterfaceRender` to function correctly

## Examples

### Basic Use

```lua
function BridgeFunction_OnInterfaceRender()
    if IsMouseHeld() then
        --Button is being held down
        UIRenderText_RenderText(100, 100, "Mouse pressed", 200, 20, 1)
    end
end
```### Drag & Drop```lua
local dragging = false
local dragStartX, dragStartY = 0, 0
local windowX, windowY = 100, 100

function BridgeFunction_OnInterfaceRender()
    if IsMouseClicked() and CheckMouseIn(windowX, windowY, 200, 30) then
        --Start drag
        dragging = true
        dragStartX = MouseX - windowX
        dragStartY = MouseY - windowY
    end
    
    if IsMouseHeld() and dragging then
        --Update window position
        windowX = MouseX - dragStartX
        windowY = MouseY - dragStartY
    else
        dragging = false
    end
    
    --Render window
    RenderImage(windowTextureId, windowX, windowY, 200, 200)
end
```### Continuous Selection```lua
function BridgeFunction_OnInterfaceRender()
    if IsMouseHeld() then
        --Draw selection area
        local startX, startY = 100, 100
        local endX, endY = MouseX, MouseY
        
        --Render selection rectangle
        --(using RenderBitmap or similar)
    end
end
```## Difference between IsMouseHeld and IsMouseClicked

- **IsMouseClicked**: Returns `true` only once when the button is pressed
- **IsMouseHeld**: Returns `true` continuously while the button is pressed

**Example:**
```lua
function BridgeFunction_OnInterfaceRender()
    if IsMouseClicked() then
        --Executes only once per click
        print("Click detected")
    end
    
    if IsMouseHeld() then
        --Runs continuously while pressed
        --Useful for drag & drop, continuous selection, etc.
    end
end
```## Important Notes

1. **Call on OnInterfaceRender**: This function must be called within `BridgeFunction_OnInterfaceRender ` 2. **Continuous**: Returns ` true` continuously while the button is pressed
3. **Combine with CheckMouseIn**: Use `CheckMouseIn` to check if the mouse is in a specific area
4. **Performance**: The function is very fast, it can be called every frame without problems

## Related Functions

- [IsMouseClicked](IsMouseClicked.md) - Checks if button was clicked
- [CheckMouseIn](CheckMouseIn.md) - Checks if the mouse is in a rectangular area
- [MouseLButton](../10-Global-Variables.md#mouselbutton) - Global left button state variable
- [Input System](../07-Input-System.md) - Complete documentation of the input system

