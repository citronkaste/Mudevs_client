# CheckMouseIn

Checks whether the mouse cursor is within a rectangular area.

## Signature

```lua
CheckMouseIn(x, y, w, h) -> bool
```

## Parameters

- `x`(number): X coordinate of the upper left corner of the rectangle
- `y`(number): Y coordinate of the upper left corner of the rectangle
- `w`(number): Width of the rectangle
- `h`(number): Height of the rectangle

## Return

`bool ` - ` true `if the mouse is within the rectangular area,` false`otherwise.

## Examples

### Hover Check

```lua
function BridgeFunction_OnInterfaceRender()
    local buttonX, buttonY = 100, 100
    local buttonW, buttonH = 200, 50
    
    --Check if the mouse is over the button
    if CheckMouseIn(buttonX, buttonY, buttonW, buttonH) then
        --Mouse is over the button (hover)
        --Render highlighted button
        UIRenderText_SetTextColor(255, 255, 0, 255) --Yellow
    else
        --Mouse is not over the button
        UIRenderText_SetTextColor(255, 255, 255, 255) --Branco
    end
    
    UIRenderText_RenderText(buttonX, buttonY, "Button", buttonW, buttonH, 1)
end
```### Click Button```lua
function BridgeFunction_OnInterfaceRender()
    local buttonX, buttonY = 100, 100
    local buttonW, buttonH = 200, 50
    
    --Check button click
    if IsMouseClicked() and CheckMouseIn(buttonX, buttonY, buttonW, buttonH) then
        --Button was clicked
        print("Button clicked!")
    end
end
```### Multiple Button System```lua
local buttons = {
    {x = 100, y = 100, w = 200, h = 50, text = "Button 1"},
    {x = 100, y = 160, w = 200, h = 50, text = "Button 2"},
    {x = 100, y = 220, w = 200, h = 50, text = "Button 3"}
}

function BridgeFunction_OnInterfaceRender()
    for i, button in ipairs(buttons) do
        local hovered = CheckMouseIn(button.x, button.y, button.w, button.h)
        
        --Render button with different color if hover
        local color = hovered and RGBA(100, 150, 255, 255) or RGBA(50, 100, 200, 255)
        
        --Check click
        if IsMouseClicked() and hovered then
            print("Button clicked:" .. button.text)
        end
    end
end
```

## Important Notes

1. **Coordinates**: Coordinates are in screen pixels (0,0 = top left corner)
2. **Inclusive area**: The check includes the edges of the rectangle
3. **Performance**: The function is very fast, can be called multiple times per frame
4. **Combine with IsMouseClicked**: Use together with `IsMouseClicked` to detect clicks in specific areas

## Related Functions

- [IsMouseClicked](IsMouseClicked.md) - Checks if button was clicked
- [IsMouseHeld](IsMouseHeld.md) - Checks if button is pressed
- [MouseX](../10-Global-Variables.md#mousex) - X position of the mouse
- [MouseY](../10-Global-Variables.md#mousey) - Y position of the mouse
- [Input System](../07-Input-System.md) - Complete documentation of the input system

