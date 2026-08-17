# IsMouseClicked

Checks whether the left mouse button was clicked in the current frame.

## Signature

```lua
IsMouseClicked() -> bool
```## Parameters

None.

## Return `bool `-` true ` if the left mouse button was clicked on the current frame,` false` otherwise.

## Features

- Return `true` just once per click
- Useful for detecting unique (non-maintained) clicks
- Must be called within `BridgeFunction_OnInterfaceRender` to function correctly

## Examples

### Basic Use

```lua
function BridgeFunction_OnInterfaceRender()
    if IsMouseClicked() then
        --Button was clicked in this frame
        UIRenderText_RenderText(100, 100, "Mouse clicked!", 200, 20, 1)
    end
end
```### Click on Specific Area```lua
function BridgeFunction_OnInterfaceRender()
    --Check button click (100, 100, 200x50)
    if IsMouseClicked() and CheckMouseIn(100, 100, 200, 50) then
        --Button was clicked
        UIRenderText_RenderText(100, 200, "Button Clicked!", 200, 20, 1)
    end
end
```### Button System```lua
local buttons = {
    {x = 100, y = 100, w = 200, h = 50, text = "Button 1"},
    {x = 100, y = 160, w = 200, h = 50, text = "Button 2"}
}

function BridgeFunction_OnInterfaceRender()
    if IsMouseClicked() then
        for i, button in ipairs(buttons) do
            if CheckMouseIn(button.x, button.y, button.w, button.h) then
                --Button clicked
                print("Button clicked:" .. button.text)
            end
        end
    end
end
```## Difference between IsMouseClicked and IsMouseHeld

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

1. **Call on OnInterfaceRender**: This function must be called within `BridgeFunction_OnInterfaceRender` to function correctly
2. **Once per frame**: Returns `true` only once per click, even if called multiple times in the same frame
3. **Combine with CheckMouseIn**: Use `CheckMouseIn` to check if the click was in a specific area
4. **Performance**: The function is very fast, it can be called every frame without problems

## Related Functions

- [IsMouseHeld](IsMouseHeld.md) - Checks if the button is being held down
- [CheckMouseIn](CheckMouseIn.md) - Checks if the mouse is in a rectangular area
- [MouseLButton](../10-Global-Variables.md#mouselbutton) - Global left button state variable
- [Input System](../07-Input-System.md) - Complete documentation of the input system

