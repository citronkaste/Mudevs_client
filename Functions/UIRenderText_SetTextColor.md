# UIRenderText_SetTextColor

Sets the color of the text.

## Signature

```lua
UIRenderText_SetTextColor(r, g, b, a) -> void
```

## Parameters

- `r `, ` g `, ` b `, ` a`(number): Cor components (0 - 255)

## Return

`nil`- This function does not return a value.

## Usage

Sets the color that will be used to render text. Configure the color before calling `UIRenderText_RenderText`.

## Examples

### Basic Colors

```lua
function BridgeFunction_OnInterfaceRender()
    --Red text
    UIRenderText_SetTextColor(255, 0, 0, 255)
    UIRenderText_RenderText(100, 100, "Red Text", 200, 20, 1)
    
    --Green text
    UIRenderText_SetTextColor(0, 255, 0, 255)
    UIRenderText_RenderText(100, 130, "Green Text", 200, 20, 1)
    
    --Blue text
    UIRenderText_SetTextColor(0, 0, 255, 255)
    UIRenderText_RenderText(100, 160, "Blue Text", 200, 20, 1)
    
    --White text
    UIRenderText_SetTextColor(255, 255, 255, 255)
    UIRenderText_RenderText(100, 190, "White Text", 200, 20, 1)
end
```### Text with Transparency```lua
function BridgeFunction_OnInterfaceRender()
    --Semi-transparent text (50%)
    UIRenderText_SetTextColor(255, 255, 255, 128)
    UIRenderText_RenderText(100, 100, "Semi-transparent text", 250, 20, 1)
end
```### Dynamic Colors```lua
function BridgeFunction_OnInterfaceRender()
    if Hero then
        --Non-HP based core
        local hpPercent = (Hero.CurHP / Hero.MaxHP) * 100
        local r, g, b = 255, 255, 255
        
        if hpPercent < 30 then
            r, g, b = 255, 0, 0 --Red (low HP)
        elseif hpPercent < 60 then
            r, g, b = 255, 255, 0 --Yellow (medium HP)
        else
            r, g, b = 0, 255, 0 --Green (High HP)
        end
        
        UIRenderText_SetTextColor(r, g, b, 255)
        local hpText = string.format("HP: %.0f%%", hpPercent)
        UIRenderText_RenderText(10, 10, hpText, 200, 20, 1)
    end
end
```

## Important Notes

1. **Set before rendering**: Set the color before calling `UIRenderText_RenderText`
2. **Components 0-255**: Use values ​​from 0 to 255 for each component
3. **Alpha**: The alpha component controls transparency (255 = opaque, 0 = transparent)
4. **Persistence**: The defined color will be used until it is changed

## Related Functions

- [UIRenderText_RenderText](UIRenderText_RenderText.md) - Renders text
- [UIRenderText_SetBgColor](UIRenderText_SetBgColor.md) - Set background color
- [RGBA](RGBA.md) - Creates color value
- [UI System](../08-UI-System.md) - Complete UI System documentation

