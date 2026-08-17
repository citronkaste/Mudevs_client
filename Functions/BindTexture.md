# BindTexture

Binds a texture for rendering.

## Signature

```lua
BindTexture(textureId) -> void
```

## Parameters

- `textureId`(number): ID of the texture to be linked

## Return

`nil`- This function does not return a value.

## Usage

Binds a texture for rendering. Usually called automatically by rendering functions, but can be used to swap textures manually.

## Examples

### Manual Linking

```lua
function BridgeFunction_OnInterfaceRender()
    --Link texture manually
    BindTexture(textureId1)
    
    --Render using linked texture
    RenderBitmap(textureId1, 100, 100, 200, 200, 0, 0, 1, 1, false, false, 1.0)
    
    --Change texture
    BindTexture(textureId2)
    RenderBitmap(textureId2, 300, 100, 200, 200, 0, 0, 1, 1, false, false, 1.0)
end
```

## Important Notes

1. **Linking**: Defines which texture will be used in future renders
2. **Automatic**: It is generally not necessary to call manually
3. **Performance**: May be useful for optimization in some cases
4. **Use with caution**: May affect subsequent renderings

## Related Functions

- [LoadBitmap](LoadBitmap.md) - Load texture
- [RenderBitmap](RenderBitmap.md) - Renders image
- [RenderImage](RenderImage.md) - Renders simplified image
- [Rendering System](../06-Rendering-System.md) - Complete rendering system documentation

