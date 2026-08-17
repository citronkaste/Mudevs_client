# EnableDepthMask

Enables written non-Z-buffer.

## Signature

```lua
EnableDepthMask() -> void
```

## Parameters

None.

## Return

`nil`- This function does not return a value.

## Usage

Enables writing to the Z-buffer, allowing objects to update the depth buffer. Use when you want objects to affect the depth buffer.

## Examples

### Depth Configuration

```lua
function BridgeFunction_OnInterfaceRender()
    --Enable written non-Z-buffer
    EnableDepthMask()
    
    --Render objects that should affect the depth buffer
    RenderBitmap(objectTexture, 100, 100, 200, 200, 0, 0, 1, 1, false, false, 1.0)
end
```

## Important Notes

1. **Z-buffer**: Controls writing to the depth buffer
2. **Use with 3D objects**: Ideal for objects that must interact with the depth buffer
3. **Performance**: May have an impact on performance depending on use
4. **Combine with DisableDepthTest**: Use together with other depth functions for complete control

## Related Functions

- [DisableDepthMask](DisableDepthMask.md) - Disables writing to the Z-buffer
- [DisableDepthTest](DisableDepthTest.md) - Disable depth test
- [Rendering System](../06-Rendering-System.md) - Complete rendering system documentation

