# RenderTipText

Renders tooltip style text.

## Signature

```lua
RenderTipText(x, y, text) -> void
```

## Parameters

- `x `, ` y`(number): Position on the screen (pixels)
- `text`(string): Texto do tooltip

## Return

`nil`- This function does not return a value.

## Usage

Renders text in tooltip format (usually with background and border). Useful for contextual information that appears when the mouse is over something.

## Examples

### Tooltip Básico

```lua
function BridgeFunction_OnInterfaceRender()
    --Check hover over item
    if CheckMouseIn(100, 100, 50, 50) then
        --Show tooltip
        RenderTipText(MouseX + 10, MouseY + 10, "Item: Sword +15")
    end
end
```### Tooltip with Information```lua
function BridgeFunction_OnInterfaceRender()
    if CheckMouseIn(100, 100, 50, 50) then
        --Tooltip with multiple information
        RenderTipText(MouseX + 10, MouseY + 10, "Sword +15\nDamage: 150-200\nDurability: 200/200")
    end
end
```### Conditional Tooltip```lua
function BridgeFunction_OnInterfaceRender()
    --Check different areas
    if CheckMouseIn(100, 100, 50, 50) then
        RenderTipText(MouseX + 10, MouseY + 10, "Button 1")
    elseif CheckMouseIn(160, 100, 50, 50) then
        RenderTipText(MouseX + 10, MouseY + 10, "Button 2")
    elseif CheckMouseIn(220, 100, 50, 50) then
        RenderTipText(MouseX + 10, MouseY + 10, "Button 3")
    end
end
```

## Important Notes

1. **Tooltip format**: Renders in specific tooltip format (with background and border)
2. **Position**: Generally positioned close to the mouse
3. **Contextual information**: Ideal for information that appears when hovering over the mouse
4. **Simple**: Simplified version, use `UIRenderText_RenderText` for more control

## Related Functions

- [UIRenderText_RenderText](UIRenderText_RenderText.md) - Renders text with complete control
- [CheckMouseIn](CheckMouseIn.md) - Checks if mouse is in area
- [UI System](../08-UI-System.md) - Complete UI System documentation

