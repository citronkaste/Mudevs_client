# UIRenderText_SetFont

Sets the current font for text rendering.

## Signature

```lua
UIRenderText_SetFont(fontHandle) -> void
```

## Parameters

- `fontHandle`(number): Source handle to be used

## Return

`nil`- This function does not return a value.

## Usage

Sets the font that will be used to render text. Configure the source before calling `UIRenderText_RenderText`.

## Examples

### Set Font

```lua
function BridgeFunction_OnInterfaceRender()
    --Set font (example: handle 0 = default font)
    UIRenderText_SetFont(0)
    
    --Render text with the defined font
    UIRenderText_RenderText(100, 100, "Text with standard font", 200, 20, 1)
end
```### Multiple Sources```lua
function BridgeFunction_OnInterfaceRender()
    --Text with standard font
    UIRenderText_SetFont(0)
    UIRenderText_RenderText(100, 100, "Normal Text", 200, 20, 1)
    
    --Text with different font
    UIRenderText_SetFont(1)
    UIRenderText_RenderText(100, 130, "Different Text", 200, 20, 1)
end
```

## Important Notes

1. **Set before rendering**: Set the font before calling `UIRenderText_RenderText`
2. **Font Handle**: The handle is usually obtained from the game's font system
3. **Persistence**: The defined font will be used until it is changed
4. **Default font**: Generally handle 0 is the default font

## Related Functions

- [UIRenderText_RenderText](UIRenderText_RenderText.md) - Renders text
- [UIRenderText_SetTextColor](UIRenderText_SetTextColor.md) - Set text color
- [UI System](../08-UI-System.md) - Complete UI System documentation

