# DisableTexture

Disables texturing (allows you to draw solid colors).

## Signature

```lua
DisableTexture(disable) -> void
```

## Parameters

- `disable `(bool):` true `to disable textures,` false`to enable

## Return

`nil`- This function does not return a value.

## Usage

Disables texturing, allowing you to render solid shapes without texture. Useful for drawing simple geometric shapes, colorful rectangles, etc.

## Examples

### Draw Solid Rectangle

```lua
function BridgeFunction_OnInterfaceRender()
    --Disable textures
    DisableTexture(true)
    
    --Configure color (using RenderBitmap or similar without texture)
    --Render solid rectangle
    --(specific implementation may vary)
    
    --Re-enable textures
    DisableTexture(false)
end
```### Geometric Shapes```lua
function BridgeFunction_OnInterfaceRender()
    --Disable textures for drawing shapes
    DisableTexture(true)
    
    --Draw solid shapes
    --(specific implementation may vary)
    
    --Re-enable textures
    DisableTexture(false)
    
    --Render textured elements normally
    RenderImage(textureId, 100, 100, 200, 200)
end
```

## Important Notes

1. **Solid Colors**: Allows you to render without texture, just colors
2. **Always rehabilitate**: Call `DisableTexture(false)` after using
3. **Use for simple shapes**: Ideal for rectangles, lines and basic geometric shapes
4. **Performance**: Can improve performance for simple elements

## Related Functions

- [RenderBitmap](RenderBitmap.md) - Renders image with texture
- [RenderImage](RenderImage.md) - Renders simplified image
- [Color4f](Color4f.md) - Creates color
- [RGBA](RGBA.md) - Creates RGBA color
- [Rendering System](../06-Rendering-System.md) - Complete rendering system documentation

