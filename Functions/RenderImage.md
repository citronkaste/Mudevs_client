# RenderImage

Simplified version of image rendering.

## Signature

```lua
RenderImage(id, x, y, w, h) -> void
```

## Parameters

- `id`(number): ID da textura
- `x `, ` y`(number): Position on the screen (pixels)
- `w `, ` h`(number): Width and height (pixels)

## Return

`nil`- This function does not return a value.

## Usage

Renders a 2D image in a simplified way, without UV control. Use for fast rendering when you don't need advanced control.

## Examples

### Basic Rendering

```lua
function BridgeFunction_OnInterfaceRender()
    --Render simple image
    RenderImage(textureId, 100, 100, 200, 200)
end
```### UI Buttons```lua
local buttonTextureId = 100

function BridgeFunction_OnInterfaceRender()
    --Render button
    RenderImage(buttonTextureId, 100, 100, 200, 50)
    
    --Render text over button
    UIRenderText_RenderText(150, 115, "Button", 100, 20, 1)
end
```### Multiple Images```lua
function BridgeFunction_OnInterfaceRender()
    --Render multiple images
    RenderImage(icon1, 10, 10, 32, 32)
    RenderImage(icon2, 50, 10, 32, 32)
    RenderImage(icon3, 90, 10, 32, 32)
end
```

## Difference between RenderImage and RenderBitmap

- **RenderImage**: Simplified, renders full texture, without UV control
- **RenderBitmap**: Complete, allows control of UV, scale and transparency

**When to use:**
- Use `RenderImage` for simple and fast rendering
- Use `RenderBitmap` when you need UV or transparency control

## Important Notes

1. **Simple and fast**: Simplified version for fast rendering
2. **Full Texture**: Always renders the full texture
3. **No UV**: Does not allow UV coordinate control
4. **Performance**: Faster than `RenderBitmap` for simple cases

## Related Functions

- [RenderBitmap](RenderBitmap.md) - Full version with UV control
- [LoadBitmap](LoadBitmap.md) - Load texture
- [BindTexture](BindTexture.md) - Links texture
- [Rendering System](../06-Rendering-System.md) - Complete rendering system documentation

