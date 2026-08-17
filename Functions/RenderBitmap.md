# RenderBitmap

Renders a 2D image with complete UV and transparency control.

## Signature

```lua
RenderBitmap(id, x, y, w, h, u, v, uw, vh, scale, startScale, alpha) -> void
```

## Parameters

- `id`(number): ID da textura
- `x `, ` y`(number): Position on the screen (pixels)
- `w `, ` h`(number): Width and height on the screen (pixels)
- `u `, ` v`(number): Initial UV coordinates (0.0 - 1.0)
- `uw `, ` vh`(number): UV Size (0.0 - 1.0)
- `scale`(bool): Apply scale
- `startScale`(bool): Initial scale
- `alpha`(number): Transparency (0.0 = transparent, 1.0 = opaque)

## Return

`nil`- This function does not return a value.

## Usage

Renders a 2D image with complete control over UV coordinates, scale and transparency. Use when you need precise control over rendering.

## Examples

### Basic Rendering

```lua
function BridgeFunction_OnInterfaceRender()
    --Render full texture
    RenderBitmap(textureId, 100, 100, 200, 200, 0, 0, 1, 1, false, false, 1.0)
end
```### Sprite Sheet (Texture Part)```lua
function BridgeFunction_OnInterfaceRender()
    --Render only part of the texture (sprite sheet)
    --u=0.25, v=0.25, uw=0.5, vh=0.5 = renders the central quarter of the texture
    RenderBitmap(textureId, 100, 100, 64, 64, 0.25, 0.25, 0.5, 0.5, false, false, 1.0)
end
```### With Transparency```lua
function BridgeFunction_OnInterfaceRender()
    --Enable alpha blending
    EnableAlphaBlend()
    
    --Render with transparency (50%)
    RenderBitmap(textureId, 100, 100, 200, 200, 0, 0, 1, 1, false, false, 0.5)
    
    --Desabilitar alpha blending
    DisableAlphaBlend()
end
```### Sprite animation```lua
local frame = 0
local frameTime = 0

function BridgeFunction_OnInterfaceRender()
    --Update animation frame
    frameTime = frameTime + 1
    if frameTime > 10 then
        frame = (frame + 1) % 4 --4 frames
        frameTime = 0
    end
    
    --Calculate UV for the current frame
    local u = (frame % 2) * 0.5 --2 columns
    local v = math.floor(frame / 2) * 0.5 --2 lines
    
    --Render animation frame
    RenderBitmap(spriteSheetId, 100, 100, 64, 64, u, v, 0.5, 0.5, false, false, 1.0)
end
```

## UV Parameters

- `u `, ` v`: Initial coordinates in the texture (0.0 = start, 1.0 = end)
- `uw `, ` vh`: Size of the area to render (0.0 = nothing, 1.0 = full texture)

**Example of UV:**
- `u=0, v=0, uw=1, vh=1`: Full texture
- `u=0.25, v=0.25, uw=0.5, vh=0.5`: Center of the texture (25% on each side)

## Important Notes

1. **Complete Control**: Gives you full control over UV, scaling and transparency
2. **Sprite sheets**: Ideal for sprite sheets and animations
3. **Alpha blending**: Habilite `EnableAlphaBlend()` before using transparency
4. **Performance**: More expensive than `RenderImage`, use only when necessary

## Related Functions

- [RenderImage](RenderImage.md) - Simplified version of rendering
- [EnableAlphaBlend](EnableAlphaBlend.md) - Enables transparency
- [LoadBitmap](LoadBitmap.md) - Load texture
- [Rendering System](../06-Rendering-System.md) - Complete rendering system documentation

