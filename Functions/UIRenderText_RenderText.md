# UIRenderText_RenderText

Renders text on the screen.

## Signature

```lua
UIRenderText_RenderText(x, y, text, w, h, sort) -> void
```

## Parameters

- `x`(number): X position on the screen (pixels)
- `y`(number): Y position on the screen (pixels)
- `text`(string): Text to be rendered
- `w`(number): Width of the text area (pixels)
- `h`(number): Text area height (pixels)
- `sort`(number): Render order (z-order, highest = rendered on top)

## Return

`nil`- This function does not return a value.

## Features

- Text will be rendered using the previously defined font, color and background
- The parameter `sort` controls the rendering order (z-order)
- Text that is too long will be cut off if it exceeds the specified width
- Must be called within `BridgeFunction_OnInterfaceRender`

## Examples

### Basic Use

```lua
function BridgeFunction_OnInterfaceRender()
    --Set text color
    UIRenderText_SetTextColor(255, 255, 255, 255) --Branco
    
    --Render text
    UIRenderText_RenderText(100, 100, "Hello World!", 200, 20, 1)
end
```### Text with Player Information```lua
function BridgeFunction_OnInterfaceRender()
    if Hero == nil then return end
    
    --Player information
    local info = string.format("Level: %d | HP: %.0f/%.0f", 
        Hero.Level, Hero.CurHP, Hero.MaxHP)
    
    UIRenderText_SetTextColor(255, 255, 255, 255)
    UIRenderText_RenderText(10, 10, info, 300, 20, 1)
end
```### Multiple Texts with Z-Order```lua
function BridgeFunction_OnInterfaceRender()
    --Background text (low sort)
    UIRenderText_SetBgColor(0, 0, 0, 200)
    UIRenderText_RenderText(100, 100, "", 200, 100, 1)
    
    --Main text (high sort, appears on top)
    UIRenderText_SetTextColor(255, 255, 255, 255)
    UIRenderText_RenderText(110, 110, "Main Text", 180, 20, 10)
    
    --Secondary text
    UIRenderText_SetTextColor(200, 200, 200, 255)
    UIRenderText_RenderText(110, 135, "Secondary Text", 180, 20, 10)
end
```### Text with Different Colors```lua
function BridgeFunction_OnInterfaceRender()
    if Hero == nil then return end
    
    --Player name (white)
    UIRenderText_SetTextColor(255, 255, 255, 255)
    UIRenderText_RenderText(10, 10, Hero.ID, 200, 20, 1)
    
    --Level (yellow)
    UIRenderText_SetTextColor(255, 255, 0, 255)
    local levelText = "Level:" .. Hero.Level
    UIRenderText_RenderText(10, 35, levelText, 200, 20, 1)
    
    --HP (further)
    UIRenderText_SetTextColor(0, 255, 0, 255)
    local hpText = string.format("HP: %.0f/%.0f", Hero.CurHP, Hero.MaxHP)
    UIRenderText_RenderText(10, 60, hpText, 200, 20, 1)
end
```

## Important Notes

1. **Set color before**: Always set the text color before calling `RenderText`
2. **Use sort for z-order**: Larger values ​​of `sort` render over
3. **Formate strings**: Use `string.format` for dynamic texts
4. **Validate objects**: Always check that objects are not `nil` before use
5. **Performance**: Avoid rendering text off-screen

## Related Functions

- [UIRenderText_SetTextColor](UIRenderText_SetTextColor.md) - Set text color
- [UIRenderText_SetBgColor](UIRenderText_SetBgColor.md) - Set background color
- [UIRenderText_SetFont](UIRenderText_SetFont.md) - Define font
- [RenderTipText](RenderTipText.md) - Renderiza tooltip
- [UI System](../08-UI-System.md) - Complete UI System documentation

