# EnableAlphaBlend

Enables standard alpha blending (additive).

## Signature

```lua
EnableAlphaBlend() -> void
```

## Parameters

None.

## Return

`nil`- This function does not return a value.

## Usage

Enables standard alpha blending, allowing you to render objects with transparency. Use before rendering transparent elements and disable afterwards with `DisableAlphaBlend`.

## Examples

### Transparency Rendering

```lua
function BridgeFunction_OnInterfaceRender()
    --Enable alpha blending
    EnableAlphaBlend()
    
    --Render image with transparency (50%)
    RenderBitmap(textureId, 100, 100, 200, 200, 0, 0, 1, 1, false, false, 0.5)
    
    --Desabilitar alpha blending
    DisableAlphaBlend()
end
```### Multiple Transparent Elements```lua
function BridgeFunction_OnInterfaceRender()
    EnableAlphaBlend()
    
    --Render multiple elements transparent
    RenderBitmap(texture1, 100, 100, 200, 200, 0, 0, 1, 1, false, false, 0.7)
    RenderBitmap(texture2, 150, 150, 200, 200, 0, 0, 1, 1, false, false, 0.5)
    RenderBitmap(texture3, 200, 200, 200, 200, 0, 0, 1, 1, false, false, 0.3)
    
    DisableAlphaBlend()
end
```### Fade In/Out```lua
local alpha = 0.0
local fadingIn = true

function BridgeFunction_OnInterfaceRender()
    --Update alpha
    if fadingIn then
        alpha = alpha + 0.01
        if alpha >= 1.0 then
            alpha = 1.0
            fadingIn = false
        end
    else
        alpha = alpha - 0.01
        if alpha <= 0.0 then
            alpha = 0.0
            fadingIn = true
        end
    end
    
    --Render with fade
    EnableAlphaBlend()
    RenderBitmap(textureId, 100, 100, 200, 200, 0, 0, 1, 1, false, false, alpha)
    DisableAlphaBlend()
end
```

## Important Notes

1. **Always disable later**: Call `DisableAlphaBlend()` after rendering transparent elements
2. **Performance**: Alpha blending has a performance cost, use only when necessary
3. **Order matters**: Set state before rendering
4. **Combine with RenderBitmap**: Use the parameter `alpha ` of `RenderBitmap` to control transparency

## Related Functions

- [DisableAlphaBlend](DisableAlphaBlend.md) - Disable alpha blending
- [EnableAlphaBlendMinus](EnableAlphaBlendMinus.md) - Enable subtrative alpha blending
- [RenderBitmap](RenderBitmap.md) - Renders image with alpha control
- [Rendering System](../06-Rendering-System.md) - Complete rendering system documentation

