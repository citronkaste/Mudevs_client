# DisableDepthMask

Disables writing to the Z-buffer.

## Signature

```lua
DisableDepthMask() -> void
```

## Parameters

None.

## Return

`nil`- This function does not return a value.

## Usage

Disables writing to the Z-buffer, allowing objects to be rendered without affecting the depth buffer. Useful for elements that should not interfere with the depth test of other objects.

## Examples

### Elements That Do Not Affect Depth

```lua
function BridgeFunction_OnInterfaceRender()
    --Disable writing to the Z-buffer
    DisableDepthMask()
    
    --Render elements that should not affect the depth buffer
    RenderBitmap(overlayTexture, 100, 100, 200, 200, 0, 0, 1, 1, false, false, 0.5)
    
    --Rehabilitate (if necessary)
    EnableDepthMask()
end
```

## Important Notes

1. **Does not affect depth**: Rendered objects do not update the Z-buffer
2. **Use for overlays**: Ideal for elements that should not interfere with the depth test
3. **Performance**: May improve performance in some cases
4. **Combine with other functions**: Use together with other depth functions for complete control

## Related Functions

- [EnableDepthMask](EnableDepthMask.md) - Enables written non-Z-buffer
- [DisableDepthTest](DisableDepthTest.md) - Disable depth test
- [Rendering System](../06-Rendering-System.md) - Complete rendering system documentation

