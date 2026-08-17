# EnableLightMap

Habilita lightmapping.

## Signature

```lua
EnableLightMap() -> void
```

## Parameters

None.

## Return

`nil`- This function does not return a value.

## Usage

Enables lightmapping, allowing objects to be affected by lightmaps. Use for rendering with pre-calculated lighting.

## Examples

### Rendering with Lightmap

```lua
function BridgeFunction_OnInterfaceRender()
    --Habilitar lightmapping
    EnableLightMap()
    
    --Render objects with lightmap
    RenderBitmap(objectWithLightmap, 100, 100, 200, 200, 0, 0, 1, 1, false, false, 1.0)
end
```

## Important Notes

1. **Lightmapping**: Pre-calculated lighting system
2. **Performance**: May improve performance in some cases
3. **Use with 3D objects**: Ideal for objects that use lightmaps
4. **Engine Specific**: Functionality specific to the rendering engine

## Related Functions

- [RenderBitmap](RenderBitmap.md) - Renders image
- [Rendering System](../06-Rendering-System.md) - Complete rendering system documentation

