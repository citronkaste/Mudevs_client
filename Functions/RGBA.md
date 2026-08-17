# RGBA

Creates a default RGBA color value.

## Signature

```lua
RGBA(r, g, b, a) -> DWORD
```

## Parameters

- `r `, ` g `, ` b `, ` a`(number): Cor components (0 - 255)

## Return

`DWORD`- Color value in DWORD format.

## Usage

Creates a color value using integer components (0 to 255). More intuitive than `Color4f` for direct values.

## Examples

### Create Common Colors

```lua
--Dull red
local red = RGBA(255, 0, 0, 255)

--Semi-transparent green
local green = RGBA(0, 255, 0, 128)

--opaque blue
local blue = RGBA(0, 0, 255, 255)

--Opaque white
local white = RGBA(255, 255, 255, 255)

--Opaque black
local black = RGBA(0, 0, 0, 255)

--dull yellow
local yellow = RGBA(255, 255, 0, 255)
```### Colors with Transparency```lua
--Red 50% transparent
local redTransparent = RGBA(255, 0, 0, 128)

--Green 25% transparent
local greenTransparent = RGBA(0, 255, 0, 64)

--Blue 75% transparent
local blueTransparent = RGBA(0, 0, 255, 192)
```

## Difference between RGBA and Color4f

- **RGBA**: Uses integer values ​​from 0-255 (more intuitive)
- **Color4f**: Uses float values ​​from 0.0-1.0 (best for calculations)

**Conversion example:**
```lua
--RGBA: 255, 0, 0, 255
--Color4f: 1.0, 0.0, 0.0, 1.0
--Both represent dull red
```

## Important Notes

1. **Intuitive**: Values ​​from 0-255 are easier to understand
2. **Standard**: Standard format for colors on many systems
3. **DWORD**: Returns DWORD value compatible with the system
4. **Common use**: More common than `Color4f` for direct values

## Related Functions

- [Color4f](Color4f.md) - Creates color using float values
- [UIRenderText_SetTextColor](UIRenderText_SetTextColor.md) - Set text color
- [Rendering System](../06-Rendering-System.md) - Complete rendering system documentation

