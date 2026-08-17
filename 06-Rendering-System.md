# Rendering System

This document describes the complete rendering and graphics system available in the Lua Client API.

## Overview

The rendering system allows you to control rendering states, load textures, render 2D images, and manipulate visual properties of 3D objects.

## Render States

### Alpha Blending

Controls transparency and color mixing.

#### EnableAlphaBlend

Enables standard alpha blending (additive).

```lua
EnableAlphaBlend() -> void
```**Use:**```lua
EnableAlphaBlend()
RenderBitmap(textureId, 100, 100, 200, 200, 0, 0, 1, 1, false, false, 0.5) --50% transparent
DisableAlphaBlend()
```

#### EnableAlphaBlendMinus

Enables subtractive alpha blending.

```lua
EnableAlphaBlendMinus() -> void
```

**Use:** For color subtraction (darkening) purposes.

#### DisableAlphaBlend

Disables alpha blending.

```lua
DisableAlphaBlend() -> void
```

### Depth Testing

Controls the Z-buffer depth test.

#### DisableDepthTest

Disables the depth test (draws over everything).

```lua
DisableDepthTest() -> void
```

**Usage:** For UI that should always appear at the front.

#### EnableDepthMask

Enables written non-Z-buffer.

```lua
EnableDepthMask() -> void
```

#### DisableDepthMask

Disables writing to the Z-buffer.

```lua
DisableDepthMask() -> void
```

**Usage:** For objects that should not affect the depth buffer.

### Texturing

#### DisableTexture

Disables texturing (allows you to draw solid colors).

```lua
DisableTexture(disable) -> void
```

**Parameters:**
- `disable `(bool):` true`to disable textures

**Use:**
```lua
DisableTexture(true)
--Draw solid shapes without texture
DisableTexture(false)
```

#### EnableLightMap

Habilita lightmapping.

```lua
EnableLightMap() -> void
```

## Texture Loading

### LoadBitmap

Loads a texture from an image file.

```lua
LoadBitmap(path, id, filter, wrap, chk, full) -> int
```

**Parameters:**
- `path`(string): Image file path
- `id`(number): Unique ID of the texture (for later reference)
- `filter`(number): Texture filter (0 = no filter, 1 = linear)
- `wrap`(number): Modo de wrap (0 = clamp, 1 = repeat)
- `chk`(number): Check flag (0 or 1)
- `full`(number): Full path flag (0 = relative, 1 = absolute)

**Return:** Operation status (0 = success, others = error).

**Example:**
```lua
function BridgeFunction_OnLoadInterface()
    local status = LoadBitmap("Interface\\CustomUI\\button.bmp", 100, 1, 0, 0, 1)
    if status == 0 then
        --Texture loaded successfully
    end
end
```

### BindTexture

Binds a texture for rendering.

```lua
BindTexture(textureId) -> void
```

**Parameters:**
- `textureId`(number): ID of the texture to be linked

**Usage:** Usually called automatically, but can be used to swap textures manually.

## 2D rendering

### RenderBitmap

Renders a 2D image with complete UV and transparency control.

```lua
RenderBitmap(id, x, y, w, h, u, v, uw, vh, scale, startScale, alpha) -> void
```

**Parameters:**
- `id`(number): ID da textura
- `x `, ` y`(number): Position on the screen (pixels)
- `w `, ` h`(number): Width and height on the screen (pixels)
- `u `, ` v`(number): Initial UV coordinates (0.0 - 1.0)
- `uw `, ` vh`(number): UV Size (0.0 - 1.0)
- `scale`(bool): Apply scale
- `startScale`(bool): Initial scale
- `alpha`(number): Transparency (0.0 = transparent, 1.0 = opaque)

**Example:**
```lua
--Render full texture
RenderBitmap(textureId, 100, 100, 200, 200, 0, 0, 1, 1, false, false, 1.0)

--Render only part of the texture (sprite sheet)
RenderBitmap(textureId, 100, 100, 64, 64, 0.25, 0.25, 0.5, 0.5, false, false, 1.0)

--Render with transparency
EnableAlphaBlend()
RenderBitmap(textureId, 100, 100, 200, 200, 0, 0, 1, 1, false, false, 0.5)
DisableAlphaBlend()
```

### RenderImage

Simplified version of image rendering.

```lua
RenderImage(id, x, y, w, h) -> void
```

**Parameters:**
- `id`(number): ID da textura
- `x `, ` y`(number): Position on the screen
- `w `, ` h`(number): Width and height

**Usage:** For fast rendering without UV control.

**Example:**
```lua
RenderImage(buttonTextureId, 100, 100, 200, 50)
```

## Cores

### Color4f

Creates a color value based on float components.

```lua
Color4f(r, g, b, a) -> DWORD
```

**Parameters:**
- `r `, ` g `, ` b `, ` a`(float): Color components (0.0 - 1.0)

**Return:** DWORD color value.

**Example:**
```lua
local red = Color4f(1.0, 0.0, 0.0, 1.0) --Dull red
local semiTransparent = Color4f(0.0, 1.0, 0.0, 0.5) --Semi-transparent green
```

### RGBA

Creates a default RGBA color value.

```lua
RGBA(r, g, b, a) -> DWORD
```

**Parameters:**
- `r `, ` g `, ` b `, ` a`(number): Cor components (0 - 255)

**Return:** DWORD color value.

**Example:**
```lua
local red = RGBA(255, 0, 0, 255) --Dull red
local green = RGBA(0, 255, 0, 128) --Semi-transparent green
```

## 3D Model Manipulation

### GameBMD Properties

Through the object `GameBMD `(obtained via ` GetModel(index)`), you can manipulate visual properties:

```lua
local model = GetModel(index)
if model then
    model.Visible = true          --Visibility
    model.Alpha = 0.8             --Transparency (0.0 - 1.0)
    model.Scale = 1.5             --Scale
    model.LightEnable = true      --Lighting
    model.ContrastEnable = false  --Contrast
end
```## Complete Example: UI System```lua
--Global variables
local buttonTextureId = 100
local backgroundTextureId = 101
local buttonHovered = false

--Load textures
function BridgeFunction_OnLoadInterface()
    LoadBitmap("Interface\\button.bmp", buttonTextureId, 1, 0, 0, 1)
    LoadBitmap("Interface\\background.bmp", backgroundTextureId, 1, 0, 0, 1)
end

--Render UI
function BridgeFunction_OnInterfaceRender()
    --Disable depth test for UI always in front
    DisableDepthTest()
    
    --Render background
    EnableAlphaBlend()
    RenderImage(backgroundTextureId, 0, 0, 800, 600)
    
    --Check button hover
    buttonHovered = CheckMouseIn(100, 100, 200, 50)
    
    --Render button with transparency if hover
    local alpha = buttonHovered and 0.8 or 1.0
    RenderBitmap(buttonTextureId, 100, 100, 200, 50, 0, 0, 1, 1, false, false, alpha)
    
    DisableAlphaBlend()
    --Re-enable depth test (if necessary)
end
```

## Good Practices

1. **Always configure states before rendering**: Enable/disable alpha blending, depth test, etc.
2. **Restores states**: If you disable something, re-enable it when you're done
3. **Load textures on startup**: Use `OnLoadInterface` to load resources
4. **Optimize rendering**: Avoid rendering things off-screen
5. **Use RenderImage for simplicity**: Use `RenderBitmap` only when you need UV control

## Related Functions

- [EnableAlphaBlend](../Functions/EnableAlphaBlend.md) - Detailed documentation
- [LoadBitmap](../Functions/LoadBitmap.md) - Detailed documentation
- [RenderBitmap](../Functions/RenderBitmap.md) - Detailed documentation
- [RenderImage](../Functions/RenderImage.md) - Detailed documentation
- [GetModel](../Functions/GetModel.md) - Gets 3D model object
- [Game Objects](04-Game-Objects.md) - GameBMD documentation

