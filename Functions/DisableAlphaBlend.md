# DisableAlphaBlend

Disables alpha blending.

## Signature

```lua
DisableAlphaBlend() -> void
```

## Parameters

None.

## Return

`nil`- This function does not return a value.

## Usage

Disables alpha blending, returning to the default rendering mode (without transparency). Always call this function after rendering transparent elements.

## Examples

### Usage Pattern

```lua
function BridgeFunction_OnInterfaceRender()
    --Enable alpha blending
    EnableAlphaBlend()
    
    --Render transparent elements
    RenderBitmap(texture1, 100, 100, 200, 200, 0, 0, 1, 1, false, false, 0.5)
    RenderBitmap(texture2, 150, 150, 200, 200, 0, 0, 1, 1, false, false, 0.7)
    
    --Desabilitar alpha blending
    DisableAlphaBlend()
    
    --Render opaque elements (no transparency)
    RenderBitmap(texture3, 200, 200, 200, 200, 0, 0, 1, 1, false, false, 1.0)
end
```### Multiple Groups```lua
function BridgeFunction_OnInterfaceRender()
    --Group 1: Transparent elements
    EnableAlphaBlend()
    RenderBitmap(transparent1, 100, 100, 200, 200, 0, 0, 1, 1, false, false, 0.5)
    DisableAlphaBlend()
    
    --Group 2: Opaque elements
    RenderBitmap(opaque1, 300, 100, 200, 200, 0, 0, 1, 1, false, false, 1.0)
    
    --Group 3: More transparent elements
    EnableAlphaBlend()
    RenderBitmap(transparent2, 100, 300, 200, 200, 0, 0, 1, 1, false, false, 0.7)
    DisableAlphaBlend()
end
```

## Important Notes

1. **Always disable**: Always call `DisableAlphaBlend()` after rendering transparent elements
2. **Performance**: Disabling when not necessary improves performance
3. **Default state**: The default state is with alpha blending disabled
4. **Order matters**: Set state before rendering

## Related Functions

- [EnableAlphaBlend](EnableAlphaBlend.md) - Enables standard alpha blending
- [EnableAlphaBlendMinus](EnableAlphaBlendMinus.md) - Enable subtrative alpha blending
- [RenderBitmap](RenderBitmap.md) - Renders image
- [Rendering System](../06-Rendering-System.md) - Complete rendering system documentation

