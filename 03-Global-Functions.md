# Global Utility Functions

This document describes the basic global functions available in the Lua Client API.

## Overview

Global functions are helper functions that can be called from any part of the script without needing to instantiate objects. They are organized into categories:

- **Input & Mouse**: Functions to capture user input
- **Rendering & Graphics**: Functions for rendering and graphics
- **Text & UI**: Functions for rendering text and UI
- **Object Management**: Functions to manage game objects

## Input & Mouse

Functions to capture and process user input (mouse and keyboard).

### IsMouseClicked

Checks whether the left mouse button was clicked in the current frame.

```lua
IsMouseClicked() -> bool
```**Return**:` true ` if the button was clicked,` false ` otherwise.

**Example:**
```lua
if IsMouseClicked() then
    --Mouse was clicked
end
```

### IsMouseHeld

Checks whether the left mouse button is being held down.

```lua
IsMouseHeld() -> bool
```**Return**:` true ` if the button is pressed,` false ` otherwise.

### CheckMouseIn

Checks whether the mouse cursor is within a rectangular area.

```lua
CheckMouseIn(x, y, w, h) -> bool
```

**Parameters:**
- `x`(number): X coordinate of the top left corner
- `y`(number): Y coordinate of the upper left corner
- `w`(number): Width of the rectangle
- `h`(number): Height of the rectangle

**Return**:`true ` if the mouse is within the area,`false` otherwise.

**Example:**
```lua
if CheckMouseIn(100, 100, 200, 50) then
    --Mouse is over the button
end
```

### SetBlockInput

Locks or unlocks game input (useful for custom UI).

```lua
SetBlockInput(block) -> void
```

**Parameters:**
- `block `(bool):` true `to block,` false`to unlock

### SEASON3B_IsPress

Checks whether a key has been pressed in the current frame.

```lua
SEASON3B_IsPress(key) -> bool
```

**Parameters:**
- `key `(number): VK code of the key (ex:` 0x4D`for M)

**Return**:`true ` if the key was pressed,`false` otherwise.

### SEASON3B_IsRelease

Checks whether a key was released in the current frame.

```lua
SEASON3B_IsRelease(key) -> bool
```

### SEASON3B_IsRepeat

Checks whether a key is being held down (repeat).

```lua
SEASON3B_IsRepeat(key) -> bool
```

### SEASON3B_IsNone

Checks whether a key is not being pressed.

```lua
SEASON3B_IsNone(key) -> bool
```

## Rendering & Graphics

Functions for controlling rendering and graphics.

### EnableAlphaBlend

Enables default alpha blending.

```lua
EnableAlphaBlend() -> void
```

### EnableAlphaBlendMinus

Enables subtractive alpha blending.

```lua
EnableAlphaBlendMinus() -> void
```

### DisableAlphaBlend

Disables alpha blending.

```lua
DisableAlphaBlend() -> void
```

### DisableDepthTest

Disables the Z-buffer depth test (draws over).

```lua
DisableDepthTest() -> void
```

### EnableDepthMask

Enables written non-Z-buffer.

```lua
EnableDepthMask() -> void
```

### DisableDepthMask

Disables writing to the Z-buffer.

```lua
DisableDepthMask() -> void
```

### DisableTexture

Disables texturing (draws solid colors).

```lua
DisableTexture(disable) -> void
```

**Parameters:**
- `disable `(bool):` true`to disable textures

### EnableLightMap

Habilita lightmapping.

```lua
EnableLightMap() -> void
```

### BindTexture

Binds a texture for rendering.

```lua
BindTexture(textureId) -> void
```

**Parameters:**
- `textureId`(number): ID of the texture to be linked

### LoadBitmap

Loads a texture from a file.

```lua
LoadBitmap(path, id, filter, wrap, chk, full) -> int
```

**Parameters:**
- `path`(string): Image file path
- `id`(number): ID da textura
- `filter`(number): Texture filter
- `wrap`(number): Modo de wrap
- `chk`(number): Check flag
- `full`(number): Full path flag

**Return**: Operation status (0 = success).

### RenderBitmap

Renders a 2D image.

```lua
RenderBitmap(id, x, y, w, h, u, v, uw, vh, scale, startScale, alpha) -> void
```

**Parameters:**
- `id`(number): ID da textura
- `x `, ` y`(number): Position on the screen
- `w `, ` h`(number): Width and height
- `u `, ` v`(number): Starting UV coordinates
- `uw `, ` vh`(number): UV Size
- `scale`(bool): Apply scale
- `startScale`(bool): Initial scale
- `alpha`(number): Transparency (0.0 - 1.0)

### RenderImage

Simplified version of image rendering.

```lua
RenderImage(id, x, y, w, h) -> void
```

### Color4f

Creates a float-based color value.

```lua
Color4f(r, g, b, a) -> DWORD
```

**Parameters:**
- `r `, ` g `, ` b `, ` a`(float): Color components (0.0 - 1.0)

**Return**: DWORD color value.

### RGBA

Creates a default RGBA color value.

```lua
RGBA(r, g, b, a) -> DWORD
```

**Parameters:**
- `r `, ` g `, ` b `, ` a`(number): Cor components (0 - 255)

**Return**: DWORD color value.

## Text & UI

Functions for text rendering and user interface.

### UIRenderText_SetFont

Sets the current font for text rendering.

```lua
UIRenderText_SetFont(fontHandle) -> void
```

**Parameters:**
- `fontHandle`(number): Handle da fonte

### UIRenderText_SetTextColor

Sets the color of the text.

```lua
UIRenderText_SetTextColor(r, g, b, a) -> void
```

**Parameters:**
- `r `, ` g `, ` b `, ` a`(number): Cor components (0 - 255)

### UIRenderText_SetBgColor

Sets the background color of the text.

```lua
UIRenderText_SetBgColor(r, g, b, a) -> void
```

### UIRenderText_RenderText

Renders text on the screen.

```lua
UIRenderText_RenderText(x, y, text, w, h, sort) -> void
```

**Parameters:**
- `x `, ` y`(number): Position on the screen
- `text`(string): Text to be rendered
- `w `, ` h`(number): Width and height of the text area
- `sort`(number): Rendering order

### RenderTipText

Renders tooltip style text.

```lua
RenderTipText(x, y, text) -> void
```

**Parameters:**
- `x `, ` y`(number): Position on the screen
- `text`(string): Texto do tooltip

### IsWriteInterfaceOpen

Checks whether the writing interface (chat/input) is open.

```lua
IsWriteInterfaceOpen() -> bool
```**Return**:` true ` if the interface is open,` false ` otherwise.

## Object Management

Functions for managing game objects.

### GetCharacter

Gets a character object (player, monster, NPC).

```lua
GetCharacter(index) -> GameCharacter
```

**Parameters:**
- `index`(number): Character index

**Return**: Object `GameCharacter` or `nil`.

### GetModel

Gets a 3D model object.

```lua
GetModel(index) -> GameBMD
```

**Parameters:**
- `index`(number): Model index

**Return**: Object `GameBMD` or `nil`.

## Related Functions

- [Input & Mouse](../Functions/README.md#-input--mouse) - Detailed documentation of input functions
- [Rendering & Graphics](../Functions/README.md#-rendering--graphics) - Detailed rendering documentation
- [Text & UI](../Functions/README.md#-text--ui) - Detailed UI documentation
- [Object Management](../Functions/README.md#-object-management) - Detailed object documentation

