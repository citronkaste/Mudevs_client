# DisableDepthTest

Disables the Z-buffer depth test (draws over everything).

## Signature

```lua
DisableDepthTest() -> void
```

## Parameters

None.

## Return

`nil`- This function does not return a value.

## Usage

Disables depth testing, allowing elements to be rendered on top of everything, regardless of distance. Useful for UI that should always appear at the front.

## Examples

### Always-on UI

```lua
function BridgeFunction_OnInterfaceRender()
    --Disable depth test for UI
    DisableDepthTest()
    
    --Render UI (always in front)
    RenderImage(uiTexture, 100, 100, 200, 200)
    UIRenderText_RenderText(110, 110, "UI Text", 180, 20, 1)
    
    --Re-enable depth test (if necessary)
    --EnableDepthTest() -- If available
end
```### Overlay the UI```lua
function BridgeFunction_OnInterfaceRender()
    --Desabilitar depth test
    DisableDepthTest()
    
    --Render overlay
    EnableAlphaBlend()
    RenderBitmap(overlayTexture, 0, 0, 800, 600, 0, 0, 1, 1, false, false, 0.5)
    DisableAlphaBlend()
    
    --Render UI elements
    UIRenderText_RenderText(10, 10, "Overlay UI", 200, 20, 1)
end
```

## Important Notes

1. **UI always in front**: Use for UI elements that should always appear in front
2. **Performance**: Disabling depth test can improve performance for 2D elements
3. **Use with caution**: May cause problems if used incorrectly with 3D elements
4. **Match with UI**: Ideal for user interfaces and overlays

## Related Functions

- [EnableDepthMask](EnableDepthMask.md) - Enables written non-Z-buffer
- [DisableDepthMask](DisableDepthMask.md) - Disables writing to the Z-buffer
- [RenderBitmap](RenderBitmap.md) - Renders image
- [Rendering System](../06-Rendering-System.md) - Complete rendering system documentation

