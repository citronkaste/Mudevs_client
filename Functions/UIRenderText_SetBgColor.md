# UIRenderText_SetBgColor

Sets the background color of the text.

## Signature

```lua
UIRenderText_SetBgColor(r, g, b, a) -> void
```

## Parameters

- `r `, ` g `, ` b `, ` a`(number): Cor components (0 - 255)

## Return

`nil`- This function does not return a value.

## Usage

Sets the background color that will be used to render text. Creates a colorful background behind text, useful for highlighting important information.

## Examples

### Basic Fund

```lua
function BridgeFunction_OnInterfaceRender()
    --Semi-transparent black background
    UIRenderText_SetBgColor(0, 0, 0, 128)
    
    --White text
    UIRenderText_SetTextColor(255, 255, 255, 255)
    UIRenderText_RenderText(100, 100, "Text with background", 200, 30, 1)
end
```### Information Highlight```lua
function BridgeFunction_OnInterfaceRender()
    --Red background for alerts
    UIRenderText_SetBgColor(255, 0, 0, 200)
    UIRenderText_SetTextColor(255, 255, 255, 255)
    UIRenderText_RenderText(100, 100, "ALERT!", 200, 30, 1)
    
    --Green background for success
    UIRenderText_SetBgColor(0, 255, 0, 200)
    UIRenderText_RenderText(100, 140, "Success!", 200, 30, 1)
end
```### Tooltip with Background```lua
function BridgeFunction_OnInterfaceRender()
    if CheckMouseIn(100, 100, 50, 50) then
        --Tooltip background
        UIRenderText_SetBgColor(30, 30, 30, 220)
        UIRenderText_RenderText(MouseX + 15, MouseY + 15, "", 200, 80, 10)
        
        --Texto do tooltip
        UIRenderText_SetTextColor(255, 255, 255, 255)
        UIRenderText_RenderText(MouseX + 20, MouseY + 20, "Tooltip Information", 190, 20, 11)
        UIRenderText_RenderText(MouseX + 20, MouseY + 45, "More information here", 190, 20, 11)
    end
end
```

## Important Notes

1. **Set before rendering**: Set the background color before calling `UIRenderText_RenderText`
2. **Components 0-255**: Use values ​​from 0 to 255 for each component
3. **Alpha**: The alpha component controls background transparency
4. **Highlight**: Useful for highlighting important information

## Related Functions

- [UIRenderText_RenderText](UIRenderText_RenderText.md) - Renders text
- [UIRenderText_SetTextColor](UIRenderText_SetTextColor.md) - Set text color
- [RenderTipText](RenderTipText.md) - Renderiza tooltip
- [UI System](../08-UI-System.md) - Complete UI System documentation

