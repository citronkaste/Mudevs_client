# EnableAlphaBlendMinus

Enables subtractive alpha blending.

## Signature

```lua
EnableAlphaBlendMinus() -> void
```

## Parameters

None.

## Return

`nil`- This function does not return a value.

## Usage

Enables subtractive alpha blending, which subtracts colors instead of adding them. Useful for darkening effects, shadows and special effects.

## Examples

### Darkening Effect

```lua
function BridgeFunction_OnInterfaceRender()
    --Enable subtrative alpha blending
    EnableAlphaBlendMinus()
    
    --Render dark overlay
    RenderBitmap(darkOverlayTexture, 0, 0, 800, 600, 0, 0, 1, 1, false, false, 0.3)
    
    --Disable
    DisableAlphaBlend()
end
```### Sombra```lua
function BridgeFunction_OnInterfaceRender()
    --Render shadow with subtractive blending
    EnableAlphaBlendMinus()
    RenderBitmap(shadowTexture, 105, 105, 200, 200, 0, 0, 1, 1, false, false, 0.5)
    DisableAlphaBlend()
    
    --Render normal object
    EnableAlphaBlend()
    RenderBitmap(objectTexture, 100, 100, 200, 200, 0, 0, 1, 1, false, false, 1.0)
    DisableAlphaBlend()
end
```

## Important Notes

1. **Subtractive effect**: Subtracts colors instead of adding, creating a darkening effect
2. **Use with caution**: May create unexpected effects if used incorrectly
3. **Always disable**: Call `DisableAlphaBlend()` after using
4. **Special effects**: Ideal for shadows, dark overlays and special visual effects

## Related Functions

- [EnableAlphaBlend](EnableAlphaBlend.md) - Enables standard alpha blending
- [DisableAlphaBlend](DisableAlphaBlend.md) - Disable alpha blending
- [RenderBitmap](RenderBitmap.md) - Renders image
- [Rendering System](../06-Rendering-System.md) - Complete rendering system documentation

